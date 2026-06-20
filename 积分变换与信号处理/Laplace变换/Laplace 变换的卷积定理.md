---
title: Laplace 变换的卷积定理
date: 2026-04-18
tags:
  - 积分变换
  - Laplace变换
  - 卷积
  - 实分析
---

# Laplace 变换的卷积定理

## 预备定义

> [!note] Laplace 变换
> 设 $f: [0, +\infty) \to \mathbb{R}$ 为局部可积函数。$f$ 的 **Laplace 变换**定义为
> $$\mathcal{L}\{f(t)\}(s) = F(s) = \int_0^{+\infty} e^{-st} f(t)\, dt,$$
> 其中 $s \in \mathbb{C}$，且积分在适当的半平面 $\operatorname{Re}(s) > \sigma_0$（$\sigma_0$ 称为收敛横标）上绝对收敛。

> [!note] 卷积
> 设 $f, g: [0, +\infty) \to \mathbb{R}$。$f$ 与 $g$ 的**卷积**（convolution）定义为
> $$(f * g)(t) = \int_0^t f(\tau)\, g(t - \tau)\, d\tau, \quad t \geq 0.$$
> 注意此处为**单边卷积**，积分下限为 $0$ 而非 $-\infty$，因为 $f$ 和 $g$ 在 $t < 0$ 时被视为零。

> [!note] 指数阶函数
> 称函数 $f: [0, +\infty) \to \mathbb{R}$ 为**指数阶**的（of exponential order），若存在常数 $M > 0$、$\sigma_0 \geq 0$ 和 $T \geq 0$，使得
> $$|f(t)| \leq M\, e^{\sigma_0 t}, \quad \forall\, t \geq T.$$
> 指数阶函数的 Laplace 变换在半平面 $\operatorname{Re}(s) > \sigma_0$ 上绝对收敛。

> [!abstract] 引理：Fubini 定理（积分换序）
> 设 $h(x, y)$ 在区域 $D \subseteq \mathbb{R}^2$ 上可测，且
> $$\iint_D |h(x, y)|\, dx\, dy < +\infty,$$
> 则累次积分可交换顺序：
> $$\int \left(\int h(x, y)\, dy\right) dx = \int \left(\int h(x, y)\, dx\right) dy.$$

---

## 定理

设 $f, g: [0, +\infty) \to \mathbb{R}$ 均为指数阶的局部可积函数，其 Laplace 变换分别为 $F(s) = \mathcal{L}\{f\}(s)$ 和 $G(s) = \mathcal{L}\{g\}(s)$。则在 $\operatorname{Re}(s)$ 充分大时，

$$F(s) \cdot G(s) = \mathcal{L}\{f * g\}(s) = \int_0^{+\infty} e^{-st} \left(\int_0^t f(\tau)\, g(t - \tau)\, d\tau\right) dt.$$

即：**Laplace 变换将卷积运算映射为乘法运算。**

---

## 证明

### 第一步：写出乘积的积分表达

由 Laplace 变换的定义，

$$F(s) \cdot G(s) = \left(\int_0^{+\infty} e^{-s\tau} f(\tau)\, d\tau\right) \left(\int_0^{+\infty} e^{-su} g(u)\, du\right). \quad \cdots (\ast)$$

由于两个积分均绝对收敛（$\operatorname{Re}(s)$ 充分大时，指数阶条件保证了这一点），$(\ast)$ 可写为二重积分：

$$F(s) \cdot G(s) = \int_0^{+\infty} \int_0^{+\infty} e^{-s(\tau + u)} f(\tau)\, g(u)\, d\tau\, du. \quad \cdots (\star)$$

### 第二步：验证 Fubini 定理的适用条件

**目标**：证明被积函数绝对可积，从而可以交换积分顺序并进行变量替换。

**已知**：$f$ 和 $g$ 为指数阶函数，即存在 $M_1, M_2 > 0$ 和 $\sigma_1, \sigma_2 \geq 0$，使得对充分大的 $t$，

