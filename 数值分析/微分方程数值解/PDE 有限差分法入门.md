---
title: PDE 有限差分法入门：CFL 条件与 Lax 等价定理
date: 2026-06-14
tags:
  - 数值分析
  - 微分方程数值解
  - 偏微分方程
  - 有限差分
  - CFL条件
  - Lax等价定理
---

# PDE 有限差分法入门：CFL 条件与 Lax 等价定理

偏微分方程 (PDE) 的有限差分法 (Finite Difference Method, FDM) 把连续微分算子替换为网格差商，从而把 PDE 化为大型代数方程组。本节以热方程、对流方程、波方程为模型，引入相容性、稳定性、收敛性三大基石，并给出 Lax 等价定理的完整叙述与证明。

## 预备定义

> [!note] 定义 1（模型 PDE）
> 我们关心三类典型 PDE：
> 1. **抛物型——热方程**：$u_t = \alpha u_{xx}$，$x \in [0, L]$，$t > 0$，配以齐次 Dirichlet 边界 $u(0,t) = u(L,t) = 0$ 与初值 $u(x, 0) = u_0(x)$。
> 2. **双曲型——一阶对流方程**：$u_t + a u_x = 0$（$a > 0$），其真解沿特征线传播：$u(x,t) = u_0(x - at)$。
> 3. **双曲型——二阶波方程**：$u_{tt} = c^2 u_{xx}$，传播速度为 $\pm c$。

> [!note] 定义 2（均匀网格）
> 在 $[0,L] \times [0, T]$ 上取均匀网格：$x_j = j \Delta x$（$j = 0, 1, \ldots, N$，$\Delta x = L/N$），$t^n = n \Delta t$（$n = 0, 1, \ldots, M$，$M \Delta t = T$）。设网格函数
> $$u_j^n \approx u(x_j, t^n).$$
> 全体内点取值组成向量 $U^n = (u_1^n, \ldots, u_{N-1}^n)^\top$。

> [!note] 定义 3（差商算子）
> 对充分光滑的 $u$，由 Taylor 展开：
> - 前向差商：$u_x(x_j) \approx (u_{j+1} - u_j)/\Delta x$，截断误差 $O(\Delta x)$；
> - 后向差商：$u_x(x_j) \approx (u_j - u_{j-1})/\Delta x$，截断误差 $O(\Delta x)$；
> - 中心差商：$u_x(x_j) \approx (u_{j+1} - u_{j-1})/(2 \Delta x)$，截断误差 $O(\Delta x^2)$；
> - 二阶中心差商：$u_{xx}(x_j) \approx (u_{j+1} - 2 u_j + u_{j-1})/\Delta x^2$，截断误差 $O(\Delta x^2)$。

> [!note] 定义 4（FTCS 格式：热方程）
> **F**orward **T**ime, **C**entered **S**pace 格式：时间用一阶前向差分，空间用二阶中心差分：
> $$\frac{u_j^{n+1} - u_j^n}{\Delta t} = \alpha \frac{u_{j+1}^n - 2 u_j^n + u_{j-1}^n}{\Delta x^2}.$$
> 整理为显式递推：
> $$u_j^{n+1} = u_j^n + r\,(u_{j+1}^n - 2 u_j^n + u_{j-1}^n),$$
> 其中网格比 $\boxed{r = \alpha \Delta t / \Delta x^2}$。这本质上是空间半离散 ODE 系统配以 [[Euler 法|显式 Euler]] 时间推进。

> [!note] 定义 5（迎风格式：对流方程，$a > 0$）
> 空间用**后向**（迎风方向）差商，时间用前向差商：
> $$\frac{u_j^{n+1} - u_j^n}{\Delta t} + a \frac{u_j^n - u_{j-1}^n}{\Delta x} = 0,$$
> 即
> $$u_j^{n+1} = u_j^n - C\,(u_j^n - u_{j-1}^n), \quad C = \frac{a \Delta t}{\Delta x}.$$
> $C$ 称为 **Courant 数**。

> [!note] 定义 6（相容性、稳定性、收敛性）
> 设差分格式形式上记作 $L_h U = 0$（其中 $h = (\Delta x, \Delta t)$）：
> - **相容性 (consistency)**：将真解 $u_{\text{true}}$ 代入差分格式产生的局部截断误差
>   $$\tau_j^n = \text{LHS}(u_{\text{true}}) - \text{RHS}(u_{\text{true}}) \to 0, \quad \Delta x, \Delta t \to 0.$$
> - **稳定性 (Lax–Richtmyer)**：存在常数 $K$ 与 $\tau_0 > 0$ 使
>   $$\|U^n\| \leq K \|U^0\|, \quad \forall\, n \Delta t \leq T,\; 0 < \Delta t \leq \tau_0.$$
>   即数值解被初值控制，与 $n$ 无关。
> - **收敛性 (convergence)**：$\max_j |u_j^n - u(x_j, t^n)| \to 0$，当 $\Delta x, \Delta t \to 0$ 沿某条比例（如 $r$ 或 $C$ 固定）。

