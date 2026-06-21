---
title: 两点边值问题与 Green 函数构造
date: 2026-06-20
tags:
  - 微分方程
  - ODE
  - 边值问题
  - Green函数
  - Sturm-Liouville
---

# 两点边值问题与 Green 函数构造

## 预备定义

> [!note] 两点边值问题（two-point boundary value problem, BVP）
> 考虑二阶线性 ODE 配上在区间 $[a, b]$ 两端各一个边界条件：
> $$\begin{cases} \mathcal{L} y := -\big(p(x)\, y'\big)' + q(x)\, y = f(x), & x \in (a, b), \\[4pt] \alpha_1 y(a) + \alpha_2 y'(a) = 0, \\[4pt] \beta_1 y(b) + \beta_2 y'(b) = 0, \end{cases} \quad \cdots (\mathrm{BVP})$$
> 其中 $p \in C^1[a, b],\ p > 0$；$q, f \in C[a, b]$；边界系数满足 $(\alpha_1, \alpha_2) \neq (0,0)$ 且 $(\beta_1, \beta_2) \neq (0,0)$。边界条件为**齐次**（右端为 $0$）；若 $f \equiv 0$ 称为齐次 BVP，否则为非齐次 BVP。

> [!note] Green 函数（Green's function）
> 对于 (BVP) 中的算子 $\mathcal{L}$ 和齐次边界条件，若存在函数 $G(x, \xi)$ 定义在 $[a, b] \times [a, b]$ 上，使得对任意 $f \in C[a, b]$，
> $$y(x) = \int_a^b G(x, \xi)\, f(\xi)\, d\xi$$
> 是 (BVP) 的唯一解，则称 $G$ 为该边值问题的 **Green 函数**。

> [!note] 自伴算子（self-adjoint / formally self-adjoint）
> 算子 $\mathcal{L} y = -(p y')' + q y$ 在齐次边界条件下满足 Lagrange 恒等式
> $$\int_a^b \big(u \mathcal{L} v - v \mathcal{L} u\big) = \Big[ p(u' v - u v') \Big]_a^b.$$
> 当 $u, v$ 均满足齐次边界条件时，右端边界项为零，故 $\langle \mathcal{L} u, v \rangle = \langle u, \mathcal{L} v \rangle$，称 $\mathcal{L}$ 在此边条件下**自伴**。自伴性是 Green 函数对称性 $G(x, \xi) = G(\xi, x)$ 的根源。

> [!abstract] 引理：齐次 BVP 的 Fredholm 二择一
> 对于 (BVP) 的齐次情形（$f \equiv 0$），要么只有零解 $y \equiv 0$，要么存在非零解（此时 $\lambda = 0$ 是本征值）。设齐次 BVP 只有零解，则非齐次 BVP 对任意 $f$ 存在唯一解。详见 [[Sturm-Liouville定理]]。

> [!abstract] 引理：常数变易法的基本解组
> 对齐次方程 $\mathcal{L} y = 0$，存在两个线性独立解 $y_1, y_2$（基本解组），其 Wronskian $W = y_1 y_2' - y_1' y_2$ 满足 Abel 公式。详见 [[Wronskian与Abel公式]]。

---

## 定理

设齐次 BVP（$f \equiv 0$）只有零解。则：

**(i)（Green 函数的存在唯一性）** 存在唯一的函数 $G(x, \xi)$ 满足：
1. $G$ 在 $[a, b] \times [a, b]$ 上连续；
2. 对每个固定 $\xi \in (a, b)$，$G(\cdot, \xi)$ 在 $[a, \xi)$ 和 $(\xi, b]$ 上分别满足 $\mathcal{L}_x G = 0$；
3. 对每个固定 $\xi$，$G(\cdot, \xi)$ 满足齐次边界条件（关于 $x$）；
4. **跳跃条件**：$\partial_x G$ 在 $x = \xi$ 处有跳跃
   $$\lim_{x \to \xi^+} \partial_x G(x, \xi) - \lim_{x \to \xi^-} \partial_x G(x, \xi) = -\frac{1}{p(\xi)}.$$

**(ii)（解的积分表示）** (BVP) 的唯一解由
$$y(x) = \int_a^b G(x, \xi)\, f(\xi)\, d\xi$$
给出，即 $G$ 是 $\mathcal{L}$ 在给定边条件下的积分核（右逆）。

**(iii)（对称性）** $G(x, \xi) = G(\xi, x)$。

**(iv)（构造公式）** $G$ 可显式构造：
$$G(x, \xi) = \frac{1}{p(\xi)\, W(\xi)} \begin{cases} u(x)\, v(\xi), & a \leq x \leq \xi, \\ u(\xi)\, v(x), & \xi \leq x \leq b, \end{cases}$$
其中 $u$ 为 $\mathcal{L} y = 0$ 满足 $x = a$ 处齐次边条件的非零解，$v$ 为满足 $x = b$ 处齐次边条件的非零解。

---

## 证明

### 第(i)部分：Green 函数的构造

#### 第一步：取两端的基本解

设 $u \not\equiv 0$ 满足 $\mathcal{L} u = 0$ 及 $x = a$ 处的齐次边条件 $\alpha_1 u(a) + \alpha_2 u'(a) = 0$。
设 $v \not\equiv 0$ 满足 $\mathcal{L} v = 0$ 及 $x = b$ 处的齐次边条件 $\beta_1 v(b) + \beta_2 v'(b) = 0$。

> [!important] $u$ 与 $v$ 线性独立
> 若 $u$ 与 $v$ 线性相关（$v = c u$），则 $u$ 同时满足两端齐次边界条件，即 $u$ 是齐次 BVP 的非零解——与假设（齐次 BVP 只有零解）矛盾。故 $u, v$ 线性独立，其 Wronskian $W = u v' - u' v \neq 0$。

#### 第二步：设拼接形式

对每个固定 $\xi \in (a, b)$，令
$$G(x, \xi) = \begin{cases} A(\xi)\, u(x), & a \leq x < \xi, \\ B(\xi)\, v(x), & \xi < x \leq b. \end{cases}$$

两段各自满足 $\mathcal{L}_x G = 0$（因 $u, v$ 是齐次解），且各自满足所在端的边界条件。

#### 第三步：确定 $A(\xi), B(\xi)$

施加 $x = \xi$ 处的连续性条件与跳跃条件：

**(a) 连续性** $G(\xi^+, \xi) = G(\xi^-, \xi)$：
$$A(\xi)\, u(\xi) = B(\xi)\, v(\xi). \quad \cdots (1)$$

**(b) 跳跃条件**：$\partial_x G(\xi^+, \xi) - \partial_x G(\xi^-, \xi) = -1 / p(\xi)$：
$$B(\xi)\, v'(\xi) - A(\xi)\, u'(\xi) = -\frac{1}{p(\xi)}. \quad \cdots (2)$$

(1)(2) 构成关于 $A, B$ 的 $2 \times 2$ 线性方程组：
$$\begin{pmatrix} u(\xi) & -v(\xi) \\ u'(\xi) & -v'(\xi) \end{pmatrix} \begin{pmatrix} A \\ B \end{pmatrix} = \begin{pmatrix} 0 \\ 1/p(\xi) \end{pmatrix}.$$

行列式 $= -u v' + u' v = -W(\xi)$。由 Cramer 规则：
$$A(\xi) = \frac{\det\begin{pmatrix} 0 & -v \\ 1/p & -v' \end{pmatrix}}{-W} = \frac{v(\xi)}{p(\xi)\, W(\xi)},$$
$$B(\xi) = \frac{\det\begin{pmatrix} u & 0 \\ u' & 1/p \end{pmatrix}}{-W} = \frac{u(\xi)}{p(\xi)\, W(\xi)}.$$

代入即得构造公式 **(iv)**。唯一性由构造过程的每一步均确定（$u, v$ 至标量倍数唯一）保证。$\square$

### 第(ii)部分：积分表示给出 (BVP) 的解

本部分验证 $y(x) = \int_a^b G(x, \xi) f(\xi) d\xi$ 满足 (BVP)。将积分在 $x$ 处断开：
$$y(x) = \int_a^x G(x, \xi) f(\xi)\, d\xi + \int_x^b G(x, \xi) f(\xi)\, d\xi.$$

在第一项中 $x \geq \xi$，$G = \frac{u(\xi) v(x)}{p W(\xi)}$；第二项中 $x \leq \xi$，$G = \frac{u(x) v(\xi)}{p W(\xi)}$。对 $x$ 求导（含参变量积分求导 + 上下限贡献），跳跃条件精确抵消 $y''$ 中的 $\delta$ 分布，得到 $\mathcal{L} y = f$。

> [!info] 完整验证概要
> 将 $G$ 的拼接式代入，$y(x) = v(x) \int_a^x \frac{u f}{p W} d\xi + u(x) \int_x^b \frac{v f}{p W} d\xi$。对 $x$ 求导两次，$y''$ 中出现的额外项 $[G_x(x, x^-) - G_x(x, x^+)] f(x) = f(x)/p(x)$ 正好使 $\mathcal{L} y = f$。边界条件由 $u$ 在 $a$ 端、$v$ 在 $b$ 端各自满足齐次边条件而自动满足。$\square$

### 第(iii)部分：对称性

由构造公式，$G(x, \xi) = \frac{1}{p(\xi) W(\xi)} \min\text{-}\max$ 形式。由 Abel 公式，
$$p(x) W(x) = \text{常数}.$$

事实上 $\frac{d}{dx}(p W) = p' W + p W' = p' W + p(-p W/p) = 0$（此处 $W$ 满足的一阶方程来自系数标准化后）。故 $p(\xi) W(\xi) = p(x) W(x)$ 为常数。于是
$$G(x, \xi) = \frac{1}{pW} \cdot \begin{cases} u(x) v(\xi), & x \leq \xi \\ u(\xi) v(x), & x \geq \xi \end{cases} = G(\xi, x). \quad \square$$

> [!important] 对称性的物理意义
> $G(x, \xi) = G(\xi, x)$ 即"在 $\xi$ 处施加单位力，在 $x$ 处产生的位移 = 在 $x$ 处施加单位力，在 $\xi$ 处产生的位移"——这是**Maxwell 互易定理**（Betti 互等定理）的一维形式，根源是算子 $\mathcal{L}$ 的自伴性。

---

## 一般解法（算法流程）

> [!tip] 构造 Green 函数 $G(x, \xi)$ 的步骤
> 1. 将方程写成自伴形式 $\mathcal{L} y := -(p y')' + q y = f$；
> 2. 求 $\mathcal{L} y = 0$ 的两个线性独立解（基本解组）；
> 3. 找出满足 $x = a$ 边条件的解 $u$，满足 $x = b$ 边条件的解 $v$；
> 4. 计算 $p(\xi) W(\xi)$（为常数）；
> 5. 套公式 $G(x, \xi) = \frac{1}{pW} \begin{cases} u(x) v(\xi), & x \leq \xi \\ u(\xi) v(x), & x \geq \xi \end{cases}$；
> 6. 解为 $y(x) = \int_a^b G(x, \xi) f(\xi) d\xi$。
>
> 具体计算见 [[Green函数例题]]。

---

## 证明思路总结

> [!tip] 关键思想
> Green 函数是微分算子 $\mathcal{L}$（配齐次边条件）的**积分逆**。构造的核心是一句话：
>
> **"在 $\xi$ 的左右两侧分别取满足各自最近端边界条件的齐次解，在 $\xi$ 处用连续性 + $1/p$ 跳跃拼接。"**
>
> 跳跃条件 $-1/p(\xi)$ 的来源：$\mathcal{L} G = \delta(x - \xi)$。对 $-(p G')' + q G = \delta$ 两端在 $[\xi^-, \xi^+]$ 上积分，$q G$ 的积分 $\to 0$（$G$ 连续），剩下 $-[p G']_{\xi^-}^{\xi^+} = 1$，即跳跃量 $= -1/p(\xi)$。
>
> Green 函数的存在性等价于**齐次 BVP 只有零解**（Fredholm 二择一），即 $\lambda = 0$ 不是 $\mathcal{L}$ 在给定边条件下的本征值。

> [!info] 与常数变易法的关系
> 取 $u = y_1, v = y_2$ 为齐次方程的任意基本解组，则 Green 函数表达式可重写为常数变易法的"分段卷积"形式：
> $$y(x) = y_1(x) \int_a^x \frac{y_2 f}{pW} d\xi + y_2(x) \int_x^b \frac{y_1 f}{pW} d\xi.$$
> 这正是 [[常数变易法]] 特解公式配上 BVP 特有的积分限（由边界条件确定）。Green 函数无非是把积分限的选择"编码"进核 $G$。

> [!info] 一维 ⇒ 高维
> 上述构造法对一维 Sturm-Liouville 算子最为干净。高维（$\Delta + k^2$ 等）Green 函数同样满足 $-\Delta_x G = \delta(x - \xi)$ + 齐次边条件，需借助本征函数展开或镜像法构造——见 [[本征值展开求解非齐次SL问题]]。
