---
title: Cholesky 分解的存在性与唯一性
date: 2026-05-24
tags:
  - 数值分析
  - 矩阵分解
  - Cholesky分解
  - 对称正定
  - 线性方程组
---

# Cholesky 分解的存在性与唯一性

## 预备定义

> [!note] 对称正定矩阵 (SPD)
> 设 $A \in \mathbb{R}^{n \times n}$。称 $A$ 为**对称正定**（symmetric positive definite, SPD），若
> 1. $A^\top = A$（对称）；
> 2. 对任意非零 $x \in \mathbb{R}^n$，$x^\top A x > 0$（正定）。
>
> 等价刻画：$A$ 对称且所有特征值 $> 0$。

> [!note] Cholesky 分解
> 设 $A \in \mathbb{R}^{n \times n}$ 对称正定。称
> $$A \;=\; L L^\top$$
> 为 $A$ 的 **Cholesky 分解**，其中 $L$ 为下三角阵且对角元 $\ell_{ii} > 0$（$i = 1,\ldots,n$）。

> [!note] LDL$^\top$ 分解
> 称 $A = L D L^\top$ 为 **LDL$^\top$ 分解**，其中 $L$ 单位下三角，$D$ 对角阵。

> [!abstract] 引理 1：SPD 阵的顺序主子式全为正
> 设 $A$ 对称正定，则其所有顺序主子式 $\det(A_k) > 0$（$k = 1,\ldots,n$）。

**证明**：对 $k \in \{1,\ldots,n\}$，取 $\mathbb{R}^n$ 中向量 $x = (y^\top, 0, \ldots, 0)^\top$，$y \in \mathbb{R}^k$ 非零。则
$$x^\top A x \;=\; y^\top A_k y \;>\; 0.$$
故 $A_k$ 对称正定（对称性由 $A$ 对称继承）。

对称正定阵的特征值全为正，故 $\det(A_k) = \prod \lambda_i(A_k) > 0$。$\square$

> [!abstract] 引理 2：SPD 阵的 LU 分解中 $U$ 的对角元为正
> 设 $A$ 对称正定，则由引理 1 与 [[LU 分解的存在性与唯一性|LU 分解的存在性与唯一性]]，$A$ 有唯一 Doolittle 分解 $A = LU$，且 $U$ 的对角元 $u_{ii} > 0$。

**证明**：由 LU 定理，$\det(A_k) = \prod_{i=1}^k u_{ii}$。又 $\det(A_k) > 0$（引理 1），归纳即得 $u_{ii} > 0$：
- $u_{11} = \det(A_1) > 0$；
- 若 $u_{11},\ldots,u_{k-1,k-1} > 0$，则 $u_{kk} = \det(A_k)/\det(A_{k-1}) > 0$。$\square$

---

## 定理

设 $A \in \mathbb{R}^{n \times n}$。则以下等价：

**(i)** $A$ 对称正定；

**(ii)** $A$ 存在 Cholesky 分解 $A = LL^\top$，$L$ 下三角且对角元 $\ell_{ii} > 0$；

**(iii)** 满足 (ii) 的 $L$ 唯一。

---

## 第(i)$\Rightarrow$(ii)部分的证明（存在性）

由引理 2，$A$ 有唯一 Doolittle 分解 $A = \widetilde L \widetilde U$，$\widetilde L$ 单位下三角，$\widetilde U$ 上三角且 $\widetilde u_{ii} > 0$。

#### 第一步：抽出对角阵 $D$

记 $D = \operatorname{diag}(\widetilde u_{11},\ldots,\widetilde u_{nn})$。$D$ 可逆，分解
$$\widetilde U \;=\; D \cdot (D^{-1} \widetilde U).$$
令 $M = D^{-1} \widetilde U$。由 $\widetilde U$ 上三角、$M$ 的第 $i$ 行为 $\widetilde U$ 第 $i$ 行除以 $\widetilde u_{ii}$，故 $M$ 上三角且对角元 $m_{ii} = 1$，即 $M$ 单位上三角。

于是 $A = \widetilde L D M$，称为 $A$ 的 **LDU 分解**。

#### 第二步：利用对称性证明 $M = \widetilde L^\top$

