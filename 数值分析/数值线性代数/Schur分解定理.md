---
title: Schur 分解定理
date: 2026-05-31
tags:
  - 数值分析
  - 数值线性代数
  - 矩阵分析
  - 矩阵分解
  - Schur分解
  - 酉相似
---

# Schur 分解定理

## 预备定义

> [!note] 酉矩阵 (unitary matrix)
> 设 $U \in \mathbb{C}^{n \times n}$。若 $U^* U = U U^* = I_n$（其中 $U^* = \overline{U}^{\mathsf T}$ 为共轭转置），则称 $U$ 为**酉矩阵**。等价地，$U$ 的列向量构成 $\mathbb{C}^n$ 的标准正交基。
>
> 实数版本（$U^{\mathsf T} U = I$）称为**正交矩阵**（orthogonal matrix）。

> [!note] 酉相似 (unitary similarity)
> 设 $A, B \in \mathbb{C}^{n \times n}$。若存在酉矩阵 $U$ 使 $B = U^* A U$，则称 $A$ 与 $B$ **酉相似**。酉相似保特征值（事实上是相似的，故谱不变）。

> [!note] 上三角矩阵 (upper triangular)
> 矩阵 $T = (t_{ij})$ 称为**上三角**，若 $i > j \Rightarrow t_{ij} = 0$。上三角阵的特征值即为其对角元 $t_{11}, t_{22}, \ldots, t_{nn}$（按重数计）。

> [!abstract] 引理：代数基本定理（黑箱使用）
> 任意 $n \geq 1$ 次的复系数多项式在 $\mathbb{C}$ 上必有根。
> **推论**：任意 $A \in \mathbb{C}^{n \times n}$ 至少有一个特征值 $\lambda \in \mathbb{C}$ 与对应非零特征向量。

> [!abstract] 引理：Gram–Schmidt 扩张
> 设 $u_1 \in \mathbb{C}^n$，$\|u_1\| = 1$。则可将 $u_1$ 扩张为 $\mathbb{C}^n$ 的一组标准正交基 $\{u_1, v_2, \ldots, v_n\}$。

**证明**：取 $u_1$ 与任意 $n - 1$ 个线性无关的向量补成 $\mathbb{C}^n$ 的基，再对后 $n - 1$ 个向量做 Gram–Schmidt 正交化并单位化即可。$\square$

---

## 定理

设 $A \in \mathbb{C}^{n \times n}$。则存在酉矩阵 $U \in \mathbb{C}^{n \times n}$ 与上三角矩阵 $T \in \mathbb{C}^{n \times n}$ 使
$$A \;=\; U\, T\, U^*. \quad \cdots (\star)$$

更进一步，$T$ 的对角元 $t_{11}, \ldots, t_{nn}$ 恰为 $A$ 的全部特征值（按代数重数计，且其排列顺序可任意指定）。

称 $(\star)$ 为 $A$ 的 **Schur 分解**。

---

## 证明

对矩阵阶数 $n$ 用数学归纳法。

### 基础情形：$n = 1$

此时 $A = (a_{11})$ 已经是上三角；取 $U = (1)$、$T = A$ 即可。$\square$

### 归纳步骤

**归纳假设**：设结论对一切 $n \times n$（$n \geq 1$）的复方阵成立。

设 $A \in \mathbb{C}^{(n+1) \times (n+1)}$。下证结论对 $A$ 成立，分四步。

#### 第一步：取一个特征值及单位特征向量

由 **代数基本定理**，$A$ 至少有一个特征值 $\lambda_1 \in \mathbb{C}$ 与对应非零特征向量 $\tilde u_1$。归一化得 $u_1 = \tilde u_1 / \|\tilde u_1\|$，则
$$A u_1 \;=\; \lambda_1 u_1, \quad \|u_1\| \;=\; 1. \quad \cdots (1)$$

#### 第二步：扩张为酉矩阵 $U_1$

由 **Gram–Schmidt 扩张引理**，把 $u_1$ 扩张为 $\mathbb{C}^{n+1}$ 的标准正交基 $\{u_1, v_2, \ldots, v_{n+1}\}$。令
$$U_1 \;=\; \bigl[\, u_1 \;\,\big|\;\, v_2 \;\,\big|\;\, \cdots \;\,\big|\;\, v_{n+1}\,\bigr] \;\in\; \mathbb{C}^{(n+1) \times (n+1)}.$$

则 $U_1$ 的列向量构成标准正交基，故 $U_1$ 为酉矩阵。$\square$

