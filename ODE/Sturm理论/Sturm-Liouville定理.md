---
title: Sturm-Liouville 定理
date: 2026-04-11
tags:
  - 常微分方程
  - Sturm-Liouville问题
  - 特征值
  - 特征函数
  - 谱理论
  - Prüfer变换
  - 正交性
  - 完备性
---

# Sturm-Liouville 定理

## 预备定义

> [!note] 正则 Sturm-Liouville 问题
> 设 $p, q, w: [a, b] \to \mathbb{R}$ 连续，$p > 0$，$w > 0$，$p \in C^1[a,b]$。**Sturm-Liouville 特征值问题**为
> $$\mathcal{L}[y] \;=\; -\frac{d}{dx}\!\left(p(x)\,\frac{dy}{dx}\right) + q(x)\,y \;=\; \lambda\, w(x)\, y, \quad x \in [a,b], \quad \cdots (SL)$$
> 附以**分离型边界条件**：
> $$\alpha_1 y(a) + \alpha_2 y'(a) = 0, \quad \beta_1 y(b) + \beta_2 y'(b) = 0, \quad \cdots (BC)$$
> 其中 $(\alpha_1, \alpha_2) \neq (0,0)$，$(\beta_1, \beta_2) \neq (0,0)$。
>
> 满足 $(SL)$ + $(BC)$ 的非平凡解 $y$ 称为**特征函数**（eigenfunction），对应的 $\lambda$ 称为**特征值**（eigenvalue）。

> [!note] 加权内积
> 在 $L^2_w([a,b])$ 上定义加权内积
> $$\langle u, v \rangle_w = \int_a^b u(x)\, v(x)\, w(x)\, dx.$$

> [!note] Lagrange 恒等式
> 对任意 $u, v \in C^2[a,b]$，
> $$v\,\mathcal{L}[u] - u\,\mathcal{L}[v] = -\frac{d}{dx}\big[p(x)(v\,u' - u\,v')\big].$$
> 积分得
> $$\langle \mathcal{L}[u], v \rangle_w - \langle u, \mathcal{L}[v] \rangle_w = -\big[p(v\,u' - u\,v')\big]_a^b,$$
> 当 $u, v$ 均满足 $(BC)$ 时，右端为零（由分离型边界条件的代数性质）。故 $\mathcal{L}$ 在满足 $(BC)$ 的函数空间上是**自伴的**（self-adjoint）。

**Lagrange 恒等式的证明**：

$$v\,\mathcal{L}[u] = -v(pu')' + qvu, \quad u\,\mathcal{L}[v] = -u(pv')' + quv.$$

相减：$v\,\mathcal{L}[u] - u\,\mathcal{L}[v] = u(pv')' - v(pu')' = [(pv')u - (pu')v]' - pv'u' + pu'v'$。

最后两项抵消，得

$$v\,\mathcal{L}[u] - u\,\mathcal{L}[v] = \frac{d}{dx}\big[p(u\,v' - v\,u')\big] \cdot (-1). \quad \square$$

**边界项为零的验证**：设 $u, v$ 均满足 $\alpha_1 y(a) + \alpha_2 y'(a) = 0$。若 $\alpha_2 \neq 0$，则 $u'(a) = -(\alpha_1/\alpha_2)u(a)$，$v'(a) = -(\alpha_1/\alpha_2)v(a)$，故 $u(a)v'(a) - v(a)u'(a) = 0$。若 $\alpha_2 = 0$，则 $u(a) = v(a) = 0$，同样为零。右端点类似。$\square$

> [!abstract] Prüfer 变换
> 对 $(SL)$ 的非平凡解 $y$，定义**Prüfer 变量** $r(x) > 0$ 和 $\theta(x)$：
> $$y(x) = r(x)\sin\theta(x), \quad p(x)\,y'(x) = r(x)\cos\theta(x).$$
> 则 $\theta$ 满足一阶 ODE（**Prüfer 方程**）：
> $$\theta'(x) = \frac{1}{p(x)}\cos^2\theta(x) + (\lambda w(x) - q(x))\sin^2\theta(x). \quad \cdots (P)$$

**推导**：对 $y = r\sin\theta$ 求导：$y' = r'\sin\theta + r\theta'\cos\theta$。与 $py' = r\cos\theta$ 结合得 $r\theta'\cos\theta = r\cos\theta/p - r'\sin\theta$... 更直接地：

$\theta' = \frac{d}{dx}\arctan\!\left(\frac{y}{py'}\cdot p\right)$... 实际上，由 $\tan\theta = py'/ \cdots$

用另一种推导：对 $y = r\sin\theta$, $py' = r\cos\theta$ 交叉消去 $r$：

$$py' \cdot y = r^2 \sin\theta\cos\theta, \quad y^2 + (py')^2/p \cdot p = r^2.$$

更系统地：$y\cos\theta - py'\sin\theta/p \cdot p$... 

直接验证：对 $y = r\sin\theta$ 求导得 $y' = r'\sin\theta + r\theta'\cos\theta$。由 $py' = r\cos\theta$ 得 $r'\sin\theta + r\theta'\cos\theta = r\cos\theta/p$。

对 $py' = r\cos\theta$ 求导得 $(py')' = r'\cos\theta - r\theta'\sin\theta$。由 $(SL)$：$(py')' = (q - \lambda w)y = (q-\lambda w)r\sin\theta$。故 $r'\cos\theta - r\theta'\sin\theta = (q-\lambda w)r\sin\theta$。

