---
title: LU 分解的存在性与唯一性
date: 2026-05-24
tags:
  - 数值分析
  - 矩阵分解
  - 高斯消元
  - LU分解
  - 线性方程组
---

# LU 分解的存在性与唯一性

## 预备定义

> [!note] 上三角矩阵 / 下三角矩阵
> 矩阵 $A = (a_{ij}) \in \mathbb{R}^{n \times n}$ 称为**上三角**，若 $a_{ij} = 0$（$i > j$）；称为**下三角**，若 $a_{ij} = 0$（$i < j$）。
>
> 若下三角阵的对角元全为 $1$，称为**单位下三角矩阵** (unit lower triangular)。

> [!note] 顺序主子式 (leading principal minor)
> 对 $A \in \mathbb{R}^{n \times n}$ 与 $k \in \{1,\ldots,n\}$，记 $A_k$ 为 $A$ 左上角 $k \times k$ 子块：
> $$A_k \;=\; \begin{pmatrix} a_{11} & \cdots & a_{1k} \\ \vdots & & \vdots \\ a_{k1} & \cdots & a_{kk} \end{pmatrix}.$$
> 称 $\det(A_k)$ 为 $A$ 的**第 $k$ 阶顺序主子式**。

> [!note] LU 分解（Doolittle 形式）
> 设 $A \in \mathbb{R}^{n \times n}$。若存在单位下三角阵 $L$ 与上三角阵 $U$ 使
> $$A \;=\; L U,$$
> 称之为 $A$ 的 **LU 分解（Doolittle 形式）**。

> [!abstract] 引理 1：三角阵的代数封闭性
> (a) 两个下三角阵的乘积仍为下三角阵；上三角同理。
> (b) 两个单位下三角阵的乘积仍为单位下三角阵。
> (c) 可逆单位下三角阵的逆仍为单位下三角阵。

**证明**：(a) 设 $L, M$ 为下三角阵，$C = LM$。当 $i < j$ 时，
$$c_{ij} \;=\; \sum_{k=1}^{n} \ell_{ik} m_{kj}.$$
若 $\ell_{ik} \neq 0$，需 $k \leq i < j$，故 $k < j$，则 $m_{kj} = 0$。故 $c_{ij} = 0$。

(b) 在 (a) 基础上，对 $i = j$，$c_{ii} = \sum_{k} \ell_{ik} m_{ki}$。$\ell_{ik} \neq 0$ 需 $k \leq i$，$m_{ki} \neq 0$ 需 $k \geq i$，故 $k = i$，$c_{ii} = \ell_{ii} m_{ii} = 1 \cdot 1 = 1$。

(c) 单位下三角阵 $L$ 的对角元为 $1$，故 $\det L = 1 \neq 0$，可逆。由 Cramer 法则或归纳逐列求解 $LX = I$，可验证 $X$ 单位下三角。$\square$

> [!abstract] 引理 2：分块矩阵的 LU 一致性
> 若 $A = LU$ 为 Doolittle 分解，则对每个 $k \in \{1,\ldots,n\}$，
> $$A_k \;=\; L_k U_k,$$
> 其中 $A_k, L_k, U_k$ 分别为各矩阵左上角 $k \times k$ 子块；且 $L_k$ 单位下三角、$U_k$ 上三角。

**证明**：将 $L, U$ 按 $k$ 阶分块：
$$L \;=\; \begin{pmatrix} L_k & 0 \\ L_{21} & L_{22} \end{pmatrix}, \quad U \;=\; \begin{pmatrix} U_k & U_{12} \\ 0 & U_{22} \end{pmatrix}.$$
由分块乘法，
$$A \;=\; LU \;=\; \begin{pmatrix} L_k U_k & L_k U_{12} \\ L_{21} U_k & L_{21} U_{12} + L_{22} U_{22} \end{pmatrix}.$$
左上块即 $A_k = L_k U_k$。$L_k, U_k$ 显然继承单位下三角与上三角性质。$\square$

---

## 定理

设 $A \in \mathbb{R}^{n \times n}$。则以下结论成立：

**(i)（存在性）** 若 $A$ 的所有顺序主子式非零，即 $\det(A_k) \neq 0$（$k = 1,\ldots,n$），则 $A$ 存在 Doolittle 形式的 LU 分解 $A = LU$。

