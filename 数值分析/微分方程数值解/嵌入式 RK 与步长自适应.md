---
title: 嵌入式 RK 与步长自适应
date: 2026-06-09
tags:
  - 数值分析
  - 微分方程数值解
  - 嵌入式RK
  - 自适应步长
  - PI控制器
---

# 嵌入式 RK 与步长自适应

固定步长的 [[Runge-Kutta方法的收敛性|经典 RK 方法]] 在求解非均匀光滑度的 ODE 时效率低下：光滑段浪费计算，急变段精度不足。**嵌入式 Runge-Kutta 对**（embedded RK pair）通过在同一组 $k_i$ 上构造两个不同阶的近似解，几乎零额外成本地估计局部误差，并据此动态调整步长。这是现代 ODE 求解器（MATLAB `ode45`、SciPy `solve_ivp`、SUNDIALS）的核心机制。

## 预备定义

> [!note] 定义 1：Butcher 表
> 一个 $s$ 级显式 RK 方法由 Butcher 表
> $$
> \begin{array}{c|c}
> c & A \\
> \hline
> & b^T
> \end{array}
> $$
> 给出，其中 $A \in \mathbb{R}^{s \times s}$ 严格下三角，$b, c \in \mathbb{R}^s$。一步更新为
> $$ k_i = f\!\left(t_n + c_i h, \ y_n + h \sum_{j=1}^{i-1} a_{ij} k_j\right), \quad y_{n+1} = y_n + h \sum_{i=1}^s b_i k_i. $$

> [!note] 定义 2：嵌入式 RK 对
> **嵌入式 RK 对** $(p, \hat{p})$ 是共享 $A, c$ 但带两组权重 $b, \hat{b}$ 的 RK 方法：
> $$
> \begin{array}{c|c}
> c & A \\
> \hline
> & b^T \quad (p \text{ 阶}) \\
> & \hat{b}^T \quad (\hat{p} \text{ 阶})
> \end{array}
> $$
> 通常 $|\hat{p} - p| = 1$。两个解分别为 $y_{n+1} = y_n + h \sum b_i k_i$ 与 $\hat{y}_{n+1} = y_n + h \sum \hat{b}_i k_i$。

> [!note] 定义 3：局部误差估计
> 嵌入式对的**局部误差估计**为
> $$ \text{est} = \| y_{n+1} - \hat{y}_{n+1} \| = h \left\| \sum_{i=1}^s (b_i - \hat{b}_i) k_i \right\| \approx C h^{p+1}, $$
> 其中 $p = \min(p, \hat{p})$ 为低阶解的阶数。该估计反映当前步的真实误差量级。

> [!note] 定义 4：误差容限与归一化
> 用户给定**绝对容限** $\text{atol}$ 与**相对容限** $\text{rtol}$。逐分量归一化误差为
> $$ \text{err} = \sqrt{\frac{1}{d} \sum_{i=1}^d \left( \frac{e_i}{\text{atol} + \text{rtol} \cdot \max(|y_i|, |\hat{y}_i|)} \right)^2}, $$
> 接受条件为 $\text{err} \leq 1$。

## 引理

> [!abstract] 引理（最优步长公式）
> 设当前步长 $h$ 给出误差估计 $\text{est} \approx C h^{p+1}$，且低阶解阶数为 $p$。则使 $\text{est}_{\text{new}} = \text{tol}$ 的理想步长为
> $$ h_{\text{opt}} = h \cdot \left( \frac{\text{tol}}{\text{est}} \right)^{1/(p+1)}. $$
> 加入安全系数 $S \in (0, 1)$（通常 $S = 0.9$）防止接近边界，实际取 $h_{\text{new}} = S \cdot h_{\text{opt}}$。

## 主定理