从这两个方程消去 $r'$：第一个 $\times\cos\theta$ + 第二个 $\times\sin\theta$：

$$r\theta'\cos^2\theta + r\theta'\sin^2\theta = \frac{r\cos^2\theta}{p} - (q-\lambda w)r\sin^2\theta.$$

即 $r\theta' = r[\cos^2\theta/p + (\lambda w - q)\sin^2\theta]$，由 $r > 0$ 消去得 $(P)$。$\square$

> [!abstract] 紧致自伴算子的谱定理
> 设 $T: H \to H$ 为可分 Hilbert 空间上的紧致自伴算子。则：
> 1. $T$ 的特征值构成至多可数集，唯一的聚点为 $0$；
> 2. 不同特征值的特征向量正交；
> 3. $H$ 有由 $T$ 的特征向量组成的**完备正交基**。

---

## 定理

设 $(SL)$ + $(BC)$ 为正则 Sturm-Liouville 问题。则：

**(i)** 特征值均为**实数**。

**(ii)** 不同特征值的特征函数在 $L^2_w([a,b])$ 中**正交**。

**(iii)** 特征值构成严格递增无界序列
$$\lambda_1 < \lambda_2 < \lambda_3 < \cdots, \quad \lambda_n \to +\infty.$$
每个特征值是**简单的**（对应的特征函数在常数倍意义下唯一）。

**(iv)**（**振荡定理**）第 $n$ 个特征函数 $y_n$ 在 $(a, b)$ 内恰有 $n - 1$ 个零点。

**(v)** 特征函数 $\{y_n\}_{n=1}^{\infty}$ 在 $L^2_w([a,b])$ 中**完备**：对任意 $f \in L^2_w([a,b])$，
$$f = \sum_{n=1}^{\infty} c_n\, y_n, \quad c_n = \frac{\langle f, y_n \rangle_w}{\langle y_n, y_n \rangle_w},$$
收敛在 $L^2_w$ 范数下成立。

---

## 第(i)部分的证明：特征值为实数

设 $\lambda$ 为特征值，$y$ 为对应的特征函数。对 $(SL)$ 两边乘以 $\bar{y}$（复共轭）并积分：

$$\langle \mathcal{L}[y], y \rangle_w = \lambda \langle y, y \rangle_w.$$

取复共轭：$\overline{\langle \mathcal{L}[y], y \rangle_w} = \bar{\lambda}\, \langle y, y \rangle_w$。

由 $\mathcal{L}$ 的自伴性和 $p, q, w$ 为实值，$\langle \mathcal{L}[y], y \rangle_w$ 为实数。

> [!info] $\langle \mathcal{L}[y], y \rangle_w$ 为实数的验证
> 分部积分得
> $$\int_a^b \bar{y}\,\mathcal{L}[y]\, dx = \int_a^b p|y'|^2\, dx + \int_a^b q|y|^2\, dx - [p\bar{y}y']_a^b.$$
> 边界项由 $(BC)$ 为实数（或零），积分项亦为实数。

故 $\lambda = \bar{\lambda}$，即 $\lambda \in \mathbb{R}$。$\square$

---

## 第(ii)部分的证明：正交性

设 $\lambda \neq \mu$ 为两个特征值，$u, v$ 为对应的特征函数：$\mathcal{L}[u] = \lambda w u$，$\mathcal{L}[v] = \mu w v$。

