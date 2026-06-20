---
title: Lebesgue 外测度与 Carathéodory 可测集
date: 2026-05-28
tags:
  - 实分析
  - 测度论
  - Lebesgue测度
  - 外测度
  - Carathéodory
  - σ-代数
---

# Lebesgue 外测度与 Carathéodory 可测集

## 预备定义

> [!note] 外测度
> 设 $X$ 为非空集合。称映射 $\mu^\ast: \mathcal{P}(X) \to [0, +\infty]$ 为 $X$ 上的**外测度**（outer measure），若满足：
> 1. $\mu^\ast(\varnothing) = 0$；
> 2. **单调性**：$A \subseteq B \Rightarrow \mu^\ast(A) \leq \mu^\ast(B)$；
> 3. **可数次可加性**：对任意可数族 $\{A_n\}_{n=1}^\infty \subseteq \mathcal{P}(X)$，
>    $$\mu^\ast\!\left(\bigcup_{n=1}^\infty A_n\right) \leq \sum_{n=1}^\infty \mu^\ast(A_n).$$

> [!note] Lebesgue 外测度
> 对 $A \subseteq \mathbb{R}^n$，称
> $$m^\ast(A) = \inf\left\{\sum_{k=1}^\infty \operatorname{vol}(I_k) : A \subseteq \bigcup_{k=1}^\infty I_k,\ I_k \text{ 为开方块} \right\}$$
> 为 $A$ 的 **Lebesgue 外测度**。其中 $\operatorname{vol}(I) = \prod_{i=1}^n (b_i - a_i)$ 是开方块 $I = \prod (a_i, b_i)$ 的体积。

> [!note] Carathéodory 可测集
> 设 $\mu^\ast$ 为 $X$ 上的外测度。称 $A \subseteq X$ 为 **Carathéodory 可测**（简称 $\mu^\ast$-可测），若对任意 $E \subseteq X$，
> $$\mu^\ast(E) = \mu^\ast(E \cap A) + \mu^\ast(E \cap A^c). \quad \cdots (\mathrm{C})$$
> 记所有 $\mu^\ast$-可测集为 $\mathcal{M}$。

