---
title: 一致有界性原理（Banach-Steinhaus 定理）
date: 2026-04-11
tags:
  - 泛函分析
  - Banach空间
  - 有界线性算子
  - Baire范畴定理
  - Banach-Steinhaus定理
---

# 一致有界性原理（Banach-Steinhaus 定理）

## 预备定义

> [!note] Banach 空间
> 称赋范线性空间 $(X, \|\cdot\|)$ 为 **Banach 空间**（Banach space），若 $X$ 关于 $\|\cdot\|$ 诱导的度量是完备的，即 $X$ 中每个 Cauchy 序列都收敛。

> [!note] 有界线性算子
> 设 $X, Y$ 为赋范空间。称线性映射 $T : X \to Y$ 为**有界线性算子**（bounded linear operator），若存在常数 $C \geq 0$ 使得
> $$\|Tx\|_Y \leq C\|x\|_X, \quad \forall\, x \in X.$$
> 最小的这样的 $C$ 称为 $T$ 的**算子范数**：
> $$\|T\| = \sup_{\|x\| \leq 1} \|Tx\| = \sup_{\|x\| = 1} \|Tx\| = \sup_{x \neq 0} \frac{\|Tx\|}{\|x\|}.$$
> 全体 $X \to Y$ 的有界线性算子记为 $\mathcal{B}(X, Y)$。

> [!note] 无处稠密集与 Baire 范畴
> 设 $(X, d)$ 为度量空间。
> - 称集合 $A \subseteq X$ 为**无处稠密的**（nowhere dense），若 $\overline{A}$ 的内部为空，即 $\operatorname{int}(\overline{A}) = \varnothing$。
> - 称集合 $A$ 为**第一范畴集**（meagre / first category），若 $A$ 可表示为可数个无处稠密集的并。
> - 称集合 $A$ 为**第二范畴集**（non-meagre / second category），若 $A$ 不是第一范畴集。

> [!abstract] 引理：Baire 范畴定理
> 设 $(X, d)$ 为完备度量空间。则 $X$ 是第二范畴集，即 $X$ 不能表示为可数个无处稠密集的并。
>
> 等价表述：若 $X = \bigcup_{n=1}^{\infty} F_n$，其中每个 $F_n$ 为闭集，则至少存在某个 $F_N$ 有非空内部（即 $\operatorname{int}(F_N) \neq \varnothing$）。

---

## 定理

设 $X$ 为 Banach 空间，$Y$ 为赋范空间，$\{T_\alpha\}_{\alpha \in \Lambda} \subseteq \mathcal{B}(X, Y)$ 为一族有界线性算子。若该族算子**逐点有界**，即

$$\sup_{\alpha \in \Lambda} \|T_\alpha x\| < \infty, \quad \forall\, x \in X,$$

则该族算子**一致有界**，即

$$\sup_{\alpha \in \Lambda} \|T_\alpha\| < \infty.$$

---

## 证明

### 第一步：构造闭集覆盖

对每个 $n \in \mathbb{N}$，令

$$F_n = \bigl\{ x \in X : \sup_{\alpha \in \Lambda} \|T_\alpha x\| \leq n \bigr\} = \bigcap_{\alpha \in \Lambda} \bigl\{ x \in X : \|T_\alpha x\| \leq n \bigr\}.$$

#### $F_n$ 是闭集

对每个固定的 $\alpha$，映射 $x \mapsto \|T_\alpha x\|$ 是连续的（因为 $T_\alpha$ 有界），故 $\{x : \|T_\alpha x\| \leq n\}$ 是闭集。$F_n$ 作为任意多个闭集的交，仍为闭集。$\square$

#### $\{F_n\}$ 覆盖 $X$

由逐点有界条件，对每个 $x \in X$，存在 $n \in \mathbb{N}$ 使得 $\sup_\alpha \|T_\alpha x\| \leq n$，即 $x \in F_n$。故

$$X = \bigcup_{n=1}^{\infty} F_n. \quad \square$$

### 第二步：应用 Baire 范畴定理