由 Lagrange 恒等式（预备定义中已证边界项为零）：

$$\langle \mathcal{L}[u], v \rangle_w = \langle u, \mathcal{L}[v] \rangle_w.$$

即 $\lambda \langle u, v \rangle_w = \mu \langle u, v \rangle_w$。由 $\lambda \neq \mu$，得

$$\langle u, v \rangle_w = \int_a^b u(x)\, v(x)\, w(x)\, dx = 0. \quad \square$$

---

## 第(iii)部分的证明：特征值简单且离散

### 特征值简单

设 $y_1, y_2$ 是同一特征值 $\lambda$ 的两个特征函数。两者均满足相同的二阶 ODE $(SL)$ 和同一边界条件 $\alpha_1 y(a) + \alpha_2 y'(a) = 0$。

设 $\alpha_2 \neq 0$（$\alpha_2 = 0$ 的情形类似）。则 $y_i'(a) = -(\alpha_1/\alpha_2)y_i(a)$，即 $(y_i(a), y_i'(a))$ 在一维子空间上。不妨设 $y_2(a) = c\, y_1(a)$，则 $y_2'(a) = c\, y_1'(a)$。由 [[Picard-Lindelöf定理]] 的唯一性，$y_2 = c\, y_1$。

故每个特征值的特征空间为一维（**简单特征值**）。$\square$

### 特征值的存在与离散性（Prüfer 方法）

用 Prüfer 变换将问题转化为角度函数 $\theta$ 的分析。

#### 第一步：初始角度由左端边界条件确定

由 $\alpha_1 y(a) + \alpha_2 y'(a) = 0$，在 Prüfer 变量中：

$$\alpha_1 r\sin\theta(a) + \frac{\alpha_2}{p(a)} r\cos\theta(a) = 0.$$

这确定了初始角度 $\theta(a) = \theta_0$（模 $\pi$），选取 $\theta_0 \in [0, \pi)$。

$\square$

#### 第二步：特征值等价于 $\theta(b)$ 的特定值

右端边界条件 $\beta_1 y(b) + \beta_2 y'(b) = 0$ 类似地给出

$$\beta_1 \sin\theta(b) + \frac{\beta_2}{p(b)}\cos\theta(b) = 0,$$

即 $\theta(b) \equiv \theta_1 \pmod{\pi}$ 对某个固定的 $\theta_1 \in (0, \pi]$。

**$\lambda$ 是特征值当且仅当 $\theta(b; \lambda) = \theta_1 + (n-1)\pi$ 对某个 $n \in \mathbb{N}^+$。**

$\square$

#### 第三步：$\theta(b; \lambda)$ 关于 $\lambda$ 严格递增

**断言**：对固定的 $x$，角度 $\theta(x; \lambda)$ 关于 $\lambda$ 不减；在 $\theta = k\pi$ 处（解的零点处）严格递增。

> [!important] 角度函数的单调性——Sturm 比较定理的 Prüfer 版本
> 由 Prüfer 方程 $(P)$，$\lambda$ 增大使得 $\theta' = \cos^2\theta/p + (\lambda w - q)\sin^2\theta$ 增大（在 $\sin\theta \neq 0$ 的区域）。更精确地：比较 $\lambda_1 < \lambda_2$ 对应的角度 $\theta_1, \theta_2$，由 [[Sturm比较定理]] 的 Prüfer 版本，$\theta_2(x) \geq \theta_1(x)$ 对一切 $x$，且在每个 $\theta = k\pi$ 处严格增长。

$\square$

#### 第四步：$\theta(b; \lambda) \to 0^+$ 当 $\lambda \to -\infty$，$\theta(b; \lambda) \to +\infty$ 当 $\lambda \to +\infty$

**$\lambda \to -\infty$ 时**：Prüfer 方程 $(P)$ 中 $(\lambda w - q)\sin^2\theta$ 项趋于 $-\infty$，使 $\theta$ 强烈递减。$\theta$ 被"压低"，最终 $\theta(b; \lambda) < \theta_1$，无法满足右端边界条件。

**$\lambda \to +\infty$ 时**：$(\lambda w - q)\sin^2\theta$ 项趋于 $+\infty$，使 $\theta$ 快速增长。$\theta(b; \lambda)$ 穿越越来越多的 $\pi$ 的整数倍。

> [!info] 严格论证需要对 Prüfer 方程作精细估计
> 可以证明：$\theta(b; \lambda) \sim C\sqrt{\lambda}$ 当 $\lambda \to +\infty$（与 Weyl 渐近律一致）。

