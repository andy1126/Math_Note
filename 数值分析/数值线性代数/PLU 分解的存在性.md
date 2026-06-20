---
title: PLU 分解的存在性
date: 2026-06-06
tags:
  - 数值分析
  - 数值线性代数
  - PLU分解
  - 高斯消元
  - 主元交换
  - 部分主元
---

# PLU 分解的存在性

## 预备定义

> [!note] 置换矩阵
> 设 $\pi$ 是 $\{1,\ldots,n\}$ 的置换。称
> $$P_\pi \;=\; \bigl[e_{\pi(1)}\ \ e_{\pi(2)}\ \cdots\ e_{\pi(n)}\bigr]^\top \;\in\; \mathbb{R}^{n\times n}$$
> 为 $\pi$ 对应的**置换矩阵**：其作用于向量 $x$ 时给出 $(P_\pi x)_i = x_{\pi(i)}$。
>
> **基本性质**：$P_\pi^\top P_\pi = I$（正交矩阵），$P_\pi^{-1} = P_\pi^\top$，$\det P_\pi = \mathrm{sgn}(\pi) = \pm 1$。

> [!note] 部分主元（partial pivoting）
> 在高斯消元第 $k$ 步：先在第 $k$ 列的子块 $\{a_{ik}^{(k-1)} : i \geq k\}$ 中找模最大元 $a_{i_k k}^{(k-1)}$，再把第 $k$ 行与第 $i_k$ 行交换，最后做消元。该策略**保证消元乘子 $|\ell_{ik}| \leq 1$**。

> [!note] PLU 分解
> 称分解 $PA = LU$ 为 $A$ 的 **PLU 分解**，其中 $P$ 是置换矩阵，$L$ 是单位下三角阵，$U$ 是上三角阵。

> [!abstract] 引理 1：置换矩阵的封闭性
> 两个置换矩阵的乘积仍是置换矩阵；置换矩阵的转置（即逆）仍是置换矩阵。

**证明**：直接验证。若 $P_\sigma P_\tau = P_{\sigma\tau}$（置换的复合）即得。$\square$

> [!abstract] 引理 2：非奇异矩阵的某列必有非零元
> 设 $A \in \mathbb{R}^{n\times n}$ 非奇异。则 $A$ 的每一列都至少含一个非零元。

**证明**：若第 $k$ 列全零，则 $A e_k = 0$，$A$ 有非零核向量 $e_k$，与可逆矛盾。$\square$

> [!abstract] 引理 3：部分主元保证乘子有界
> 在部分主元策略下，第 $k$ 步行交换后 $|a_{kk}^{(k-1)}| = \max_{i \geq k}|a_{ik}^{(k-1)}|$，故乘子
> $$|\ell_{ik}| \;=\; \left|\frac{a_{ik}^{(k-1)}}{a_{kk}^{(k-1)}}\right| \;\leq\; 1.$$

---

## 定理（PLU 分解的存在性）

设 $A \in \mathbb{R}^{n\times n}$ 非奇异。则存在置换矩阵 $P$、单位下三角阵 $L$（满足 $|\ell_{ij}| \leq 1$）与非奇异上三角阵 $U$ 使
$$PA \;=\; LU.$$

---

## 证明（数学归纳法）

### 基础情形 $n = 1$

$A = (a_{11})$，$a_{11} \neq 0$。取 $P = (1)$、$L = (1)$、$U = (a_{11})$。$\square$

### 归纳步骤

**归纳假设**：对所有 $\leq n-1$ 阶非奇异矩阵，PLU 分解存在。

#### 第一步：选主元 + 行交换

由引理 2，$A$ 第 1 列至少含一个非零元。设 $|a_{i_1, 1}| = \max_i |a_{i,1}|$。令 $P_1$ 为对换 $(1, i_1)$ 的置换矩阵。则
$$P_1 A \;=\; \begin{pmatrix} \alpha & v^\top \\ w & B \end{pmatrix}, \qquad \alpha = a_{i_1, 1} \neq 0,$$
其中 $v \in \mathbb{R}^{n-1}$、$w \in \mathbb{R}^{n-1}$、$B \in \mathbb{R}^{(n-1)\times(n-1)}$。

#### 第二步：一步消元

令 $\ell = w/\alpha \in \mathbb{R}^{n-1}$。由引理 3，$\|\ell\|_\infty \leq 1$。构造 Frobenius 矩阵
$$L_1 \;=\; \begin{pmatrix} 1 & 0 \\ -\ell & I_{n-1} \end{pmatrix}.$$
则
$$L_1 P_1 A \;=\; \begin{pmatrix} \alpha & v^\top \\ 0 & B - \ell v^\top \end{pmatrix} \;=:\; \begin{pmatrix} \alpha & v^\top \\ 0 & \widetilde A \end{pmatrix},$$
其中 $\widetilde A = B - \ell v^\top \in \mathbb{R}^{(n-1)\times(n-1)}$。

#### 第三步：$\widetilde A$ 非奇异

