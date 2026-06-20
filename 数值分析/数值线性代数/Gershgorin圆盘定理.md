---
title: Gershgorin 圆盘定理
date: 2026-05-31
tags:
  - 数值分析
  - 数值线性代数
  - 矩阵分析
  - 特征值估计
  - Gershgorin定理
  - 对角占优
---

# Gershgorin 圆盘定理

## 预备定义

> [!note] 特征值与特征向量
> 设 $A \in \mathbb{C}^{n \times n}$。若存在 $\lambda \in \mathbb{C}$ 与非零向量 $x \in \mathbb{C}^n$，使
> $$A x \;=\; \lambda x,$$
> 则称 $\lambda$ 为 $A$ 的**特征值**（eigenvalue），$x$ 为对应的**特征向量**（eigenvector）。$A$ 的全体特征值之集记作 $\sigma(A)$，称为 $A$ 的**谱**（spectrum）。

> [!note] Gershgorin 圆盘
> 设 $A = (a_{ij}) \in \mathbb{C}^{n \times n}$。定义**第 $i$ 个 Gershgorin 圆盘**为
> $$D_i(A) \;=\; \left\{ z \in \mathbb{C} \,:\, |z - a_{ii}| \leq R_i \right\}, \quad R_i \;=\; \sum_{\substack{j=1 \\ j \neq i}}^{n} |a_{ij}|.$$
> 即以**对角元 $a_{ii}$ 为圆心**、以**第 $i$ 行非对角元绝对值之和 $R_i$ 为半径**的闭圆盘。
> 全部 $n$ 个圆盘之并称为 $A$ 的 **Gershgorin 区域**：
> $$G(A) \;=\; \bigcup_{i=1}^{n} D_i(A).$$

> [!note] 严格对角占优矩阵
> 称 $A = (a_{ij}) \in \mathbb{C}^{n \times n}$ 为**按行严格对角占优**（strictly diagonally dominant，简记 SDD），若
> $$|a_{ii}| \;>\; \sum_{j \neq i} |a_{ij}|, \quad \forall\, i = 1, 2, \ldots, n.$$
> 即每个对角元的绝对值严格大于该行其余元素绝对值之和。

> [!note] 谱半径 (spectral radius)
> $\rho(A) = \max_{\lambda \in \sigma(A)} |\lambda|$。详见 [[线性迭代法收敛性的谱半径准则]]。

---

## 定理

设 $A = (a_{ij}) \in \mathbb{C}^{n \times n}$。则 $A$ 的每个特征值 $\lambda$ 都至少落在一个 Gershgorin 圆盘内，即
$$\sigma(A) \;\subseteq\; G(A) \;=\; \bigcup_{i=1}^{n} D_i(A).$$
更明确地：对每个 $\lambda \in \sigma(A)$，存在指标 $k \in \{1, \ldots, n\}$ 使
$$|\lambda - a_{kk}| \;\leq\; \sum_{j \neq k} |a_{kj}|.$$

---

## 证明

### 第一步：选取特征向量的"主元"分量

设 $\lambda \in \sigma(A)$ 为任一特征值，$x = (x_1, \ldots, x_n)^{\mathsf T} \in \mathbb{C}^n$ 为其对应的特征向量。由特征向量定义，$x \neq 0$，故
$$\|x\|_\infty \;=\; \max_{1 \leq i \leq n} |x_i| \;>\; 0.$$

取指标 $k$ 使
$$|x_k| \;=\; \|x\|_\infty \;=\; \max_{1 \leq i \leq n} |x_i|. \quad \cdots (\ast)$$

> [!important] 主元分量的关键作用
> $k$ 是 $x$ 中**绝对值最大**的分量所在位置。这一选取保证了对一切 $j$，$|x_j| / |x_k| \leq 1$，从而后续放缩时不会失控。整个证明的"全部技术含量"都集中在 $(\ast)$ 这一选取上。

### 第二步：写出特征方程第 $k$ 个分量

由 $A x = \lambda x$，比较第 $k$ 个分量：
$$\sum_{j=1}^{n} a_{kj} x_j \;=\; \lambda x_k.$$
把对角项 $a_{kk} x_k$ 单独移到左边，其余项移到右边：
$$(\lambda - a_{kk}) x_k \;=\; \sum_{\substack{j=1 \\ j \neq k}}^{n} a_{kj} x_j. \quad \cdots (\star)$$

### 第三步：放缩并除以 $|x_k|$

