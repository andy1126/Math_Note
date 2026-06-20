---
title: Chebyshev 多项式与最佳一致逼近
date: 2026-06-14
tags:
  - 数值分析
  - 插值与逼近
  - Chebyshev多项式
  - 最佳一致逼近
  - 交错定理
  - 最小最大性
---

# Chebyshev 多项式与最佳一致逼近

## 预备定义

> [!note] 定义 1（第一类 Chebyshev 多项式）
> 在区间 $[-1, 1]$ 上，第一类 Chebyshev 多项式定义为
> $$T_n(x) = \cos(n \arccos x), \quad n = 0, 1, 2, \ldots$$
> 等价地，令 $x = \cos\theta$（$\theta \in [0, \pi]$），则 $T_n(\cos\theta) = \cos(n\theta)$。
>
> 由三角恒等式 $\cos((n+1)\theta) + \cos((n-1)\theta) = 2\cos\theta \cos(n\theta)$ 立即得到**三项递推**：
> $$T_{n+1}(x) = 2x T_n(x) - T_{n-1}(x), \quad T_0(x) = 1, \; T_1(x) = x$$
>
> 由递推可知 $T_n$ 是次数恰为 $n$ 的多项式（这是非平凡事实，因为定义形式上仅是余弦的复合）。

> [!note] 定义 2（低阶显式表达式与首项系数）
> 由递推依次计算：
> - $T_2(x) = 2x^2 - 1$
> - $T_3(x) = 4x^3 - 3x$
> - $T_4(x) = 8x^4 - 8x^2 + 1$
> - $T_5(x) = 16 x^5 - 20 x^3 + 5x$
>
> 一般地，$T_n$ 的**首项系数**为 $2^{n-1}$（$n \geq 1$），$T_0$ 的首项系数为 $1$。这使得 $\tilde T_n(x) := T_n(x)/2^{n-1}$ 成为**首一**（monic）$n$ 次多项式。

> [!note] 定义 3（Chebyshev 节点 / 第一类零点）
> $T_n(x) = \cos(n\arccos x) = 0$ 当且仅当 $n\theta = (2k-1)\pi/2$，从而 $T_n$ 在 $[-1, 1]$ 上恰有 $n$ 个简单零点：
> $$x_k = \cos\left(\frac{(2k-1)\pi}{2n}\right), \quad k = 1, 2, \ldots, n$$
> 这些点称为 **Chebyshev 节点**，在区间内非均匀分布，**端点附近密集**，中部稀疏。

> [!note] 定义 4（Chebyshev 极值点 / 第二类节点）
> $\cos(n\theta)$ 在 $\theta = k\pi/n$（$k = 0, 1, \ldots, n$）处取极值 $\pm 1$，对应
> $$\xi_k = \cos\left(\frac{k\pi}{n}\right), \quad k = 0, 1, \ldots, n$$
> 共 $n + 1$ 个点（含端点 $\pm 1$）。在这些点处
> $$T_n(\xi_k) = (-1)^k$$
> 即 $T_n$ 在 $[-1, 1]$ 上以 $\pm 1$ **交替达到极值**——这是 Chebyshev 交错定理的雏形。

> [!note] 定义 5（带权正交性）
> Chebyshev 多项式族 $\{T_n\}$ 关于权函数 $w(x) = 1/\sqrt{1 - x^2}$ 在 $[-1, 1]$ 上正交：
> $$\int_{-1}^{1} \frac{T_m(x) T_n(x)}{\sqrt{1 - x^2}}\, dx = \begin{cases} 0 & m \neq n \\ \pi/2 & m = n \geq 1 \\ \pi & m = n = 0 \end{cases}$$
>
> **证明**：代换 $x = \cos\theta$，$dx = -\sin\theta\, d\theta$，$\sqrt{1-x^2} = \sin\theta$，化为
> $$\int_0^\pi \cos(m\theta) \cos(n\theta)\, d\theta$$
> 即三角函数族的标准正交性。

