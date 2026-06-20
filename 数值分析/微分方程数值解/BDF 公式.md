---
title: BDF 公式（向后微分公式）
date: 2026-06-09
tags:
  - 数值分析
  - 微分方程数值解
  - BDF
  - 刚性方程
  - A稳定性
  - 隐式多步法
---

# BDF 公式

**向后微分公式**（Backward Differentiation Formula, BDF）是为求解**刚性方程**（stiff ODE）量身设计的隐式线性多步法家族。其设计哲学与 Adams 家族相反：BDF 不在于精度的极致，而在于**稳定性的最大化**——它是工程实践中（MATLAB `ode15s`、SUNDIALS CVODE、Python `scipy.integrate.BDF`）求解刚性问题的默认选择。

## 预备定义

> [!note] 定义 1：刚性方程
> 直观上，**刚性方程**是指 ODE 系统中包含**多个时间尺度差异极大**的成分（如 $y' = -1000 y + g(t)$），使得显式方法的步长被**最快瞬态**限制，远小于解本身光滑变化所需的步长。形式刻画通常借助 Jacobian 谱：$\max_i |\mathrm{Re}(\lambda_i)| / \min_i |\mathrm{Re}(\lambda_i)| \gg 1$。详见 [[刚性方程与 A-稳定性]]。