对 $(\star)$ 两边取模，再对右侧应用三角不等式：
$$|\lambda - a_{kk}| \cdot |x_k| \;=\; \left|\sum_{j \neq k} a_{kj} x_j\right| \;\leq\; \sum_{j \neq k} |a_{kj}| \cdot |x_j|.$$

由 $(\ast)$，$|x_j| \leq |x_k|$ 对一切 $j$ 成立，故
$$|\lambda - a_{kk}| \cdot |x_k| \;\leq\; \sum_{j \neq k} |a_{kj}| \cdot |x_k| \;=\; |x_k| \sum_{j \neq k} |a_{kj}|.$$

由 $|x_k| > 0$，两边约去 $|x_k|$：
$$|\lambda - a_{kk}| \;\leq\; \sum_{j \neq k} |a_{kj}| \;=\; R_k. \quad \square$$

### 第四步：结论

第三步表明 $\lambda \in D_k(A)$。由于 $\lambda$ 任取，故
$$\sigma(A) \;\subseteq\; \bigcup_{i=1}^{n} D_i(A) \;=\; G(A). \quad \blacksquare$$

---

## 证明思路总结

> [!tip] 关键思想
> 整个证明只用了**一个技巧**：盯住特征向量绝对值最大的分量。
> 1. 设 $|x_k| = \max_i |x_i|$；
> 2. 写出 $A x = \lambda x$ 的第 $k$ 行；
> 3. 用三角不等式 + $|x_j|/|x_k| \leq 1$ 放缩。
>
> "用最大分量做归一化"是研究矩阵谱性质时的一个**通用利器**：它把对全体分量的控制问题，约化为对单一分量的不等式。这与算子范数证明中"取使 $\|Ax\|/\|x\|$ 趋近最大值的向量"的策略本质相同。

> [!warning] 圆盘内不一定每个都有特征值
> 定理只保证 $\sigma(A) \subseteq G(A)$，但**不保证每个圆盘里都有特征值**。例如可能 $n$ 个特征值全部挤在 $D_1$ 里。
>
> 不过，下面的**第二 Gershgorin 定理**给出了更精细的结论：若 $G(A)$ 的某个**连通分支**由 $m$ 个圆盘组成，则该连通分支内**恰好**含 $A$ 的 $m$ 个特征值（计入代数重数）。

> [!info] 转置同样成立 —— 按列圆盘
> 由于 $A$ 与 $A^{\mathsf T}$ 有相同的特征值，将定理用于 $A^{\mathsf T}$ 即得**按列**的 Gershgorin 圆盘：
> $$D_j'(A) \;=\; \left\{ z : |z - a_{jj}| \leq C_j \right\}, \quad C_j \;=\; \sum_{i \neq j} |a_{ij}|.$$
> 实用中，**对每个特征值取按行与按列圆盘之交**可得到更紧的估计。

---

## 应用

### 应用一：严格对角占优矩阵的非奇异性

> [!important] 推论（Lévy–Desplanques 定理）
> 严格对角占优矩阵 $A$ 必非奇异（即 $\det A \neq 0$）。

**证明**：反证。若 $A$ 奇异，则 $0 \in \sigma(A)$。由 Gershgorin 定理，存在 $k$ 使
$$|0 - a_{kk}| \;\leq\; \sum_{j \neq k} |a_{kj}|,$$
即 $|a_{kk}| \leq \sum_{j \neq k} |a_{kj}|$，与严格对角占优矛盾。故 $A$ 非奇异。$\square$

> [!info] 数值意义
> 这一推论是数值线性代数中**判定矩阵可逆性的最廉价工具**：只需扫一遍每一行做加法，复杂度 $O(n^2)$，远低于直接计算 $\det A$ 的 $O(n^3)$。在 PDE 离散化得到的大型稀疏矩阵中，严格对角占优是**默认结构**，由此可直接断言系数矩阵可解。

### 应用二：Jacobi 迭代法的收敛性

考虑解线性方程组 $A x = b$ 的 **Jacobi 迭代**：将 $A = D - L - U$（$D$ 为对角部分，$L, U$ 分别为严格下三角与严格上三角的负部分），迭代格式为
$$x^{(m+1)} \;=\; B_J\, x^{(m)} + D^{-1} b, \quad B_J \;=\; D^{-1}(L + U).$$

> [!important] 推论
> 若 $A$ 按行严格对角占优，则 Jacobi 迭代对任意初值都收敛。

