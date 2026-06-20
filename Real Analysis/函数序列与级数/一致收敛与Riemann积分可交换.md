---
title: 一致收敛与 Riemann 积分可交换
date: 2026-04-11
tags:
  - 实分析
  - 一致收敛
  - Riemann积分
  - 函数序列
  - 极限交换
---

# 一致收敛与 Riemann 积分可交换

## 预备定义

> [!note] 一致收敛
> 设 $(f_n)_{n=1}^\infty$ 为从 $[a, b]$ 到 $\mathbb{R}$ 的函数序列。称 $f_n$ **一致收敛**于 $f: [a, b] \to \mathbb{R}$，若
> $$\|f_n - f\|_\infty = \sup_{x \in [a, b]} |f_n(x) - f(x)| \to 0 \quad (n \to \infty).$$

> [!note] Riemann 可积
> 有界函数 $f: [a, b] \to \mathbb{R}$ 是 **Riemann 可积**的，若对任意 $\varepsilon > 0$，存在分划 $P$ 使得 $U(f, P) - L(f, P) < \varepsilon$。

> [!abstract] 引理：Riemann 积分的线性与有界性
> 设 $f, g: [a, b] \to \mathbb{R}$ Riemann 可积。则：
> 1. **线性**：$\int_a^b (f + g) = \int_a^b f + \int_a^b g$，$\int_a^b cf = c \int_a^b f$。
> 2. **绝对值不等式**：$\left|\int_a^b f\right| \leq \int_a^b |f|$。
> 3. **上界估计**：$\left|\int_a^b f\right| \leq (b - a) \cdot \|f\|_\infty$。

---

## 定理

设 $f_n: [a, b] \to \mathbb{R}$（$n = 1, 2, \dots$）是 Riemann 可积函数序列，且 $f_n$ 一致收敛于 $f: [a, b] \to \mathbb{R}$。则：

**(i)** $f$ 是 Riemann 可积的。

**(ii)** $\displaystyle\int_a^b f = \lim_{n \to \infty} \int_a^b f_n$，即

$$\int_a^b \lim_{n \to \infty} f_n(x)\, dx = \lim_{n \to \infty} \int_a^b f_n(x)\, dx.$$

---

## 证明

### 第(i)部分的证明：$f$ Riemann 可积

#### 第一步：$f$ 有界

由 $f_n \to f$ 一致收敛，取 $\varepsilon = 1$，存在 $N$ 使得 $\|f_N - f\|_\infty < 1$。对所有 $x$：

$$|f(x)| \leq |f(x) - f_N(x)| + |f_N(x)| < 1 + \|f_N\|_\infty.$$

由 $f_N$ Riemann 可积故有界，$f$ 有界。$\square$

#### 第二步：验证 Riemann 可积的判定准则

给定 $\varepsilon > 0$。由一致收敛，存在 $N$ 使得

$$\|f_N - f\|_\infty < \frac{\varepsilon}{3(b - a)}. \quad \cdots (\ast)$$

由 $f_N$ Riemann 可积，存在分划 $P$ 使得

$$U(f_N, P) - L(f_N, P) < \frac{\varepsilon}{3}. \quad \cdots (\star)$$

> [!important] 上下和的比较
> 对任意函数 $g, h: [a, b] \to \mathbb{R}$ 和分划 $P = \{x_0, \dots, x_m\}$，若 $\|g - h\|_\infty < \delta$，则在每个子区间 $[x_{k-1}, x_k]$ 上：
> $$\sup_{[x_{k-1}, x_k]} g \leq \sup_{[x_{k-1}, x_k]} h + \delta, \qquad \inf_{[x_{k-1}, x_k]} g \geq \inf_{[x_{k-1}, x_k]} h - \delta.$$
> 故 $U(g, P) \leq U(h, P) + \delta(b - a)$，$L(g, P) \geq L(h, P) - \delta(b - a)$，从而
> $$U(g, P) - L(g, P) \leq U(h, P) - L(h, P) + 2\delta(b - a). \quad \cdots (\diamond)$$

对 $g = f$，$h = f_N$，$\delta = \varepsilon / (3(b-a))$，由 $(\ast)$、$(\star)$ 和 $(\diamond)$：

$$U(f, P) - L(f, P) \leq U(f_N, P) - L(f_N, P) + 2 \cdot \frac{\varepsilon}{3(b-a)} \cdot (b - a) < \frac{\varepsilon}{3} + \frac{2\varepsilon}{3} = \varepsilon.$$

由 Riemann 可积的判定准则，$f$ Riemann 可积。$\square$

---

### 第(ii)部分的证明：积分的极限交换

对任意 $n$，$f$ 和 $f_n$ 均 Riemann 可积（$f$ 由第(i)部分），故 $f - f_n$ Riemann 可积。由引理的上界估计：

$$\left|\int_a^b f - \int_a^b f_n\right| = \left|\int_a^b (f - f_n)\right| \leq (b - a) \cdot \|f - f_n\|_\infty. \quad \cdots (1)$$

由 $f_n \to f$ 一致收敛，$\|f - f_n\|_\infty \to 0$。故 $(1)$ 的右端趋于 $0$，即

$$\lim_{n \to \infty} \int_a^b f_n = \int_a^b f. \quad \square$$

---

### 结论

1. $f$ 是 Riemann 可积的。 ✓
2. $\displaystyle\int_a^b f = \lim_{n \to \infty} \int_a^b f_n$。 ✓

$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明分为两个独立的部分：
>
> **(i) $f$ Riemann 可积**：核心是上下和的传递估计 $(\diamond)$。一致收敛保证 $f$ 与某个 $f_N$ 一致地接近（$\|f - f_N\|_\infty$ 小），这将 $f$ 的上下和之差控制在 $f_N$ 的上下和之差加上一个可控的修正项以内。$f_N$ 可积保证其上下和之差小，从而 $f$ 的上下和之差也小。
>
> **(ii) 积分可交换**：更加直接——积分的差被 $(b-a) \cdot \|f - f_n\|_\infty$ 控制，一致收敛让右端趋于零。
>
> 两部分共同的要点：**一致收敛提供了与 $x$ 无关的全局误差控制**，使得逐点操作（积分是"对所有 $x$ 求和"）可以与极限交换。

> [!warning] 逐点收敛不够
> 若仅有逐点收敛，两个结论都可以失败：
>
> - **$f$ 可能不 Riemann 可积**：令 $\{r_1, r_2, \dots\}$ 为 $[0, 1] \cap \mathbb{Q}$ 的枚举，$f_n = \mathbf{1}_{\{r_1, \dots, r_n\}}$。每个 $f_n$ Riemann 可积（有限个不连续点），但 $f_n \to \mathbf{1}_\mathbb{Q}$（Dirichlet 函数）逐点收敛，$\mathbf{1}_\mathbb{Q}$ 不 Riemann 可积。
>
> - **积分极限可能不等于极限的积分**：令 $f_n(x) = n^2 x (1 - x^2)^n$ 在 $[0, 1]$ 上。$f_n(x) \to 0$ 逐点收敛（对每个固定 $x$），但 $\int_0^1 f_n \to \infty \neq 0 = \int_0^1 0$。
