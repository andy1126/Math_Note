---
title: 奇异值分解 SVD
date: 2026-06-06
tags:
  - 数值分析
  - 数值线性代数
  - 奇异值分解
  - SVD
  - 矩阵分解
  - 伪逆
---

# 奇异值分解 SVD

## 预备定义

> [!note] 奇异值分解
> 设 $A \in \mathbb{R}^{m\times n}$。**奇异值分解**（SVD）指分解
> $$A \;=\; U \Sigma V^\top,$$
> 其中 $U \in \mathbb{R}^{m\times m}$、$V \in \mathbb{R}^{n\times n}$ 是正交矩阵，$\Sigma \in \mathbb{R}^{m\times n}$ 是"对角"矩阵：$\Sigma_{ii} = \sigma_i \geq 0$，其他元素为零，$\sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_{\min(m,n)} \geq 0$。
>
> $\sigma_i$ 称为 $A$ 的**奇异值**；$U$ 的列称**左奇异向量**，$V$ 的列称**右奇异向量**。

> [!note] 经济型 SVD
> 设 $r = \operatorname{rank}(A)$。**经济型 SVD**：
> $$A \;=\; U_r \Sigma_r V_r^\top,$$
> 其中 $U_r \in \mathbb{R}^{m\times r}$、$V_r \in \mathbb{R}^{n\times r}$ 列正交，$\Sigma_r = \mathrm{diag}(\sigma_1, \ldots, \sigma_r)$ 严格正对角阵。

> [!abstract] 引理 1：$A^\top A$ 与 $A A^\top$ 的谱
> $A^\top A \in \mathbb{R}^{n\times n}$ 与 $A A^\top \in \mathbb{R}^{m\times m}$ 都是对称半正定的，且具有相同的非零特征值集合 $\{\sigma_1^2, \ldots, \sigma_r^2\}$。

**证明**：对称半正定 trivial。非零特征值同集合：设 $A^\top A v = \mu v$，$\mu \neq 0$。则 $A v \neq 0$（否则 $A^\top A v = 0$），令 $w = Av$。$A A^\top w = A A^\top A v = A (\mu v) = \mu w$，故 $\mu$ 也是 $A A^\top$ 的特征值。反之同理。$\square$

---

## 主定理：SVD 的存在性

> [!abstract] 定理（SVD 存在性）
> 任意 $A \in \mathbb{R}^{m\times n}$ 存在 SVD $A = U \Sigma V^\top$。

### 证明（构造性）

#### 第一步：构造 $V$

$A^\top A \in \mathbb{R}^{n\times n}$ 对称半正定。由[[Schur分解定理|Schur 分解]]（实对称情形即谱分解）：存在正交 $V$ 使
$$V^\top (A^\top A) V \;=\; \mathrm{diag}(\sigma_1^2, \ldots, \sigma_n^2), \quad \sigma_1 \geq \cdots \geq \sigma_n \geq 0.$$

设 $r$ 是非零 $\sigma_i$ 的个数。记 $V = [V_r \mid V_0]$，$V_r$ 对应 $\sigma_1, \ldots, \sigma_r > 0$，$V_0$ 对应 $\sigma_{r+1} = \cdots = \sigma_n = 0$。

#### 第二步：构造 $U_r$

对 $i = 1, \ldots, r$，令
$$u_i \;=\; \frac{A v_i}{\sigma_i}.$$

**验证正交**：
$$u_i^\top u_j \;=\; \frac{1}{\sigma_i \sigma_j} v_i^\top A^\top A v_j \;=\; \frac{1}{\sigma_i \sigma_j} v_i^\top (\sigma_j^2 v_j) \;=\; \frac{\sigma_j}{\sigma_i} v_i^\top v_j \;=\; \delta_{ij}.$$

故 $U_r = [u_1, \ldots, u_r]$ 列正交。

#### 第三步：扩展 $U_r$ 为正交 $U$

$U_r \in \mathbb{R}^{m\times r}$ 列正交但不是方阵。用 Gram-Schmidt 或 Householder（[[Gram-Schmidt 与 QR 分解]]、[[Householder 反射与 Givens 旋转]]）扩展为正交 $U = [U_r \mid U_0]$，$U_0$ 的列在 $\mathcal{R}(A)^\perp$ 中。

#### 第四步：验证 $A = U \Sigma V^\top$

由 $A v_i = \sigma_i u_i$（$i \leq r$）与 $A v_i = 0$（$i > r$，因 $\|Av_i\|^2 = v_i^\top A^\top A v_i = 0$）：

$$A V \;=\; [A v_1, \ldots, A v_n] \;=\; [\sigma_1 u_1, \ldots, \sigma_r u_r, 0, \ldots, 0] \;=\; U \Sigma.$$

右乘 $V^\top$：$A = U \Sigma V^\top$。$\square$

---

## 唯一性讨论