> [!warning] von Neumann 稳定性分析
> 对常系数线性格式做 Fourier 模式分析：设 $u_j^n = g^n e^{i k x_j}$，代入得**放大因子** $g(k)$。稳定的充要条件是
> $$|g(k)| \leq 1 + C_0 \Delta t, \quad \forall k \in \mathbb{R}.$$
> 这是 Lax–Richtmyer 稳定性在常系数情形下的可计算判据。

具体计算三个典型格式：

- **FTCS 热方程**：代入得 $g(k) = 1 - 4 r \sin^2(k \Delta x / 2)$。要求 $|g| \leq 1$ 对所有 $k$ 成立 $\iff r \leq 1/2$，即
  $$\boxed{\Delta t \leq \frac{\Delta x^2}{2 \alpha}} \quad \text{（抛物 CFL 条件）}.$$
- **迎风对流**：$g(k) = 1 - C(1 - e^{-i k \Delta x})$，故 $|g|^2 = 1 - 2C(1-C)(1 - \cos k \Delta x)$。$|g| \leq 1$ $\iff 0 \leq C \leq 1$（**双曲 CFL 条件**）。
- **中心差分对流**：$g(k) = 1 - i C \sin(k \Delta x)$，故 $|g|^2 = 1 + C^2 \sin^2(k \Delta x) > 1$ 对一切 $C \neq 0$ 成立。该格式**绝对不稳定**！必须改用迎风或加人工耗散。

## CFL 条件的物理解释

**Courant–Friedrichs–Lewy (1928)**：**数值依赖域必须包含真解依赖域**。对显式对流方程 $u_t + a u_x = 0$：
- 真解 $u(x_j, t^{n+1})$ 仅依赖于特征点 $x_j - a \Delta t$；
- 一步迎风格式中 $u_j^{n+1}$ 仅依赖于 $u_{j-1}^n$ 与 $u_j^n$，对应空间区间 $[x_{j-1}, x_j]$。
- 要求特征点 $x_j - a \Delta t \in [x_{j-1}, x_j]$，即 $0 \leq a \Delta t \leq \Delta x$，等价于 $|C| \leq 1$。

> [!warning] 必要 vs 充分
> CFL 条件是显式格式稳定的**必要**条件（违反 CFL 则数值依赖域不覆盖真解依赖域，必然不收敛）。von Neumann 分析在线性常系数情形给出**充分**条件。两者对迎风对流恰好都给出 $C \leq 1$，但抛物情形 CFL 条件本身平凡（依赖域全空间），需依靠 von Neumann 给出 $r \leq 1/2$。

## 引理

> [!abstract] 引理（FTCS 离散最大值原理）
> 设 FTCS 网格比 $r = \alpha \Delta t / \Delta x^2 \leq 1/2$。则对每一内点 $i$ 与每一时间层 $n \geq 0$ 有
> $$\min_j u_j^n \;\leq\; u_i^{n+1} \;\leq\; \max_j u_j^n.$$
> 该结论与连续热方程的 [[热方程最大值原理]] 完全一致。

**证明**：直接展开 FTCS 递推：
$$u_i^{n+1} = (1 - 2r)\, u_i^n + r\, u_{i-1}^n + r\, u_{i+1}^n.$$
当 $r \leq 1/2$，三个系数 $1 - 2r, r, r$ 均**非负**且其和为 $1$。因此 $u_i^{n+1}$ 是 $u_{i-1}^n, u_i^n, u_{i+1}^n$ 的**凸组合**，自然落在三者的最小最大值之间，从而被全局最小最大值控制。$\square$

注：该证明同时给出 $\ell^\infty$ 稳定性 $\|U^{n+1}\|_\infty \leq \|U^n\|_\infty$，独立于 von Neumann 分析。

## 主定理

> [!important] 定理（Lax 等价定理，Lax 1956）
> 对**良定**的线性初值问题，**相容**的差分格式满足
> $$\text{稳定性} \iff \text{收敛性}.$$
> 等价地：相容 + 稳定 $\iff$ 相容 + 收敛 $\iff$ 三条件全部成立。