> [!note] 定义 2：A-稳定性
> 设方法应用于 Dahlquist 试验方程 $y' = \lambda y$（$\mathrm{Re}\,\lambda < 0$），得递推 $y_{n+1} = R(h\lambda) y_n$（单步法）或更一般的特征方程。**稳定域**为
> $$\mathcal{S} = \{ \mu \in \mathbb{C} : \text{方法对} \;y' = \lambda y\;\text{的所有解有界，}\mu = h\lambda\}.$$
> 称方法 **A-稳定**，若 $\mathcal{S} \supseteq \mathbb{C}^- = \{\mu : \mathrm{Re}\,\mu \leq 0\}$。

> [!note] 定义 3：A($\alpha$)-稳定性
> 称方法 **A($\alpha$)-稳定**（$0 < \alpha \leq 90°$），若稳定域包含无界扇形
> $$W_\alpha = \{ \mu \in \mathbb{C} : |\arg(-\mu)| < \alpha,\; \mu \neq 0 \}.$$
> $\alpha = 90°$ 即 A-稳定。$\alpha < 90°$ 时排除虚轴附近——对纯振荡问题不利，但对**衰减占主导的刚性问题**仍非常有用。

> [!note] 定义 4：BDF$k$ 公式
> $k$ 步 BDF 公式利用过去 $k$ 步的解值通过**反向有限差分**逼近 $y'(t_{n+k})$，并令其等于 $f(t_{n+k}, y_{n+k})$：
> $$\sum_{j=0}^{k} \alpha_j y_{n+j} = h\, \beta_k f(t_{n+k}, y_{n+k}).$$
> 对应 $\sigma(z) = \beta_k z^k$（**仅在最新点**求 $f$）。系数 $\{\alpha_j\}$ 与 $\beta_k$ 由 $p = k$ 阶相容性条件
> $$\sum_{j=0}^k \alpha_j j^q = q \beta_k k^{q-1}, \quad q = 0, 1, \ldots, k$$
> 唯一确定（在归一化 $\alpha_k$ 后）。

> [!note] 定义 5：Dahlquist 第二壁垒
> Dahlquist (1963)：A-稳定的线性多步法的阶 $p \leq 2$，达到的方法中**误差常数**最小的是**梯形法**（即 AM2）。这一壁垒是 BDF 设计动机的核心——为了突破 $p = 2$，必须**放弃** A-稳定，转求 A($\alpha$)-稳定。

## 引理

> [!abstract] 引理 1：BDF 系数的生成函数
> BDF$k$ 的系数由形式幂级数恒等
> $$\sum_{j=0}^{k} \alpha_j z^j = \beta_k\, z^k\, \sum_{l=1}^{k} \frac{1}{l}\left(1 - z^{-1}\right)^l \cdot \text{（截断到 }k\text{ 阶）}$$
> 等价地，$\rho(z) = \sum_j \alpha_j z^j$ 满足 $\rho(z) / \sigma(z) \approx \log(z)$（$z \to 1$）的 Padé 型逼近。这导出标准化系数表（见下）。

> [!abstract] 引理 2：BDF 的零稳定性边界
> BDF$k$ 在 $k = 1, 2, 3, 4, 5, 6$ 时**零稳定**（即 [[线性多步法与 Dahlquist 等价定理]] 的根条件成立），故收敛；当 $k \geq 7$ 时 $\rho$ 出现 $|z| > 1$ 的根，**零不稳定**，**不收敛**。这一现象由 Cryer (1971) 数值证实并由 Mitchell-Craggs 系统分析。

## 主定理

> [!important] 定理：BDF 的稳定性谱
> 1. **BDF1**（即 [[Euler 法|隐式 Euler]]）：$1$ 阶，**A-稳定**且 **L-稳定**。
> 2. **BDF2**：$2$ 阶，**A-稳定**（边界为 Dahlquist 第二壁垒所允许的最大 BDF 阶）。
> 3. **BDF3**：$3$ 阶，**A($86.03°$)-稳定**。
> 4. **BDF4**：$4$ 阶，**A($73.35°$)-稳定**。
> 5. **BDF5**：$5$ 阶，**A($51.84°$)-稳定**。
> 6. **BDF6**：$6$ 阶，**A($17.84°$)-稳定**。
> 7. **BDF$k$（$k \geq 7$）**：零不稳定，**不收敛**，工程上不可用。

## 证明

我们给出 BDF1 与 BDF2 的稳定性证明，并简述 BDF$k$（$k \geq 3$）数值确定 $\alpha$ 的方法。

**(1) BDF1 = 隐式 Euler**：
$$y_{n+1} - y_n = h f_{n+1}.$$
对试验方程 $y' = \lambda y$：$y_{n+1} (1 - h\lambda) = y_n$，即 $R(\mu) = (1 - \mu)^{-1}$。$|R(\mu)| \leq 1 \iff |1 - \mu| \geq 1 \iff \mu$ 在以 $1$ 为圆心的单位圆**外**。该区域包含整个左半平面 $\mathrm{Re}\,\mu \leq 0$，故 **A-稳定**。又 $|R(\mu)| \to 0$ 当 $\mu \to -\infty$，故 **L-稳定**。

**(2) BDF2**：
$$\frac{3}{2} y_{n+2} - 2 y_{n+1} + \frac{1}{2} y_n = h f_{n+2}.$$
试验方程下，特征方程
$$\left(\frac{3}{2} - \mu\right) z^2 - 2 z + \frac{1}{2} = 0, \quad \mu = h\lambda.$$
两根的模 $|z_i(\mu)|$ 关于 $\mu$ 连续。$\mu = 0$ 时根为 $z = 1, 1/3$，模为 $1, 1/3$（边界 $z = 1$ 为单根，根条件成立）。

要证 **A-稳定**，需 $\mathrm{Re}\,\mu \leq 0$ 时 $|z_1|, |z_2| \leq 1$（且 $|z_i| = 1$ 处为单根）。一种途径是用 Schur-Cohn 判据，或直接验证：稳定域**边界**由 $|z| = 1$ 即 $z = e^{i\theta}$ 给出，回代得
$$\mu(\theta) = \frac{3}{2} - 2 e^{-i\theta} + \frac{1}{2} e^{-2 i\theta} = \frac{3}{2} - 2 e^{-i\theta} + \frac{1}{2} e^{-2 i\theta}.$$
$\theta \in [0, 2\pi)$ 时该曲线把复平面分为内外。计算表明该曲线**完全位于右半平面**（$\mathrm{Re}\,\mu \geq 0$，仅在 $\theta = 0$ 处与原点相切），故**整个左半平面**位于稳定域内。BDF2 **A-稳定**。

**(3) BDF$k$，$k = 3, 4, 5, 6$**：用边界轨迹方法。令
$$\mu(\theta) = \frac{\rho(e^{i\theta})}{\sigma(e^{i\theta})} = \frac{\rho(e^{i\theta})}{\beta_k e^{ik\theta}},$$
该曲线为稳定域边界。数值绘制显示该曲线**进入左半平面**一定区域，但仍保留以负实轴为对称的扇形 $W_\alpha$ 完全在稳定域中。$\alpha$ 的精确值由数值最优化得到表中给出的角度。

**(4) $k \geq 7$**：直接数值求 $\rho$ 的根，可见出现 $|z| > 1$ 的根。例如 BDF7 的 $\rho$ 在单位圆外有一对复根，违反根条件。由 Dahlquist 等价定理（[[线性多步法与 Dahlquist 等价定理]]），方法不收敛。

## 总结

> [!info] BDF 的设计哲学
> - **目标**：突破 Dahlquist 第二壁垒 $p \leq 2$（A-稳定）的限制。
> - **代价**：放弃 A-稳定，仅追求 A($\alpha$)-稳定，且阶 $\leq 6$（再高则零不稳定）。
> - **结构**：$\sigma(z) = \beta_k z^k$ 的简单形式使每步只需在 $t_{n+k}$ 求一次 $f$，配合 Newton 迭代有效求解隐式方程。
> - **实践**：MATLAB `ode15s`、SUNDIALS CVODE、SciPy `BDF` 均以 BDF1-BDF5 为骨干，配合自适应步长、自适应阶数（变阶变步长 VSVO）。

> [!warning] 实现陷阱
> - **启动困难**：BDF$k$ 需要 $k$ 个一致初值。常见做法是从 BDF1 启动，逐步**升阶**至 BDF$k$。
> - **Newton 迭代收敛**要求 $h \cdot \|J\| \cdot |\beta_k|$ 不太大；对极强刚性需要特殊预处理。
> - **变步长会破坏稳定性**：变步长 BDF（VSBDF）只在步长比 $\omega = h_{\text{new}} / h_{\text{old}}$ 适中时（典型上界 $1.3 \sim 2$）保持稳定。
> - BDF**不适合**纯振荡问题（如 $y'' + y = 0$）：A($\alpha$)-稳定的扇形不含虚轴附近，会引入显著的**人工耗散**。

## 应用

### 应用 1：BDF2 求解强刚性线性问题

$$y' = -1000\, y, \quad y(0) = 1, \quad t \in [0, 1].$$
真解 $y(t) = e^{-1000 t}$，$t \geq 0.01$ 后已小于 $10^{-4}$，但**衰减阶段**对显式方法极具挑战。

- **显式 Euler**：稳定要求 $|1 + h\lambda| \leq 1 \Rightarrow h \leq 0.002$。
- **BDF2**：A-稳定，**任意 $h > 0$** 都稳定。

取 $h = 0.01$（10 倍于显式 Euler 的稳定上界），用 BDF1 自启动得 $y_1$。BDF2 推进：
$$\frac{3}{2} y_{n+2} - 2 y_{n+1} + \frac{1}{2} y_n = -1000 h\, y_{n+2} \implies y_{n+2} = \frac{2 y_{n+1} - \tfrac{1}{2} y_n}{\tfrac{3}{2} + 1000 h}.$$

| $n$ | $t_n$ | $y_n^{\text{BDF2}}$ | $y(t_n) = e^{-1000 t_n}$ |
|-----|-------|---------------------|--------------------------|
| 0   | 0.00  | $1.000$             | $1.000$                  |
| 1   | 0.01  | $\approx 9.1\times 10^{-5}$ | $4.5\times 10^{-5}$ |
| 2   | 0.02  | $\approx 8\times 10^{-9}$ | $2.1\times 10^{-9}$    |
| 5   | 0.05  | $\approx 0$         | $\approx 0$              |

数值衰减比物理衰减略慢，但**有界且单调正**，远好于显式 Euler 在 $h = 0.01$ 下的指数振荡爆炸。

### 应用 2：Van der Pol 振子刚性极限 $\mu = 1000$

考虑非线性方程
$$y'' - \mu (1 - y^2) y' + y = 0, \quad y(0) = 2, y'(0) = 0.$$
当 $\mu \gg 1$，解呈现**慢-快交替**：长时间缓慢演化，间或出现极薄的快速过渡层（厚度 $\sim 1/\mu$）。

- **显式 RK4**：步长在过渡层中被迫降至 $O(1/\mu)$，全局耗费极大。
- **BDF5**（如 MATLAB `ode15s`，自适应阶 $1$ 至 $5$）：
  - 在慢段使用大步长（$h \sim 0.1$），高阶 BDF 维持精度；
  - 在过渡层自适应缩小步长并降阶到 BDF2-BDF3；
  - 总步数比显式 RK4 少 $1$ 至 $2$ 个数量级。

这是 BDF 在工程中（化学反应网络、电路仿真、燃烧模拟）作为**默认刚性求解器**的典型场景。

### 应用 3：化学动力学反应网络

刚性常微分方程系统（如 ROBER 测试问题）：
$$\begin{cases} y_1' = -0.04\, y_1 + 10^4\, y_2 y_3, \\ y_2' = 0.04\, y_1 - 10^4\, y_2 y_3 - 3\times 10^7\, y_2^2, \\ y_3' = 3\times 10^7\, y_2^2. \end{cases}$$
特征值跨 $10$ 个数量级。BDF（CVODE / `ode15s`）在 $t \in [0, 10^{11}]$ 上仅需千余步即可完成，而显式方法需 $\sim 10^{15}$ 步。

## 算法关键点

> [!tip] BDF 实施要点
> 1. **公式选择**：实用上 $k \leq 5$（BDF6 的 A($17°$)-稳定较弱）；变阶 VSVO 通常自适应在 $1 \leq k \leq 5$ 间切换。
> 2. **每步求解**：隐式方程 $\frac{1}{\beta_k}\sum_j \alpha_j y_{n+j} = h f(t_{n+k}, y_{n+k})$ 用 **简化 Newton 法**：固定 Jacobian $J \approx \partial f / \partial y$ 数步，必要时重算。Newton 矩阵为 $\frac{\alpha_k}{\beta_k} I - h J$。
> 3. **启动**：通常以 BDF1（隐式 Euler）单步启动，逐步升阶。也有用 [[Runge-Kutta方法的收敛性|Runge-Kutta]] 启动的实现。
> 4. **步长控制**：基于 Milne-type 误差估计（比较 BDF$k$ 与 BDF$(k-1)$ 或 BDF$(k+1)$），通过 PI 控制器调整 $h$。
> 5. **阶数控制**：尝试 $k-1, k, k+1$ 的预测误差，选最优。
> 6. **稀疏 Jacobian**：大型 ODE 系统中（PDE 半离散化、化学反应）必须利用稀疏性求解 Newton 系统；CVODE 提供 GMRES、BiCGStab 等迭代选项。
> 7. **与 [[线性多步法与 Dahlquist 等价定理]] 的联系**：BDF 仅是**收敛性**理论中"相容 + 零稳定"框架内的特定家族；其特殊价值在于 $A(\alpha)$-稳定带来的对刚性的鲁棒性。

$\blacksquare$