> [!important] 奇异值的唯一性
> $\sigma_i$ 由 $A^\top A$ 的谱完全决定 → **奇异值唯一**（按降序）。

> [!warning] 奇异向量的非唯一性
> - 若 $\sigma_i$ 重复，则对应的奇异向量在子空间中**可任意选正交基**；
> - 即使 $\sigma_i$ 互异，每对 $(u_i, v_i)$ 仍可同步反号 $(u_i, v_i) \to (-u_i, -v_i)$；
> - $\sigma_i = 0$ 时 $u_i$ 仅由"扩展到正交"约束确定，非唯一。

---

## SVD 的几何与代数刻画

> [!abstract] 性质（几何）
> SVD 描述 $A$ 把单位球 $S = \{x : \|x\|_2 = 1\}$ 映成椭球：
> - 右奇异向量 $v_i$ → 单位球的主轴方向；
> - $A v_i = \sigma_i u_i$；
> - 左奇异向量 $u_i$ → 椭球的主轴方向；
> - $\sigma_i$ → 该主轴半长。

> [!abstract] 性质（代数）
> 1. $\|A\|_2 = \sigma_1$（最大奇异值，即谱范数）；
> 2. $\|A\|_F = \sqrt{\sigma_1^2 + \cdots + \sigma_r^2}$；
> 3. $\operatorname{rank}(A) = r$（非零奇异值个数）；
> 4. $\mathcal{N}(A) = \mathrm{span}\{v_{r+1}, \ldots, v_n\}$，$\mathcal{R}(A) = \mathrm{span}\{u_1, \ldots, u_r\}$；
> 5. **条件数**：$\kappa_2(A) = \sigma_1/\sigma_r$（$A$ 满秩方阵时）。

---

## Eckart-Young 定理：最佳低秩逼近

> [!abstract] 定理（Eckart-Young）
> 设 $A = U \Sigma V^\top$，$1 \leq k < r$。定义 $A_k = \sum_{i=1}^k \sigma_i u_i v_i^\top$（截断 SVD）。则
> $$\|A - A_k\|_2 \;=\; \sigma_{k+1}, \qquad \|A - A_k\|_F \;=\; \sqrt{\sigma_{k+1}^2 + \cdots + \sigma_r^2}.$$
> 且 $A_k$ 是 $A$ 在**所有秩 $\leq k$ 矩阵**中关于 2-范数与 Frobenius 范数的**最佳逼近**。

**证明概要**（2-范数情形）：

**上界**：$\|A - A_k\|_2 = \|\sum_{i>k} \sigma_i u_i v_i^\top\|_2 = \sigma_{k+1}$（最大奇异值）。

**下界**：设 $B$ 秩 $\leq k$。则 $\mathcal{N}(B) \cap \mathrm{span}\{v_1, \ldots, v_{k+1}\}$ 非平凡（维数 $\geq (n-k) + (k+1) - n = 1$）。取 $z$ 为其中单位向量。$Bz = 0$ 且 $\|Az\|_2^2 = \sum_{i \leq k+1} \sigma_i^2 (v_i^\top z)^2 \geq \sigma_{k+1}^2 \|z\|^2 = \sigma_{k+1}^2$。故 $\|A - B\|_2 \geq \|(A - B)z\|_2 / \|z\|_2 \geq \sigma_{k+1}$。$\square$

> [!important] 应用：数据压缩
> 图像 $A$（像素值矩阵）可由前 $k$ 个奇异值-向量近似，压缩比 $mn : k(m + n + 1)$。$k \ll \min(m,n)$ 时大幅压缩。

---

## Moore-Penrose 伪逆

> [!note] 伪逆
> 设 $A = U \Sigma V^\top$，定义
> $$A^+ \;=\; V \Sigma^+ U^\top,$$
> 其中 $\Sigma^+$ 把 $\Sigma$ 中非零对角元 $\sigma_i$ 取倒数 $1/\sigma_i$，零保持零，再转置。

> [!abstract] 性质（四个 Moore-Penrose 公理）
> $A^+$ 是唯一满足以下四条件的矩阵：
> 1. $A A^+ A = A$；
> 2. $A^+ A A^+ = A^+$；
> 3. $(A A^+)^\top = A A^+$；
> 4. $(A^+ A)^\top = A^+ A$.

> [!important] 与最小二乘的关系
> $x^+ = A^+ b$ 是最小二乘问题
> $$\min_x \|Ax - b\|_2$$
> 的**最小 2-范数解**：在所有 LS 解中范数最小。详见 [[最小二乘问题]]。

---

## 具体应用

### 应用一：2×2 SVD 算例

$A = \begin{pmatrix} 4 & 0 \\ 3 & -5 \end{pmatrix}$.

$A^\top A = \begin{pmatrix} 25 & -15 \\ -15 & 25 \end{pmatrix}$，特征值 $\lambda = 40, 10$ ⇒ $\sigma_1 = \sqrt{40} = 2\sqrt{10}$、$\sigma_2 = \sqrt{10}$.