$X$ 是 Banach 空间（完备度量空间），且 $X = \bigcup_{n=1}^{\infty} F_n$，其中每个 $F_n$ 为闭集。由 Baire 范畴定理，存在 $N \in \mathbb{N}$ 使得 $F_N$ 有非空内部。即存在 $x_0 \in X$ 和 $r > 0$ 使得

$$B_r(x_0) \subseteq F_N. \quad \cdots (\ast)$$

> [!important] Baire 范畴定理的核心运用
> 这是完备性发挥作用的关键一步。若 $X$ 不完备，Baire 定理不适用，所有 $F_n$ 可能都是无处稠密的，定理的结论将不成立。

### 第三步：从逐点界推导一致界

**目标**：证明 $\|T_\alpha\| \leq \dfrac{2N}{r}$ 对一切 $\alpha \in \Lambda$ 成立。

设 $x \in X$ 满足 $\|x\| \leq 1$。则 $x_0 + rx \in B_r(x_0)$，由 $(\ast)$ 得 $x_0 + rx \in F_N$，即

$$\sup_{\alpha} \|T_\alpha(x_0 + rx)\| \leq N. \quad \cdots (1)$$

又 $x_0 \in B_r(x_0) \subseteq F_N$，故

$$\sup_{\alpha} \|T_\alpha x_0\| \leq N. \quad \cdots (2)$$

由三角不等式和线性性，对任意 $\alpha \in \Lambda$：

$$r\|T_\alpha x\| = \|T_\alpha(rx)\| = \|T_\alpha(x_0 + rx) - T_\alpha x_0\| \leq \|T_\alpha(x_0 + rx)\| + \|T_\alpha x_0\|.$$

结合 $(1)$ 和 $(2)$：

$$r\|T_\alpha x\| \leq N + N = 2N.$$

因此

$$\|T_\alpha x\| \leq \frac{2N}{r}, \quad \forall\, \|x\| \leq 1,\; \forall\, \alpha \in \Lambda.$$

取上确界得

$$\sup_{\alpha \in \Lambda} \|T_\alpha\| = \sup_{\alpha} \sup_{\|x\| \leq 1} \|T_\alpha x\| \leq \frac{2N}{r} < \infty. \quad \blacksquare$$

---

## 证明思路总结

> [!tip] 关键思想
> 证明的本质是将**逐点条件**（对每个 $x$ 的约束）转化为**一致条件**（对所有算子的约束），桥梁是 Baire 范畴定理：
> 1. 用逐点有界性构造闭集覆盖 $X = \bigcup F_n$；
> 2. 由 Baire 定理（完备性！），某个 $F_N$ 包含一个球 $B_r(x_0)$——这提供了一个"均匀好"的邻域；
> 3. 利用线性性将任意单位球中的点平移到该邻域中，从而将局部的界转化为全局的界。
>
> 核心不等式 $\|T_\alpha\| \leq 2N/r$ 中，$N$ 来自 Baire 定理给出的闭集编号，$r$ 来自内部球的半径。

> [!warning] Banach 空间条件的必要性
> $X$ 的完备性**不可省略**。反例：取 $X = c_{00}$（有限支撑序列空间，配 $\ell^\infty$ 范数），定义 $T_n : X \to \mathbb{R}$ 为
> $$T_n(x) = n \cdot x_n.$$
> 则 $\|T_n\| = n \to \infty$（不一致有界），但对每个固定的 $x \in c_{00}$，$x$ 仅有有限个非零分量，故 $T_n(x) = 0$ 当 $n$ 充分大时（逐点有界）。这不矛盾，因为 $c_{00}$ 不完备。

> [!tip] 经典应用：Fourier 级数的发散
> 一致有界性原理可用来证明**存在连续函数其 Fourier 级数在某点发散**。令 $T_n(f) = S_n f(0)$（Fourier 部分和在原点的值），可以证明 $\|T_n\| = \|D_n\|_{L^1} \to \infty$（Dirichlet 核的 $L^1$ 范数趋于无穷）。若对一切连续函数 $f$ 均有 $\sup_n |S_n f(0)| < \infty$，则由一致有界性原理 $\sup_n \|T_n\| < \infty$，矛盾。故存在连续函数使得 $\sup_n |S_n f(0)| = \infty$。
