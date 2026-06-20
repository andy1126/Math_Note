---
title: Picard-Lindelöf 定理（初值问题的存在唯一性）
date: 2026-04-11
tags:
  - 常微分方程
  - 初值问题
  - Lipschitz条件
  - Banach不动点定理
  - Picard迭代
---

# Picard-Lindelöf 定理

## 预备定义

> [!note] 初值问题（IVP）
> 给定函数 $f: U \to \mathbb{R}^n$（$U \subseteq \mathbb{R} \times \mathbb{R}^n$ 为开集）和初始条件 $(t_0, y_0) \in U$，**初值问题**（initial value problem）是求函数 $y: I \to \mathbb{R}^n$（$I$ 为包含 $t_0$ 的区间）使得
> $$y'(t) = f(t, y(t)), \quad y(t_0) = y_0.$$

> [!note] Lipschitz 条件
> 设 $f: U \to \mathbb{R}^n$。称 $f$ 关于第二个变量满足 **Lipschitz 条件**（Lipschitz condition），若存在常数 $L \geq 0$，使得对一切 $(t, y_1), (t, y_2) \in U$，
> $$\|f(t, y_1) - f(t, y_2)\| \leq L \|y_1 - y_2\|.$$
> 常数 $L$ 称为 **Lipschitz 常数**。

> [!note] Banach 空间 $C([a,b], \mathbb{R}^n)$
> 记 $C([a,b], \mathbb{R}^n)$ 为 $[a,b]$ 上连续函数全体，赋以上确界范数
> $$\|\varphi\|_\infty = \max_{t \in [a,b]} \|\varphi(t)\|.$$
> 这是一个完备赋范空间（Banach 空间）。

> [!abstract] 引理：Banach 不动点定理（压缩映射原理）
> 设 $(X, d)$ 为完备度量空间，$T: X \to X$ 为压缩映射，即存在 $0 \leq q < 1$ 使得
> $$d(T(x), T(y)) \leq q \, d(x, y) \quad \forall\, x, y \in X.$$
> 则 $T$ 有唯一的不动点 $x^\ast \in X$，且对任意初始点 $x_0 \in X$，迭代序列 $x_{n+1} = T(x_n)$ 收敛于 $x^\ast$。

---

## 定理

设 $f: [t_0 - a, \, t_0 + a] \times \overline{B}(y_0, b) \to \mathbb{R}^n$ 连续，且关于第二个变量满足 Lipschitz 条件（Lipschitz 常数为 $L$）。令

$$M = \max_{(t,y) \in [t_0-a, \, t_0+a] \times \overline{B}(y_0, b)} \|f(t, y)\|, \qquad \delta = \min\!\left(a, \, \frac{b}{M}\right).$$

则初值问题

$$y'(t) = f(t, y(t)), \quad y(t_0) = y_0$$

在区间 $[t_0 - \delta, \, t_0 + \delta]$ 上有**唯一**解。

---

## 证明

证明分三个阶段：将微分方程转化为积分方程，构造压缩映射，最后应用 Banach 不动点定理。

### 第一阶段：等价转化为积分方程

> [!important] 积分形式是 Picard 迭代的基础
> 微分方程的积分形式既消除了对可微性的直接依赖，又自然地产生了用于不动点论证的算子。

#### 第一步：微分方程 $\Longrightarrow$ 积分方程

设 $y$ 是 IVP 的解，即 $y'(t) = f(t, y(t))$ 且 $y(t_0) = y_0$。对两边从 $t_0$ 到 $t$ 积分：

$$y(t) = y_0 + \int_{t_0}^{t} f(s, y(s)) \, ds. \quad \cdots (\ast)$$

$\square$

#### 第二步：积分方程 $\Longrightarrow$ 微分方程

反过来，若连续函数 $y$ 满足 $(\ast)$，则 $y(t_0) = y_0$，且由微积分基本定理，

$$y'(t) = f(t, y(t)).$$

故 IVP 与积分方程 $(\ast)$ **等价**。$\square$

### 第二阶段：构造压缩映射

令 $I = [t_0 - \delta, \, t_0 + \delta]$，定义闭集

$$\mathcal{S} = \left\{\varphi \in C(I, \mathbb{R}^n) : \|\varphi - y_0\|_\infty \leq b\right\},$$

其中将常值函数 $y_0$ 也视为 $C(I, \mathbb{R}^n)$ 的元素。$\mathcal{S}$ 是完备度量空间 $(C(I, \mathbb{R}^n), \|\cdot\|_\infty)$ 中的闭子集，故本身完备。

定义 **Picard 算子** $T: \mathcal{S} \to C(I, \mathbb{R}^n)$：

$$(T\varphi)(t) = y_0 + \int_{t_0}^{t} f(s, \varphi(s)) \, ds.$$

求解积分方程 $(\ast)$ 等价于求 $T$ 的不动点。

#### 第一步：$T$ 将 $\mathcal{S}$ 映入自身

对任意 $\varphi \in \mathcal{S}$ 及 $t \in I$，

$$\|(T\varphi)(t) - y_0\| = \left\|\int_{t_0}^{t} f(s, \varphi(s)) \, ds\right\| \leq |t - t_0| \cdot M \leq \delta M \leq b,$$

其中最后一步由 $\delta \leq b/M$。故 $T\varphi \in \mathcal{S}$。$\square$

#### 第二步：在加权范数下 $T$ 是压缩映射