由 $\det(L_1 P_1 A) = \det L_1 \cdot \det P_1 \cdot \det A = (\pm 1) \cdot \det A \neq 0$。又由分块行列式
$$\det(L_1 P_1 A) \;=\; \alpha \cdot \det \widetilde A,$$
故 $\det \widetilde A \neq 0$，$\widetilde A$ 非奇异。

#### 第四步：对 $\widetilde A$ 应用归纳假设

存在 $\widetilde P \in \mathbb{R}^{(n-1)\times(n-1)}$ 置换、$\widetilde L$ 单位下三角（$|\widetilde \ell_{ij}| \leq 1$）、$\widetilde U$ 上三角非奇异，使
$$\widetilde P \widetilde A \;=\; \widetilde L \widetilde U.$$

#### 第五步：处理"延迟置换"，拼装 $PA = LU$

令分块 $\overline P = \begin{pmatrix} 1 & 0 \\ 0 & \widetilde P \end{pmatrix}$，左乘 $L_1 P_1 A$：
$$\overline P L_1 P_1 A \;=\; \begin{pmatrix} 1 & 0 \\ 0 & \widetilde P \end{pmatrix} \begin{pmatrix} \alpha & v^\top \\ 0 & \widetilde A \end{pmatrix} \;=\; \begin{pmatrix} \alpha & v^\top \\ 0 & \widetilde P \widetilde A \end{pmatrix} \;=\; \begin{pmatrix} \alpha & v^\top \\ 0 & \widetilde L \widetilde U \end{pmatrix}.$$

**技术难点**：$\overline P L_1 \neq L_1' \overline P$ 一般不成立，但可证明
$$\overline P L_1 \;=\; \begin{pmatrix} 1 & 0 \\ 0 & \widetilde P \end{pmatrix} \begin{pmatrix} 1 & 0 \\ -\ell & I \end{pmatrix} \;=\; \begin{pmatrix} 1 & 0 \\ -\widetilde P \ell & \widetilde P \end{pmatrix} \;=\; \begin{pmatrix} 1 & 0 \\ -\widetilde P \ell & I \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & \widetilde P \end{pmatrix} \;=\; L_1'\, \overline P,$$
其中 $L_1' = I - \widehat \ell e_1^\top$，$\widehat \ell = \begin{pmatrix} 0 \\ \widetilde P \ell \end{pmatrix}$，仍是 Frobenius 矩阵且 $\|\widehat \ell\|_\infty = \|\ell\|_\infty \leq 1$（置换只重排不改大小）。