> [!important] 定理（嵌入式 RK 步长自适应的最优性）
> 设嵌入式对 $(p, p+1)$ 的低阶解全局误差为 $O(h^p)$。若使用步长控制策略
> $$ h_{n+1} = h_n \cdot \min\!\left( \alpha_{\max}, \ \max\!\left(\alpha_{\min}, \ S \left(\frac{\text{tol}}{\text{est}_n}\right)^{1/(p+1)}\right) \right), $$
> 则在 $f \in C^{p+1}$ 假设下，自适应算法**渐进等分布局部误差**（每步 $\text{est}_n \approx \text{tol}$），且总步数最优至常数倍。

## 证明

**第一步：误差模型。** 由 LTE 理论，对足够光滑的 $f$，嵌入式对给出
$$
\text{est}_n = \| y_{n+1} - \hat{y}_{n+1} \| = C(t_n) h_n^{p+1} + O(h_n^{p+2}),
$$
其中 $C(t)$ 是真解处依赖于 $f$ 高阶导的局部常数。

**第二步：步长公式来源。** 设理想步长 $h^\star$ 满足 $C(t_n) (h^\star)^{p+1} = \text{tol}$。两式相除消去 $C(t_n)$：
$$
\frac{\text{tol}}{\text{est}_n} = \left( \frac{h^\star}{h_n} \right)^{p+1} \implies h^\star = h_n \left( \frac{\text{tol}}{\text{est}_n} \right)^{1/(p+1)}.
$$
这正是引理中的最优步长。

**第三步：等分布与最优性。** 若 $h_{n+1} = h^\star$，则下一步预计误差 $\approx \text{tol}$，即各步误差近似相等。在等分布下，总步数 $N$ 满足
$$
\sum_n h_n \approx \int_{t_0}^T \left( \frac{\text{tol}}{C(t)} \right)^{1/(p+1)} dt,
$$
而总累积误差 $\sum_n \text{est}_n \approx N \cdot \text{tol}$。最小化 $N$ 在固定总误差下即对应等分布（Lagrange 乘子法），故策略最优。

**第四步：截断保护。** 因 $C(t_n)$ 仅是 $C(t_{n+1})$ 的近似，加入截断 $\alpha_{\min} = 0.1$、$\alpha_{\max} = 5$ 防止步长剧变；安全系数 $S = 0.9$ 留出余量减少拒绝率。

## 总结

> [!info] 总结
> 嵌入式 RK 对在同一组 $k_i$ 上同时算出 $p$ 阶与 $p+1$ 阶解，差值即为可信的局部误差估计。基于该估计的 I 控制器或 PI 控制器实现误差等分布的步长自适应，是现代非刚性 ODE 求解器的标配。RKF45（Fehlberg 1969）与 DP5（Dormand-Prince 1980）是工业标准；后者 First-Same-As-Last（FSAL）性质使每步仅 6 次有效 $f$ 求值。

## 应用

### 应用 1：RKF45 求解光滑 IVP

考虑 $y'(t) = y - t^2 + 1$，$y(0) = 0.5$，$t \in [0, 2]$，真解 $y(t) = (t+1)^2 - 0.5 e^t$。设 $\text{tol} = 10^{-4}$，初始步长 $h_0 = 0.2$。

RKF45 一步给出 4 阶与 5 阶估计，前 5 步如下（典型行为）：

| 步 | $t_n$ | $h_n$ | est | 接受？ | $h_{n+1}$ |
|---|---|---|---|---|---|
| 1 | 0.0 | 0.2000 | 3.1e-5 | 是 | 0.260 |
| 2 | 0.2 | 0.2600 | 9.4e-5 | 是 | 0.265 |
| 3 | 0.46 | 0.2650 | 1.3e-4 | **否** | 0.225 |
| 3' | 0.46 | 0.2250 | 7.0e-5 | 是 | 0.245 |
| 4 | 0.685 | 0.2450 | 1.0e-4 | 是 | 0.245 |
| 5 | 0.930 | 0.2450 | 1.1e-4 | 是 | 0.240 |

第 3 步因误差超容限被拒绝，步长缩至 $0.9 \cdot 0.265 \cdot (10^{-4}/1.3 \cdot 10^{-4})^{1/5} \approx 0.225$ 重做。光滑区域中步长稳定在 $0.24$ 附近，无需用户干预。