> [!info] 为何引入加权范数
> 在标准上确界范数下，$T$ 的 Lipschitz 常数为 $L\delta$，未必小于 $1$。引入加权范数 $\|\cdot\|_\lambda$ 可使压缩常数任意小，从而无需缩短区间。

对 $\lambda > 0$（稍后选取），在 $C(I, \mathbb{R}^n)$ 上定义加权范数

$$\|\varphi\|_\lambda = \max_{t \in I} \left(e^{-\lambda |t - t_0|} \|\varphi(t)\|\right).$$

此范数与 $\|\cdot\|_\infty$ 等价（因 $e^{-\lambda \delta} \|\varphi\|_\infty \leq \|\varphi\|_\lambda \leq \|\varphi\|_\infty$），故 $(\mathcal{S}, \|\cdot\|_\lambda)$ 仍完备。

对 $\varphi, \psi \in \mathcal{S}$，不妨设 $t \geq t_0$（$t < t_0$ 的情形完全类似），

$$\|(T\varphi)(t) - (T\psi)(t)\| \leq \int_{t_0}^{t} \|f(s, \varphi(s)) - f(s, \psi(s))\| \, ds \leq L \int_{t_0}^{t} \|\varphi(s) - \psi(s)\| \, ds.$$

将 $\|\varphi(s) - \psi(s)\|$ 用加权范数表达：$\|\varphi(s) - \psi(s)\| \leq e^{\lambda|s - t_0|} \|\varphi - \psi\|_\lambda$，代入得

$$\|(T\varphi)(t) - (T\psi)(t)\| \leq L \|\varphi - \psi\|_\lambda \int_{t_0}^{t} e^{\lambda(s - t_0)} \, ds = \frac{L}{\lambda} \|\varphi - \psi\|_\lambda \left(e^{\lambda(t - t_0)} - 1\right).$$

故

$$\|(T\varphi)(t) - (T\psi)(t)\| \leq \frac{L}{\lambda} \, e^{\lambda(t - t_0)} \|\varphi - \psi\|_\lambda.$$

两边乘以 $e^{-\lambda|t-t_0|}$，对 $t \in I$ 取上确界：

$$\|T\varphi - T\psi\|_\lambda \leq \frac{L}{\lambda} \|\varphi - \psi\|_\lambda. \quad \cdots (\star)$$

取 $\lambda = 2L$（若 $L = 0$ 则 $f$ 不依赖 $y$，唯一性显然），则压缩常数 $q = \dfrac{L}{\lambda} = \dfrac{1}{2} < 1$。$\square$

### 第三阶段：应用 Banach 不动点定理

由 $(\star)$，$T: \mathcal{S} \to \mathcal{S}$ 在完备度量空间 $(\mathcal{S}, \|\cdot\|_\lambda)$ 上是压缩映射。由 Banach 不动点定理，$T$ 有**唯一**不动点 $y^\ast \in \mathcal{S}$，即

$$y^\ast(t) = y_0 + \int_{t_0}^{t} f(s, y^\ast(s)) \, ds \quad \forall\, t \in I.$$

由第一阶段的等价性，$y^\ast$ 是 IVP 在 $I = [t_0 - \delta, \, t_0 + \delta]$ 上的唯一解。

> [!important] Picard 迭代的构造性
> Banach 不动点定理不仅给出存在唯一性，还给出**构造方法**：从 $\varphi_0(t) \equiv y_0$ 出发，令
> $$\varphi_{n+1}(t) = y_0 + \int_{t_0}^{t} f(s, \varphi_n(s))\, ds,$$
> 则 $\varphi_n \to y^\ast$ 一致收敛。这就是经典的 **Picard 迭代**（Picard iteration）。

$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明将 ODE 初值问题**等价转化为积分方程的不动点问题**，然后在函数空间上应用 Banach 不动点定理：
> 1. **等价转化**：$y' = f(t,y),\; y(t_0) = y_0$ 等价于 $y = T(y)$，其中 $T$ 是 Picard 积分算子；
> 2. **闭子集**：在 $C(I, \mathbb{R}^n)$ 中选取闭球 $\mathcal{S}$，利用 $\delta \leq b/M$ 保证 $T$ 自映射；
> 3. **加权范数技巧**：引入 $e^{-\lambda|t-t_0|}$ 加权范数，将压缩常数降为 $L/\lambda$，取 $\lambda > L$ 即可；
> 4. **不动点 = 解**：Banach 定理直接给出存在性、唯一性和 Picard 迭代的收敛性。
>
> 这一论证是**分析方法解决 ODE 问题的范本**：将微分问题转化为积分问题，再将积分问题转化为泛函分析中的不动点问题。

> [!warning] Lipschitz 条件的必要性与 Peano 定理的对比
> - 若仅要求 $f$ 连续而**不要求 Lipschitz 条件**，则由 **Peano 存在定理**，解仍然存在，但**唯一性可能丧失**。
> - 经典反例：$y' = \sqrt{|y|}$，$y(0) = 0$。函数 $f(t,y) = \sqrt{|y|}$ 在 $y = 0$ 处不满足 Lipschitz 条件。该 IVP 有无穷多解：对任意 $c \geq 0$，
> $$y_c(t) = \begin{cases} 0, & t \leq c, \\ \frac{1}{4}(t - c)^2, & t > c \end{cases}$$
> 均为解。
> - 实践中，若 $f$ 关于 $y$ 有连续偏导数，则由中值定理自动满足局部 Lipschitz 条件，Picard-Lindelöf 定理即可适用。