故
$$L_1' \overline P P_1 A \;=\; \begin{pmatrix} \alpha & v^\top \\ 0 & \widetilde L \widetilde U \end{pmatrix}.$$
左乘 $(L_1')^{-1}$：
$$\overline P P_1 A \;=\; (L_1')^{-1} \begin{pmatrix} \alpha & v^\top \\ 0 & \widetilde L \widetilde U \end{pmatrix} \;=\; \begin{pmatrix} 1 & 0 \\ \widetilde P \ell & I \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & \widetilde L \end{pmatrix} \begin{pmatrix} \alpha & v^\top \\ 0 & \widetilde U \end{pmatrix}.$$

#### 第六步：完成分解

令
$$P \;=\; \overline P P_1, \qquad L \;=\; \begin{pmatrix} 1 & 0 \\ \widetilde P \ell & \widetilde L \end{pmatrix}, \qquad U \;=\; \begin{pmatrix} \alpha & v^\top \\ 0 & \widetilde U \end{pmatrix}.$$

由引理 1，$P$ 仍为置换矩阵。$L$ 单位下三角（左上 $1$、第 1 列下方为 $\widetilde P \ell$，模 $\leq 1$；右下块 $\widetilde L$ 单位下三角且乘子 $|\widetilde \ell_{ij}| \leq 1$）。$U$ 上三角，$\det U = \alpha \cdot \det \widetilde U \neq 0$。

$PA = LU$ 即得证。$\square$

---

## 唯一性讨论

> [!warning] PLU 分解不唯一
> 不同主元选择可能给出不同的 $(P, L, U)$。如部分主元 vs 完全主元结果不同；甚至同一策略下，模相同的两个候选主元可任选其一。
>
> **但**：固定主元策略 + 决胜规则（如"取索引最小"）后，PLU 唯一。

> [!info] 何时 $P = I$
> 由 [[LU 分解的存在性与唯一性]] 定理 (i)：若 $A$ 所有顺序主子式非零，则 $A$ 有 Doolittle LU 分解。此时部分主元算法可能恰好 $P = I$，但不必然——部分主元仍可能因"模最大"原则交换行。

---

## 具体应用

### 应用一：3×3 PLU 演算

取
$$A \;=\; \begin{pmatrix} 0 & 2 & 3 \\ 1 & 1 & 1 \\ 2 & 3 & 1 \end{pmatrix}.$$
$a_{11} = 0$，Doolittle LU 不存在；需主元交换。

#### 第 1 步：第 1 列主元

$\max(|0|, |1|, |2|) = 2$ 在第 3 行。$P_1 = (1\ 3)$（对换 1、3）。
$$P_1 A \;=\; \begin{pmatrix} 2 & 3 & 1 \\ 1 & 1 & 1 \\ 0 & 2 & 3 \end{pmatrix}.$$
主元 $2$，乘子 $\ell_{21} = 1/2$、$\ell_{31} = 0$。消去：
$$L_1 P_1 A \;=\; \begin{pmatrix} 2 & 3 & 1 \\ 0 & -1/2 & 1/2 \\ 0 & 2 & 3 \end{pmatrix}.$$

#### 第 2 步：第 2 列主元

$\max(|-1/2|, |2|) = 2$ 在第 3 行。$\widetilde P = (2\ 3)$，整体置换 $P_2 = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 0 & 1 \\ 0 & 1 & 0 \end{pmatrix}$。

交换后：
$$\begin{pmatrix} 2 & 3 & 1 \\ 0 & 2 & 3 \\ 0 & -1/2 & 1/2 \end{pmatrix}.$$
乘子 $\ell_{32} = -1/4$，消去：
$$U \;=\; \begin{pmatrix} 2 & 3 & 1 \\ 0 & 2 & 3 \\ 0 & 0 & 5/4 \end{pmatrix}.$$

#### 拼装

总置换 $P = P_2 P_1$，对应 $\pi = (3, 1, 2) \to (3, 2, 1)$ 复合，最终
$$P \;=\; \begin{pmatrix} 0 & 0 & 1 \\ 1 & 0 & 0 \\ 0 & 1 & 0 \end{pmatrix}, \quad PA \;=\; \begin{pmatrix} 2 & 3 & 1 \\ 0 & 2 & 3 \\ 1 & 1 & 1 \end{pmatrix}.$$

收集乘子（注意延迟置换：$\ell_{21} = 1/2$ 需被 $\widetilde P$ 重排为 $L$ 的第 1 列第 3 位）：
$$L \;=\; \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 1/2 & -1/4 & 1 \end{pmatrix}.$$

验证 $LU = PA$ ✓。

### 应用二：用 PLU 求解 $Ax = b$

$PA = LU \Rightarrow A x = b \Leftrightarrow LU x = P b$。两步：

1. **前代**：解 $L y = Pb$，$O(n^2)$；
2. **回代**：解 $U x = y$，$O(n^2)$。

总复杂度同 LU：分解 $\frac{2}{3}n^3$ + 求解 $O(n^2)$。

### 应用三：部分主元 vs 完全主元 vs 标度部分主元

> [!info] 完全主元（complete pivoting）
> 第 $k$ 步在整个余下子块 $\{a_{ij}^{(k-1)} : i,j \geq k\}$ 找模最大元，需两个置换：$P A Q = L U$。
> - **优**：理论上最稳定；可作为秩 revealing；
> - **劣**：每步选主元 $O((n-k)^2)$ 比较，总开销 $O(n^3)$，与消元同阶但常数大；实际很少用。

> [!info] 标度部分主元（scaled partial pivoting）
> 按每行的最大模 $s_i = \max_j |a_{ij}|$ 归一化后再比较 $|a_{ik}|/s_i$。可应对**行尺度严重不均**的情形。

> [!important] 默认选择：部分主元
> 部分主元在绝大多数实际矩阵上给出与完全主元相当的稳定性，但额外开销仅 $O(n^2)$。**LAPACK 默认**。

---

## 算法关键点

> [!tip] 部分主元的代价与收益
> 每步多 $O(n-k)$ 的比较选主元，整体 $O(n^2)$ 额外开销——相比 $\frac{2}{3}n^3$ 消元微不足道。换来的是 $|\ell_{ij}| \leq 1$，避免舍入误差的指数放大。**几乎免费的稳定性提升**。

> [!warning] PLU 不总是后向稳定的
> Wilkinson 反例：
> $$A \;=\; \begin{pmatrix} 1 & & & & 1 \\ -1 & 1 & & & 1 \\ -1 & -1 & 1 & & 1 \\ \vdots & & \ddots & & \vdots \\ -1 & -1 & \cdots & -1 & 1 \end{pmatrix}.$$
> 部分主元后增长因子 $\max|u_{ij}|/\max|a_{ij}| = 2^{n-1}$，舍入误差呈指数放大。**实践中极少触发**（高斯消元后向稳定的"伪定理"几十年来始终成立），但理论上需用完全主元防御。

> [!important] 实现细节
> - In-place：$L$ 的乘子覆盖到 $A$ 已清零的位置；$U$ 占据上三角；$P$ 用整数置换数组 $n$ 个元素记录；
> - LAPACK `dgetrf`：返回紧凑 $LU$ + 置换数组 `ipiv`，内存仅 $A$ 本身。

详细的工程实现与稳定性分析参见 [[浮点运算与后向稳定性]]、[[矩阵条件数与扰动分析]]。

$\blacksquare$