$v_1$ 对应 $\lambda = 40$：$(A^\top A - 40 I) v_1 = 0$ ⇒ $v_1 = (1, -1)^\top / \sqrt{2}$。
$v_2 = (1, 1)^\top / \sqrt{2}$.

$u_1 = A v_1/\sigma_1 = \frac{1}{2\sqrt{10}} \begin{pmatrix} 4/\sqrt{2} \\ 8/\sqrt{2} \end{pmatrix} = \frac{1}{\sqrt{20}}\binom{2}{4} = (1, 2)^\top/\sqrt{5}$.
$u_2 = A v_2/\sigma_2 = \frac{1}{\sqrt{10}} \binom{4/\sqrt{2}}{-2/\sqrt{2}} = (2, -1)^\top/\sqrt{5}$.

$$A \;=\; \frac{1}{\sqrt{5}}\begin{pmatrix} 1 & 2 \\ 2 & -1 \end{pmatrix} \begin{pmatrix} 2\sqrt{10} & 0 \\ 0 & \sqrt{10} \end{pmatrix} \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ -1 & 1 \end{pmatrix}.$$

### 应用二：与 Schur 分解、谱分解的关系

对称半正定 $A$（如 $A^\top A$）：SVD 与谱分解一致：
$$A \;=\; U \Sigma U^\top \quad\text{（一般实对称半正定）}.$$

[[Schur分解定理|Schur 分解]] 对一般复方阵给出 $A = Q T Q^*$（$T$ 上三角），SVD 对一般实矩阵给出 $U \Sigma V^\top$——二者**不同分解但密切相关**。详见 [[矩阵分解综合题解]]。

### 应用三：主成分分析 (PCA)

数据矩阵 $X \in \mathbb{R}^{m\times n}$（$m$ 样本、$n$ 特征），中心化后 SVD $X = U \Sigma V^\top$。

- $V$ 的列：**主成分方向**（特征空间中按方差降序）；
- $\sigma_i^2 / (m-1)$：第 $i$ 主成分的方差；
- $U \Sigma$：数据在主成分坐标下的投影。

降维：保留前 $k$ 主成分，重构 $X_k = U_k \Sigma_k V_k^\top$（Eckart-Young）。

### 应用四：图像与信号去噪

低秩近似 $A_k$（前 $k$ 奇异值）通常对应"主要信号"，舍弃的小奇异值对应"噪声"。截断 SVD 是非参数去噪的经典方法。

### 应用五：求解病态最小二乘（TSVD）

[[最小二乘问题]] 中提到的截断 SVD：
$$x_{\text{TSVD}} \;=\; \sum_{\sigma_i > \tau} \frac{u_i^\top b}{\sigma_i} v_i.$$
$\tau$ 是阈值，忽略 $\sigma_i \leq \tau$ 的项以避免噪声放大。

### 应用六：极分解 (Polar Decomposition)

$A = QP$，$Q$ 正交、$P$ 对称半正定。由 SVD：
$$A \;=\; U \Sigma V^\top \;=\; (U V^\top)(V \Sigma V^\top) \;=:\; Q P.$$
$Q = U V^\top$ 正交，$P = V \Sigma V^\top$ 对称半正定。详见 [[矩阵分解综合题解]]。

---

## 算法关键点

> [!tip] SVD 是矩阵分解的"皇冠"
> SVD 同时给出：
> - 范数（$\|A\|_2, \|A\|_F$）；
> - 秩与条件数；
> - 列/零空间正交基；
> - 伪逆；
> - 最佳低秩近似。
>
> **任何矩阵问题"理论上"都可用 SVD 解决**。代价：$O(mn \min(m,n))$ 但常数较大。

> [!important] 数值计算 SVD 的算法
> - **Golub-Reinsch 算法**（1965）：先 Householder 双对角化（$A \to B$ 双对角），再隐式 QR 迭代化为对角。$O(mn^2 + n^3)$；
> - **Jacobi SVD**：精度极高但慢；
> - **分治法（D&C）**：现代大规模情形，LAPACK `dgesdd`；
> - **截断/随机 SVD**：仅需前 $k$ 奇异值时，复杂度 $O(mnk)$，机器学习中主流。

> [!warning] SVD 不是构造性证明
> 上述证明依赖于 $A^\top A$ 的谱分解（[[Schur分解定理]]）——非构造性。实际算法是迭代 QR-like 过程，详见数值教材的 Golub-Kahan 双对角化。

> [!info] 在机器学习中的中心地位
> - PCA、LSI（潜在语义索引）、推荐系统的协同过滤、深度学习中的低秩近似——全部依赖 SVD。
> - **大型 SVD 的算法挑战**：经典 $O(mn^2)$ 不可承受时，用 **随机 SVD**（Halko-Martinsson-Tropp）$O(mn \log k)$。

$\blacksquare$
