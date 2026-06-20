---
title: Gram-Schmidt 与 QR 分解
date: 2026-06-06
tags:
  - 数值分析
  - 数值线性代数
  - QR分解
  - Gram-Schmidt
  - 正交化
---

# Gram-Schmidt 与 QR 分解

## 预备定义

> [!note] 正交矩阵
> $Q \in \mathbb{R}^{n\times n}$ 称为**正交矩阵**，若 $Q^\top Q = I$（等价于 $Q Q^\top = I$、$Q^{-1} = Q^\top$）。其列向量构成 $\mathbb{R}^n$ 的正交标准基（orthonormal basis）。

> [!note] 半正交矩阵
> $Q \in \mathbb{R}^{m\times n}$（$m \geq n$）称为**半正交**或**列正交**，若 $Q^\top Q = I_n$。其 $n$ 个列向量是 $\mathbb{R}^m$ 中的正交标准组（不构成基）。

> [!note] QR 分解
> 设 $A \in \mathbb{R}^{m \times n}$，$m \geq n$。称分解
> $$A = QR$$
> 为 $A$ 的 **(经济型) QR 分解**，若 $Q \in \mathbb{R}^{m\times n}$ 半正交，$R \in \mathbb{R}^{n\times n}$ 上三角。
>
> 若 $Q \in \mathbb{R}^{m\times m}$ 完全正交、$R \in \mathbb{R}^{m\times n}$ 上三角（下方填零），称**完全 QR 分解**。

> [!abstract] 引理 1：正交矩阵保 2-范数与内积
> 正交矩阵 $Q$ 满足 $\|Qx\|_2 = \|x\|_2$、$\langle Qx, Qy \rangle = \langle x, y \rangle$。

**证明**：$\|Qx\|_2^2 = x^\top Q^\top Q x = x^\top x = \|x\|_2^2$。$\square$

> [!important] 数值意义
> 正交矩阵的 $\kappa_2 = 1$，是所有正交化算法稳定的根本——见 [[向量范数与矩阵范数]]、[[矩阵条件数与扰动分析]]。

---

## 主定理：QR 分解的存在性与唯一性

> [!abstract] 定理
> 设 $A \in \mathbb{R}^{m \times n}$，$m \geq n$，$\operatorname{rank}(A) = n$（满列秩）。则：
>
> **(i) 存在性**：$A$ 存在经济型 QR 分解 $A = QR$，$Q$ 半正交，$R$ 上三角且对角元 $r_{ii} > 0$。
>
> **(ii) 唯一性**：在 $r_{ii} > 0$ 约束下，QR 分解唯一。

---

## 证明 (i)：构造性证明（Gram-Schmidt 正交化）

设 $A = [a_1 \mid a_2 \mid \cdots \mid a_n]$，$\{a_j\}$ 线性无关。

### 经典 Gram-Schmidt 算法 (CGS)

对 $j = 1, 2, \ldots, n$：

1. **正交化**：
$$v_j \;=\; a_j - \sum_{i=1}^{j-1} \langle a_j, q_i \rangle\, q_i;$$

2. **归一化**：
$$r_{jj} \;=\; \|v_j\|_2, \qquad q_j \;=\; v_j / r_{jj};$$

3. **记录系数**：
$$r_{ij} \;=\; \langle a_j, q_i \rangle, \quad i < j; \qquad r_{ii} = \|v_i\|_2.$$

### 验证 $A = QR$

由步骤 1-2，$a_j = r_{jj} q_j + \sum_{i<j} r_{ij} q_i = \sum_{i \leq j} r_{ij} q_i$。即 $A$ 的第 $j$ 列等于 $Q$ 的前 $j$ 列与 $R$ 的第 $j$ 列上半截的线性组合。

矩阵形式 $A = QR$，$Q = [q_1 \mid \cdots \mid q_n]$ 半正交，$R$ 上三角且 $r_{jj} = \|v_j\|_2 > 0$（由满秩 ⇒ $v_j \neq 0$）。$\square$

> [!info] 关键观察
> 满秩条件保证 $v_j \neq 0$（否则 $a_j \in \mathrm{span}\{a_1,\ldots,a_{j-1}\}$，与无关矛盾）。故 $r_{jj} > 0$。

---

## 证明 (ii)：唯一性

**反证法**。设 $A = Q_1 R_1 = Q_2 R_2$ 为两个经济型 QR 分解（$r_{ii}^{(k)} > 0$）。