$\square$

#### 第五步：综合——特征值序列的存在

$\theta(b; \lambda)$ 是 $\lambda$ 的连续严格递增函数（由第三步和 Prüfer 方程解对参数的连续依赖性），值域从 $< \theta_1$ 到 $+\infty$。

由中值定理，$\theta(b; \lambda) = \theta_1 + (n-1)\pi$ 对每个 $n = 1, 2, 3, \ldots$ 恰有唯一的 $\lambda = \lambda_n$。

由 $\theta(b; \cdot)$ 严格递增，$\lambda_1 < \lambda_2 < \lambda_3 < \cdots$。

由 $\theta(b; \lambda) \to +\infty$，$\lambda_n \to +\infty$。$\square$

---

## 第(iv)部分的证明：振荡定理

**目标**：$y_n$（对应 $\lambda_n$）在 $(a, b)$ 内恰有 $n - 1$ 个零点。

### 零点与 Prüfer 角度的关系

$y(x) = r(x)\sin\theta(x)$ 在 $x_0$ 处为零当且仅当 $\theta(x_0) = k\pi$（$k \in \mathbb{Z}$）。

Prüfer 方程 $(P)$ 在 $\theta = k\pi$ 处给出 $\theta'(x_0) = 1/p(x_0) > 0$。

> [!important] $\theta$ 在每个 $k\pi$ 处严格递增
> 当 $\theta = k\pi$ 时 $\sin\theta = 0$，$(P)$ 简化为 $\theta' = \cos^2\theta/p = 1/p > 0$。故 $\theta$ 每到达 $k\pi$ 就严格穿越，不会"回弹"。

### 零点计数

$y_n$ 在 $(a, b)$ 内的零点数等于 $\theta$ 在 $(a, b)$ 内穿越 $k\pi$（$k \in \mathbb{Z}$）的次数。

由第(iii)部分，$\theta(a) = \theta_0 \in [0, \pi)$ 且 $\theta(b; \lambda_n) = \theta_1 + (n-1)\pi \in ((n-1)\pi, n\pi]$。

$\theta$ 从 $\theta_0 \in [0, \pi)$ 连续递增（在零点处严格穿越）到 $\theta_1 + (n-1)\pi \in ((n-1)\pi, n\pi]$。在此过程中，$\theta$ 恰好穿越 $\pi, 2\pi, \ldots, (n-1)\pi$，共 $n - 1$ 次。

故 $y_n$ 在 $(a, b)$ 内恰有 $n - 1$ 个零点。$\square$

---

## 第(v)部分的证明：完备性

完备性的证明需要泛函分析工具。核心思路：构造 $\mathcal{L}$ 的逆算子，证明它是 $L^2_w$ 上的紧致自伴算子，再应用谱定理。

### 第一步：Green 函数的存在

取 $\mu$ 不是特征值（例如取 $\mu < \lambda_1$）。考虑非齐次问题

$$\mathcal{L}[y] - \mu\, w\, y = w\, f, \quad y \text{ 满足 } (BC). \quad \cdots (\dagger)$$

由 $\mu$ 不是特征值，齐次问题仅有零解，故由 Fredholm 择一定理，$(\dagger)$ 对每个 $f \in C[a,b]$ 有唯一解。此解可表示为

$$y(x) = \int_a^b G(x, \xi)\, f(\xi)\, w(\xi)\, d\xi = (Tf)(x),$$

其中 $G(x, \xi)$ 为 **Green 函数**（依赖于 $\mu$）。

> [!info] Green 函数的构造
> 设 $\phi$ 为满足左端边界条件的 $(\mathcal{L} - \mu w)y = 0$ 的非平凡解，$\psi$ 为满足右端边界条件的非平凡解。由 $\mu$ 非特征值，$\phi$ 和 $\psi$ 线性无关。Green 函数为
> $$G(x, \xi) = \begin{cases} \dfrac{\phi(x)\,\psi(\xi)}{p(\xi)\,W(\xi)}, & a \leq x \leq \xi, \\[6pt] \dfrac{\phi(\xi)\,\psi(x)}{p(\xi)\,W(\xi)}, & \xi \leq x \leq b, \end{cases}$$
> 其中 $W = \phi\psi' - \phi'\psi$ 为 Wronskian。由 [[Liouville公式]]，$p W = \text{const} \neq 0$。

$\square$