**(ii)（唯一性）** 在 (i) 的条件下，该分解唯一。

**(iii)（必要性）** 反之，若 $A$ 存在 Doolittle 分解 $A = LU$ 且 $U$ 的所有对角元 $u_{ii} \neq 0$，则 $A$ 的所有顺序主子式非零。

---

## 第(i)部分的证明（存在性）

**数学归纳法**对矩阵阶数 $n$ 进行归纳。

### 基础情形：$n = 1$

$A = (a_{11})$，$\det(A_1) = a_{11} \neq 0$。取 $L = (1)$，$U = (a_{11})$，显然 $A = LU$。$\square$

### 归纳步骤

**归纳假设**：设结论对所有阶数 $\leq n-1$ 的矩阵成立。

**目标**：对 $n$ 阶矩阵 $A$，$\det(A_k) \neq 0$（$k = 1,\ldots,n$），构造 $A = LU$。

#### 第一步：分块写法

将 $A$ 按 $(n-1) + 1$ 分块：
$$A \;=\; \begin{pmatrix} A_{n-1} & b \\ c^\top & a_{nn} \end{pmatrix},$$
其中 $A_{n-1} \in \mathbb{R}^{(n-1)\times(n-1)}$ 即 $A$ 的 $(n-1)$ 阶顺序主子块，$b, c \in \mathbb{R}^{n-1}$。

#### 第二步：对 $A_{n-1}$ 应用归纳假设

$A_{n-1}$ 的顺序主子式即 $A_1, \ldots, A_{n-1}$ 的行列式，由假设均非零。由归纳假设，存在单位下三角 $\widetilde L \in \mathbb{R}^{(n-1)\times(n-1)}$ 与上三角 $\widetilde U \in \mathbb{R}^{(n-1)\times(n-1)}$ 使
$$A_{n-1} \;=\; \widetilde L \widetilde U. \quad \cdots (1)$$

由 $\det(A_{n-1}) \neq 0$，$\widetilde L, \widetilde U$ 均可逆。又 $\widetilde L$ 单位下三角，由引理 1，$\widetilde L^{-1}$ 单位下三角。

#### 第三步：构造 $L, U$ 的最后一行/列

寻找 $\ell \in \mathbb{R}^{n-1}$、$u \in \mathbb{R}^{n-1}$、$u_{nn} \in \mathbb{R}$，使
$$A \;=\; \begin{pmatrix} \widetilde L & 0 \\ \ell^\top & 1 \end{pmatrix} \begin{pmatrix} \widetilde U & u \\ 0 & u_{nn} \end{pmatrix} \;=\; \begin{pmatrix} \widetilde L \widetilde U & \widetilde L u \\ \ell^\top \widetilde U & \ell^\top u + u_{nn} \end{pmatrix}.$$

对照分块条目：

| 条目 | 等式 |
| --- | --- |
| 左上 | $\widetilde L \widetilde U = A_{n-1}$ ✓（由 (1)） |
| 右上 | $\widetilde L u = b$ |
| 左下 | $\ell^\top \widetilde U = c^\top$ |
| 右下 | $\ell^\top u + u_{nn} = a_{nn}$ |

由 $\widetilde L$ 可逆，唯一求得 $u = \widetilde L^{-1} b$；由 $\widetilde U$ 可逆，唯一求得 $\ell^\top = c^\top \widetilde U^{-1}$；最后取 $u_{nn} = a_{nn} - \ell^\top u$。

#### 第四步：验证 $L$ 单位下三角、$U$ 上三角

由构造，$L$ 的左上 $(n-1)\times(n-1)$ 块为 $\widetilde L$（单位下三角），最后一行为 $(\ell^\top, 1)$，故 $L$ 单位下三角。同理 $U$ 上三角。$\square$

---

## 第(ii)部分的证明（唯一性）

**反证法**。假设 $A = L_1 U_1 = L_2 U_2$ 为两个 Doolittle 分解。

#### 第一步：由顺序主子式非零推出 $U_i$ 可逆

由引理 2，$A_n = A = L_i U_i$，故
$$\det(A) \;=\; \det(L_i) \det(U_i) \;=\; 1 \cdot \prod_{k=1}^n u_{kk}^{(i)}.$$
由 $\det(A) = \det(A_n) \neq 0$，故 $u_{kk}^{(i)} \neq 0$ 对一切 $k$，$U_i$ 可逆。同理 $L_i$ 可逆（其行列式为 $1$）。