#### 第一步：$R_k$ 可逆

满秩 $\Rightarrow R_k$ 满秩 $\Rightarrow R_k$ 可逆。

#### 第二步：推出正交关系

由 $Q_1 R_1 = Q_2 R_2 \Rightarrow Q_1 = Q_2 R_2 R_1^{-1}$。记 $T = R_2 R_1^{-1}$ 上三角。

$Q_1$ 半正交：$Q_1^\top Q_1 = I$。代入：
$$I \;=\; Q_1^\top Q_1 \;=\; T^\top Q_2^\top Q_2 T \;=\; T^\top T.$$

即 $T^\top T = I$。

#### 第三步：上三角且 $T^\top T = I$ 推出 $T$ 为对角阵

$T$ 上三角 ⇒ $T^\top$ 下三角。$T^\top T = I$ 写成：第 $i$ 行 = 第 $i$ 列对角下方元 + 对角元。

具体：$(T^\top T)_{ij} = \sum_k t_{ki} t_{kj}$。$T$ 上三角 $\Rightarrow t_{ki} \neq 0$ 仅当 $k \leq i$；$t_{kj} \neq 0$ 仅当 $k \leq j$。

当 $i < j$：$(T^\top T)_{ij} = \sum_{k \leq i} t_{ki} t_{kj}$，需 $= 0$。$i = 1$ 时给出 $t_{11} t_{1j} = 0 \Rightarrow t_{1j} = 0$（$j > 1$，$t_{11} > 0$）。

归纳：$t_{ij} = 0$（$i < j$）。结合 $T$ 上三角即 $T$ 为对角阵。

#### 第四步：对角元正性 ⇒ $T = I$

$T^\top T = I$ + $T = \operatorname{diag}(t_1, \ldots, t_n)$ + $t_i^2 = 1 \Rightarrow t_i = \pm 1$。

由 $R_2 = T R_1$ 比较对角：$r_{ii}^{(2)} = t_i r_{ii}^{(1)} > 0$。$r_{ii}^{(1)} > 0$ ⇒ $t_i = 1$。

故 $T = I \Rightarrow R_1 = R_2$、$Q_1 = Q_2$。$\square$

---

## 修正 Gram-Schmidt (MGS)：稳定性改进

经典 GS 的稳定性问题：浮点下 $q_j$ 可能严重失正交。**修正 GS** 仅小改算法但稳定性显著提升。

### MGS 算法

初始化 $v_j = a_j$（$j = 1, \ldots, n$）。对 $j = 1, \ldots, n$：

1. $r_{jj} = \|v_j\|_2$，$q_j = v_j/r_{jj}$；
2. 对 $k = j+1, \ldots, n$（**立即正交化所有后续列**）：
   $$r_{jk} = \langle q_j, v_k \rangle, \quad v_k \leftarrow v_k - r_{jk} q_j.$$

### CGS vs MGS 的区别

- **CGS**：对当前列 $a_j$ 同时减去前面 $j-1$ 个投影；
- **MGS**：每得到一个 $q_i$ 立刻"清扫"所有后续列。

二者**数学上等价**，但 MGS 浮点下 $\|Q^\top Q - I\| = O(\kappa(A) \varepsilon)$，CGS 为 $O(\kappa(A)^2 \varepsilon)$。**MGS 几乎免费换取一阶稳定性提升**。

> [!warning] MGS 仍非最优稳定
> 即使 MGS，对极病态 $A$（$\kappa \sim 10^8$）仍可能失正交。更稳定的方案是 [[Householder 反射与 Givens 旋转]]——Householder QR 给出严格正交的 $Q$。

---

## 具体应用

### 应用一：3×3 数值算例

$A = \begin{pmatrix} 1 & 1 & 0 \\ 1 & 0 & 1 \\ 0 & 1 & 1 \end{pmatrix}$。用 CGS 算 QR。

#### 第 1 列

$v_1 = a_1 = (1, 1, 0)^\top$，$r_{11} = \sqrt{2}$，$q_1 = (1/\sqrt{2}, 1/\sqrt{2}, 0)^\top$。

#### 第 2 列

$r_{12} = \langle a_2, q_1 \rangle = 1/\sqrt{2}$；$v_2 = a_2 - r_{12} q_1 = (1/2, -1/2, 1)^\top$；$r_{22} = \sqrt{1/4 + 1/4 + 1} = \sqrt{3/2}$；$q_2 = (1, -1, 2)^\top / \sqrt{6}$.

