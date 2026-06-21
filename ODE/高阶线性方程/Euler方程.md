---
title: Euler 方程
date: 2026-06-20
tags:
  - 微分方程
  - ODE
  - 高阶线性方程
  - Euler方程
  - Cauchy-Euler
  - 等维度方程
---

# Euler 方程

## 预备定义

> [!note] Euler 方程（Cauchy–Euler / 等维度方程）
> 形如
> $$x^n y^{(n)} + a_{n-1} x^{n-1} y^{(n-1)} + \cdots + a_1 x y' + a_0 y = 0, \quad x > 0 \quad \cdots (\mathrm{E})$$
> 的方程称为 **Euler 方程**（或 Cauchy–Euler 方程、等维度方程 equidimensional equation），其中 $a_0, \ldots, a_{n-1} \in \mathbb{R}$ 为常数。
>
> 特征：第 $k$ 阶导数 $y^{(k)}$ 的系数乘了 $x^k$，使每个项在缩放变换 $x \mapsto \lambda x$ 下具有**相同的量纲**（dimension），故得"等维度"之名。

> [!note] 指标方程（indicial equation）
> 对 (E) 作试探解 $y = x^r$（$r \in \mathbb{C}$），代入后提取因子 $x^r$，所得关于 $r$ 的**代数方程**称为 (E) 的**指标方程**。该名称与 [[正则奇点与Frobenius方法]] 中的"指标方程"一致——事实上 Euler 方程是所有系数 $x^k a_{n-k}(x)$ 为常数（即 $a_{n-k}(x)$ 为纯 $1/x^{k}$ 形式）的正则奇点方程的特殊情形。

> [!note] 算子 $\vartheta = x D$
> 记 $\vartheta := x \dfrac{d}{dx}$（即 $x D$）。其在多项式上的作用为 $\vartheta(x^r) = r x^r$。算子 $\vartheta$ 是 Euler 方程的自然语言：幂函数 $x^r$ 是 $\vartheta$ 的特征函数（特征值 $r$）。

> [!abstract] 引理：$\vartheta^k$ 的递推公式
> $$\vartheta(x^r) = r x^r,\quad \vartheta^2(x^r) = r^2 x^r,\quad \ldots,\quad \vartheta^k(x^r) = r^k x^r.$$
> 且 $x^k y^{(k)}$ 可通过 $\vartheta$ 的多项式表示：
> $$x y' = \vartheta y,\quad x^2 y'' = \vartheta(\vartheta - 1) y,\quad x^3 y''' = \vartheta(\vartheta - 1)(\vartheta - 2) y,$$
> 一般地 $x^k y^{(k)} = \vartheta(\vartheta - 1) \cdots (\vartheta - k + 1) y$。

> [!abstract] 引理：常系数齐次方程的解法
> 方程 $\sum b_k v^{(k)} = 0$（常系数）的通解由特征方程 $p(r) = \sum b_k r^k = 0$ 的根及其重数确定。详见 [[常系数齐次线性方程与特征方程]]。

---

## 定理

考虑 Euler 方程
$$x^n y^{(n)} + a_{n-1} x^{n-1} y^{(n-1)} + \cdots + a_1 x y' + a_0 y = 0, \quad x > 0. \quad \cdots (\mathrm{E})$$

**(i)（代换 $x = e^t$ 化为常系数）** 令 $x = e^t$（$t \in \mathbb{R}$），$v(t) := y(e^t)$。则 (E) 等价于关于 $v$ 的 **$n$ 阶常系数齐次线性方程**，其系数仅依赖于 $a_0, \ldots, a_{n-1}$。

**(ii)（试探解 $y = x^r$ 与指标方程）** 将 $y = x^r$ 代入 (E)，两端除以 $x^r$ 后得指标方程
$$r(r-1)\cdots(r-n+1) + a_{n-1} r(r-1)\cdots(r-n+2) + \cdots + a_1 r + a_0 = 0. \quad \cdots (\mathrm{Ind})$$