$$A \;=\; \widetilde L D M.$$
取转置：
$$A^\top \;=\; M^\top D \widetilde L^\top.$$
由 $A = A^\top$（对称），
$$\widetilde L D M \;=\; M^\top D \widetilde L^\top. \quad \cdots (\ast)$$

> [!important] LDU 分解的唯一性
> 与 LU 分解的唯一性证明思路相同：$\widetilde L, M^\top$ 单位下三角；$D M, D \widetilde L^\top$ 均为对角元 $> 0$ 的上三角阵。由 LDU 分解的唯一性（直接搬用 LU 的"三角性双向夹击"论证），得
> $$\widetilde L \;=\; M^\top, \qquad D M \;=\; D \widetilde L^\top.$$

故 $M = \widetilde L^\top$。

#### 第三步：构造 $L$

由第二步，
$$A \;=\; \widetilde L D \widetilde L^\top.$$
由 $D$ 对角元 $\widetilde u_{ii} > 0$，可定义 $D^{1/2} = \operatorname{diag}(\sqrt{\widetilde u_{11}},\ldots,\sqrt{\widetilde u_{nn}})$。令
$$L \;=\; \widetilde L D^{1/2}.$$
$L$ 为下三角（下三角乘对角仍下三角），对角元 $\ell_{ii} = 1 \cdot \sqrt{\widetilde u_{ii}} > 0$。则
$$L L^\top \;=\; \widetilde L D^{1/2} (D^{1/2})^\top \widetilde L^\top \;=\; \widetilde L D \widetilde L^\top \;=\; A. \quad \square$$

---

## 第(ii)$\Rightarrow$(i)部分的证明

设 $A = LL^\top$，$L$ 下三角且 $\ell_{ii} > 0$。

#### 对称性

$$A^\top \;=\; (LL^\top)^\top \;=\; L L^\top \;=\; A. \quad \checkmark$$

#### 正定性

对任意非零 $x \in \mathbb{R}^n$，
$$x^\top A x \;=\; x^\top L L^\top x \;=\; (L^\top x)^\top (L^\top x) \;=\; \|L^\top x\|_2^2 \;\geq\; 0.$$

> [!info] 等号何时成立
> $\|L^\top x\|_2 = 0 \Leftrightarrow L^\top x = 0$。$L$ 下三角且对角元 $\ell_{ii} > 0$，故 $\det L = \prod \ell_{ii} > 0$，$L$ 可逆，$L^\top$ 也可逆。于是 $L^\top x = 0 \Leftrightarrow x = 0$。

故 $x \neq 0 \Rightarrow x^\top A x > 0$。$A$ 正定。$\square$

---

## 第(iii)部分的证明（唯一性）

**反证法**。设 $A = L_1 L_1^\top = L_2 L_2^\top$ 为两个 Cholesky 分解。

#### 第一步：化为下三角与上三角等式

$L_1, L_2$ 下三角且对角元 $> 0$，故可逆。由 $L_1 L_1^\top = L_2 L_2^\top$ 移项：
$$L_2^{-1} L_1 \;=\; L_2^\top L_1^{-\top}. \quad \cdots (\star)$$

> [!info] 记号说明
> $L_1^{-\top}$ 表示 $(L_1^\top)^{-1} = (L_1^{-1})^\top$。

#### 第二步：三角性双向夹击

- 左边 $L_2^{-1} L_1$：两个下三角阵乘积 $\Rightarrow$ 下三角。
- 右边 $L_2^\top L_1^{-\top}$：两个上三角阵乘积 $\Rightarrow$ 上三角。

由 $(\star)$，同一矩阵既下三角又上三角，故为对角阵，记为 $\Lambda$。

#### 第三步：刻画对角阵 $\Lambda$

由 $L_2^{-1} L_1 = \Lambda$，得 $L_1 = L_2 \Lambda$。比较对角元：
$$\ell_{ii}^{(1)} \;=\; \ell_{ii}^{(2)} \cdot \lambda_{ii}, \qquad i = 1,\ldots,n.$$

另一方面，由 $\Lambda = L_2^\top L_1^{-\top}$，转置得 $\Lambda^\top = L_1^{-1} L_2$，即 $\Lambda = L_1^{-1} L_2$（对角阵转置为本身）。故 $L_2 = L_1 \Lambda$，比较对角元：
$$\ell_{ii}^{(2)} \;=\; \ell_{ii}^{(1)} \cdot \lambda_{ii}. \quad \cdots (1)$$