#### 第二步：建立等式 $L_2^{-1} L_1 = U_2 U_1^{-1}$

由 $L_1 U_1 = L_2 U_2$ 两边左乘 $L_2^{-1}$、右乘 $U_1^{-1}$：
$$L_2^{-1} L_1 \;=\; U_2 U_1^{-1}. \quad \cdots (\star)$$

#### 第三步：两边的三角性矛盾分析

由引理 1：
- $L_1, L_2$ 单位下三角 $\Rightarrow L_2^{-1}$ 单位下三角 $\Rightarrow L_2^{-1} L_1$ 单位下三角；
- $U_1, U_2$ 上三角且可逆 $\Rightarrow U_1^{-1}$ 上三角 $\Rightarrow U_2 U_1^{-1}$ 上三角。

由 $(\star)$，**同一个矩阵既单位下三角又上三角**，故其只能是单位矩阵 $I$：
$$L_2^{-1} L_1 \;=\; I \;=\; U_2 U_1^{-1}.$$

#### 第四步：推出 $L_1 = L_2$、$U_1 = U_2$

由上式得 $L_1 = L_2$ 与 $U_2 = U_1$，分解唯一。$\square$

---

## 第(iii)部分的证明（必要性）

设 $A = LU$，$u_{ii} \neq 0$（$i = 1,\ldots,n$）。由引理 2，$A_k = L_k U_k$，故
$$\det(A_k) \;=\; \det(L_k) \det(U_k) \;=\; 1 \cdot \prod_{i=1}^k u_{ii} \;\neq\; 0.$$
即 $A$ 的所有顺序主子式非零。$\square$

---

## 总结

综合三部分：

1. 存在性：顺序主子式非零 $\Rightarrow$ Doolittle 分解存在。 ✓
2. 唯一性：在 (i) 条件下分解唯一。 ✓
3. 必要性：Doolittle 分解（且 $U$ 对角非零）$\Rightarrow$ 顺序主子式非零。 ✓

故 **$A$ 有唯一 Doolittle LU 分解（$U$ 非奇异）$\Leftrightarrow$ $A$ 的所有顺序主子式非零**。$\blacksquare$

---

## 具体应用

### 应用一：用 LU 分解求解 $Ax = b$

求解线性方程组 $Ax = b$ 的标准两步法：

#### 第一步：前代 (forward substitution)

由 $A = LU$，方程变为 $L(Ux) = b$。令 $y = Ux$，先解 $Ly = b$：
$$y_1 = b_1, \qquad y_i = b_i - \sum_{j=1}^{i-1} \ell_{ij} y_j \quad (i = 2,\ldots,n).$$
因 $L$ 单位下三角，无需除法。运算量 $O(n^2)$。

#### 第二步：回代 (back substitution)

再解 $Ux = y$：
$$x_n = \frac{y_n}{u_{nn}}, \qquad x_i = \frac{1}{u_{ii}}\Bigl(y_i - \sum_{j=i+1}^{n} u_{ij} x_j\Bigr) \quad (i = n-1,\ldots,1).$$
运算量 $O(n^2)$。

**总复杂度**：LU 分解本身 $O\!\left(\frac{2}{3}n^3\right)$；分解一次后，**对不同右端 $b$ 反复求解只需 $O(n^2)$**，这是 LU 分解相对直接 Gauss 消元的最大优势。

### 应用二：具体数值例子

求解
$$\begin{pmatrix} 2 & 1 & 1 \\ 4 & 3 & 3 \\ 8 & 7 & 9 \end{pmatrix} x \;=\; \begin{pmatrix} 4 \\ 11 \\ 29 \end{pmatrix}.$$

#### 步骤 1：验证条件
- $\det(A_1) = 2$
- $\det(A_2) = 2 \cdot 3 - 1 \cdot 4 = 2$
- $\det(A_3) = \det(A) = 2$

均非零，存在唯一 LU 分解。

#### 步骤 2：求 LU 分解

按高斯消元过程：
$$L = \begin{pmatrix} 1 & 0 & 0 \\ 2 & 1 & 0 \\ 4 & 3 & 1 \end{pmatrix}, \quad U = \begin{pmatrix} 2 & 1 & 1 \\ 0 & 1 & 1 \\ 0 & 0 & 2 \end{pmatrix}.$$

