---
title: Hilbert空间正交基的基数不变性
date: 2026-04-05
tags:
  - 泛函分析
  - Hilbert空间
  - 正交基
  - 基数
  - Parseval恒等式
---

# Hilbert空间正交基的基数不变性

## 预备定义

> [!note] Hilbert空间
> 称完备的**内积空间**为**Hilbert空间**。即 $H$ 为Hilbert空间，若其上装备内积 $\langle \cdot, \cdot \rangle: H \times H \to \mathbb{K}$，满足：
> 1. **共轭对称性**：$\langle x, y \rangle = \overline{\langle y, x \rangle}$；
> 2. **对第一个变元的线性性**：$\langle \alpha x + \beta y, z \rangle = \alpha \langle x, z \rangle + \beta \langle y, z \rangle$；
> 3. **正定性**：$\langle x, x \rangle \geq 0$，且 $\langle x, x \rangle = 0 \iff x = 0$；
>
> 且 $H$ 关于诱导范数 $\|x\| = \sqrt{\langle x, x \rangle}$ 完备。

> [!note] 正交基（Orthonormal Basis）
> 子集 $B \subseteq H$ 称为 $H$ 的**正交基**，若满足：
> 1. $B$ 是**标准正交集**：$\langle e, f \rangle = \delta_{ef}$（当 $e = f$ 时为 $1$，否则为 $0$）；
> 2. $B$ 是**极大的**：若 $x \in H$ 满足 $\langle x, e \rangle = 0$ 对所有 $e \in B$ 成立，则 $x = 0$。
>
> 等价地，$B$ 为正交基当且仅当对每个 $x \in H$，有Fourier展开
> $$x = \sum_{e \in B} \langle x, e \rangle \, e,$$
> 其中求和按范数收敛（仅可数个系数非零）。

> [!note] 集合的基数（Cardinality）
> 两个集合**等势**（或称有**相同基数**），若其间存在双射。基数关系满足Schröder-Bernstein定理：若 $|A| \leq |B|$ 且 $|B| \leq |A|$，则 $|A| = |B|$。

---

## 定理

设 $H$ 为Hilbert空间。$H$ 的任意两个正交基具有相同的基数。

> [!info] 术语说明
> 该定理说明Hilbert空间的**维数**（dimension）是良定义的，即任意正交基的基数相同。此基数称为 $H$ 的**Hilbert维数**。

---

## 证明

设 $B$ 和 $C$ 为 $H$ 的两个正交基。需证 $|B| = |C|$（即存在 $B$ 与 $C$ 之间的双射）。

证明分两个情形：**有限维**与**无限维**。

---

### 情形一：$H$ 为有限维

#### 第一步：有限维空间的正交基是Hamel基

设 $\dim H = n < \infty$。标准线性代数结果：有限维空间的所有Hamel基（线性代数基）具有相同基数（等于维数 $n$）。

需验证：在有限维内积空间中，正交基必是Hamel基。

设 $B = \{e_1, \dots, e_m\}$ 为正交基。由正交性，$B$ 线性无关：若 $\sum_{i=1}^m \alpha_i e_i = 0$，则对每个 $j$，

$$0 = \left\langle \sum_{i=1}^m \alpha_i e_i, e_j \right\rangle = \sum_{i=1}^m \alpha_i \langle e_i, e_j \rangle = \alpha_j.$$

故所有系数为零，$B$ 线性无关。

#### 第二步：正交基张成整个空间

任取 $x \in H$。由正交基的极大性定义，考虑 $y = x - \sum_{i=1}^m \langle x, e_i \rangle e_i$。

对每个 $j$，

$$\langle y, e_j \rangle = \langle x, e_j \rangle - \sum_{i=1}^m \langle x, e_i \rangle \langle e_i, e_j \rangle = \langle x, e_j \rangle - \langle x, e_j \rangle = 0.$$

由正交基的极大性，$y = 0$，故 $x = \sum_{i=1}^m \langle x, e_i \rangle e_i$。因此 $\text{span}(B) = H$。

#### 第三步：结论

$B$ 为 $H$ 的Hamel基，故 $|B| = \dim H = n$。同理 $|C| = n$。因此 $|B| = |C|$。$\square$

---

### 情形二：$H$ 为无限维

此时 $B$ 和 $C$ 均为无限集。证明策略：

1. 利用Parseval恒等式证明：对每个 $b \in B$，与 $b$ 非正交的 $c \in C$ 至多可数；
2. 证明 $C = \bigcup_{b \in B} C_b$（其中 $C_b = \{c \in C : \langle b, c \rangle \neq 0\}$）；
3. 由此得 $|C| \leq |B| \cdot \aleph_0 = |B|$（无限基数算术）；
4. 对称地得 $|B| \leq |C|$；
5. 由Schröder-Bernstein定理得 $|B| = |C|$。

---

#### 引理：非零Fourier系数的可数性

> [!abstract] 引理
> 设 $\{e_\alpha\}_{\alpha \in A}$ 为 $H$ 中的标准正交集。对任意 $x \in H$，集合
> $$A_x = \{\alpha \in A : \langle x, e_\alpha \rangle \neq 0\}$$
> 至多为可数集。

**证明**：对 $n \in \mathbb{N}$，令

$$A_{x,n} = \left\{\alpha \in A : |\langle x, e_\alpha \rangle| \geq \frac{1}{n}\right\}.$$