**(iii)（根与解的对应）** 根据指标方程根的类型，对应的实解为：
| 根的类型 | 重数 | 贡献的实解（$x > 0$） |
|---|---|---|
| 单实根 $r$ | $1$ | $x^r$ |
| $m$ 重实根 $r$ | $m$ | $x^r,\ x^r \ln x,\ \ldots,\ x^r (\ln x)^{m-1}$ |
| 单对复根 $r = \alpha \pm i\beta$ | $1$ | $x^\alpha \cos(\beta \ln x),\ x^\alpha \sin(\beta \ln x)$ |
| $m$ 重复根 $\alpha \pm i\beta$ | $m$ | $x^\alpha (\ln x)^k \cos(\beta \ln x),\ x^\alpha (\ln x)^k \sin(\beta \ln x),\ k=0,\ldots,m-1$ |

全部 $n$ 个解线性独立，构成基本解组。

---

## 第(i)部分的证明：化为常系数

### 第一步：代换 $x = e^t$

设 $x > 0$，令 $x = e^t$（即 $t = \ln x$），$v(t) := y(e^t) = y(x)$。由链式法则，
$$y'(x) = \frac{dv}{dt}\cdot\frac{dt}{dx} = v'(t)\cdot\frac{1}{x}.$$

故 $x y'(x) = v'(t) = \vartheta y$。

### 第二步：高阶导数的转化

