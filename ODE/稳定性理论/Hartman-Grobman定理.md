---
title: Hartman-Grobman 定理
date: 2026-04-11
tags:
  - 常微分方程
  - 动力系统
  - 双曲平衡点
  - 拓扑共轭
  - 线性化
  - Banach不动点定理
---

# Hartman-Grobman 定理

## 预备定义

> [!note] 双曲平衡点
> 对自治系统 $x' = f(x)$（$f \in C^1$），平衡点 $x^\ast$（$f(x^\ast) = 0$）称为**双曲的**（hyperbolic），若 Jacobi 矩阵 $A = Df(x^\ast)$ 的所有特征值的实部均不为零：
> $$\operatorname{Re}(\lambda_j) \neq 0 \quad \forall\, j = 1, \ldots, n.$$
> 即 $A$ 没有纯虚特征值（包括零）。

> [!note] 拓扑共轭
> 两个自治系统 $x' = f(x)$ 和 $y' = g(y)$ 在各自平衡点附近称为**拓扑共轭的**（topologically conjugate），若存在同胚 $h: U \to V$（$U, V$ 为平衡点的邻域），将一个系统的轨道映为另一个系统的轨道，且保持时间参数化：
> $$h(\varphi_t(x)) = \psi_t(h(x)),$$
> 其中 $\varphi_t, \psi_t$ 分别为两个系统的流。
>
> 拓扑共轭保持相图的所有定性特征：轨道的拓扑结构、稳定/不稳定流形、$\omega$-极限集等。

> [!note] 双曲线性映射
> 线性映射 $A: \mathbb{R}^n \to \mathbb{R}^n$ 称为**双曲的**，若 $A$ 的所有特征值的模均不等于 $1$。
>
> 此时 $\mathbb{R}^n$ 分解为 $A$-不变子空间 $E^s \oplus E^u$：
> - $E^s$（稳定子空间）：$A|_{E^s}$ 的特征值 $|\lambda| < 1$，即 $\|A^k|_{E^s}\| \to 0$；
> - $E^u$（不稳定子空间）：$A|_{E^u}$ 的特征值 $|\lambda| > 1$，即 $\|A^{-k}|_{E^u}\| \to 0$。
>
> 存在适应范数使得 $\|A_s\| \leq \mu < 1$ 且 $\|A_u^{-1}\| \leq \mu < 1$。

> [!note] 有界连续函数空间
> 记 $C_b(\mathbb{R}^n, \mathbb{R}^n)$ 为所有有界连续函数 $u: \mathbb{R}^n \to \mathbb{R}^n$ 的空间，赋以上确界范数 $\|u\|_\infty = \sup_x \|u(x)\|$。这是一个 Banach 空间。

---

## 定理

### 离散版本（微分同胚）

设 $A: \mathbb{R}^n \to \mathbb{R}^n$ 为双曲线性映射，$F = A + \phi$，其中 $\phi: \mathbb{R}^n \to \mathbb{R}^n$ 满足 $\phi(0) = 0$ 且 $\operatorname{Lip}(\phi)$ 充分小。则存在同胚 $h: \mathbb{R}^n \to \mathbb{R}^n$，使得

$$h \circ F = A \circ h,$$

即 $F$ 与 $A$ 拓扑共轭。且 $h = \operatorname{id} + u$，其中 $u \in C_b(\mathbb{R}^n, \mathbb{R}^n)$。

### 连续版本（微分方程）

设 $x^\ast = 0$ 为 $x' = f(x)$（$f \in C^1$）的双曲平衡点，$A = Df(0)$。则存在 $0$ 的邻域 $U$ 和同胚 $h: U \to h(U)$，使得在 $U$ 中

$$h(\varphi_t(x)) = e^{At}\, h(x),$$

其中 $\varphi_t$ 为非线性流。即**非线性系统在双曲平衡点附近拓扑共轭于其线性化 $y' = Ay$**。

> [!info] 定理的含义
> 双曲平衡点附近的相图与线性系统 $y' = Ay$ 的相图**拓扑等价**——鞍点仍是鞍点，稳定结点仍是稳定结点，稳定焦点仍是稳定焦点。"看特征值画相图"是有理论保障的。
>
> 但 $h$ 仅是同胚（连续双射），一般**不是微分同胚**。轨道的拓扑形状保持，但切线方向和速度可能改变。

---

## 证明（离散版本）

### 预处理：截断非线性项