验证：$LU = A$ ✓。

#### 步骤 3：前代解 $Ly = b$

$$y_1 = 4, \quad y_2 = 11 - 2 \cdot 4 = 3, \quad y_3 = 29 - 4 \cdot 4 - 3 \cdot 3 = 4.$$

#### 步骤 4：回代解 $Ux = y$

$$x_3 = \frac{4}{2} = 2, \quad x_2 = 3 - 1 \cdot 2 = 1, \quad x_1 = \frac{1}{2}(4 - 1 \cdot 1 - 1 \cdot 2) = \frac{1}{2}.$$

解为 $x = (1/2,\ 1,\ 2)^\top$。

### 应用三：行列式的快速计算

由 $A = LU$ 及 $\det L = 1$：
$$\det(A) \;=\; \det(U) \;=\; \prod_{i=1}^n u_{ii}.$$

上例：$\det(A) = 2 \cdot 1 \cdot 2 = 4$。

> [!info] 对比传统方法
> 直接展开 $n$ 阶行列式按定义需 $O(n!)$ 次乘法；用 LU 分解后只需 $O(n^3)$，是数值线性代数计算行列式的标准做法。

### 应用四：何时必须主元交换 (PA = LU)

> [!warning] LU 分解可能不存在
> 即使 $\det(A) \neq 0$，若某顺序主子式为零，Doolittle 分解仍不存在。例如
> $$A \;=\; \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \quad \det(A_1) = 0.$$
> 假设 $A = LU$，由 $\ell_{11} u_{11} = 0$（$\ell_{11} = 1$）得 $u_{11} = 0$，故 $\det(A) = u_{11} u_{22} = 0$，矛盾。

**解决方案**：引入行置换矩阵 $P$，求 **PLU 分解** $PA = LU$。对任意可逆 $A$，PLU 分解总存在（部分主元高斯消元保证）。上例：
$$\begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix} \;=\; \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} \;=\; I \cdot I.$$

即取 $P$ 为对换 $(1,2)$ 的置换阵后即化为单位阵的平凡 LU 分解。

> [!important] 部分主元的数值意义
> 即使 $\det(A_k) \neq 0$，若某 $u_{kk}$ 很小，回代时除以小数会**放大舍入误差**。实际算法（如 LAPACK 的 `dgetrf`）默认采用**部分主元 (partial pivoting)** 策略，每一步选当前列模最大元为主元，提升数值稳定性。

---

## 证明思路总结

> [!tip] 关键思想
> 三部分构成 LU 分解理论的"铁三角"：
>
> 1. **存在性证明用归纳法 + 分块构造**：把 $n$ 阶问题归约到 $(n-1)$ 阶子块，再在最后一行/列上"添加"一行 $\ell^\top$ 与一列 $u$。这本质就是高斯消元法第 $n$ 步的代数刻画。
>
> 2. **唯一性证明用"三角性双向夹击"**：从 $L_1 U_1 = L_2 U_2$ 移项得 $L_2^{-1} L_1 = U_2 U_1^{-1}$。左边单位下三角，右边上三角——同一个矩阵两种性质并存，必为单位阵。这是矩阵分解唯一性证明的**通用模板**（Cholesky、QR 唯一性同理）。
>
> 3. **必要性来自行列式分块**：$\det(A_k) = \det(L_k)\det(U_k)$，与单位下三角阵行列式为 $1$ 结合，立刻得到 $\det(A_k) = \prod u_{ii}$。

> [!warning] 顺序主子式非零是"过强"条件
> 该定理给出 Doolittle LU 分解的**充要条件**，但并非可逆矩阵的 LU 分解的充要条件——
> - **可逆但无 LU**：如 $\begin{pmatrix}0&1\\1&0\end{pmatrix}$，必须用 PLU。
> - **不可逆但有 LU**：如 $\begin{pmatrix}1&1\\1&1\end{pmatrix} = \begin{pmatrix}1&0\\1&1\end{pmatrix}\begin{pmatrix}1&1\\0&0\end{pmatrix}$，分解存在但 $U$ 奇异，定理 (iii) 的"$u_{ii} \neq 0$"条件失败。
>
> 实际计算中**总是使用 PLU**，普适且数值稳定。
