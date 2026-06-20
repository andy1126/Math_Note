---
title: Euler-Lagrange 方程（变分原理）
date: 2026-05-28
tags:
  - 应用数学
  - 变分法
  - Euler-Lagrange方程
  - 泛函极值
  - 分部积分
---

# Euler-Lagrange 方程（变分原理）

## 预备定义

> [!note] 容许函数类
> 给定 $a < b$，端点值 $\alpha, \beta \in \mathbb{R}$。定义容许函数类
> $$\mathcal{A} := \{ y \in C^2[a, b] : y(a) = \alpha,\ y(b) = \beta \}.$$

> [!note] 变分（test function）
> 称 $\eta \in C^2[a, b]$ 为**变分**（test function / variation），若 $\eta(a) = \eta(b) = 0$。记 $\mathcal{A}_0 = \{ \eta \in C^2[a, b] : \eta(a) = \eta(b) = 0\}$。

> [!note] 泛函
> 给定 **Lagrangian** $L: [a, b] \times \mathbb{R} \times \mathbb{R} \to \mathbb{R}$，$L \in C^2$。定义泛函
> $$J[y] := \int_a^b L(x, y(x), y'(x))\,dx, \quad y \in \mathcal{A}.$$

> [!note] 极值与稳定点
> 称 $y_0 \in \mathcal{A}$ 为 $J$ 的**（弱）局部极小**，若存在 $\varepsilon > 0$ 使得 $J[y_0] \leq J[y]$ 对一切 $y \in \mathcal{A}$ 满足 $\|y - y_0\|_{C^1} < \varepsilon$ 成立。称为**稳定点**（critical point），若一阶变分为 $0$（见下）。

> [!abstract] 引理：分部积分
> 对 $C^1$ 函数 $u, v$，$\int_a^b u'v\,dx = [uv]_a^b - \int_a^b u v'\,dx$。

> [!abstract] 引理：变分法基本引理（du Bois-Reymond）
> 设 $g \in C[a, b]$。若
> $$\int_a^b g(x)\, \eta(x)\,dx = 0, \quad \forall\, \eta \in \mathcal{A}_0,$$
> 则 $g \equiv 0$ 在 $[a, b]$ 上。
>
> **证明**：反证。设 $g(x_0) > 0$，$x_0 \in (a, b)$。由 $g$ 连续，存在 $[x_0 - \delta, x_0 + \delta] \subset (a, b)$ 使 $g \geq g(x_0)/2 > 0$。取**支集紧致**的测试函数
> $$\eta(x) = \begin{cases} \left[\delta^2 - (x - x_0)^2\right]^2, & |x - x_0| \leq \delta \\ 0, & \text{else} \end{cases}$$
> 则 $\eta \in C^2$，$\eta \in \mathcal{A}_0$，且 $\int g\eta \geq \int_{x_0-\delta}^{x_0+\delta} g(x_0)/2 \cdot \eta\,dx > 0$，矛盾。$g(x_0) < 0$ 类似。$\square$

---

## 定理（Euler-Lagrange 方程）

设 $L \in C^2$，$y_0 \in \mathcal{A}$ 为泛函 $J[y] = \int_a^b L(x, y, y')\,dx$ 的稳定点（特别地，局部极值）。则 $y_0$ 满足

$$\boxed{\dfrac{\partial L}{\partial y}(x, y_0, y_0') - \dfrac{d}{dx}\!\left[\dfrac{\partial L}{\partial y'}(x, y_0, y_0')\right] = 0, \quad x \in [a, b].}$$

称 $L$ 的 **Euler-Lagrange 方程**（E-L 方程）。

---

## 证明

### 第一步：构造单参数族

固定 $y_0 \in \mathcal{A}$ 与变分 $\eta \in \mathcal{A}_0$。对 $\varepsilon \in \mathbb{R}$，
$$y_\varepsilon(x) := y_0(x) + \varepsilon\,\eta(x).$$

端点条件保持：$y_\varepsilon(a) = y_0(a) + 0 = \alpha$，类似 $y_\varepsilon(b) = \beta$。故 $y_\varepsilon \in \mathcal{A}$。

### 第二步：定义沿 $\eta$ 方向的"实变函数"

$$\Phi(\varepsilon) := J[y_\varepsilon] = \int_a^b L(x, y_0 + \varepsilon\eta,\ y_0' + \varepsilon\eta')\,dx.$$

由 $L \in C^2$ 与积分号下求导（被积函数对 $\varepsilon$ 光滑），$\Phi \in C^2(\mathbb{R})$。

**关键观察**：$y_0$ 是 $J$ 的局部极小 $\Rightarrow$ $\Phi$ 在 $\varepsilon = 0$ 处取局部极小 $\Rightarrow$ $\Phi'(0) = 0$。

### 第三步：计算 $\Phi'(0)$

积分号下求导（用链式法则）：
$$\Phi'(\varepsilon) = \int_a^b \left[\frac{\partial L}{\partial y}(x, y_\varepsilon, y_\varepsilon')\, \eta + \frac{\partial L}{\partial y'}(x, y_\varepsilon, y_\varepsilon')\, \eta'\right] dx.$$

代入 $\varepsilon = 0$：
$$\Phi'(0) = \int_a^b \left[L_y(x, y_0, y_0')\, \eta + L_{y'}(x, y_0, y_0')\, \eta'\right] dx. \quad \cdots (\ast)$$

为简洁，下面省略偏导的参数：$L_y := L_y(x, y_0(x), y_0'(x))$，$L_{y'}$ 类似。

### 第四步：分部积分处理 $L_{y'} \eta'$ 项

由 $L \in C^2$ 与 $y_0 \in C^2$，$x \mapsto L_{y'}(x, y_0, y_0')$ 是 $C^1$。分部积分：
$$\int_a^b L_{y'}\, \eta'\,dx = \left[L_{y'}\, \eta\right]_a^b - \int_a^b \frac{d}{dx}(L_{y'})\, \eta\,dx.$$

边界项：$\eta(a) = \eta(b) = 0$ 故 $[L_{y'} \eta]_a^b = 0$。

代入 $(\ast)$：
$$0 = \Phi'(0) = \int_a^b \left[L_y - \frac{d}{dx} L_{y'}\right] \eta\,dx, \quad \forall\, \eta \in \mathcal{A}_0. \quad \cdots (\sharp)$$

### 第五步：应用变分法基本引理

被括号 $g(x) := L_y(x, y_0, y_0') - \dfrac{d}{dx}\!\left[L_{y'}(x, y_0, y_0')\right]$ 是 $[a, b]$ 上的连续函数（由 $L \in C^2$，$y_0 \in C^2$）。

$(\sharp)$ 对一切 $\eta \in \mathcal{A}_0$ 成立。由基本引理 $g \equiv 0$：
$$L_y(x, y_0, y_0') - \frac{d}{dx}\!\left[L_{y'}(x, y_0, y_0')\right] = 0, \quad \forall\, x \in [a, b]. \quad \blacksquare$$

---

## 证明思路总结

> [!tip] 关键思想
> 变分法把"无限维优化问题"$\min J[y]$ 化归为"一族实变函数 $\Phi(\varepsilon)$ 的极值问题"：
> 1. **单参数族**：沿任意变分 $\eta$ 取 $y_\varepsilon = y_0 + \varepsilon \eta$，把 $J$ 限制到这条线上得 $\Phi(\varepsilon)$；
> 2. **必要条件**：极值要求 $\Phi'(0) = 0$ 对**所有** $\eta$ 成立；
> 3. **分部积分**：把 $\eta'$ 转到 $L_{y'}$ 上，边界项因 $\eta(a) = \eta(b) = 0$ 消失；
> 4. **基本引理**：内积形 $\int g \eta = 0$ 对所有 $\eta$ 成立 $\Rightarrow$ $g \equiv 0$。
>
> 哲学：变分法是"无限维 Fermat 定理"——稳定点处方向导数为零，方向遍历所有变分。

> [!important] 端点条件 $\eta(a) = \eta(b) = 0$ 的作用
> 变分 $\eta$ 在端点必须为零，否则 $y_\varepsilon$ 跳出 $\mathcal{A}$。这一约束保证：
> 1. 单参数族 $y_\varepsilon$ 始终满足端点条件；
> 2. 分部积分的边界项 $[L_{y'}\,\eta]_a^b = 0$。
>
> 若问题允许端点变动（自由端点），则边界项给出**自然边界条件** $L_{y'}|_a = L_{y'}|_b = 0$，是 E-L 方程之外的额外约束。

> [!warning] 必要而非充分
> E-L 方程是稳定点的必要条件，不充分。极小、极大、鞍点都满足 E-L。区分需要**二阶变分**或 **Legendre 条件**：
> $$L_{y'y'}(x, y_0, y_0') \geq 0 \quad \text{（弱极小的必要条件）}.$$
> 完整充分性需 **Jacobi 条件**（解的共轭点分析）。

> [!info] 经典应用
>
> **(1) 测地线（最短路径）**：$L = \sqrt{1 + (y')^2}$。E-L 给出
> $$\frac{d}{dx}\!\left(\frac{y'}{\sqrt{1 + (y')^2}}\right) = 0 \Longrightarrow y' = \text{常数} \Longrightarrow y \text{ 为直线}.$$
> 即"两点间直线最短"。
>
> **(2) 最速降线（Brachistochrone）**：$L = \sqrt{\dfrac{1 + (y')^2}{2 g y}}$。E-L + Beltrami 恒等式（$L$ 不显含 $x$ 时的简化）给出**摆线**（cycloid）。Bernoulli 1696 年的著名问题。
>
> **(3) 极小曲面**：$L = \sqrt{1 + |\nabla u|^2}$。E-L 给出**极小曲面方程** $\operatorname{div}(\nabla u / \sqrt{1 + |\nabla u|^2}) = 0$；其线性化为 Laplace 方程。皂膜的几何模型。

> [!info] Hamilton 力学
> 经典力学 Lagrangian $L(t, q, \dot q) = T - V$（动能减位能）。E-L 方程
> $$\frac{d}{dt}\!\left(\frac{\partial L}{\partial \dot q}\right) = \frac{\partial L}{\partial q}$$
> 即 **Lagrange 运动方程**。在牛顿力学中 $L = \frac{1}{2}m\dot q^2 - V(q)$ 给出 $m\ddot q = -V'(q) = F$。
>
> 进一步变换（Legendre 变换）得 **Hamilton 方程** $\dot q = \partial H/\partial p$、$\dot p = -\partial H/\partial q$。

> [!info] 推广方向
>
> **(1) 多重积分 / PDE 弱解**：$J[u] = \int_\Omega L(x, u, \nabla u)\,dx$ 的 E-L 是椭圆型 PDE
> $$\frac{\partial L}{\partial u} - \nabla \cdot \frac{\partial L}{\partial (\nabla u)} = 0.$$
> 这是 [[Lax-Milgram定理]] 弱解框架的源头。
>
> **(2) 带约束的变分**：用 Lagrange 乘子法。等周问题（最大面积/固定周长）的 E-L 给出圆。
>
> **(3) Noether 定理**：每个连续对称性对应一守恒量（时间平移→能量守恒，空间平移→动量守恒）。E-L 方程的几何对偶视角。
