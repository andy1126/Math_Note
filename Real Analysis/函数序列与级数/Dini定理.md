---
title: Dini 定理
date: 2026-04-11
tags:
  - 实分析
  - 函数序列
  - 一致收敛
  - 紧致性
  - 连续函数
---

# Dini 定理

## 预备定义

> [!note] 逐点收敛
> 设 $\{f_n\}$ 为定义在集合 $X$ 上的实值函数序列，$f: X \to \mathbb{R}$。称 $f_n$ **逐点收敛**（pointwise convergence）于 $f$，若对每个 $x \in X$，
> $$\lim_{n \to \infty} f_n(x) = f(x).$$

> [!note] 一致收敛
> 设 $\{f_n\}$ 为定义在集合 $X$ 上的实值函数序列，$f: X \to \mathbb{R}$。称 $f_n$ **一致收敛**（uniform convergence）于 $f$，若
> $$\lim_{n \to \infty} \sup_{x \in X} |f_n(x) - f(x)| = 0.$$
> 即：对任意 $\varepsilon > 0$，存在 $N \in \mathbb{N}$，使得对一切 $n \geq N$ 及一切 $x \in X$，均有 $|f_n(x) - f(x)| < \varepsilon$。

> [!note] 紧致集
> 度量空间 $(X, d)$ 的子集 $K$ 称为**紧致的**（compact），若 $K$ 的每个开覆盖都有有限子覆盖。
> 在 $\mathbb{R}^n$ 中，由 Heine-Borel 定理，紧致等价于有界且闭。

> [!abstract] 引理：紧致集上的连续函数有最大值
> 设 $K$ 为紧致度量空间，$g: K \to \mathbb{R}$ 为连续函数。则 $g$ 在 $K$ 上取到最大值和最小值。

---

## 定理

设 $K$ 为紧致度量空间，$\{f_n\}$ 为 $K$ 上的连续实值函数序列，$f: K \to \mathbb{R}$ 为连续函数。若

1. $f_n$ 逐点收敛于 $f$；
2. 对每个 $x \in K$，序列 $\{f_n(x)\}$ 关于 $n$ 单调递减（即 $f_1(x) \geq f_2(x) \geq \cdots$），

则 $f_n$ **一致收敛**于 $f$。

---

## 证明

令 $g_n = f_n - f$。则：
- 每个 $g_n$ 连续（连续函数之差仍连续）；
- $g_n(x) \geq 0$（因 $f_n(x) \geq f(x)$，由单调递减及逐点极限）；
- $g_n(x) \geq g_{n+1}(x)$（因 $f_n(x) \geq f_{n+1}(x)$）；
- $g_n(x) \to 0$ 对每个 $x \in K$。

**目标**：证明 $\sup_{x \in K} g_n(x) \to 0$。

### 构造开覆盖

任取 $\varepsilon > 0$。对每个 $n \in \mathbb{N}$，定义

$$K_n = \{x \in K : g_n(x) < \varepsilon\}.$$

#### 第一步：$K_n$ 是开集

由 $g_n$ 的连续性，$K_n = g_n^{-1}((-\infty, \varepsilon))$ 是开集 $(-\infty, \varepsilon)$ 在连续映射下的原像，故 $K_n$ 是 $K$ 中的开集。$\square$

#### 第二步：$\{K_n\}$ 是递增的

若 $x \in K_n$，则 $g_n(x) < \varepsilon$。由 $g_{n+1}(x) \leq g_n(x) < \varepsilon$，得 $x \in K_{n+1}$。

故 $K_1 \subseteq K_2 \subseteq K_3 \subseteq \cdots$。$\square$

#### 第三步：$\{K_n\}$ 覆盖 $K$

对任意 $x \in K$，由 $g_n(x) \to 0$，存在 $N_x$ 使得 $g_{N_x}(x) < \varepsilon$，即 $x \in K_{N_x}$。

故 $K = \bigcup_{n=1}^{\infty} K_n$。$\square$

### 应用紧致性

$\{K_n\}_{n=1}^{\infty}$ 是 $K$ 的一个开覆盖。由 $K$ 的紧致性，存在有限子覆盖：

$$K = K_{n_1} \cup K_{n_2} \cup \cdots \cup K_{n_p}.$$

由 $\{K_n\}$ 的递增性，令 $N = \max\{n_1, n_2, \ldots, n_p\}$，则

$$K = K_N.$$

> [!important] 递增覆盖 + 紧致性 = 有限步覆盖
> 由于 $K_1 \subseteq K_2 \subseteq \cdots$，有限子覆盖中最大的那个 $K_N$ 就已经覆盖了整个 $K$。这是本证明最关键的一步。

### 得出一致收敛

$K = K_N$ 意味着：对一切 $x \in K$，$g_N(x) < \varepsilon$。

对任意 $n \geq N$，由 $g_n(x) \leq g_N(x) < \varepsilon$ 对一切 $x \in K$ 成立，得

$$\sup_{x \in K} g_n(x) \leq \varepsilon \quad \text{对一切 } n \geq N.$$

由 $\varepsilon > 0$ 的任意性，

$$\sup_{x \in K} g_n(x) \to 0 \quad (n \to \infty),$$

即 $f_n$ 一致收敛于 $f$。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明的核心是将**逐点收敛转化为开覆盖问题**，再利用**紧致性**从中提取有限子覆盖：
> 1. 令 $g_n = f_n - f \geq 0$，将问题归结为证明 $\sup g_n \to 0$；
> 2. 利用 $g_n$ 的连续性，构造开集 $K_n = \{g_n < \varepsilon\}$；
> 3. 单调性保证 $\{K_n\}$ 递增，逐点收敛保证 $\{K_n\}$ 覆盖 $K$；
> 4. 紧致性给出有限子覆盖，而递增性使有限子覆盖退化为**单个 $K_N$**；
> 5. 从而一举获得对一切 $x$ 同时成立的估计。
>
> 这一论证展示了**分析中紧致性的典型用法**：将依赖于 $x$ 的局部信息（逐点收敛）提升为全局一致的结论。

> [!warning] 各条件的必要性
> Dini 定理的四个条件（紧致性、$f_n$ 连续、$f$ 连续、单调性）**缺一不可**：
> - **去掉紧致性**：$f_n(x) = x^n$ 在 $[0, 1)$ 上逐点趋于 $0$ 但不一致收敛。
> - **去掉 $f_n$ 的连续性**：令 $f_n = \mathbf{1}_{\{1/n, 2/n, \ldots, 1\}}$ 在 $[0,1]$ 上，逐点趋于 $\mathbf{1}_{(0,1] \cap \mathbb{Q}}$，但不一致。
> - **去掉 $f$ 的连续性**：$f_n(x) = x^n$ 在 $[0, 1]$ 上，逐点极限 $f$ 在 $x = 1$ 处不连续，收敛不一致。
> - **去掉单调性**：可构造在 $[0,1]$ 上"漫游的尖峰"函数序列，逐点趋于 $0$ 但 $\sup$ 不趋于 $0$。