### 应用 2：振动方程自适应步长

考虑 $y'' + y = 0$，$y(0) = 1$，$y'(0) = 0$。化为一阶系统：
$$
\begin{aligned}
u'(t) &= v(t), \\
v'(t) &= -u(t),
\end{aligned}
\qquad (u, v)(0) = (1, 0).
$$
真解为 $u(t) = \cos t$，$v(t) = -\sin t$。

用 DP5 自适应求解 $t \in [0, 20]$，$\text{tol} = 10^{-6}$：步长 $h(t)$ 在轨道光滑处稳定在 $\approx 0.15$；但若改为带阻尼共振强迫的方程 $y'' + 0.01 y' + y = \cos t$，则在 $t$ 接近共振相位（$t = 2\pi k$）时，解的高阶导数增大，$C(t)$ 增大，自适应器自动将 $h$ 缩至 $\approx 0.03$；离开共振峰后又恢复到 $\approx 0.15$。**步长曲线 $h(t)$ 呈现周期性凹陷**，准确反映解的局部复杂度。

> [!tip] PI 控制器的优势
> 单纯的 I 控制器（只用 $\text{est}_n$）在误差敏感区域常出现"接受-拒绝-接受"的振荡，浪费计算。**PI 控制器**
> $$ h_{n+1} = h_n \cdot S \cdot \left( \frac{\text{tol}}{\text{est}_n} \right)^{\alpha} \left( \frac{\text{est}_{n-1}}{\text{est}_n} \right)^{\beta} $$
> 引入误差的"动量"项，典型 $\alpha = 0.7/(p+1)$，$\beta = 0.4/(p+1)$。Gustafsson (1991) 证明 PI 控制将拒绝率降低 30%-50%。

### 应用 3：常用嵌入式对参数表

工业级求解器中常见的嵌入式 RK 对参数汇总：

| 方法 | 阶数对 | 级数 $s$ | FSAL | 主要用途 |
|---|---|---|---|---|
| Heun-Euler | 2(1) | 2 | 否 | 教学、低精度场景 |
| Bogacki-Shampine | 3(2) | 4 | 是 | MATLAB `ode23` |
| RKF45 (Fehlberg) | 5(4) | 6 | 否 | 经典工程算例 |
| Dormand-Prince | 5(4) | 7 | 是 | MATLAB `ode45`, SciPy 默认 |
| Verner 6(5) | 6(5) | 9 | 否 | 高精度需求 |
| Dormand-Prince 8(7) | 8(7) | 13 | 是 | $\text{tol} \leq 10^{-10}$ |

**选择策略**：$\text{tol} \approx 10^{-3} \sim 10^{-6}$ 选 DP5；$\text{tol} \leq 10^{-10}$ 选 DP87 或 Verner 8(9)；刚性问题切换 Radau IIA 隐式对。

## 算法关键点 / 证明思路总结

> [!tip] 关键要点
> 1. **零额外成本估计误差**：嵌入式利用同一 $\{k_i\}$ 同时算两个阶的解，差值即为可信的误差代理，对比"步长减半比较"方法节省一半计算。
> 2. **DP5 + FSAL**：Dormand-Prince 5(4) 对的 $k_7$ 等于下一步的 $k_1$，每步实际只需 6 次 $f$ 求值，是 MATLAB `ode45` 的实现核心。
> 3. **I 控制 vs PI 控制**：PI 控制器引入误差比率作为反馈，显著降低拒绝率，已成为现代求解器（DOPRI、CVODE）默认。
> 4. **拒绝步是必要代价**：安全系数 $S < 1$、截断系数 $\alpha_{\min/\max}$ 与少量拒绝步是鲁棒性的代价，目标是控制拒绝率在 5%-15% 之间。
> 5. **刚性问题需切换方法**：嵌入式显式 RK 不适用于刚性 ODE，此时应切换至嵌入式隐式 RK（如 Radau IIA、SDIRK 对）或 BDF 方法。

$\blacksquare$
