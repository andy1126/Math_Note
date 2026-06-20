---
title: 不存在可数无限的Power Set
tags:
  - real-analysis
  - set-theory
  - cardinality
  - cantor
---

# 不存在可数无限的Power Set

## 命题

对任意集合 $X$，其 power set $\mathcal{P}(X)$ 不是 countably infinite 的。换言之，不存在集合 $X$ 使得 $\mathcal{P}(X)$ 与 $\mathbb{N}$ 之间存在 bijection。

## 前置定义与定理

> [!info] 定义：Power Set（幂集）
> 设 $X$ 是一个集合。$X$ 的 **power set** 定义为 $X$ 的所有子集构成的集合，记作
> $$\mathcal{P}(X) := \{A : A \subseteq X\}.$$
> 例如，若 $X = \{1, 2\}$，则 $\mathcal{P}(X) = \{\emptyset, \{1\}, \{2\}, \{1,2\}\}$。

> [!info] 定义：Countably Infinite（可数无限）
> 一个集合 $S$ 称为 **countably infinite** 的，当且仅当存在一个从 $\mathbb{N}$ 到 $S$ 的 bijection，即 $S$ 与自然数集 $\mathbb{N}$ 具有相同的 cardinality。记作 $|S| = \aleph_0$（或 $|S| = |\mathbb{N}|$）。

> [!info] 定义：有限集（Finite Set）
> 一个集合 $S$ 称为**有限的**，当且仅当存在自然数 $n$ 使得 $S$ 与 $\{1, 2, \ldots, n\}$ 之间存在 bijection（当 $n = 0$ 时即 $S = \emptyset$）。此时记 $|S| = n$。

> [!info] 定义：Uncountable（不可数）
> 一个集合 $S$ 称为 **uncountable** 的，当且仅当 $S$ 是 infinite 的但不是 countably infinite 的。等价地，$|S| > \aleph_0$。

> [!info] 引理：有限集的 Power Set 是有限的
> 若 $X$ 是有限集且 $|X| = n$，则 $|\mathcal{P}(X)| = 2^n$。
>
> **证明概要**：对 $X$ 的每个元素，一个子集 $A \subseteq X$ 要么包含它、要么不包含它，共有 $2$ 种选择。$n$ 个元素独立选择，共 $2^n$ 种组合，故 $|\mathcal{P}(X)| = 2^n$。$\blacksquare$

> [!important] Cantor 定理
> 设 $X$ 是任意集合。则不存在从 $X$ 到 $\mathcal{P}(X)$ 的 surjection。
>
> 等价地，$|X| < |\mathcal{P}(X)|$，即 power set 的 cardinality 严格大于原集合的 cardinality。

### Cantor 定理的证明

此证明使用经典的**对角线论证法**（diagonal argument）。

**用反证法。** 假设存在一个 surjection $g: X \to \mathcal{P}(X)$。即对 $\mathcal{P}(X)$ 中的每一个元素（即 $X$ 的每一个子集），都存在 $X$ 中的某个元素映射到它。

**构造关键集合。** 定义集合

$$
B := \{x \in X : x \notin g(x)\}.
$$

注意 $g(x) \subseteq X$（因为 $g(x) \in \mathcal{P}(X)$），所以 $x \notin g(x)$ 是良定义的条件。显然 $B \subseteq X$，故 $B \in \mathcal{P}(X)$。

**利用 surjection 假设。** 由于 $g$ 是 surjection，且 $B \in \mathcal{P}(X)$，故存在某个 $x_0 \in X$ 使得

$$
g(x_0) = B.
$$

**导出矛盾。** 现在考虑 $x_0$ 是否属于 $B$：

- **情形一：$x_0 \in B$。** 由 $B$ 的定义，$x_0 \in B$ 意味着 $x_0 \notin g(x_0)$。但 $g(x_0) = B$，故 $x_0 \notin B$。这与 $x_0 \in B$ 矛盾。

- **情形二：$x_0 \notin B$。** 由 $B$ 的定义，$x_0 \notin B$ 意味着条件 "$x_0 \notin g(x_0)$" 不成立，即 $x_0 \in g(x_0)$。但 $g(x_0) = B$，故 $x_0 \in B$。这与 $x_0 \notin B$ 矛盾。

两种情形均导致矛盾，故假设不成立。因此不存在从 $X$ 到 $\mathcal{P}(X)$ 的 surjection。

又因为映射 $x \mapsto \{x\}$ 是从 $X$ 到 $\mathcal{P}(X)$ 的 injection，所以 $|X| \leq |\mathcal{P}(X)|$。结合不存在 surjection，我们得到

$$
|X| < |\mathcal{P}(X)|. \quad \blacksquare
$$

## 主命题的证明

我们证明：对任意集合 $X$，$\mathcal{P}(X)$ 不是 countably infinite 的。

分三种情形讨论：

### 情形一：$X$ 是有限集

设 $|X| = n$，其中 $n$ 是自然数。由上述引理，$|\mathcal{P}(X)| = 2^n$。

由于 $2^n$ 是自然数，$\mathcal{P}(X)$ 是一个有限集。有限集不是 countably infinite 的（countably infinite 要求集合是 infinite 的），故在此情形下 $\mathcal{P}(X)$ 不是 countably infinite 的。

### 情形二：$X$ 是 countably infinite 的

此时 $|X| = \aleph_0$。由 Cantor 定理，

$$
|\mathcal{P}(X)| > |X| = \aleph_0.
$$

这意味着 $\mathcal{P}(X)$ 的 cardinality 严格大于 $\aleph_0$，故 $\mathcal{P}(X)$ 是 uncountable 的。Uncountable 集合不是 countably infinite 的，故在此情形下 $\mathcal{P}(X)$ 不是 countably infinite 的。

### 情形三：$X$ 是 uncountable 的

此时 $|X| > \aleph_0$。由 Cantor 定理，

$$
|\mathcal{P}(X)| > |X| > \aleph_0.
$$

同样地，$\mathcal{P}(X)$ 是 uncountable 的，故不是 countably infinite 的。

### 结论

在所有情形中，$\mathcal{P}(X)$ 要么是有限的，要么是 uncountable 的，==从不是 countably infinite 的==。

$$
\boxed{\text{不存在集合 } X \text{ 使得 } \mathcal{P}(X) \text{ 是 countably infinite 的。}}
$$

$\blacksquare$

> [!note] 备注
> 本命题的核心在于 Cantor 定理：power set 的 cardinality 总是严格大于原集合。这一定理的深刻之处在于它对**任意**集合成立——无论有限还是无限。它表明不存在"最大的"cardinality：给定任意集合 $X$，总可以通过取 power set 得到一个严格更大的集合。这也是集合论中 cardinality 层级
> $$\aleph_0 < 2^{\aleph_0} < 2^{2^{\aleph_0}} < \cdots$$
> 的来源。