> [!info] 关于 Carathéodory 条件
> 条件 $(\mathrm{C})$ 称为**分裂条件**：$A$ 必须能将任意"测试集" $E$ 干净地切成两块。由外测度的次可加性，$\leq$ 方向总成立；故 $(\mathrm{C})$ 等价于
> $$\mu^\ast(E) \geq \mu^\ast(E \cap A) + \mu^\ast(E \cap A^c). \quad \cdots (\mathrm{C}')$$
> 当 $\mu^\ast(E) = +\infty$ 时 $(\mathrm{C}')$ 自动成立，故只需对 $\mu^\ast(E) < +\infty$ 的 $E$ 验证。

> [!abstract] 引理：σ-代数的定义
> 称 $\mathcal{M} \subseteq \mathcal{P}(X)$ 为 $X$ 上的 **σ-代数**，若：(1) $X \in \mathcal{M}$；(2) $A \in \mathcal{M} \Rightarrow A^c \in \mathcal{M}$；(3) $\{A_n\} \subseteq \mathcal{M} \Rightarrow \bigcup_n A_n \in \mathcal{M}$。

---

## 定理（Carathéodory）

设 $\mu^\ast$ 为非空集合 $X$ 上的外测度，$\mathcal{M}$ 为全体 $\mu^\ast$-可测集。则：

**(i)** $\mathcal{M}$ 是 $X$ 上的 σ-代数；

**(ii)** $\mu^\ast$ 在 $\mathcal{M}$ 上是**可数可加**的，即对两两不相交的 $\{A_n\} \subseteq \mathcal{M}$，
$$\mu^\ast\!\left(\bigsqcup_{n=1}^\infty A_n\right) = \sum_{n=1}^\infty \mu^\ast(A_n).$$

特别地，$(\mathcal{X}, \mathcal{M}, \mu^\ast|_{\mathcal{M}})$ 是一个测度空间。

**推论**：Lebesgue 外测度 $m^\ast$ 在其可测集族 $\mathcal{M}_L$ 上是 $\mathbb{R}^n$ 上的 Lebesgue 测度 $m$，且 $\mathcal{M}_L$ 包含全体 Borel 集。

---

## 第(i)部分的证明：$\mathcal{M}$ 是 σ-代数

### 第一步：$X \in \mathcal{M}$ 与对补封闭

对任意 $E$，$E \cap X = E$，$E \cap X^c = \varnothing$，由 $\mu^\ast(\varnothing) = 0$ 得 $\mu^\ast(E) = \mu^\ast(E \cap X) + \mu^\ast(E \cap X^c)$。故 $X \in \mathcal{M}$。

条件 $(\mathrm{C})$ 关于 $A$ 与 $A^c$ 对称，故 $A \in \mathcal{M} \Rightarrow A^c \in \mathcal{M}$。$\square$

### 第二步：对有限并封闭（即 $\mathcal{M}$ 是代数）

**目标**：设 $A, B \in \mathcal{M}$。证 $A \cup B \in \mathcal{M}$。

取任意 $E$。由 $A \in \mathcal{M}$，
$$\mu^\ast(E) = \mu^\ast(E \cap A) + \mu^\ast(E \cap A^c). \quad \cdots (1)$$

将 $E \cap A^c$ 视作新测试集，由 $B \in \mathcal{M}$，
$$\mu^\ast(E \cap A^c) = \mu^\ast(E \cap A^c \cap B) + \mu^\ast(E \cap A^c \cap B^c). \quad \cdots (2)$$

代入 $(1)$：
$$\mu^\ast(E) = \mu^\ast(E \cap A) + \mu^\ast(E \cap A^c \cap B) + \mu^\ast(E \cap A^c \cap B^c). \quad \cdots (3)$$

注意 $A \cup B = A \cup (A^c \cap B)$，故
$$E \cap (A \cup B) = (E \cap A) \cup (E \cap A^c \cap B).$$

由次可加性，
$$\mu^\ast(E \cap (A \cup B)) \leq \mu^\ast(E \cap A) + \mu^\ast(E \cap A^c \cap B). \quad \cdots (4)$$

又 $(A \cup B)^c = A^c \cap B^c$，所以 $(3)$ 改写为
$$\mu^\ast(E) = \mu^\ast(E \cap A) + \mu^\ast(E \cap A^c \cap B) + \mu^\ast(E \cap (A \cup B)^c).$$

结合 $(4)$：
$$\mu^\ast(E) \geq \mu^\ast(E \cap (A \cup B)) + \mu^\ast(E \cap (A \cup B)^c).$$

由 $(\mathrm{C}')$，$A \cup B \in \mathcal{M}$。$\square$

### 第三步：不相交并的可数可加性（关键引理）

> [!important] 关键引理
> 设 $A_1, \ldots, A_n \in \mathcal{M}$ **两两不相交**。则对任意 $E \subseteq X$，
> $$\mu^\ast\!\left(E \cap \bigsqcup_{k=1}^n A_k\right) = \sum_{k=1}^n \mu^\ast(E \cap A_k). \quad \cdots (\ast)$$

**对 $n$ 归纳**。$n = 1$ 平凡。

设结论对 $n-1$ 成立。令 $B_n = \bigsqcup_{k=1}^n A_k$。由 $A_n \in \mathcal{M}$，以 $E \cap B_n$ 为测试集：
$$\mu^\ast(E \cap B_n) = \mu^\ast(E \cap B_n \cap A_n) + \mu^\ast(E \cap B_n \cap A_n^c).$$

由不相交性，$B_n \cap A_n = A_n$，$B_n \cap A_n^c = B_{n-1}$。故
$$\mu^\ast(E \cap B_n) = \mu^\ast(E \cap A_n) + \mu^\ast(E \cap B_{n-1}) = \sum_{k=1}^n \mu^\ast(E \cap A_k). \quad \square$$

### 第四步：对可数并封闭

**目标**：设 $\{A_n\}_{n=1}^\infty \subseteq \mathcal{M}$。证 $A = \bigcup_n A_n \in \mathcal{M}$。

**化为不相交并**：令 $B_n = A_n \setminus \bigcup_{k<n} A_k$。由第二步，$\mathcal{M}$ 是代数，故 $B_n \in \mathcal{M}$；又 $\{B_n\}$ 两两不相交，$\bigsqcup_n B_n = \bigcup_n A_n = A$。下证 $A \in \mathcal{M}$。

取任意 $E$。令 $C_N = \bigsqcup_{k=1}^N B_k$。由第二步，$C_N \in \mathcal{M}$，故
$$\mu^\ast(E) = \mu^\ast(E \cap C_N) + \mu^\ast(E \cap C_N^c).$$

由 $(\ast)$，$\mu^\ast(E \cap C_N) = \sum_{k=1}^N \mu^\ast(E \cap B_k)$。又 $C_N \subseteq A \Rightarrow C_N^c \supseteq A^c$，由单调性 $\mu^\ast(E \cap C_N^c) \geq \mu^\ast(E \cap A^c)$。故
$$\mu^\ast(E) \geq \sum_{k=1}^N \mu^\ast(E \cap B_k) + \mu^\ast(E \cap A^c).$$

$N \to \infty$：
$$\mu^\ast(E) \geq \sum_{k=1}^\infty \mu^\ast(E \cap B_k) + \mu^\ast(E \cap A^c). \quad \cdots (\star)$$

由次可加性，$\sum_{k=1}^\infty \mu^\ast(E \cap B_k) \geq \mu^\ast\!\left(\bigsqcup_k (E \cap B_k)\right) = \mu^\ast(E \cap A)$。故
$$\mu^\ast(E) \geq \mu^\ast(E \cap A) + \mu^\ast(E \cap A^c).$$

由 $(\mathrm{C}')$，$A \in \mathcal{M}$。$\square$

综合：$\mathcal{M}$ 含 $X$、对补、对可数并封闭，故为 σ-代数。$\blacksquare$（(i)）

---

## 第(ii)部分的证明：$\mu^\ast$ 在 $\mathcal{M}$ 上可数可加

设 $\{A_n\} \subseteq \mathcal{M}$ 两两不相交，$A = \bigsqcup_n A_n$。

由 $(\star)$，取 $E = A$，并注意 $A \cap B_k = A_k$（因为 $B_k$ 已经是不相交化的 $A_k$，且 $A_n$ 本就两两不相交故 $B_k = A_k$）、$A \cap A^c = \varnothing$：
$$\mu^\ast(A) \geq \sum_{k=1}^\infty \mu^\ast(A_k).$$

反向由次可加性显然。故 $\mu^\ast(A) = \sum \mu^\ast(A_k)$。$\blacksquare$（(ii)）

---

## 总结

> [!tip] 关键思想
> Carathéodory 的天才在于**把可测性定义为"对任意测试集都能干净分裂"**。这一定义看似抽象，但好处巨大：
> 1. 直接由次可加性 + 分裂条件推出可数可加性，**绕开了构造 σ-代数的传统困难**；
> 2. 第二步将 $A, B$ 两个可测集的并归结为对 $(A, A^c \cap B)$ 的两次分裂；
> 3. 第四步用"不相交化" $B_n = A_n \setminus \bigcup_{k<n} A_k$ 将可数并问题化归为不相交并问题，再由关键引理 $(\ast)$ 处理。
>
> 由 $(\star)$ 同时得到 σ-代数封闭性与可数可加性——这正是 Carathéodory 构造的"一石二鸟"。

> [!warning] 完备性附赠
> Carathéodory 构造的测度 $\mu^\ast|_{\mathcal{M}}$ 自动是**完备的**：若 $\mu^\ast(N) = 0$，则对任意 $E$ 由单调性 $\mu^\ast(E \cap N) = 0$，$\mu^\ast(E \cap N^c) \leq \mu^\ast(E)$，故 $\mu^\ast(E) \geq \mu^\ast(E \cap N) + \mu^\ast(E \cap N^c)$，即 $N \in \mathcal{M}$。Lebesgue 测度因此天然完备；Borel 测度则不然。

> [!info] 与 Lebesgue 测度的关系
> 对 Lebesgue 外测度 $m^\ast$（由开方块覆盖定义），可以验证 $m^\ast$ 确为外测度（关键是可数次可加性需用 ε/2ⁿ 技巧）。Carathéodory 定理直接给出 $\mathbb{R}^n$ 上的 Lebesgue 测度 $m$，其定义域 $\mathcal{M}_L$ 严格大于 Borel σ-代数 $\mathcal{B}(\mathbb{R}^n)$（差距正是完备化）。开方块 $(a, b)$ 满足 $m^\ast((a, b)) = b - a$，且全体开集都属于 $\mathcal{M}_L$。
