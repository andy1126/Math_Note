---
title: Weierstrass M-判别法
date: 2026-04-11
tags:
  - 实分析
  - 函数级数
  - 一致收敛
  - 绝对收敛
  - Weierstrass
---

# Weierstrass M-判别法

## 预备定义

> [!note] 函数级数的逐点收敛与绝对收敛
> 设 $(f_n)_{n=1}^\infty$ 为从集合 $X$ 到 $\mathbb{R}$（或赋范空间）的函数序列。称级数 $\sum_{n=1}^\infty f_n$ **逐点收敛**，若对每个 $x \in X$，数值级数 $\sum_{n=1}^\infty f_n(x)$ 收敛。称其**逐点绝对收敛**，若对每个 $x \in X$，$\sum_{n=1}^\infty |f_n(x)|$ 收敛。

> [!note] 函数级数的一致收敛
> 称级数 $\sum_{n=1}^\infty f_n$ **一致收敛**，若其部分和序列 $S_N(x) = \sum_{n=1}^N f_n(x)$ 一致收敛于某函数 $S: X \to \mathbb{R}$，即
> $$\sup_{x \in X} \left|S(x) - S_N(x)\right| = \sup_{x \in X} \left|\sum_{n=N+1}^\infty f_n(x)\right| \to 0 \quad (N \to \infty).$$

> [!note] 上确界范数
> 设 $f: X \to \mathbb{R}$ 有界。定义**上确界范数**（sup norm）为
> $$\|f\|_\infty = \sup_{x \in X} |f(x)|.$$
> 一致收敛等价于 $\|S - S_N\|_\infty \to 0$。

> [!abstract] 引理：级数的 Cauchy 准则
> 数值级数 $\sum a_n$ 收敛，当且仅当对任意 $\varepsilon > 0$，存在 $N$ 使得对所有 $m > n \geq N$：
> $$\left|\sum_{k=n+1}^m a_k\right| < \varepsilon.$$

---

## 定理

设 $(f_n)_{n=1}^\infty$ 为从集合 $X$ 到 $\mathbb{R}$ 的函数序列。设 $(M_n)_{n=1}^\infty$ 为非负实数序列，满足：

**(i)** $|f_n(x)| \leq M_n$，$\forall\, x \in X$，$\forall\, n \geq 1$；

**(ii)** $\sum_{n=1}^\infty M_n$ 收敛。

则 $\sum_{n=1}^\infty f_n$ 一致收敛且逐点绝对收敛。

---

## 证明

### 第一步：逐点绝对收敛

对任意固定的 $x \in X$，由条件 (i)：

$$0 \leq |f_n(x)| \leq M_n, \quad \forall\, n.$$

由条件 (ii)，$\sum M_n$ 收敛。由比较判别法（非负项级数），$\sum |f_n(x)|$ 收敛。

由 [[绝对收敛判别法|绝对收敛判别法]]，$\sum f_n(x)$ 也收敛。

由 $x$ 的任意性，$\sum f_n$ 逐点绝对收敛。$\square$

### 第二步：一致收敛

需证对任意 $\varepsilon > 0$，存在 $N$ 使得

$$\sup_{x \in X} \left|\sum_{n=N+1}^\infty f_n(x)\right| < \varepsilon. \quad \cdots (\dagger)$$

#### 2a. 利用 $\sum M_n$ 收敛控制尾部

由 $\sum M_n$ 收敛，其部分和 $T_N = \sum_{n=1}^N M_n$ 构成 Cauchy 序列。对任意 $\varepsilon > 0$，存在 $N_0$ 使得对所有 $m > N \geq N_0$：

$$\sum_{n=N+1}^m M_n < \varepsilon. \quad \cdots (\ast)$$

$\square$

#### 2b. 对 $f_n$ 的部分和取绝对值估计

对任意 $x \in X$ 和 $m > N \geq N_0$，由三角不等式和条件 (i)：

$$\left|\sum_{n=N+1}^m f_n(x)\right| \leq \sum_{n=N+1}^m |f_n(x)| \leq \sum_{n=N+1}^m M_n < \varepsilon.$$

> [!important] 估计与 $x$ 无关
> 右端 $\sum_{n=N+1}^m M_n$ 是常数，不依赖于 $x$。这正是 $M_n$ 作为**一致控制量**的作用——它将所有 $x$ 的尾部估计统一为单一的数值级数尾部。

$\square$

#### 2c. 令 $m \to \infty$ 得到无穷尾部的估计

对固定的 $x \in X$ 和 $N \geq N_0$，由第一步 $\sum f_n(x)$ 收敛，故可令 $m \to \infty$：

$$\left|\sum_{n=N+1}^\infty f_n(x)\right| = \lim_{m \to \infty} \left|\sum_{n=N+1}^m f_n(x)\right| \leq \varepsilon.$$

由 $x$ 的任意性：

$$\sup_{x \in X} \left|\sum_{n=N+1}^\infty f_n(x)\right| \leq \varepsilon, \quad \forall\, N \geq N_0.$$

这给出 $(\dagger)$，故 $\sum f_n$ 一致收敛。$\square$

---

### 结论

1. $\sum f_n$ 逐点绝对收敛。 ✓
2. $\sum f_n$ 一致收敛。 ✓

$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明的核心是**一致控制**：常数序列 $M_n$ 将所有 $x$ 处的尾部估计统一为单一数值级数的尾部估计。
>
> $$\left|\sum_{n=N+1}^m f_n(x)\right| \leq \sum_{n=N+1}^m |f_n(x)| \leq \sum_{n=N+1}^m M_n$$
>
> 右端与 $x$ 无关。$\sum M_n$ 收敛保证右端可任意小，从而**一致地**控制了左端。
>
> 逻辑链为：
> $$|f_n| \leq M_n \xRightarrow{\sum M_n \text{ 收敛}} \text{尾部 } \sum_{n>N} M_n \to 0 \xRightarrow{\text{与 } x \text{ 无关}} \sup_x \left|\sum_{n>N} f_n(x)\right| \to 0$$

> [!warning] M-判别法是充分条件，非必要条件
> 一致收敛的函数级数不一定有满足条件的 $M_n$。例如，$\sum_{n=1}^\infty \frac{(-1)^n}{n} x^n$ 在 $[0, 1]$ 上一致收敛（由 Abel/Dirichlet 判别法），但 $\sup_{x \in [0,1]} \left|\frac{(-1)^n}{n} x^n\right| = \frac{1}{n}$，而 $\sum 1/n$ 发散。即无法找到满足条件的 $M_n$。
>
> 直觉上，M-判别法牺牲了符号信息（用 $|f_n|$ 取代 $f_n$），故无法处理依赖消去的条件收敛情形。