> [!note] 定义 6（最佳一致逼近问题）
> 设 $f \in C[a, b]$，$\mathbb{P}_n$ 为次数不超过 $n$ 的多项式空间。**最佳一致逼近多项式** $p^* \in \mathbb{P}_n$ 定义为
> $$\|f - p^*\|_\infty = \min_{p \in \mathbb{P}_n} \|f - p\|_\infty, \quad \|g\|_\infty := \max_{x \in [a, b]} |g(x)|$$
> 此问题属 **minimax 问题**，相对最小二乘逼近（$L^2$ 内积下投影）困难得多——$\|\cdot\|_\infty$ 范数不来自内积。

## 引理

> [!abstract] 引理 1（Chebyshev 最小最大性 / Markov 定理）
> 在所有首一 $n$ 次多项式中（$n \geq 1$），$\tilde{T}_n(x) := T_n(x)/2^{n-1}$ 在 $[-1, 1]$ 上具有**最小**的一致范数：
> $$\|\tilde{T}_n\|_\infty = \frac{1}{2^{n-1}} = \min_{\substack{p \in \mathbb{P}_n \\ \text{首一}}} \|p\|_\infty$$

**证明**（反证）：假设存在首一 $n$ 次多项式 $p$ 满足 $\|p\|_\infty < 1/2^{n-1}$。

考虑差 $q(x) := \tilde{T}_n(x) - p(x)$。由于 $\tilde T_n$ 与 $p$ 都首一，最高次项相消，$\deg q \leq n - 1$。

在 Chebyshev 极值点 $\xi_k = \cos(k\pi/n)$（$k = 0, 1, \ldots, n$）处：
$$\tilde{T}_n(\xi_k) = \frac{(-1)^k}{2^{n-1}}, \quad |\tilde T_n(\xi_k)| = \frac{1}{2^{n-1}}$$

而由假设 $|p(\xi_k)| < 1/2^{n-1}$。因此 $q(\xi_k)$ 的符号被 $\tilde T_n(\xi_k)$ 主导：
- 当 $k$ 偶，$\tilde T_n(\xi_k) = +1/2^{n-1}$，$q(\xi_k) > 0$；
- 当 $k$ 奇，$\tilde T_n(\xi_k) = -1/2^{n-1}$，$q(\xi_k) < 0$。

故 $q$ 在 $\xi_0, \xi_1, \ldots, \xi_n$ 共 $n + 1$ 个点上**符号交替** $n$ 次。由中间值定理 $q$ 在每两相邻 $\xi_k$ 之间至少有一个零点，共 $\geq n$ 个零点。但 $\deg q \leq n - 1$，故 $q \equiv 0$，与 $\|p\|_\infty < 1/2^{n-1} = \|\tilde T_n\|_\infty$ 矛盾。$\blacksquare$

> [!abstract] 引理 2（Chebyshev 节点是最优插值节点）
> 在 [[Lagrange插值误差估计|Lagrange 插值]] 误差公式
> $$f(x) - L_n(x) = \frac{f^{(n+1)}(\xi)}{(n+1)!} \omega(x), \quad \omega(x) = \prod_{k=0}^{n}(x - x_k)$$
> 中，节点多项式 $\omega$ 是首一 $(n+1)$ 次多项式。最小化 $\|\omega\|_\infty$ 的节点选择由引理 1 给出：
> $$\omega(x) = \tilde{T}_{n+1}(x) = T_{n+1}(x)/2^n$$
> 即节点 $x_k$ 取为 $T_{n+1}$ 的零点（Chebyshev 节点）：
> $$x_k = \cos\left(\frac{(2k+1)\pi}{2(n+1)}\right), \quad k = 0, 1, \ldots, n$$
> 此时 $\|\omega\|_\infty = 1/2^n$，**指数级**优于等距节点。

**注**：等距节点的 $\|\omega\|_\infty$ 增长为 $\sim n!/4^n \cdot (b-a)^{n+1}$，相对 $1/2^n$ 在大 $n$ 时差距巨大。这正是 **Runge 现象** 在等距节点出现而 Chebyshev 节点几乎无的根源。

## 主定理