#### 第三步：相似化为分块上三角

计算 $U_1^* A U_1$。注意 $U_1^* = (U_1)^{-1}$，且 $U_1^* u_1 = e_1$（$\mathbb{C}^{n+1}$ 的第一个标准基向量），这是因为 $u_1$ 是 $U_1$ 的第一列、$U_1$ 各列彼此正交。

逐列计算 $U_1^* A U_1$：

- **第一列**：$(U_1^* A U_1) e_1 = U_1^* A (U_1 e_1) = U_1^* A u_1 \overset{(1)}{=} U_1^* (\lambda_1 u_1) = \lambda_1 e_1$。

所以 $U_1^* A U_1$ 的第一列只有第 $1$ 位为 $\lambda_1$，其余为零。其余列无任何约束，记其上方为 $b^* \in \mathbb{C}^n$（行向量）、下方为 $A_1 \in \mathbb{C}^{n \times n}$，则
$$U_1^* A U_1 \;=\; \begin{pmatrix} \lambda_1 & b^* \\ \mathbf{0} & A_1 \end{pmatrix}. \quad \cdots (2)$$

> [!important] 第一列被压平是关键
> $U_1^* A U_1$ 第一列为 $\lambda_1 e_1$ 这一事实，正是把 $u_1$ 放进 $U_1$ 第一列的目的：把 $A$ 在不变方向 $u_1$ 上的作用"挤"到 $(1,1)$ 位置，余下的"未知"$n \times n$ 块 $A_1$ 留给归纳处理。

#### 第四步：对子块 $A_1$ 应用归纳假设

$A_1 \in \mathbb{C}^{n \times n}$，由归纳假设，存在酉矩阵 $U_2 \in \mathbb{C}^{n \times n}$ 与上三角阵 $T_1 \in \mathbb{C}^{n \times n}$ 使
$$U_2^* A_1 U_2 \;=\; T_1. \quad \cdots (3)$$

构造分块酉矩阵
$$V \;=\; \begin{pmatrix} 1 & \mathbf{0} \\ \mathbf{0} & U_2 \end{pmatrix} \;\in\; \mathbb{C}^{(n+1) \times (n+1)}.$$

**验证 $V$ 为酉矩阵**：
$$V^* V \;=\; \begin{pmatrix} 1 & \mathbf{0} \\ \mathbf{0} & U_2^* \end{pmatrix} \begin{pmatrix} 1 & \mathbf{0} \\ \mathbf{0} & U_2 \end{pmatrix} \;=\; \begin{pmatrix} 1 & \mathbf{0} \\ \mathbf{0} & U_2^* U_2 \end{pmatrix} \;=\; I_{n+1}. \;\checkmark$$

将 $V^* (\cdot) V$ 作用于 $(2)$：
$$V^* U_1^* A U_1 V \;=\; \begin{pmatrix} 1 & \mathbf{0} \\ \mathbf{0} & U_2^* \end{pmatrix} \begin{pmatrix} \lambda_1 & b^* \\ \mathbf{0} & A_1 \end{pmatrix} \begin{pmatrix} 1 & \mathbf{0} \\ \mathbf{0} & U_2 \end{pmatrix} \;=\; \begin{pmatrix} \lambda_1 & b^* U_2 \\ \mathbf{0} & U_2^* A_1 U_2 \end{pmatrix} \overset{(3)}{=} \begin{pmatrix} \lambda_1 & b^* U_2 \\ \mathbf{0} & T_1 \end{pmatrix}.$$

记上式右边为 $T$。由 $T_1$ 上三角及第一列下方为零，$T$ 整体上三角。$\square$

#### 第五步：合并酉变换

令 $U = U_1 V$。两个酉矩阵之积仍是酉矩阵：
$$U^* U \;=\; (U_1 V)^* (U_1 V) \;=\; V^* U_1^* U_1 V \;=\; V^* V \;=\; I_{n+1}.$$

由第四步，$U^* A U = T$ 上三角。换言之，
$$A \;=\; U T U^*.$$

### 对角元为特征值的验证

由酉相似保谱，$\sigma(A) = \sigma(T)$。而上三角阵 $T$ 的特征值为其对角元（按重数计），故 $T$ 的对角元正是 $A$ 的全部特征值。