$$|f(t)| \leq M_1\, e^{\sigma_1 t}, \qquad |g(t)| \leq M_2\, e^{\sigma_2 t}.$$

取 $\operatorname{Re}(s) = \sigma > \sigma_1 + \sigma_2$，则

$$\int_0^{+\infty}\!\!\int_0^{+\infty} \left|e^{-s(\tau+u)} f(\tau)\, g(u)\right| d\tau\, du \leq M_1 M_2 \int_0^{+\infty} e^{-(\sigma - \sigma_1)\tau}\, d\tau \cdot \int_0^{+\infty} e^{-(\sigma - \sigma_2)u}\, du < +\infty.$$

因此由 Fubini 定理，$(\star)$ 中的积分顺序可以自由交换，且允许变量替换。$\square$

### 第三步：变量替换

在 $(\star)$ 中作替换 $t = \tau + u$（固定 $\tau$，令 $u = t - \tau$，$du = dt$）。当 $u$ 从 $0$ 到 $+\infty$ 时，$t$ 从 $\tau$ 到 $+\infty$。

$$F(s) \cdot G(s) = \int_0^{+\infty} \int_\tau^{+\infty} e^{-st}\, f(\tau)\, g(t - \tau)\, dt\, d\tau.$$

### 第四步：交换积分顺序

积分区域为 $\{(\tau, t) : 0 \leq \tau < +\infty,\; \tau \leq t < +\infty\}$，等价于 $\{(\tau, t) : 0 \leq t < +\infty,\; 0 \leq \tau \leq t\}$。

交换积分顺序（由第二步，Fubini 定理适用）：

$$F(s) \cdot G(s) = \int_0^{+\infty} e^{-st} \left(\int_0^t f(\tau)\, g(t - \tau)\, d\tau\right) dt.$$

> [!info] 积分区域的变换
> 原区域：先对 $\tau$ 从 $0$ 到 $+\infty$，再对 $t$ 从 $\tau$ 到 $+\infty$。这是一个无界三角形区域 $0 \leq \tau \leq t < +\infty$。交换后：先对 $t$ 从 $0$ 到 $+\infty$，再对 $\tau$ 从 $0$ 到 $t$。

### 第五步：识别卷积与 Laplace 变换

内层积分

$$\int_0^t f(\tau)\, g(t - \tau)\, d\tau = (f * g)(t)$$

恰为 $f$ 与 $g$ 的卷积。因此

$$F(s) \cdot G(s) = \int_0^{+\infty} e^{-st}\, (f * g)(t)\, dt = \mathcal{L}\{f * g\}(s).$$

### 总结

综合以上各步：

1. 将 $F(s) \cdot G(s)$ 写为二重积分。 ✓
2. 验证绝对可积性，确保 Fubini 定理适用。 ✓
3. 作变量替换 $t = \tau + u$。 ✓
4. 交换积分顺序。 ✓
5. 识别出卷积的定义和 Laplace 变换的形式。 ✓

因此 $F(s) \cdot G(s) = \mathcal{L}\{f * g\}(s)$。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明的核心技巧是**变量替换与积分换序**。具体而言：
> 1. 将两个 Laplace 变换的**乘积**展开为 $(\tau, u)$ 平面上的**二重积分**；
> 2. 作替换 $t = \tau + u$，将指数因子合并为 $e^{-st}$；
> 3. 交换积分顺序（Fubini 定理），使内层积分恰好成为卷积的定义。
>
> 从本质上看，Laplace 变换之所以能将卷积转化为乘法，是因为**指数函数的可加性** $e^{-s(\tau+u)} = e^{-s\tau} \cdot e^{-su}$ 与卷积中变量的**求和结构** $t = \tau + u$ 完美匹配。

> [!warning] 收敛性条件不可忽略
> 卷积定理的成立依赖于 $\operatorname{Re}(s)$ 足够大，使得 Fubini 定理可用。若 $f$ 或 $g$ 增长过快（超过任何指数阶），则 Laplace 变换本身可能不存在，定理不适用。此外，即使两个变换各自收敛，**乘积对应的卷积积分是否收敛**也需要单独验证。