由Bessel不等式，对任意有限子集 $F \subseteq A_{x,n}$：

$$\sum_{\alpha \in F} |\langle x, e_\alpha \rangle|^2 \leq \|x\|^2.$$

因此

$$\frac{|F|}{n^2} \leq \sum_{\alpha \in F} |\langle x, e_\alpha \rangle|^2 \leq \|x\|^2,$$

故 $|F| \leq n^2 \|x\|^2$。这说明 $A_{x,n}$ 为有限集（基数不超过 $n^2 \|x\|^2$）。

于是

$$A_x = \bigcup_{n=1}^\infty A_{x,n}$$

为可数个有限集之并，故至多可数。$\square$

---

#### 第一步：定义关键集合

对每个 $b \in B$，定义

$$C_b = \{c \in C : \langle b, c \rangle \neq 0\}.$$

由上述引理（取 $x = b$，正交集为 $C$），每个 $C_b$ 至多可数。

---

#### 第二步：证明 $C = \bigcup_{b \in B} C_b$

**包含 "$\supseteq$"**：显然，因每个 $C_b \subseteq C$。

**包含 "$\subseteq$"**：任取 $c \in C$。需证存在 $b \in B$ 使得 $\langle b, c \rangle \neq 0$。

假设不然：设 $\langle b, c \rangle = 0$ 对所有 $b \in B$ 成立。由正交基 $B$ 的极大性，必有 $c = 0$。

但 $c \in C$ 为标准正交集的元素，$\|c\| = 1 \neq 0$，矛盾！

因此每个 $c \in C$ 必属于某个 $C_b$。即 $C \subseteq \bigcup_{b \in B} C_b$。

综上，$C = \bigcup_{b \in B} C_b$。$\square$

> [!important] 关键点
> 正交基的极大性保证了：若 $c$ 与 $B$ 中所有元素正交，则 $c = 0$。这是证明 $C \subseteq \bigcup_{b \in B} C_b$ 的核心。

---

#### 第三步：基数估计 $|C| \leq |B|$

由第二步，$C = \bigcup_{b \in B} C_b$，其中每个 $|C_b| \leq \aleph_0$（可数）。

因此

$$|C| = \left|\bigcup_{b \in B} C_b\right| \leq \sum_{b \in B} |C_b| \leq \sum_{b \in B} \aleph_0 = |B| \cdot \aleph_0.$$

> [!info] 基数算术回顾
> 对无限基数 $\kappa$，有 $\kappa \cdot \aleph_0 = \kappa$。这是因为 $\kappa \cdot \aleph_0 = \max(\kappa, \aleph_0) = \kappa$（选择公理下的无限基数算术）。

由于 $B$ 为无限集，$|B| \cdot \aleph_0 = |B|$。故

$$|C| \leq |B|. \quad \cdots (1)$$

---

#### 第四步：对称地得 $|B| \leq |C|$

将上述论证中 $B$ 与 $C$ 的角色互换：

- 对每个 $c \in C$，定义 $B_c = \{b \in B : \langle b, c \rangle \neq 0\}$；
- 由引理，每个 $B_c$ 至多可数；
- 由正交基 $C$ 的极大性，$B = \bigcup_{c \in C} B_c$；
- 因此 $|B| \leq |C| \cdot \aleph_0 = |C|$（因 $C$ 无限）。

即

$$|B| \leq |C|. \quad \cdots (2)$$

---

#### 第五步：应用Schröder-Bernstein定理

由 $(1)$ 和 $(2)$：

$$|B| \leq |C| \quad \text{且} \quad |C| \leq |B|.$$

根据 **Schröder-Bernstein定理**，存在 $B$ 与 $C$ 之间的双射，故

$$|B| = |C|. \quad \blacksquare$$

---

### 结论

无论 $H$ 为有限维还是无限维，其任意两个正交基均具有相同基数。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 
> **有限维情形**：正交基是Hamel基，线性代数保证所有Hamel基等势。
>
> **无限维情形**：核心是**可数性 + 覆盖论证**：
> 
> 1. **非零系数的可数性**（Bessel不等式）：对每个 $b \in B$，仅可数个 $c \in C$ 满足 $\langle b, c \rangle \neq 0$；
> 2. **正交基的极大性**：每个 $c \in C$ 必与某个 $b \in B$ 非正交（否则 $c \perp B$ 导致 $c = 0$，与 $\|c\|=1$ 矛盾）；
> 3. **覆盖关系**：$C = \bigcup_{b \in B} C_b$，其中 $|C_b| \leq \aleph_0$；
> 4. **基数算术**：$|C| \leq |B| \cdot \aleph_0 = |B|$（无限基数性质）；
> 5. **对称性**：同理 $|B| \leq |C|$；
> 6. **Schröder-Bernstein**：$|B| = |C|$。
>
> 此证明充分利用了Hilbert空间的**几何结构**（Parseval恒等式/Bessel不等式）与**集合论工具**（基数算术），是泛函分析中"代数-拓扑-集合"互动的典范。

> [!warning] 对比：代数基与正交基
> 对于**代数基**（Hamel基），该结论在纯向量空间中也成立（需选择公理证明所有基等势）。但对于Hilbert空间，正交基的基数比较不需要选择公理来"选取"基——我们直接从两个已知的正交基出发，利用内积结构进行比较。实际上，构造正交基本身需要Zorn引理（或等价的选择公理形式）。