#### 第 3 列

$r_{13} = \langle a_3, q_1 \rangle = 1/\sqrt{2}$；$r_{23} = \langle a_3, q_2 \rangle = (0 - 1 + 2)/\sqrt{6} = 1/\sqrt{6}$；$v_3 = a_3 - r_{13} q_1 - r_{23} q_2$.

计算：$a_3 - (1/\sqrt{2}) q_1 = (0,0,1) - (1/2, 1/2, 0) = (-1/2, -1/2, 1)$；再减 $(1/\sqrt{6}) q_2 = (1/6, -1/6, 2/6)$：$v_3 = (-2/3, -1/3, 2/3)$。

$r_{33} = \sqrt{4/9 + 1/9 + 4/9} = \sqrt{1} = 1$。等等，$\sqrt{9/9} = 1$。重新算：$4/9 + 1/9 + 4/9 = 9/9 = 1$，故 $r_{33} = 1$（注意此处 $v_3$ 应该再除归一化但已是单位长度——巧合）。$q_3 = (-2/3, -1/3, 2/3)^\top$。

### 应用二：最小二乘问题的 QR 法

求 $\min_x \|Ax - b\|_2$（$A \in \mathbb{R}^{m\times n}$ 满秩）。

QR 分解 $A = QR$（经济型）。则
$$\|Ax - b\|_2^2 \;=\; \|QR x - b\|_2^2.$$
扩展为完全 QR $A = \begin{pmatrix} Q & Q_\perp \end{pmatrix} \begin{pmatrix} R \\ 0 \end{pmatrix}$，由 $Q$ 完全正交保 2-范数：
$$\|Ax - b\|_2^2 \;=\; \left\|\begin{pmatrix} R \\ 0 \end{pmatrix} x - \begin{pmatrix} Q^\top b \\ Q_\perp^\top b \end{pmatrix}\right\|_2^2 \;=\; \|Rx - Q^\top b\|_2^2 + \|Q_\perp^\top b\|_2^2.$$

最优解：$Rx = Q^\top b$，残差 $\|Q_\perp^\top b\|_2$。详见 [[最小二乘问题]]。

### 应用三：与 LU 分解的对比

| 方面 | LU | QR |
|---|---|---|
| 复杂度 | $\frac{2}{3}n^3$ | $2mn^2 - \frac{2}{3}n^3$（$m \geq n$） |
| 稳定性 | 需部分主元，可能 $\rho_n$ 增长 | 严格正交，$\kappa$ 不放大 |
| 适用 | 方阵线性系统 | 长方阵、最小二乘 |
| 条件数 | $\kappa(A)$ | $\kappa(A)$（不放大） |

QR 是 LU 在长方阵情形的推广，代价大约 3 倍。

### 应用四：QR 与正交化在迭代法中的应用

- **QR 算法**（特征值）：每步 $A_k = Q_k R_k$ 然后 $A_{k+1} = R_k Q_k$，详见 [[QR 算法]]。
- **Arnoldi / Lanczos**（Krylov 子空间）：本质是 Gram-Schmidt 应用于 Krylov 向量序列——见 [[Krylov 子空间与 GMRES]]。

---

## 算法关键点

> [!tip] QR 是"正交化 = 矩阵分解"的代数化
> Gram-Schmidt 把"逐步正交化向量组"翻译成"矩阵分解 $A = QR$"。两者等价但视角不同：
> - **向量视角**：找正交基；
> - **矩阵视角**：把 $A$ 写成正交 × 上三角。

> [!important] 三种 QR 算法的稳定性谱
> | 算法 | $\|Q^\top Q - I\|$ |
> |---|---|
> | CGS | $O(\kappa^2 \varepsilon)$ |
> | MGS | $O(\kappa \varepsilon)$ |
> | Householder | $O(\varepsilon)$（机器精度级） |
>
> LAPACK `dgeqrf` 用 Householder——见 [[Householder 反射与 Givens 旋转]]。

> [!warning] 经济型 vs 完全型
> 经济型 $Q \in \mathbb{R}^{m \times n}$ 仅记录 $A$ 列空间的正交基；完全型 $Q \in \mathbb{R}^{m \times m}$ 额外含**正交补** $Q_\perp$。最小二乘的残差由 $Q_\perp^\top b$ 给出，故需要完全型——但实际算法通常以隐式表示 $Q_\perp$（Householder 反射器序列），无需显式构造。

$\blacksquare$
