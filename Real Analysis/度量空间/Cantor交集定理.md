---
title: Cantor 交集定理
date: 2026-04-11
tags:
  - 实分析
  - 度量空间
  - 完备性
  - 紧致性
  - Cantor
  - 嵌套闭集
---

# Cantor 交集定理

## 预备定义

> [!note] 完备度量空间
> 称度量空间 $(X, d)$ 是**完备**的（complete），若 $X$ 中的每个 Cauchy 序列都收敛于 $X$ 中的某个点。

> [!note] 集合的直径
> 设 $(X, d)$ 为度量空间，$A \subseteq X$ 非空。$A$ 的**直径**（diameter）定义为
> $$\operatorname{diam}(A) = \sup\{d(x, y) : x, y \in A\}.$$
> 若 $\operatorname{diam}(A) < \infty$，称 $A$ 为**有界**的。

> [!note] 嵌套序列
> 称集合序列 $(F_n)_{n=1}^\infty$ 为**嵌套**的（nested），若
> $$F_1 \supseteq F_2 \supseteq F_3 \supseteq \cdots$$

---

## 定理

设 $(X, d)$ 为完备度量空间，$(F_n)_{n=1}^\infty$ 为非空闭集的嵌套序列，且

$$\operatorname{diam}(F_n) \to 0 \quad (n \to \infty).$$

则交集恰好是一个单点：存在唯一的 $p \in X$ 使得

$$\bigcap_{n=1}^\infty F_n = \{p\}.$$

---

## 证明

### 第一步：构造 Cauchy 序列

对每个 $n \geq 1$，$F_n \neq \varnothing$，取 $x_n \in F_n$。

**断言**：$(x_n)$ 是 Cauchy 序列。

对任意 $\varepsilon > 0$。由 $\operatorname{diam}(F_n) \to 0$，存在 $N$ 使得

$$n \geq N \implies \operatorname{diam}(F_n) < \varepsilon. \quad \cdots (\ast)$$

对任意 $m, n \geq N$（不妨设 $m \geq n$）：由嵌套性 $F_m \subseteq F_n \subseteq F_N$，故 $x_m, x_n \in F_N$。由 $(\ast)$：

$$d(x_m, x_n) \leq \operatorname{diam}(F_N) < \varepsilon.$$

故 $(x_n)$ 是 Cauchy 序列。$\square$

### 第二步：Cauchy 序列收敛

由 $X$ 完备，$(x_n)$ 收敛于某个 $p \in X$：

$$x_n \to p. \quad \cdots (\star)$$

$\square$

### 第三步：$p$ 属于每个 $F_n$

取任意 $n \geq 1$。对所有 $k \geq n$，由嵌套性 $x_k \in F_k \subseteq F_n$。故 $(x_k)_{k \geq n}$ 是 $F_n$ 中的序列，且 $x_k \to p$。

由 $F_n$ 是闭集，闭集包含其中序列的所有极限，故

$$p \in F_n.$$

由 $n$ 的任意性：

$$p \in \bigcap_{n=1}^\infty F_n. \quad \cdots (1)$$

$\square$

### 第四步：交集中至多一个点

设 $q \in \bigcap_{n=1}^\infty F_n$。则对每个 $n$，$p, q \in F_n$，故

$$0 \leq d(p, q) \leq \operatorname{diam}(F_n).$$

由 $\operatorname{diam}(F_n) \to 0$，得 $d(p, q) = 0$，即 $q = p$。$\square$

### 结论

由 $(1)$，$p \in \bigcap F_n$，故交集非空。由第四步，交集中仅有 $p$。因此

$$\bigcap_{n=1}^\infty F_n = \{p\}. \quad \blacksquare$$

---

## 证明思路总结

> [!tip] 关键思想
> 证明的逻辑链清晰且每步不可或缺：
>
> $$\text{嵌套 + } \operatorname{diam} \to 0 \xRightarrow{} (x_n) \text{ Cauchy} \xRightarrow{\text{完备}} x_n \to p \xRightarrow{F_n \text{ 闭}} p \in \bigcap F_n \xRightarrow{\operatorname{diam} \to 0} \bigcap F_n = \{p\}$$
>
> 三个假设各司其职：
> - **嵌套**：保证 $x_m, x_n$ 同处于 $F_{\min(m,n)}$，使距离可用直径控制；
> - **$\operatorname{diam}(F_n) \to 0$**：保证序列是 Cauchy 的，且交集至多一个点；
> - **闭**：保证极限点 $p$ 不会"逃出" $F_n$；
> - **完备**：保证 Cauchy 序列有极限。

> [!warning] 每个条件都不可省略
>
> **去掉完备性**：$X = (0, 1)$（不完备），$F_n = (0, 1/n]$ 闭（在 $X$ 中）、嵌套、直径趋零，但 $\bigcap F_n = \varnothing$。
>
> **去掉闭性**：$X = \mathbb{R}$，$F_n = (0, 1/n)$ 开、嵌套、直径趋零，$\bigcap F_n = \varnothing$。
>
> **去掉 $\operatorname{diam} \to 0$**：$X = \mathbb{R}$，$F_n = [n, +\infty)$ 闭、嵌套、非空，但 $\bigcap F_n = \varnothing$。此时交集可以为空，且即使非空也可能不是单点（例如 $F_n = [0, 1]$ 对所有 $n$，交集是整个 $[0,1]$）。
>
> **紧致版本**：若将"完备 + 闭 + $\operatorname{diam} \to 0$"替换为"紧致"，则仅需嵌套和非空即可保证 $\bigcap F_n \neq \varnothing$（有限交性质），但不保证单点。紧致版本中直径趋零仍是保证交集为单点的条件。