**证明**：由 [[线性迭代法收敛性的谱半径准则]]，迭代收敛 $\Longleftrightarrow$ $\rho(B_J) < 1$。

注意 $B_J = D^{-1}(L + U)$ 的元素为
$$(B_J)_{ij} \;=\; \begin{cases} 0, & j = i, \\ -a_{ij}/a_{ii}, & j \neq i. \end{cases}$$

对 $B_J$ 应用 Gershgorin 定理：对任意特征值 $\mu \in \sigma(B_J)$，存在 $k$ 使
$$|\mu - 0| \;\leq\; \sum_{j \neq k} \left|\frac{a_{kj}}{a_{kk}}\right| \;=\; \frac{1}{|a_{kk}|} \sum_{j \neq k} |a_{kj}|.$$

由 $A$ 严格对角占优，$\sum_{j \neq k} |a_{kj}| < |a_{kk}|$，故 $|\mu| < 1$。即 $\rho(B_J) < 1$。$\square$

### 应用三：特征值范围的快速估计

> [!info] 例：对称矩阵的特征值定位
> 设
> $$A \;=\; \begin{pmatrix} 5 & 1 & 0 \\ 1 & 6 & 1 \\ 0 & 1 & 7 \end{pmatrix}.$$
> 三个 Gershgorin 圆盘为
> $$D_1 = \{|z - 5| \leq 1\}, \quad D_2 = \{|z - 6| \leq 2\}, \quad D_3 = \{|z - 7| \leq 1\}.$$
> 故 $\sigma(A) \subseteq [4, 8]$。又 $A$ 实对称 $\Rightarrow$ 全部特征值为实数 $\Rightarrow$ 它们落在 $[4, 8]$ 上。
>
> 这给出了**不计算特征多项式**的特征值区间估计 —— 这一思想是设计预条件子（preconditioner）、估计条件数、判定迭代法收敛速度的基础。

### 应用四：判断矩阵的正定性

> [!important] 推论
> 设 $A$ 实对称、对角元全为正，且按行严格对角占优。则 $A$ 正定。

**证明**：$A$ 实对称 $\Rightarrow$ 特征值全实。任取 $\lambda \in \sigma(A)$，由 Gershgorin 定理存在 $k$ 使
$$\lambda \;\geq\; a_{kk} - \sum_{j \neq k} |a_{kj}| \;>\; 0$$
（最后一步用了 $a_{kk} > 0$ 与严格对角占优）。故全部特征值为正，$A$ 正定。$\square$

> [!info] 与 Cholesky 分解的衔接
> 这一推论提供了**正定性的廉价充分条件**，从而保证 [[Cholesky 分解的存在性与唯一性|Cholesky 分解]] 可行。在有限元 / 有限差分得到的刚度矩阵上，正对角元 + 对角占优是常见结构，因此可直接调用 Cholesky 求解，无需先验证正定性。

### 应用五：扰动下的特征值稳定性

考虑扰动矩阵 $\tilde A = A + E$，其中 $A = \operatorname{diag}(d_1, \ldots, d_n)$ 为对角阵、$E$ 为"小"扰动。由 Gershgorin 定理，$\tilde A$ 的每个特征值落在某个圆盘
$$|\lambda - (d_i + e_{ii})| \;\leq\; \sum_{j \neq i} |e_{ij}|$$
内。这是 **Bauer–Fike 定理**与**矩阵摄动论**的最直接特例 —— 特征值对元素扰动的敏感度被对角占优结构所控制。

---

## 推广：第二 Gershgorin 定理（无证明）

> [!abstract] 定理（第二 Gershgorin 定理）
> 设 $A \in \mathbb{C}^{n \times n}$。若 Gershgorin 区域 $G(A)$ 可拆为两个**不相交闭集** $G_1, G_2$，且 $G_1$ 由 $m$ 个圆盘组成、$G_2$ 由 $n - m$ 个圆盘组成，则 $A$ 在 $G_1$ 内（计入代数重数）恰有 $m$ 个特征值，在 $G_2$ 内恰有 $n - m$ 个。

> [!tip] 应用：孤立圆盘 = 单个特征值
> 当某个 Gershgorin 圆盘与其余圆盘**互不相交**时，该圆盘内**恰好含 1 个特征值**。这是迭代算法初值选取（如反幂法、Rayleigh 商迭代）中"近似特征值"的标准来源。
