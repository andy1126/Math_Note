---
title: Green 函数例题
date: 2026-06-20
tags:
  - 题解
  - 微分方程
  - ODE
  - 边值问题
  - Green函数
---

# Green 函数例题

## 题目

> 求边值问题
> $$\begin{cases} -y'' = f(x), & 0 < x < 1, \\ y(0) = 0, \quad y(1) = 0 \end{cases}$$
> 的 **Green 函数** $G(x, \xi)$，并用它写出解的积分表达式。由此显式计算 $f(x) \equiv 1$ 时的解。

---

## 预备定义与定理

> [!note] 边值问题的自伴形式
> 方程 $-y'' = f$ 已是自伴形式 $\mathcal{L} y := -(p y')' + q y$，其中 $p \equiv 1,\ q \equiv 0$。边界条件为 **Dirichlet 型**（两端给定函数值）。详见 [[两点边值问题与Green函数构造]]。

> [!abstract] 定理：Green 函数的构造公式
> 对 $\mathcal{L} y := -(p y')' + q y = f$ 配齐次边条件（齐次 BVP 只有零解），Green 函数为
> $$G(x, \xi) = \frac{1}{p(\xi) W(\xi)} \begin{cases} u(x) v(\xi), & x \leq \xi, \\ u(\xi) v(x), & x \geq \xi, \end{cases}$$
> 其中 $u$ 满足 $x = a$ 边条件，$v$ 满足 $x = b$ 边条件，$W = uv' - u'v$。详见 [[两点边值问题与Green函数构造]]。

> [!abstract] 引理：齐次 BVP 只有零解
> 齐次方程 $-y'' = 0$ 的通解为 $y = C_1 + C_2 x$。施加 $y(0) = y(1) = 0$ 得 $C_1 = 0,\ C_1 + C_2 = 0$，故 $C_1 = C_2 = 0$，只有零解。因此非齐次 BVP 对任意 $f$ 存在唯一解，Green 函数存在。

---

## 解答

### 第一步：求齐次方程的基本解组

齐次方程 $-y'' = 0$ 即 $y'' = 0$，通解为
$$y_h = C_1 + C_2 x.$$

取基本解组 $y_1 = 1,\ y_2 = x$（或任何两个线性独立的一次函数）。

Wronskian：$W = y_1 y_2' - y_1' y_2 = 1 \cdot 1 - 0 \cdot x = 1$（常数）。

### 第二步：找出满足各自端边条件的解

- **$x = 0$ 端**：边条件 $y(0) = 0$。齐次解 $y = C_1 + C_2 x$ 在 $x = 0$ 处 $y(0) = C_1 = 0$，故取
  $$u(x) = x.$$

- **$x = 1$ 端**：边条件 $y(1) = 0$。齐次解在 $x = 1$ 处 $C_1 + C_2 = 0$，即 $C_2 = -C_1$，故取
  $$v(x) = 1 - x.$$

> [!info] 非线性缩放可弃
> $u$ 与 $v$ 各自至标量倍数唯一；任何倍数在 Green 函数公式中会同时出现在分子和 $W$ 中，相互抵消——最终 $G$ 唯一。故取最简形式即可。

### 第三步：计算 $p(\xi) W(\xi)$

$p(\xi) \equiv 1$，$W = u v' - u' v = x \cdot (-1) - 1 \cdot (1 - x) = -x - 1 + x = -1$。

故 $p(\xi) W(\xi) = -1$（常数，与 Abel 公式一致）。

### 第四步：写出 Green 函数

由构造公式（$pW = -1$）：
$$G(x, \xi) = \frac{1}{-1} \begin{cases} u(x) v(\xi), & x \leq \xi \\ u(\xi) v(x), & x \geq \xi \end{cases} = \begin{cases} -x(1 - \xi), & 0 \leq x \leq \xi, \\ -(1 - x)\xi, & \xi \leq x \leq 1. \end{cases}$$

调号：令 $G \mapsto -G$（等价地将两个解同时取负，$W$ 变号，$G$ 不变），得标准形式
$$\boxed{ G(x, \xi) = \begin{cases} x(1 - \xi), & 0 \leq x \leq \xi, \\ \xi(1 - x), & \xi \leq x \leq 1. } \end{cases}$$

> [!info] 验核
> $G$ 连续：在 $x = \xi$ 处两段均给出 $\xi(1 - \xi)$。跳跃条件：$\partial_x G(\xi^+, \xi) - \partial_x G(\xi^-, \xi) = -\xi - (1 - \xi) = -1 = -1/p$。对称性：$G(x, \xi) = G(\xi, x)$（交换即见）。边界条件：$G(0, \xi) = 0 \cdot (1 - \xi) = 0$；$G(1, \xi) = \xi(1 - 1) = 0$。✓

### 第五步：解的积分表示

对任意 $f \in C[0, 1]$，
$$y(x) = \int_0^1 G(x, \xi)\, f(\xi)\, d\xi = \int_0^x \xi(1 - x) f(\xi)\, d\xi + \int_x^1 x(1 - \xi) f(\xi)\, d\xi.$$

### 第六步：特例 $f(x) \equiv 1$

$$y(x) = (1 - x) \int_0^x \xi\, d\xi + x \int_x^1 (1 - \xi)\, d\xi.$$

计算：
$$\int_0^x \xi\, d\xi = \frac{x^2}{2},$$
$$\int_x^1 (1 - \xi)\, d\xi = \Big[\xi - \frac{\xi^2}{2}\Big]_x^1 = \left(1 - \frac{1}{2}\right) - \left(x - \frac{x^2}{2}\right) = \frac{1}{2} - x + \frac{x^2}{2}.$$

故
$$y(x) = (1 - x) \cdot \frac{x^2}{2} + x \cdot \left(\frac{1}{2} - x + \frac{x^2}{2}\right)$$
$$= \frac{x^2 - x^3}{2} + \frac{x}{2} - x^2 + \frac{x^3}{2} = \frac{x}{2} - \frac{x^2}{2} = \frac{x(1 - x)}{2}.$$

**验算**：$y = \frac{x - x^2}{2}$，$y' = \frac{1 - 2x}{2}$，$y'' = -1$，$-y'' = 1 = f$。$y(0) = 0,\ y(1) = 0$。$\checkmark$

> [!info] Green 函数法的力量
> 一旦求出 $G$，任意 $f$ 的解只需**一次积分**——无需重新解 ODE。$G$ 本身仅依赖微分算子和边界条件，与右端 $f$ 无关。

---

## 答案

$$\boxed{ G(x, \xi) = \begin{cases} x(1 - \xi), & 0 \leq x \leq \xi, \\ \xi(1 - x), & \xi \leq x \leq 1. \end{cases} }$$

对 $f(x) \equiv 1$：$\boxed{ y(x) = \dfrac{x(1 - x)}{2} }.$

---

## 变形与延伸

> [!info] 变形 1（混合边条件）
> 求 $-y'' = f,\ y(0) = 0,\ y'(1) = 0$ 的 Green 函数。
>
> **提示**：$u(x) = x$（满足 $y(0)=0$），$v(x) = 1$（满足 $y'(1)=0$）。$W = x \cdot 0 - 1 \cdot 1 = -1$。Green 函数是分段线性的，形状与 Dirichlet 情形形成对比。

> [!info] 变形 2（Robin 边条件）
> 求 $-y'' = f,\ y(0) = 0,\ y(1) + y'(1) = 0$ 的 Green 函数。
>
> **提示**：$u = x$；$v$ 需满足 $v(1) + v'(1) = 0$，取 $v(x) = 1 + x - 2x = \cdots$ 实为 $v = 2 - x$（验证：$v(1)=1,\ v'(1)=-1$，$1+(-1)=0$ ✓）。Robin 条件的 Green 函数仍对称。

> [!info] 变形 3（用本征函数展开核 $G$）
> 验证 $\displaystyle G(x, \xi) = \frac{2}{\pi^2} \sum_{n=1}^{\infty} \frac{\sin(n\pi x)\, \sin(n\pi \xi)}{n^2}$ 与上述分段线性核一致。
>
> **提示**：对固定的 $\xi$，将分段线性函数 $G(\cdot, \xi)$ 展为 Fourier 正弦级数。系数恰为 $\frac{2 \sin(n\pi\xi)}{n^2 \pi^2}$。这种展开将 Green 函数与 [[Sturm-Liouville定理]] 的本征函数联系起来，见 [[本征值展开求解非齐次SL问题]]。

> [!info] 延伸（Green 函数 = Laplace 算子的逆）
> 在一维，$-d^2/dx^2$ 在 Dirichlet 边条件下的逆就是积分算子 $(T f)(x) = \int_0^1 G(x,\xi) f(\xi) d\xi$。$G$ 的对称性、正定性（Mercer 定理）等性质是泛函分析中紧自伴算子的谱定理的具体实现。