> [!important] 定理（Chebyshev 交错定理 / Equi-oscillation Theorem）
> 设 $f \in C[a, b]$，$p^* \in \mathbb{P}_n$。则 $p^*$ 是 $f$ 在 $\mathbb{P}_n$ 中的**最佳一致逼近** $\iff$ 误差函数 $e(x) := f(x) - p^*(x)$ 在 $[a, b]$ 上至少存在 $n + 2$ 个点
> $$a \leq t_0 < t_1 < \cdots < t_{n+1} \leq b$$
> 满足
> $$e(t_k) = \sigma\, (-1)^k\, \|f - p^*\|_\infty, \quad k = 0, 1, \ldots, n + 1, \quad \sigma \in \{+1, -1\}$$
>
> 即 $e$ 以**等振幅、符号交替**地达到最大绝对值至少 $n + 2$ 次。
>
> 此外，最佳逼近多项式 $p^*$ **唯一存在**。

## 证明

记 $E := \|f - p^*\|_\infty$。

**充分性**：设存在 $n + 2$ 个交错点 $t_0 < t_1 < \cdots < t_{n+1}$ 使 $e(t_k) = \sigma(-1)^k E$。

反证：假设存在 $q \in \mathbb{P}_n$ 使 $\|f - q\|_\infty < E$。则在每个 $t_k$ 处：
$$|f(t_k) - q(t_k)| < E = |f(t_k) - p^*(t_k)|$$

考虑差 $r(x) := p^*(x) - q(x) \in \mathbb{P}_n$。在 $t_k$ 处：
$$r(t_k) = (f(t_k) - q(t_k)) - (f(t_k) - p^*(t_k))$$
- 第二项绝对值 $= E$，符号 $\sigma(-1)^k$
- 第一项绝对值 $< E$

故 $r(t_k)$ 的符号被第二项主导（第一项无法翻转），即 $\operatorname{sgn} r(t_k) = -\sigma(-1)^k$，**符号交替** $n + 1$ 次。

由中间值定理，$r$ 在 $[t_0, t_{n+1}]$ 上至少有 $n + 1$ 个零点。但 $\deg r \leq n$，故 $r \equiv 0$，即 $q = p^*$，与 $\|f - q\|_\infty < E$ 矛盾。

**必要性**（构造性反证）：设 $p^*$ 是最佳逼近。设误差 $e = f - p^*$ 的极值点（即 $|e(t)| = E$ 处）数 $\leq n + 1$，记为 $t_0 < \cdots < t_m$，$m \leq n$。

将 $[a, b]$ 按符号变化分段，构造低阶辅助多项式 $r \in \mathbb{P}_n$（次数 $\leq m \leq n$，故可在 $\mathbb{P}_n$ 中实现），使 $\operatorname{sgn} r(t_k) = \operatorname{sgn} e(t_k)$ 在所有极值点上一致。

取 $\delta > 0$ 充分小，令 $\tilde p := p^* + \delta r$。则
$$f - \tilde p = e - \delta r$$
在每个极值点附近 $|f - \tilde p| < E$；在远离极值点处由连续性 $|e| < E$ 留有余量，$\delta$ 小时不破坏。整体 $\|f - \tilde p\|_\infty < E$，与 $p^*$ 最佳矛盾。

**唯一性**：设 $p_1^*, p_2^*$ 均为最佳，$\|f - p_i^*\|_\infty = E$。令 $p_3 := (p_1^* + p_2^*)/2 \in \mathbb{P}_n$，则
$$\|f - p_3\|_\infty = \tfrac{1}{2}\|(f - p_1^*) + (f - p_2^*)\|_\infty \leq \tfrac{1}{2}(E + E) = E$$

故 $p_3$ 也是最佳。由充分性，$f - p_3$ 有 $n + 2$ 个等振幅交错点 $t_k$。在每 $t_k$ 处：
$$|f(t_k) - p_3(t_k)| = E$$
强制 $f(t_k) - p_1^*(t_k) = f(t_k) - p_2^*(t_k) = \pm E$（同号同值，否则三角不等式严格），即 $p_1^*(t_k) = p_2^*(t_k)$ 在 $n + 2$ 点。$\deg(p_1^* - p_2^*) \leq n$ 而有 $n + 2$ 个零点，故 $p_1^* \equiv p_2^*$。$\blacksquare$

## 总结