二阶：
$$y'' = \frac{d}{dx}\!\left(\frac{v'}{x}\right) = \frac{v'' \cdot (1/x) \cdot (1/x) - v' \cdot (1/x^2)}{1} = \frac{v'' - v'}{x^2}.$$

故 $x^2 y'' = v''(t) - v'(t) = \vartheta(\vartheta - 1) y$。

由引理归纳可得：对任意 $k$，
$$x^k y^{(k)}(x) = \vartheta(\vartheta - 1) \cdots (\vartheta - k + 1)\, v(t) =: P_k(\vartheta)\, v(t).$$

### 第三步：写出 $v(t)$ 的常系数方程

将各项 $x^k y^{(k)} = P_k(\vartheta) v$ 代入 (E)：
$$\sum_{k=0}^n a_k\, P_k(\vartheta)\, v = 0,$$

其中 $a_n = 1$ 且 $P_n(\vartheta) = \vartheta(\vartheta - 1)\cdots(\vartheta - n + 1)$。由于 $\vartheta = d/dt$（在自变量 $t$ 下），$P_k(\vartheta)$ 是 $\vartheta$ 的 $k$ 次多项式，展开后得到关于 $v$ 的 $n$ 阶**常系数**齐次线性方程
$$v^{(n)}(t) + b_{n-1} v^{(n-1)}(t) + \cdots + b_1 v'(t) + b_0 v(t) = 0,$$

其中 $b_j$ 由 $a_k$ 经算子多项式 $P_k(r)$ 展开并合并同类项得到。$\square$

> [!info] 二阶与三阶的具体公式
> - **$n = 2$**：$x^2 y'' + a_1 x y' + a_0 y = 0 \;\xrightarrow{x=e^t}\; \ddot{v} + (a_1 - 1) \dot{v} + a_0 v = 0$。
> - **$n = 3$**：$x^3 y''' + a_2 x^2 y'' + a_1 x y' + a_0 y = 0 \;\xrightarrow{x=e^t}\; \dddot{v} + (a_2 - 3) \ddot{v} + (a_1 - a_2 + 2) \dot{v} + a_0 v = 0$。

---

## 第(ii)部分的证明：指标方程

将 $y = x^r$ 直接代入 (E)。由 $y^{(k)} = r(r-1)\cdots(r-k+1)\, x^{r-k}$，乘 $x^k$ 后：
$$x^k y^{(k)} = r(r-1)\cdots(r-k+1)\, x^r.$$

代入 (E)，各项均含公因子 $x^r \neq 0$（$x > 0$），约去后得：
$$r(r-1)\cdots(r-n+1) + a_{n-1} r(r-1)\cdots(r-n+2) + \cdots + a_1 r + a_0 = 0.$$

这正是指标方程 $(\mathrm{Ind})$。$\square$

> [!important] 指标方程与第(i)部分中常系数方程的特征方程等价
> 代换 $x = e^t$ 后，$y = x^r = e^{rt}$ 恰为常系数解法中的指数试探解。因此 $(\mathrm{Ind})$ 的根 $r$ 与对应常系数方程的特征根完全一致——两个视角给出同一组解，只是表出形式不同：
> $$e^{rt} \;\longleftrightarrow\; x^r, \qquad t^k e^{rt} \;\longleftrightarrow\; (\ln x)^k x^r.$$

---

## 第(iii)部分的证明：解的对应关系

由第(i)部分，$v(t)$ 满足一个常系数齐次方程。由[[常系数齐次线性方程与特征方程]]的定理：
- 特征方程（即 $(\mathrm{Ind})$）的单实根 $r$ → 解 $v(t) = e^{rt}$ → 回代 $y(x) = e^{r \ln x} = x^r$；
- $m$ 重实根 $r$ → 解 $v(t) = e^{rt}, t e^{rt}, \ldots, t^{m-1} e^{rt}$ → 回代 $y(x) = x^r, x^r \ln x, \ldots, x^r (\ln x)^{m-1}$；
- 复共轭根 $\alpha \pm i\beta$ → 复解 $e^{(\alpha \pm i\beta)t}$ → 实化 $e^{\alpha t}\cos\beta t, e^{\alpha t}\sin\beta t$ → 回代 $x^\alpha \cos(\beta \ln x), x^\alpha \sin(\beta \ln x)$；
- $m$ 重复根同理，多出 $(\ln x)^k$ 因子。

线性独立性由常系数情形继承（Vandermonde $\to$ 合流推广），或直接对 $\{x^{r_j} (\ln x)^k\}$ 计算 Wronskian，由 [[Wronskian与Abel公式]] 确认为基本解组。$\blacksquare$

---

## 一般解法（算法流程）

> [!tip] 求解 Euler 方程 $x^n y^{(n)} + \cdots + a_0 y = 0$（$x > 0$）
>
> **方法一（试探解 $y = x^r$）**：
> 1. 设 $y = x^r$，代入得指标方程 $(\mathrm{Ind})$；
> 2. 求 $(\mathrm{Ind})$ 的全部根（实根、复根）及重数；
> 3. 按上表写出 $n$ 个线性独立解；
> 4. 通解为它们的线性组合。
>
> **方法二（代换 $x = e^t$）**：
> 1. 令 $x = e^t$，$v(t) = y(e^t)$；
> 2. 写出 $v$ 的常系数方程（或用算子 $\vartheta$ 展开）；
> 3. 解常系数方程（特征根法）；
> 4. 回代 $t = \ln x$ 得 $y(x)$。
>
> 对 $x < 0$ 的情形，令 $x = -e^t$（即 $|x| = e^t$），所有 $\ln x$ 换成 $\ln|x|$，$x^r$ 中的 $r$ 非整数时需慎取分支。
>
> 具体计算见 [[Euler方程例题]]（$x^2 y'' - 3xy' + 4y = 0$）。

---

## 证明思路总结

> [!tip] 关键思想
> Euler 方程的本质是"**通过对数代换 $x = e^t$ 把尺度不变的方程变成平移不变的方程**"。
>
> 1. 原方程在缩放 $x \mapsto \lambda x$ 下每一项乘以 $\lambda$ 的同一个幂（等维度），故有尺度不变性；
> 2. 取对数 $t = \ln x$ 后，缩放变成平移 $t \mapsto t + \ln\lambda$，尺度不变性变为平移不变性；
> 3. 平移不变的线性 ODE 即**常系数**方程（系数不依赖 $t$），而常系数方程总是可解的。
>
> 代数上，$\vartheta = x D$ 在 $\{x^r\}$ 上对角化（$\vartheta(x^r) = r x^r$），把微分方程化为关于 $r$ 的代数方程——完全平行于 $D$ 在 $\{e^{rt}\}$ 上对角化（$D(e^{rt}) = r e^{rt}$）。

> [!info] 与 Frobenius 方法的联系
> Euler 方程是[[正则奇点与Frobenius方法]]中最简单的模型：在 $x = 0$ 处，所有系数 $x p(x), x^2 q(x), \ldots$ 均为常数（零次多项式）。Frobenius 的指标方程正是 Euler 指标方程在变系数情形下的推广——$p_0, q_0$ 代替了 $a_1, a_0$。Frobenius 级数解 $y = x^r \sum a_n x^n$ 的第一项 $a_0 x^r$ 就是"零阶近似"的 Euler 解。