### 第二步：$T$ 是 $L^2_w([a,b])$ 上的紧致自伴算子

**自伴性**：$G(x, \xi) = G(\xi, x)$（Green 函数对称），故

$$\langle Tf, g \rangle_w = \int\!\!\int G(x,\xi)\, f(\xi)\, g(x)\, w(\xi)\, w(x)\, d\xi\, dx = \langle f, Tg \rangle_w.$$

**紧致性**：$G$ 在 $[a,b]^2$ 上连续（虽在对角线上导数跳跃，但函数值连续），故 $T$ 是 Hilbert-Schmidt 积分算子，从而紧致。

$\square$

### 第三步：$T$ 的特征值与 $\mathcal{L}$ 的特征值的关系

$Tf = y$ 意味着 $(\mathcal{L} - \mu w)y = wf$。若 $f = \nu y$（$y$ 是 $T$ 的特征函数），则

$$\mathcal{L}[y] = \mu\, w\, y + \nu^{-1}\, w\, y = (\mu + \nu^{-1})\, w\, y.$$

故 $y$ 是 $\mathcal{L}$ 的特征函数，对应特征值 $\lambda = \mu + 1/\nu$。

反过来，$\mathcal{L}$ 的每个特征值 $\lambda_n \neq \mu$ 对应 $T$ 的特征值 $\nu_n = 1/(\lambda_n - \mu)$。

$\square$

### 第四步：应用紧致自伴算子的谱定理

由谱定理，$T$ 的特征函数构成 $L^2_w([a,b])$ 的完备正交系。

由第三步，$T$ 的特征函数恰好是 $\mathcal{L}$ 的特征函数 $\{y_n\}$。

故 $\{y_n\}_{n=1}^{\infty}$ 在 $L^2_w([a,b])$ 中**完备**：对任意 $f \in L^2_w$，

$$f = \sum_{n=1}^{\infty} \frac{\langle f, y_n \rangle_w}{\langle y_n, y_n \rangle_w}\, y_n,$$

收敛在 $L^2_w$ 范数下成立。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> Sturm-Liouville 定理的五个结论各有其核心工具：
>
> | 结论 | 核心工具 |
> |------|----------|
> | (i) 特征值实 | 自伴性（Lagrange 恒等式） |
> | (ii) 正交性 | 自伴性 + $\lambda \neq \mu$ |
> | (iii) 离散性 | Prüfer 变换：$\theta(b;\lambda)$ 严格递增且值域无界 |
> | (iv) 振荡定理 | Prüfer 角度穿越 $k\pi$ 的计数 |
> | (v) 完备性 | Green 函数 → 紧致自伴算子 → 谱定理 |
>
> **Prüfer 变换**是贯穿 (iii)(iv) 的灵魂：它将二阶非线性特征值问题化为一阶角度方程 $\theta' = \cos^2\theta/p + (\lambda w - q)\sin^2\theta$，使得零点计数变成了角度穿越的简单计数。
>
> **完备性**的证明则跨越了从 ODE 到泛函分析的桥梁：将微分算子 $\mathcal{L}$ 的谱问题转化为紧致积分算子 $T$ 的谱问题，再借助 Hilbert 空间的谱定理一举解决。

> [!warning] 推广与联系
> - **奇异 Sturm-Liouville 问题**：当区间无界（如 $[0, \infty)$）或 $p(a) = 0$（如 Bessel 方程）时，谱可能包含连续部分，特征值未必全离散。Weyl 的极限点/极限圆分类处理此情形。
> - **经典特殊函数**：Legendre、Hermite、Laguerre、Chebyshev 多项式均为特定 SL 问题的特征函数。它们的正交性和完备性是 SL 定理的直接推论。
> - **与 Fourier 级数的关系**：$-y'' = \lambda y$（$y(0) = y(\pi) = 0$）是最简单的 SL 问题，特征函数为 $\sin(nx)$，SL 定理的完备性即 Fourier 正弦级数的完备性。
> - **与已有笔记的关联**：
>   - 振荡定理 (iv) 是 [[Sturm比较定理]] 的精细化：不同特征值对应不同的 $q_{\text{eff}} = q - \lambda w$，$\lambda$ 越大 $q_{\text{eff}}$ 越小，解振荡越快（零点越多）。
>   - Green 函数中用到 [[Liouville公式]] 保证 Wronskian 非零。
>   - 特征值的简单性用到 [[Picard-Lindelöf定理]] 的唯一性。