**顺序可任意指定**：在第一步中可任意选取 $A$ 的某个特征值作为 $\lambda_1$，故依次可让对角元按指定顺序排列。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 整个证明用**两个工具**：代数基本定理（保证有特征值）+ 归纳（处理子块）。
>
> 每一步把 $A$ 的一个**不变方向 $u_1$ 旋转到第一坐标轴**，借酉相似把 $A$ 化为
> $$\begin{pmatrix} \lambda_1 & * \\ 0 & A_1 \end{pmatrix},$$
> 再对 $A_1$ 重复同样操作。最后得到一个完全上三角的矩阵 —— 这正是用酉相似可达到的最简结构（实矩阵上不能再约化为对角阵，因实矩阵可能有复特征值）。

> [!warning] Schur 分解不唯一
> 不同的特征值选取顺序、不同的 Gram–Schmidt 扩张方式都会给出不同的 $(U, T)$。但对角元（作为多重集）总是 $A$ 的谱。这一非唯一性在 [[Cholesky 分解的存在性与唯一性|Cholesky]] 与正定矩阵上的 QR 分解（后者要求对角元 > 0）那种"可加约束使其唯一"的情形不同。

> [!info] 实 Schur 分解
> 对实矩阵 $A \in \mathbb{R}^{n \times n}$，复特征值成对出现。若只允许正交相似，则可化为**实 Schur 形**：分块上三角，对角块为 $1 \times 1$（对应实特征值）或 $2 \times 2$（对应复共轭特征值对）。这是数值实现 QR 算法时的标准输出。

---

## 应用

### 应用一：正规矩阵的谱定理

> [!important] 定理（谱定理）
> 设 $A \in \mathbb{C}^{n \times n}$。下面三条等价：
> 1. $A$ 是**正规矩阵**，即 $A^* A = A A^*$。
> 2. $A$ 可酉对角化，即存在酉矩阵 $U$ 与对角阵 $\Lambda$ 使 $A = U \Lambda U^*$。
> 3. $\mathbb{C}^n$ 中存在 $A$ 的一组标准正交特征基。

**证明 (1) $\Rightarrow$ (2)**：由 **Schur 分解定理**，存在酉 $U$ 与上三角 $T$ 使 $A = U T U^*$。则
$$T^* T \;=\; U^* A^* U \cdot U^* A U \;=\; U^* A^* A U \;\overset{\text{正规}}{=}\; U^* A A^* U \;=\; T T^*.$$
即 $T$ 也是正规上三角阵。

**关键引理**：正规的上三角矩阵必为对角矩阵。

由 $T T^* = T^* T$ 取 $(1,1)$ 位置：
$$\sum_{j=1}^n |t_{1j}|^2 \;=\; |t_{11}|^2.$$
故 $t_{12} = t_{13} = \cdots = t_{1n} = 0$。再取 $(2,2)$ 位置：
$$|t_{22}|^2 + \sum_{j=3}^n |t_{2j}|^2 \;=\; |t_{22}|^2$$
（左侧上方贡献已为零）。故 $t_{2j} = 0$ ($j \geq 3$)。逐行重复，得 $T$ 是对角阵。$\square$

(2) $\Rightarrow$ (3) 与 (3) $\Rightarrow$ (1) 平凡。$\blacksquare$

> [!info] 数值意义
> 谱定理保证 **Hermitian 矩阵**（特例：$A^* = A$）、**酉矩阵**（$A^* A = I$）、**反 Hermitian 矩阵**等都可酉对角化。这是 PCA、谱聚类、量子力学算符离散化的数学基础。

### 应用二：迹与行列式的特征值表示

> [!important] 推论
> 设 $A \in \mathbb{C}^{n \times n}$ 的特征值（按代数重数计）为 $\lambda_1, \ldots, \lambda_n$。则
> $$\operatorname{tr}(A) \;=\; \sum_{i=1}^n \lambda_i, \qquad \det(A) \;=\; \prod_{i=1}^n \lambda_i.$$

**证明**：由 Schur 分解 $A = U T U^*$。

- $\operatorname{tr}(A) = \operatorname{tr}(U T U^*) = \operatorname{tr}(T U^* U) = \operatorname{tr}(T) = \sum_i t_{ii} = \sum_i \lambda_i$（用迹的循环不变性）。
- $\det(A) = \det(U) \det(T) \det(U^*) = |\det(U)|^2 \det(T) = \det(T) = \prod_i t_{ii} = \prod_i \lambda_i$（酉矩阵的行列式模为 $1$）。$\square$

### 应用三：Cayley–Hamilton 定理

