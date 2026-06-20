---
title: Hausdorff 空间中紧致子集是闭的
date: 2026-04-11
tags:
  - 实分析
  - 拓扑
  - Hausdorff空间
  - 紧致性
  - 闭集
---

# Hausdorff 空间中紧致子集是闭的

## 预备定义

> [!note] 拓扑空间
> **拓扑空间** $(X, \mathcal{T})$ 由集合 $X$ 和开集族 $\mathcal{T} \subseteq \mathcal{P}(X)$ 组成，满足：
> 1. $\varnothing, X \in \mathcal{T}$；
> 2. 有限交封闭：$U_1, \dots, U_n \in \mathcal{T} \implies U_1 \cap \cdots \cap U_n \in \mathcal{T}$；
> 3. 任意并封闭：$\{U_\alpha\}_{\alpha \in A} \subseteq \mathcal{T} \implies \bigcup_{\alpha \in A} U_\alpha \in \mathcal{T}$。
>
> 度量空间 $(X, d)$ 自然诱导一个拓扑，其中 $U$ 为开集当且仅当 $U$ 中每个点都有一个完全包含在 $U$ 中的开球。

> [!note] Hausdorff 空间
> 称拓扑空间 $X$ 为 **Hausdorff 空间**（$T_2$ 空间），若对任意 $x, y \in X$（$x \neq y$），存在开集 $U, V$ 使得
> $$x \in U, \quad y \in V, \quad U \cap V = \varnothing.$$
> 即任意两个不同的点可用不相交的开集分离。
>
> 所有度量空间都是 Hausdorff 的：取 $r = d(x, y)/2$，令 $U = B(x, r)$，$V = B(y, r)$。

> [!note] 紧致集
> 设 $X$ 为拓扑空间，$K \subseteq X$。称 $K$ 是**紧致**的，若 $K$ 的每一个开覆盖都有有限子覆盖。

> [!note] 闭集
> 设 $X$ 为拓扑空间。称 $F \subseteq X$ 为**闭集**，若其补集 $X \setminus F$ 为开集。等价地，$F$ 包含其所有极限点。

---

## 定理

设 $X$ 为 Hausdorff 空间，$K \subseteq X$ 紧致。则 $K$ 是闭集。

---

## 证明

**目标**：证明 $X \setminus K$ 是开集。即对任意 $p \in X \setminus K$，存在 $p$ 的开邻域 $W$ 使得 $W \subseteq X \setminus K$（即 $W \cap K = \varnothing$）。

取任意 $p \in X \setminus K$。

### 第一步：对 $K$ 中每个点用 Hausdorff 性质分离

对每个 $q \in K$，由 $p \neq q$（因为 $p \notin K$ 而 $q \in K$）和 $X$ 的 Hausdorff 性质，存在开集 $U_q, V_q$ 使得

$$p \in U_q, \quad q \in V_q, \quad U_q \cap V_q = \varnothing. \quad \cdots (\ast)$$

$\square$

### 第二步：构造 $K$ 的开覆盖并提取有限子覆盖

开集族 $\{V_q\}_{q \in K}$ 覆盖 $K$（每个 $q \in K$ 属于 $V_q$）。由 $K$ 紧致，存在有限个点 $q_1, \dots, q_m \in K$ 使得

$$K \subseteq V_{q_1} \cup V_{q_2} \cup \cdots \cup V_{q_m}. \quad \cdots (\star)$$

$\square$

### 第三步：取有限交得到 $p$ 的开邻域

令

$$W = U_{q_1} \cap U_{q_2} \cap \cdots \cap U_{q_m}.$$

- **$W$ 是开集**：有限个开集的交是开集。
- **$p \in W$**：由 $(\ast)$，$p \in U_{q_i}$ 对所有 $1 \leq i \leq m$。

$\square$

### 第四步：证明 $W \cap K = \varnothing$

设 $x \in W$。则 $x \in U_{q_i}$ 对所有 $1 \leq i \leq m$。

由 $(\ast)$，$U_{q_i} \cap V_{q_i} = \varnothing$，故 $x \notin V_{q_i}$ 对所有 $i$。因此

$$x \notin V_{q_1} \cup \cdots \cup V_{q_m}.$$

由 $(\star)$，$K \subseteq V_{q_1} \cup \cdots \cup V_{q_m}$，故 $x \notin K$。

这对任意 $x \in W$ 成立，故 $W \cap K = \varnothing$，即 $W \subseteq X \setminus K$。$\square$

### 结论

对任意 $p \in X \setminus K$，找到了开邻域 $W$ 使得 $W \subseteq X \setminus K$。故 $X \setminus K$ 是开集，从而 $K$ 是闭集。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明的核心手法是**先分离后压缩**：
>
> 1. **Hausdorff 分离**：对 $K$ 中的每个点 $q$，用 Hausdorff 性质将 $p$ 和 $q$ 分离到不相交的开集 $U_q$ 和 $V_q$ 中；
> 2. **紧致压缩**：$\{V_q\}$ 覆盖 $K$，紧致性提取有限子覆盖 $V_{q_1}, \dots, V_{q_m}$；
> 3. **有限交**：对应的 $U_{q_1}, \dots, U_{q_m}$ 取**有限交** $W = \bigcap U_{q_i}$——有限交保持开集性。$W$ 是 $p$ 的邻域，且与 $K$ 不相交。
>
> 要点在于：Hausdorff 性质对**每对点**给出一对分离开集，但分离 $p$ 与**所有** $q \in K$ 需要无穷多对。紧致性将其压缩为有限多对，使得有限交仍为开集。

> [!warning] Hausdorff 条件不可省略
> 在非 Hausdorff 空间中，紧致子集未必闭。例如，取 $X = \{0, 1\}$，拓扑 $\mathcal{T} = \{\varnothing, \{0\}, \{0,1\}\}$（Sierpiński 空间）。子集 $\{0\}$ 是紧致的（有限集），但 $X \setminus \{0\} = \{1\}$ 不是开集，故 $\{0\}$ 不是闭集。
>
> 反过来，**闭子集未必紧致**（即使在 Hausdorff 空间中）：$\mathbb{R}$ 是 Hausdorff 的，$[0, +\infty)$ 是闭集但不紧致。然而在**紧致** Hausdorff 空间中，闭子集一定紧致——两者在紧致 Hausdorff 空间中等价。
