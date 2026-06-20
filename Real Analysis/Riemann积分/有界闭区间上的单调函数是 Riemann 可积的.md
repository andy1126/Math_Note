---
title: 有界闭区间上的单调函数是 Riemann 可积的
date: 2026-04-11
tags:
  - 实分析
  - Riemann积分
  - 单调函数
  - Darboux和
---

# 有界闭区间上的单调函数是 Riemann 可积的

## 预备定义

> [!note] 分划
> 设 $[a, b]$ 为有界闭区间。$[a, b]$ 的一个**分划**（partition）是一个有限递增序列
> $$P = \{x_0, x_1, \dots, x_n\}, \quad a = x_0 < x_1 < \cdots < x_n = b.$$
> 每个 $[x_{k-1}, x_k]$（$k = 1, \dots, n$）称为 $P$ 的一个**子区间**，其长度为 $\Delta x_k = x_k - x_{k-1}$。

> [!note] 上和与下和
> 设 $f: [a, b] \to \mathbb{R}$ 为有界函数，$P = \{x_0, \dots, x_n\}$ 为 $[a, b]$ 的分划。定义：
> - $M_k = \sup_{x \in [x_{k-1}, x_k]} f(x)$，$m_k = \inf_{x \in [x_{k-1}, x_k]} f(x)$；
> - **上和**（upper Darboux sum）：$U(f, P) = \displaystyle\sum_{k=1}^{n} M_k \, \Delta x_k$；
> - **下和**（lower Darboux sum）：$L(f, P) = \displaystyle\sum_{k=1}^{n} m_k \, \Delta x_k$。

> [!note] Riemann 可积的判定准则
> 有界函数 $f: [a, b] \to \mathbb{R}$ 是 **Riemann 可积**的，当且仅当对任意 $\varepsilon > 0$，存在 $[a, b]$ 的分划 $P$，使得
> $$U(f, P) - L(f, P) < \varepsilon.$$

---

## 定理

设 $f: [a, b] \to \mathbb{R}$ 为单调函数。则 $f$ 是 Riemann 可积的。

---

## 证明

不失一般性，设 $f$ 在 $[a, b]$ 上**单调递增**（递减的情形完全类似）。

### 第一步：构造等距分划

对任意正整数 $n$，取 $[a, b]$ 的等距分划

$$P_n = \{x_0, x_1, \dots, x_n\}, \quad x_k = a + k \cdot \frac{b - a}{n}, \quad k = 0, 1, \dots, n.$$

每个子区间长度为

$$\Delta x_k = \frac{b - a}{n}, \quad \forall\, k = 1, \dots, n.$$

$\square$

### 第二步：利用单调性确定各子区间上的上确界与下确界

由于 $f$ 单调递增，在每个子区间 $[x_{k-1}, x_k]$ 上：

$$m_k = \inf_{[x_{k-1}, x_k]} f = f(x_{k-1}), \quad M_k = \sup_{[x_{k-1}, x_k]} f = f(x_k).$$

$\square$

### 第三步：计算 $U(f, P_n) - L(f, P_n)$

$$U(f, P_n) - L(f, P_n) = \sum_{k=1}^{n} (M_k - m_k)\, \Delta x_k = \sum_{k=1}^{n} [f(x_k) - f(x_{k-1})] \cdot \frac{b - a}{n}.$$

提取公因子 $\dfrac{b - a}{n}$，得

$$= \frac{b - a}{n} \sum_{k=1}^{n} [f(x_k) - f(x_{k-1})].$$

> [!important] 伸缩求和
> 上式中的求和是一个**伸缩和**（telescoping sum）：
> $$\sum_{k=1}^{n} [f(x_k) - f(x_{k-1})] = f(x_n) - f(x_0) = f(b) - f(a).$$
> 中间项全部消去，仅留首尾之差。

因此

$$U(f, P_n) - L(f, P_n) = \frac{(b - a)[f(b) - f(a)]}{n}. \quad \cdots (\ast)$$

$\square$

### 第四步：验证 Riemann 可积判定准则

对任意 $\varepsilon > 0$，取正整数 $n$ 满足

$$n > \frac{(b - a)[f(b) - f(a)]}{\varepsilon}.$$

> [!info] 为何这样的 $n$ 存在
> 由 Archimedes 性质，对任意正实数，总存在大于它的正整数。若 $f(b) = f(a)$（即 $f$ 为常数函数），则 $(\ast)$ 式右端对一切 $n$ 均为 $0 < \varepsilon$，任取 $n = 1$ 即可。

由 $(\ast)$，

$$U(f, P_n) - L(f, P_n) = \frac{(b - a)[f(b) - f(a)]}{n} < \varepsilon.$$

由 Riemann 可积的判定准则，$f$ 在 $[a, b]$ 上 Riemann 可积。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明的核心是**等距分划 + 伸缩求和**：
>
> 1. **等距分划**使每个子区间长度为 $\dfrac{b-a}{n}$，可以作为公因子提出；
> 2. **单调性**使上确界与下确界恰好在子区间端点取到，从而 $M_k - m_k = f(x_k) - f(x_{k-1})$；
> 3. **伸缩求和**将 $n$ 项之和化为 $f(b) - f(a)$，与 $n$ 无关；
> 4. 最终 $U - L = \dfrac{(b-a)[f(b)-f(a)]}{n} \to 0$，由 $n$ 的任意性即得。
>
> 本质上，单调函数的"振幅总量"是固定的（$= f(b) - f(a)$），等距分划只是把它均匀摊开，每份振幅为 $O(1/n)$。

> [!warning] 单调性的本质作用
> 单调性保证了**端点即为极值点**，这是伸缩求和能奏效的关键。对于一般的有界函数，$\sum (M_k - m_k)$ 未必能化简为伸缩和，上和与下和之差的控制需要更精细的分析（如一致连续性）。