> [!important] 定理（Cayley–Hamilton）
> 记 $A$ 的特征多项式为 $p_A(z) = \det(zI - A) = \prod_i (z - \lambda_i)$。则 $p_A(A) = 0$。

**证明**：由 Schur 分解 $A = U T U^*$，且对任意多项式 $p$，$p(A) = U\, p(T)\, U^*$。故只需证 $p_A(T) = 0$。

由 $A$ 与 $T$ 谱相同，$p_A(z) = \prod_i (z - t_{ii})$。考察 $\prod_i (T - t_{ii} I)$：每个因子 $T - t_{ii} I$ 是上三角阵且第 $i$ 个对角元为 $0$。

**关键观察**：$(T - t_{11} I) e_1 = 0$，故 $(T - t_{11} I)$ 的第一列为零。一般地，逐次相乘
$$(T - t_{ii} I)(T - t_{i-1, i-1} I) \cdots (T - t_{11} I)$$
得到的矩阵前 $i$ 列均为零（细节：每次乘 $T - t_{ii} I$ 会把"前 $i - 1$ 列零矩阵"再多杀掉一列）。

当 $i = n$ 时，前 $n$ 列全为零，即整个矩阵为零。$\square$

### 应用四：矩阵函数的计算（Parlett 递推）

> [!info] 矩阵函数 $f(A)$
> 对解析函数 $f$，若 $A = U T U^*$ 是 Schur 分解，则
> $$f(A) \;=\; U f(T) U^*.$$
> 问题归约为**计算上三角矩阵的函数**。

**Parlett 递推公式**：设 $T$ 上三角，$F = f(T)$ 也上三角。对角元：$F_{ii} = f(t_{ii})$。对超对角元（$i < j$），由 $F T = T F$（因 $F$ 是 $T$ 的多项式（局部），与 $T$ 交换）逐项比较得
$$F_{ij} \;=\; \frac{t_{ij}(F_{ii} - F_{jj}) + \sum_{k = i+1}^{j-1} (F_{ik} t_{kj} - t_{ik} F_{kj})}{t_{ii} - t_{jj}}, \quad (t_{ii} \neq t_{jj}).$$

> [!info] 应用场景
> 数值计算 $e^A$（控制论、量子演化）、$\log A$（矩阵对数与流形几何）、$A^{1/2}$（半定规划、Lyapunov 方程）都走这条路。**MATLAB 的 `funm`、SciPy 的 `scipy.linalg.funm`** 内部即是 Schur + Parlett。

### 应用五：QR 算法的理论基础

**QR 迭代**：给定 $A_0 = A$，反复做 QR 分解再重组：
$$A_k \;=\; Q_k R_k, \quad A_{k+1} \;=\; R_k Q_k. \quad \cdots (\dagger)$$

> [!important] 结论
> 在适当条件下（特征值模不同、子模为 $1$ 时另作处理），$(\dagger)$ 中的 $A_k$ 收敛到 $A$ 的 Schur 形 $T$，对角元给出 $A$ 的特征值。

**为什么是 Schur 形**：由 $(\dagger)$，$A_{k+1} = R_k Q_k = Q_k^* (Q_k R_k) Q_k = Q_k^* A_k Q_k$。故 $A_k$ 与 $A$ 始终**酉相似**。若收敛到上三角，则其对角元即特征值。这一目标正是 Schur 分解所担保的"用酉相似可达"。

> [!info] 数值现实
> Schur 分解是**所有现代特征值算法的目标形态**：实矩阵走实 Schur 形（块上三角），Hermitian 矩阵更优（直接到对角阵）。LAPACK 的 `*GEES`（一般 Schur）、`*GEEV`（特征值）、`*SYEV` / `*HEEV`（Hermitian）都以此为蓝本。

### 应用六：谱半径的算子范数极限公式（Gelfand 公式雏形）

> [!info] 推论
> 对任意 $A \in \mathbb{C}^{n \times n}$，
> $$\lim_{k \to \infty} \|A^k\|^{1/k} \;=\; \rho(A).$$
> 详见 [[线性迭代法收敛性的谱半径准则]]。

利用 Schur 分解可直接证明 $\rho(A) < 1 \Rightarrow A^k \to 0$：因 $A^k = U T^k U^*$，且当 $\max_i |t_{ii}| < 1$ 时上三角阵幂 $T^k \to 0$（先证对角阵情形再加上"幂零超对角扰动"分解 $T = D + N$，$D$ 对角，$N$ 严格上三角故 $N^n = 0$）。