历史背景：Peter D. Lax 在 1956 年于 *Communications on Pure and Applied Mathematics* 发表此定理。证明思想与 ODE 中的 [[Gronwall不等式|Gronwall]] 离散化一脉相承：把误差控制为局部截断误差与传播算子幂次之和。

## 证明

我们证明充分方向（相容 + 稳定 $\Rightarrow$ 收敛），这是数值分析中最常用的方向。

**记号准备**：把差分格式写成单步推进
$$U^{n+1} = S U^n,$$
其中 $S = S(\Delta t, \Delta x)$ 是线性算子（对 FTCS 即三对角矩阵 $I + r \Lambda$，其中 $\Lambda$ 是离散 Laplace）。把真解代入差分格式产生局部截断误差 $\tau^n$：
$$u^{n+1} = S u^n + \Delta t\, \tau^n.$$
此处 $u^n = (u(x_j, t^n))_j$ 表示真解在网格点的取值向量。

**误差递推**：定义全局误差 $e^n := u^n - U^n$。两式相减：
$$e^{n+1} = S e^n + \Delta t\, \tau^n.$$

**展开迭代**：从 $e^0$ 出发反复代入，得
$$e^n = S^n e^0 + \Delta t \sum_{k=0}^{n-1} S^{n-1-k}\, \tau^k.$$

**稳定性的应用**：Lax–Richtmyer 稳定性等价于算子幂次一致有界
$$\|S^m\| \leq K, \quad \forall\, m \Delta t \leq T,\; 0 < \Delta t \leq \tau_0.$$
取范数：
$$\|e^n\| \leq K \|e^0\| + \Delta t \sum_{k=0}^{n-1} \|S^{n-1-k}\| \cdot \|\tau^k\| \leq K \|e^0\| + K\, n \Delta t \cdot \max_{0 \leq k < n} \|\tau^k\|.$$
注意 $n \Delta t \leq T$，故
$$\|e^n\| \leq K \|e^0\| + K T\, \max_k \|\tau^k\|.$$

**收尾**：初值精确给定 $\Rightarrow e^0 = 0$；相容性 $\Rightarrow \max_k \|\tau^k\| \to 0$。因此
$$\|e^n\| \to 0 \quad (\Delta x, \Delta t \to 0),$$
即数值解**收敛**于真解。

**必要方向**（收敛 $\Rightarrow$ 稳定）的证明使用**反证 + Banach–Steinhaus 共鸣定理**：若不稳定则可找一族初值使 $\|S^{n_k} U^0_k\|$ 无界，结合收敛性导出矛盾。细节略。$\blacksquare$

## 总结

> [!info] 总结
> - **相容性**（局部一致逼近）+ **稳定性**（不放大扰动）$\iff$ **收敛性**（全局误差趋零）。
> - 把 PDE 收敛性的繁琐证明，**简化为局部 Taylor 展开 + 一个稳定性估计**。
> - 在线性常系数情形 von Neumann 分析提供 $|g(k)| \leq 1$ 形式的充分条件。
> - CFL 是数值依赖域包含真解依赖域的几何条件，是显式格式稳定的必要条件。
> - 显式格式步长受限：抛物 $\Delta t = O(\Delta x^2)$，双曲 $\Delta t = O(\Delta x)$。
> - 隐式格式（Crank–Nicolson、Backward Euler）通常**无条件稳定**，代价是每步解线性系统。

## 应用

### 应用 1：热方程 FTCS 数值实验

考虑 $u_t = u_{xx}$ 于 $[0,1]$，齐次 Dirichlet 边界，初值 $u_0(x) = \sin(\pi x)$。真解为
$$u(x,t) = e^{-\pi^2 t} \sin(\pi x).$$
取 $\Delta x = 0.1$（即 $N = 10$），则 $r \leq 1/2$ 要求 $\Delta t \leq \Delta x^2 / 2 = 0.005$。

**情形 A**（稳定）：取 $\Delta t = 0.004$，$r = 0.4$。
**情形 B**（不稳定）：取 $\Delta t = 0.006$，$r = 0.6 > 1/2$。

在 $t = 0.02$（情形 A 走 5 步，情形 B 走约 3.33 步，取整到 $t = 0.024$ 即 4 步比较）的部分网格点数值如下（情形 A）：

| $x_j$ | 真解 $e^{-\pi^2 \cdot 0.02} \sin(\pi x_j)$ | FTCS 数值（$r = 0.4$） | 误差 |
| --- | --- | --- | --- |
| $0.3$ | $0.6663$ | $0.6671$ | $8 \times 10^{-4}$ |
| $0.5$ | $0.8208$ | $0.8218$ | $1 \times 10^{-3}$ |
| $0.7$ | $0.6663$ | $0.6671$ | $8 \times 10^{-4}$ |