原始的 $F = A + \phi$ 中 $\phi$ 仅在 $0$ 附近 Lipschitz 常数小。取光滑截断函数 $\chi$（$\chi = 1$ 在 $0$ 附近，$\chi = 0$ 在远处），令 $\tilde{\phi} = \chi \cdot \phi$。则 $\tilde{F} = A + \tilde{\phi}$ 在全空间上定义，$\operatorname{Lip}(\tilde{\phi})$ 可以任意小（缩小截断半径），且 $\tilde{F}$ 在 $0$ 附近与 $F$ 一致。

以下设 $\phi$ 已是全局定义的，$\operatorname{Lip}(\phi) \leq \varepsilon$（$\varepsilon$ 稍后选取），$\phi(0) = 0$。

$\square$

### 第一步：建立函数方程

设 $h = \operatorname{id} + u$（$u \in C_b$）。$h \circ F = A \circ h$ 即

$$F(x) + u(F(x)) = A(x + u(x)),$$

即 $(A + \phi)(x) + u(F(x)) = Ax + Au(x)$。化简：

$$u(F(x)) - Au(x) = -\phi(x). \quad \cdots (\ast)$$

记线性算子 $\mathcal{L}: C_b \to C_b$ 为 $\mathcal{L}(u) = u \circ A - Au$。则 $(\ast)$ 可写为

$$\mathcal{L}(u) = -\phi + [u \circ A - u \circ F]. \quad \cdots (\star)$$

$\square$

### 第二步（关键引理）：$\mathcal{L}$ 在 $C_b$ 上可逆

**断言**：$\mathcal{L}(u) = u \circ A - Au$ 是 $C_b(\mathbb{R}^n, \mathbb{R}^n)$ 上的有界可逆算子。

**证明**：利用双曲分解 $\mathbb{R}^n = E^s \oplus E^u$，将 $u = (u_s, u_u)$ 分量分别处理。取适应范数使得 $\|A_s\| \leq \mu < 1$，$\|A_u^{-1}\| \leq \mu < 1$。

对 $w = (w_s, w_u) \in C_b$，需解 $\mathcal{L}(u) = w$，即

$$u_s(Ax) - A_s u_s(x) = w_s(x), \quad u_u(Ax) - A_u u_u(x) = w_u(x).$$

**稳定分量**：将 $x$ 替换为 $A^{-1}x$：

$$u_s(x) = A_s u_s(A^{-1}x) + w_s(A^{-1}x).$$

迭代：$u_s(x) = \sum_{k=0}^{N-1} A_s^k\, w_s(A^{-(k+1)}x) + A_s^N u_s(A^{-N}x)$。

由 $\|A_s^N\| \leq \mu^N \to 0$ 和 $u_s$ 有界，余项趋于零。故

$$u_s(x) = \sum_{k=0}^{\infty} A_s^k\, w_s(A^{-(k+1)}x). \quad \cdots (S_s)$$

级数收敛（$\|A_s^k\| \leq \mu^k$），且 $\|u_s\|_\infty \leq \frac{1}{1-\mu}\|w_s\|_\infty$。

**不稳定分量**：由 $u_u(Ax) = A_u u_u(x) + w_u(x)$，得

$$u_u(x) = A_u^{-1}u_u(Ax) - A_u^{-1}w_u(x).$$

迭代：

$$u_u(x) = -\sum_{k=0}^{\infty} A_u^{-(k+1)}\, w_u(A^k x). \quad \cdots (S_u)$$

收敛（$\|A_u^{-(k+1)}\| \leq \mu^{k+1}$），且 $\|u_u\|_\infty \leq \frac{\mu}{1-\mu}\|w_u\|_\infty$。

综合两个分量，$\mathcal{L}^{-1}$ 存在且 $\|\mathcal{L}^{-1}\| \leq C_\mu$（仅依赖 $\mu$）。$\square$

### 第三步：压缩映射论证

将 $(\star)$ 改写为不动点方程：

$$u = \mathcal{L}^{-1}\!\big(-\phi + u \circ A - u \circ F\big) =: \mathcal{T}(u). \quad \cdots (\dagger)$$

**$\mathcal{T}$ 是 $C_b$ 上的压缩映射**：对 $u_1, u_2 \in C_b$，

$$\mathcal{T}(u_1) - \mathcal{T}(u_2) = \mathcal{L}^{-1}\!\big[(u_1 - u_2) \circ A - (u_1 - u_2) \circ F\big].$$

对任意 $x$：

$$\|(u_1 - u_2)(Ax) - (u_1 - u_2)(Fx)\| \leq \|u_1 - u_2\|_\infty \cdot 0 + \ldots$$

这里需要更细致的估计。实际上注意 $F = A + \phi$，故

$$\|(u_1 - u_2)(Ax) - (u_1 - u_2)(Ax + \phi(x))\|.$$