> [!info] 核心结果概览
> 1. **Chebyshev 多项式**：$T_n(\cos\theta) = \cos(n\theta)$，由三项递推生成；首项系数 $2^{n-1}$。
> 2. **最小最大性**：在所有首一 $n$ 次多项式中，$T_n/2^{n-1}$ 最小化 $\|\cdot\|_\infty$，最小值 $1/2^{n-1}$。
> 3. **节点最优性**：Chebyshev 节点最小化 Lagrange 余项中的节点多项式，**指数级**优于等距，抑制 Runge 现象。
> 4. **交错定理**：$p^*$ 最佳 $\iff$ 误差 $f - p^*$ 有 $\geq n + 2$ 个等振幅交错极值点；$p^*$ 唯一。
> 5. **正交性**：关于权 $1/\sqrt{1-x^2}$ 正交，区别于 [[Legendre多项式的正交性|Legendre]] 的等权 $w \equiv 1$。

## 应用

### 应用 1：$f(x) = e^x$ 在 $[-1, 1]$ 上最佳 1 次逼近

设 $p^*(x) = a + bx$，最佳 1 次逼近误差需有 $n + 2 = 3$ 个交错点。由 $e^x$ 严格凸，误差 $e(x) = e^x - a - bx$ 至多有 1 个内部极小（导数 $= 0$ 即 $e^x = b$），故交错点结构为：

$$t_0 = -1, \quad t_1 = x^* \in (-1, 1), \quad t_2 = 1$$

需 $e(-1) = e(1) = -e(x^*) = E$（或反号）。条件：
1. $e^{-1} - a + b = E$
2. $e^{1} - a - b = E$
3. $e^{x^*} - a - b x^* = -E$
4. $e'(x^*) = e^{x^*} - b = 0 \;\Rightarrow\; b = e^{x^*}$

由 (1)(2) 相减：$b = (e - e^{-1})/2 = \sinh 1 \approx 1.1752$。
由 (4)：$x^* = \ln b = \ln \sinh 1 \approx 0.1614$。
由 (1)(2) 相加：$2a = e + e^{-1} - 2E$，结合 (3)：
$$E = \frac{1}{2}\Big( \cosh 1 - \sinh 1 (1 + \ln \sinh 1)\Big) \approx 0.2788$$

对比 Taylor 多项式 $T_1(x) = 1 + x$ 在 $[-1, 1]$ 上的最大误差 $\max|e^x - 1 - x| = e - 2 \approx 0.7183$——**最佳逼近优 2.6 倍**。

### 应用 2：用 Chebyshev 节点插值 Runge 函数 $1/(1+25x^2)$

Runge 函数 $f(x) = 1/(1 + 25 x^2)$ 是经典反例。

| 节点类型 | $n$ | $\max\|f - L_n\|$ |
|---|---|---|
| 等距 | 10 | $\approx 1.92$（边界振荡发散）|
| 等距 | 20 | $\approx 60$（剧烈发散）|
| Chebyshev | 10 | $\approx 0.109$ |
| Chebyshev | 20 | $\approx 0.015$ |
| Chebyshev | 40 | $\approx 3 \times 10^{-4}$ |

Chebyshev 节点在 $n = 10$（11 个节点）时为：
$$x_k = \cos\left(\frac{(2k+1)\pi}{22}\right), \quad k = 0, 1, \ldots, 10$$

数值上 $x_0 \approx 0.9898$，$x_5 = 0$，$x_{10} \approx -0.9898$。

**关键观察**：由引理 2，$\|\omega\|_\infty = 1/2^{10} \approx 9.77 \times 10^{-4}$，但 $f^{(n+1)}$ 在虚轴极点 $\pm i/5$ 附近增长，故实际收敛速度由 Bernstein 椭圆决定，对 Runge 函数为 $\rho = 5(\sqrt{26} - 5) \approx 0.198$ 的几何级数，即误差 $\sim \rho^n$。

### 应用 3：Remez 算法（最佳逼近的迭代构造）

交错定理是存在性 + 刻画定理，但不直接给出 $p^*$。**Remez 第二算法**给出可计算实现：