代回前式：$\ell_{ii}^{(1)} = \ell_{ii}^{(1)} \lambda_{ii}^2$，故 $\lambda_{ii}^2 = 1$，$\lambda_{ii} = \pm 1$。

由 $\ell_{ii}^{(1)}, \ell_{ii}^{(2)} > 0$ 及 $(1)$，$\lambda_{ii} = \ell_{ii}^{(2)}/\ell_{ii}^{(1)} > 0$，故 $\lambda_{ii} = 1$，$\Lambda = I$。

故 $L_1 = L_2$。$\square$

---

## 总结

综合三部分：

1. SPD $\Rightarrow$ Cholesky 分解存在（通过 LDU 分解构造）。 ✓
2. Cholesky 分解（对角 $> 0$）$\Rightarrow$ SPD。 ✓
3. 对角 $> 0$ 的限制下，Cholesky 分解唯一。 ✓

故 **$A$ 有唯一 Cholesky 分解 $A = LL^\top$（$L$ 下三角，对角 $> 0$）$\Leftrightarrow$ $A$ 对称正定**。$\blacksquare$

---

## Cholesky 算法

按 $A = LL^\top$ 逐元比较，对 $i \geq j$ 有
$$a_{ij} \;=\; \sum_{k=1}^{j} \ell_{ik} \ell_{jk}.$$

按列推进（$j = 1,2,\ldots,n$）：

#### 对角元
$$\ell_{jj} \;=\; \sqrt{\,a_{jj} - \sum_{k=1}^{j-1} \ell_{jk}^2\,}.$$

#### 列下方元素（$i > j$）
$$\ell_{ij} \;=\; \frac{1}{\ell_{jj}}\Bigl(a_{ij} - \sum_{k=1}^{j-1} \ell_{ik} \ell_{jk}\Bigr).$$

**运算量**：约 $\dfrac{1}{3} n^3$ 次乘加，**仅为 LU 分解 $\dfrac{2}{3} n^3$ 的一半**。

> [!important] 数值稳定性的"自检"
> 算法过程中若出现 $a_{jj} - \sum \ell_{jk}^2 \leq 0$，则原矩阵**不是正定**。这给了 Cholesky 算法一个天然的"正定性检测"功能 —— 实际数值中用它检测 SPD 比直接求特征值快得多。

---

## 具体应用

### 应用一：解 SPD 线性方程组 $Ax = b$

与 LU 分解类似的两步法：

1. **前代**：解 $Ly = b$，运算量 $O(n^2)$。
2. **回代**：解 $L^\top x = y$，运算量 $O(n^2)$。

总复杂度：分解 $\dfrac{n^3}{3} + O(n^2)$，相比 LU 减少一半。

### 应用二：具体数值例子

求 $A = \begin{pmatrix} 4 & 2 & 2 \\ 2 & 5 & 1 \\ 2 & 1 & 6 \end{pmatrix}$ 的 Cholesky 分解。

#### 验证 SPD
- $\det(A_1) = 4 > 0$
- $\det(A_2) = 4 \cdot 5 - 2 \cdot 2 = 16 > 0$
- $\det(A_3) = 4(30 - 1) - 2(12 - 2) + 2(2 - 10) = 116 - 20 - 16 = 80 > 0$

由 Sylvester 准则，$A$ 对称正定。

#### 计算 $L$
$$\ell_{11} = \sqrt{4} = 2$$
$$\ell_{21} = 2/2 = 1, \qquad \ell_{31} = 2/2 = 1$$
$$\ell_{22} = \sqrt{5 - 1^2} = 2$$
$$\ell_{32} = (1 - 1 \cdot 1)/2 = 0$$
$$\ell_{33} = \sqrt{6 - 1^2 - 0^2} = \sqrt{5}$$

故
$$L \;=\; \begin{pmatrix} 2 & 0 & 0 \\ 1 & 2 & 0 \\ 1 & 0 & \sqrt{5} \end{pmatrix}.$$

验证 $LL^\top = A$ ✓。

### 应用三：最小二乘问题的正规方程