> [!info] 对 Lip 类函数的估计
> 在 Lip 类函数的空间 $C_b^{\text{Lip}}$（有界 Lipschitz 函数，$\|u\|' = \|u\|_\infty + \operatorname{Lip}(u)$）上工作。若 $\operatorname{Lip}(u_1 - u_2) \leq L$，则上式 $\leq L\|\phi(x)\| \leq L \varepsilon \|x\|$... 这不直接给出有界估计。
>
> 标准技巧：改在 $C_b$ 上工作，但利用如下事实。

采用另一种标准方法：直接在 $C_b$ 上定义 $\mathcal{T}$ 并验证压缩性。

将 $(\ast)$ 改写为

$$u \circ F = Au - \phi,$$

即 $u = (Au - \phi) \circ F^{-1}$（$F$ 为同胚，因 $\operatorname{Lip}(\phi) < 1$ 时 $F$ 是全局微分同胚）。定义

$$\mathcal{T}(u) = (Au - \phi) \circ F^{-1}. \quad \cdots (\dagger')$$

> [!important] $F^{-1}$ 的 Lipschitz 常数
> $F = A + \phi$ 可逆（$\phi$ 的 Lipschitz 常数 $\varepsilon$ 足够小），且 $\operatorname{Lip}(F^{-1}) \leq \frac{1}{\|A^{-1}\|^{-1} - \varepsilon}$。

验证 $\mathcal{T}$ 压缩（在 $C_b$ 的上确界范数下）：

$$\|\mathcal{T}(u_1) - \mathcal{T}(u_2)\|_\infty = \|A(u_1 - u_2) \circ F^{-1}\|_\infty = \|A(u_1 - u_2)\|_\infty.$$

等等，$\|A(u_1 - u_2) \circ F^{-1}\|_\infty = \sup_x \|A(u_1(F^{-1}(x)) - u_2(F^{-1}(x)))\|$。由 $F^{-1}$ 是满射，$= \sup_y \|A(u_1(y) - u_2(y))\| = \|A(u_1 - u_2)\|_\infty \leq \|A\| \|u_1 - u_2\|_\infty$。

这里 $\|A\|$ 未必 $< 1$（$A$ 有不稳定方向）。故此直接方法不给出压缩性。

正确的方法是回到分量分解。将 $(\ast)$ 分解为稳定/不稳定分量，分别构造不动点。

**稳定分量**：$u_s(Fx) = A_s u_s(x) - \phi_s(x)$。定义

$$\mathcal{T}_s(u_s)(x) = A_s u_s(x) - \phi_s(x) \text{ 的"逆推"}。$$

即将 $x$ 替换为 $F^{-1}(x)$：$u_s(x) = A_s u_s(F^{-1}x) - \phi_s(F^{-1}x)$。迭代：

$$u_s(x) = -\sum_{k=0}^{\infty} A_s^k\, \phi_s(F^{-(k+1)}x). \quad \cdots (\Sigma_s)$$

收敛（$\|A_s^k\| \leq \mu^k$），$\|u_s\|_\infty \leq \frac{\varepsilon}{1-\mu}\sup\|x\|$... 但这需要 $\phi$ 有界。由截断，$\phi$ 有界，故 $u_s \in C_b$。

**不稳定分量**：$u_u(Fx) = A_u u_u(x) - \phi_u(x)$，即 $u_u(x) = A_u^{-1}[u_u(Fx) + \phi_u(x)]$。迭代：

$$u_u(x) = \sum_{k=0}^{\infty} A_u^{-(k+1)}\, \phi_u(F^k x). \quad \cdots (\Sigma_u)$$

收敛（$\|A_u^{-(k+1)}\| \leq \mu^{k+1}$）。

$(\Sigma_s)$ 和 $(\Sigma_u)$ 直接给出 $u$ 的**显式公式**，无需抽象不动点论证。可直接验证 $u = (u_s, u_u)$ 满足 $(\ast)$。$\square$

### 第四步：$h = \operatorname{id} + u$ 是同胚

**$h$ 连续**：$u$ 由收敛级数定义，连续。$\square$

**$h$ 是双射**：构造逆映射。需要 $g = \operatorname{id} + v$ 使得 $g \circ A = F \circ g$，即

$$v(Ax) - Av(x) = \phi(x + v(x)). \quad \cdots (\ast\ast)$$

> [!important] 对称论证
> $(\ast\ast)$ 的结构与 $(\ast)$ 对称：同样是 $\mathcal{L}(v) = \text{r.h.s.}$。虽然右端依赖 $v$ 本身，但当 $\operatorname{Lip}(\phi) \leq \varepsilon$ 足够小时，右端关于 $v$ 的映射是压缩的（利用 $\mathcal{L}^{-1}$ 的有界性和 $\varepsilon$ 的小性），故由 Banach 不动点定理，$(\ast\ast)$ 有唯一解 $v \in C_b$。

设 $g = \operatorname{id} + v$ 解 $(\ast\ast)$。则：

$$h \circ g \circ A = h \circ F \circ g = A \circ h \circ g.$$

即 $h \circ g$ 与 $A$ 交换：$(h \circ g) \circ A = A \circ (h \circ g)$。写 $h \circ g = \operatorname{id} + w$，则

$$w(Ax) = Aw(x) \quad \forall\, x.$$

**断言 $w \equiv 0$**：分解 $w = (w_s, w_u)$。$w_s(Ax) = A_s w_s(x)$，迭代得 $w_s(A^n x) = A_s^n w_s(x)$。由 $w_s$ 有界和 $A^n x$ 遍历 $E^s$ 的扩大邻域（$A^{-1}$ 在 $E^s$ 上扩张），得 $w_s \equiv 0$。类似 $w_u \equiv 0$。

故 $h \circ g = \operatorname{id}$。对称地 $g \circ h = \operatorname{id}$。故 $h$ 是同胚，$h^{-1} = g$。$\square$

---

## 从离散到连续

### 推导连续版本

对 $x' = f(x)$（$f(0) = 0$，$A = Df(0)$ 双曲），取时间-1 映射 $F = \varphi_1$。则 $F(0) = 0$，$DF(0) = e^A$。

由 $A$ 双曲（特征值实部 $\neq 0$），$e^A$ 双曲（特征值模 $\neq 1$）。由离散版本，存在同胚 $h$ 使得

$$h \circ \varphi_1 = e^A \circ h. \quad \cdots (D)$$

**推广到所有 $t$**：定义 $h_t = e^{-At} \circ h \circ \varphi_t$。则

$$h_t \circ \varphi_1 = e^{-At} \circ h \circ \varphi_t \circ \varphi_1 = e^{-At} \circ h \circ \varphi_1 \circ \varphi_t = e^{-At} \circ e^A \circ h \circ \varphi_t = e^A \circ h_t.$$

故 $h_t$ 也满足 $(D)$。由离散版本中 $h$ 的唯一性（在 $\operatorname{id} + C_b$ 类中），$h_t = h$ 对一切 $t$。

故 $e^{-At} \circ h \circ \varphi_t = h$，即

$$h \circ \varphi_t = e^{At} \circ h \quad \forall\, t. \quad \blacksquare$$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明有三个核心要素：
>
> 1. **双曲分解**：$\mathbb{R}^n = E^s \oplus E^u$ 使算子 $\mathcal{L}(u) = u \circ A - Au$ 可逆——稳定分量"向前迭代"收敛，不稳定分量"向后迭代"收敛。$\mathcal{L}$ 的可逆性是双曲性的**分析体现**。
>
> 2. **显式级数**：共轭映射 $h = \operatorname{id} + u$ 由收敛级数直接给出：
> $$u_s(x) = -\sum_{k=0}^{\infty} A_s^k\, \phi_s(F^{-(k+1)}x), \quad u_u(x) = \sum_{k=0}^{\infty} A_u^{-(k+1)}\, \phi_u(F^k x).$$
> 稳定分量沿**反向**轨道求和（利用 $\|A_s^k\| \to 0$），不稳定分量沿**正向**轨道求和（利用 $\|A_u^{-k}\| \to 0$）。
>
> 3. **对称性得同胚**：$h$ 的逆由对称的函数方程给出；$h \circ h^{-1}$ 与 $A$ 交换且有界，双曲性迫使它为恒等。

> [!warning] 局限性与推广
> - **仅拓扑共轭，非光滑共轭**：$h$ 一般不可微（甚至不 Hölder 连续）。Sternberg 定理给出**光滑**共轭的充分条件（非共振条件）。
> - **双曲性不可去除**：若 $A$ 有纯虚特征值（非双曲），则线性化可能失效。经典例子：$x' = -y + x(x^2+y^2)$，$y' = x + y(x^2+y^2)$，线性化是中心（纯虚特征值），但非线性系统有不稳定螺旋。此时需要**中心流形定理**处理。
> - **与 [[Lyapunov稳定性定理]] 的关系**：Lyapunov 方法判定稳定性但不描述轨道结构；Hartman-Grobman 给出完整的**拓扑相图**，但仅限于双曲情形。两者互补。
> - **与 [[解对初值的可微依赖性]] 的关系**：变分方程 $\Phi' = Df(\varphi(t))\Phi$ 描述的线性近似正是 Hartman-Grobman 定理中"线性化"的精确含义。