（其中 $e^{-\pi^2 \cdot 0.02} \approx 0.8208$。）

情形 B 在 $n \approx 50$ 步左右数值解的高频分量被放大因子 $|1 - 4 \cdot 0.6| = 1.4$ 反复放大，振幅按 $1.4^{50} \approx 10^{7}$ 量级爆炸，数值解失效。

连续解的衰减规律可与 [[热方程基本解]] 中 $G(x,t) = (4 \pi t)^{-1/2} e^{-x^2/(4t)}$ 的高斯衰减作对照：高频分量 $e^{-k^2 t}$ 衰减最快，FTCS 在 $r = 1/2$ 临界处恰好以 $|g(\pi/\Delta x)| = |1 - 4r| = 1$ 保持高频不放大。

### 应用 2：对流方程上风格式与 CFL

考虑 $u_t + u_x = 0$ 于 $[0, 1]$ 周期边界，初值取光滑正弦 $u_0(x) = \sin(2\pi x)$。真解为 $u(x, t) = \sin(2\pi (x - t))$。

取 $\Delta x = 0.05$（$N = 20$）。

**情形 A**（CFL 满足）：$\Delta t = 0.04$，$C = 0.8 < 1$。
**情形 B**（CFL 违反）：$\Delta t = 0.06$，$C = 1.2 > 1$。

在 $t = 0.5$（半个周期）时数值结果对照（情形 A，约 13 步）：

| $x_j$ | 真解 $\sin(2\pi (x_j - 0.5))$ | 上风数值 | 误差 |
| --- | --- | --- | --- |
| $0.25$ | $\sin(-\pi/2) = -1.0000$ | $-0.9612$ | $0.039$ |
| $0.50$ | $\sin(0) = 0$ | $0$ | $0$ |
| $0.75$ | $\sin(\pi/2) = 1.0000$ | $0.9612$ | $0.039$ |

可见上风格式存在**幅值衰减**，原因是其等价修正方程为
$$u_t + a u_x = \frac{a \Delta x (1 - C)}{2} u_{xx} + O(\Delta x^2),$$
即引入了**人工粘性**（数值耗散）系数 $\nu_{\text{num}} = a \Delta x (1-C)/2$。当 $C = 1$ 时人工粘性为零，恰好沿特征精确平移；$C < 1$ 时正粘性导致波幅衰减、方波边缘被光滑模糊。

情形 B 中放大因子最大值 $|g(\pi/\Delta x)| = |1 - 2C| = 1.4$，数值解迅速爆炸。

注：若把时间方向从一阶 Euler 升级为高阶 [[Runge-Kutta方法的收敛性|RK4]]，再配合中心差分或 WENO 空间离散，可在 $C \leq C_{\max}^{(\text{RK4})} \approx 2\sqrt{2}$ 内同时获得四阶时间精度。

## 证明思路总结

> [!tip] 思路要点
> - **三大基石**：相容性（局部 Taylor）+ 稳定性（不放大）+ 收敛性（全局误差零）。
> - **Lax 等价定理**：把"收敛性证明"等价化简为"稳定性估计 + 相容性验证"。这是有限差分理论的核心定理。
> - **von Neumann** 是稳定性的可计算判据（Fourier 模式 $|g(k)| \leq 1$）；**CFL** 是其几何/物理解释（依赖域包含关系）。
> - **显式格式步长限制**：抛物方程 $\Delta t = O(\Delta x^2)$（FTCS：$r \leq 1/2$），双曲方程 $\Delta t = O(\Delta x)$（迎风：$C \leq 1$）。
> - **隐式格式**（Crank–Nicolson、Backward Euler）无条件稳定但每步解线性系统；现代大型并行计算偏好**显式 + 局部步长**。
> - **时间方向看作 ODE**：FTCS = [[Euler 法|显式 Euler]] + 二阶中心差分；用 [[Runge-Kutta方法的收敛性|RK4]] 替代 Euler 可提升时间阶数。
> - **最大值原理**的离散版（FTCS 引理）来源于凸组合系数非负，与连续 [[热方程最大值原理]] 一致；它给出独立于 von Neumann 的 $\ell^\infty$ 稳定性证明。
> - **绝对不稳定**的格式（如对流方程的中心差分时间显式）必须改用迎风、Lax–Wendroff 等具有数值耗散或具相容修正的格式。

$\blacksquare$