给定超定方程组 $Ax \approx b$，$A \in \mathbb{R}^{m \times n}$，$m > n$，$\operatorname{rank}(A) = n$。最小二乘解满足**正规方程**：
$$(A^\top A)\, x \;=\; A^\top b.$$

由 $\operatorname{rank}(A) = n$，$A^\top A$ 对称正定（验证：$x^\top A^\top A x = \|Ax\|^2 > 0$，$x \neq 0$ 时 $Ax \neq 0$）。

故可用 Cholesky 分解 $A^\top A = L L^\top$，然后两步回代求 $x$。

> [!warning] 正规方程的条件数恶化
> $\kappa_2(A^\top A) = \kappa_2(A)^2$。条件数被平方放大，对病态问题会损失大量精度。**实际数值实践更推荐对 $A$ 直接做 QR 分解或 SVD**，但 Cholesky 解正规方程因复杂度低，在 $A$ 良态时仍是主流（如线性回归 $X^\top X$）。

### 应用四：有限元方法中的刚度矩阵

二阶椭圆 PDE（如 Poisson 方程 $-\Delta u = f$）的有限元离散得到线性系统
$$K \mathbf{u} \;=\; \mathbf{f},$$
其中 $K$ 称为**刚度矩阵**（stiffness matrix）。

> [!important] 刚度矩阵的 SPD 性
> 对 Lax-Milgram 框架下的对称强制双线性形式 $a(\cdot,\cdot)$，刚度矩阵
> $$K_{ij} \;=\; a(\varphi_j, \varphi_i)$$
> 自动对称正定（对称性由 $a$ 对称，正定性由 $a$ 强制性）。故有限元代数系统总能用 Cholesky 分解。

进一步，对于 1D 与 2D 的 Lagrange 元，$K$ 通常是**带状矩阵**，可设计带状 Cholesky 分解将复杂度降至 $O(n \cdot p^2)$（$p$ 为带宽），这是椭圆 PDE 求解器的核心。

### 应用五：多元正态分布的采样

设需从 $\mathcal{N}(\mu, \Sigma)$ 采样，$\Sigma$ 对称正定协方差阵。Cholesky 分解 $\Sigma = LL^\top$，取标准正态向量 $z \sim \mathcal{N}(0, I)$，则
$$x \;=\; \mu + L z \;\sim\; \mathcal{N}(\mu, \Sigma).$$
验证：$\operatorname{Cov}(Lz) = L\,I\,L^\top = LL^\top = \Sigma$。

这是 Monte Carlo 模拟、Kalman 滤波、Gaussian Process 回归中**相关高斯样本生成**的标准方法。

---

## 证明思路总结

> [!tip] 关键思想
> Cholesky 分解的证明体现了一个**"LU $\to$ LDU $\to$ Cholesky"** 的精细化过程：
>
> 1. SPD $\Rightarrow$ 顺序主子式 $> 0$（引理 1），故由 LU 定理得 $A = \widetilde L \widetilde U$；
> 2. 抽出 $\widetilde U$ 的对角得 LDU 分解 $A = \widetilde L D M$；
> 3. 由 $A$ 对称 + LDU 唯一性 $\Rightarrow M = \widetilde L^\top$，即 $A = \widetilde L D \widetilde L^\top$；
> 4. 由 $D$ 正定 $\Rightarrow$ 开平方 $D^{1/2}$ 存在，吸收入 $L = \widetilde L D^{1/2}$ 即得 Cholesky。
>
> **唯一性证明**完全平行 LU 的"三角性双向夹击"，只是这次夹击得到的是对角阵而非单位阵，再用对角元正性收尾。

> [!warning] 若不要求 $\ell_{ii} > 0$，分解不唯一
> 任何对角元符号翻转 $L \to L \cdot S$（$S$ 为对角阵，对角元 $\pm 1$）都给出 $A = L S S^\top L^\top = L L^\top$，仍是合法分解（但部分对角元为负）。**对角元 $> 0$ 的约束是唯一性的关键**。

> [!warning] 半正定矩阵的 Cholesky 退化
> 若 $A$ 仅半正定（$x^\top A x \geq 0$ 但可能 $= 0$），Cholesky 分解仍存在但 $L$ 不再唯一，且某些 $\ell_{ii} = 0$ 时除法失败。实际算法（如 LAPACK `dpstrf`）改用 **pivoted Cholesky** 应对半正定情形。