1. **初值**：取 $n + 2$ 个节点 $t_0^{(0)} < \cdots < t_{n+1}^{(0)}$（典型为 Chebyshev 极值点 $\xi_k$）。
2. **求解线性系统**：设 $p = \sum_{j=0}^n c_j x^j$，引入未知振幅 $h$，求解
   $$f(t_k^{(s)}) - \sum_{j=0}^n c_j (t_k^{(s)})^j = (-1)^k h, \quad k = 0, 1, \ldots, n + 1$$
   共 $n + 2$ 方程 $n + 2$ 未知量 $(c_0, \ldots, c_n, h)$，给出当前 $p^{(s)}$ 与试探振幅 $h^{(s)}$。
3. **极值搜索**：在 $[a, b]$ 上找 $f - p^{(s)}$ 的所有极值点（实际 $\geq n + 2$ 个候选）。
4. **节点更新**：选取交错符号且绝对值最大的 $n + 2$ 个新节点 $t_k^{(s+1)}$。
5. **收敛**：当 $|h^{(s)}| \approx \|f - p^{(s)}\|_\infty$ 时停止。通常 2–10 次迭代二次收敛。

工业级实现：MATLAB **Chebfun** `remez`，Python **scipy.signal.remez**（数字滤波器设计）。

### 应用 4：Chebyshev 与 [[Legendre多项式的正交性|Legendre]] 对比

| 性质 | Chebyshev $T_n$ | Legendre $P_n$ |
|---|---|---|
| 权函数 $w(x)$ | $1/\sqrt{1-x^2}$ | $1$ |
| 区间 | $[-1, 1]$ | $[-1, 1]$ |
| 三项递推 | $T_{n+1} = 2x T_n - T_{n-1}$ | $(n+1) P_{n+1} = (2n+1) x P_n - n P_{n-1}$ |
| 节点用途 | 最佳一致逼近、Clenshaw–Curtis 求积 | Gauss 求积、$L^2$ 投影 |
| 极值分布 | 端点密集（避 Runge）| 内部分散 |
| 闭式 | $T_n(\cos\theta) = \cos n\theta$ | Rodrigues 公式 |

二者均为 **Sturm–Liouville 特征函数**，由不同权下的内积 $\langle f, g\rangle_w = \int_{-1}^{1} f g w\, dx$ 通过 Gram–Schmidt 自然产生。Chebyshev 优于 Legendre 在 $L^\infty$（一致）问题，Legendre 优于 Chebyshev 在 $L^2$（最小二乘、能量）问题。

## 证明思路总结

> [!tip] 核心思路与脉络
> - **桥梁**：$T_n(\cos\theta) = \cos(n\theta)$ 把多项式分析与三角分析直接连通，所有性质（递推、正交、零点、极值）都可由余弦的对应性质平移得到。
> - **最小最大性的本质**：首一 $n$ 次多项式构成仿射子集；$\tilde T_n$ 是其中 $\|\cdot\|_\infty$ 最小元，证法是**反证 + 中间值定理 + 次数限制**——这一三段论是逼近论标准技术。
> - **节点最优性**：把 Lagrange 余项的"节点多项式"$\omega$ 视为首一多项式，最优化即归约为引理 1，自动给出 Chebyshev 节点。
> - **交错定理证明套路**：误差函数若有 $n + 2$ 等振幅交错点，则任何更优逼近的差 $p^* - q$ 必符号交替 $n + 1$ 次，与 $\deg \leq n$ 矛盾。同样的"符号交替 + 中间值 + 次数限制"模式。
> - **Remez 算法**：交错定理的直接计算化身——猜节点、解线性系统、修正节点，二次收敛。
> - **与 [[Lagrange插值误差估计]] 衔接**：Lagrange 余项 $f - L_n = \omega f^{(n+1)}/(n+1)!$ 给出节点选择的准则，引理 2 完成最优化。
> - **与 [[Legendre多项式的正交性|Legendre]] 对比**：同为正交多项式，但权函数（即内积）不同决定了适用问题：$L^\infty$ minimax 用 Chebyshev，$L^2$ 投影/Gauss 求积用 Legendre。
> - **更高观点**：最佳一致逼近在抽象 Banach 空间 $C[a,b]$ 中是非内积的最小化问题，Chebyshev 是把它**显式化**的关键工具；这种"非自伴问题被特殊正交族驯服"的现象在数值分析中反复出现。

$\blacksquare$
