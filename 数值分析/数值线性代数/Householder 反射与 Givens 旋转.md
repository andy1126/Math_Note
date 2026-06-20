---
title: Householder 反射与 Givens 旋转
date: 2026-06-06
tags:
  - 数值分析
  - 数值线性代数
  - Householder反射
  - Givens旋转
  - QR分解
  - 正交矩阵
---

# Householder 反射与 Givens 旋转

## 预备定义

> [!note] Householder 反射器
> 给定单位向量 $v \in \mathbb{R}^n$（$\|v\|_2 = 1$），称
> $$H \;=\; I - 2 v v^\top$$
> 为关于 $v^\perp$（$v$ 的正交补超平面）的 **Householder 反射器**。

> [!note] Givens 旋转
> 给定 $(c, s) \in \mathbb{R}^2$ 满足 $c^2 + s^2 = 1$，在指标 $(i, j)$ 上的 **Givens 旋转**为
> $$G(i,j;c,s) \;=\; I + (c-1)(e_i e_i^\top + e_j e_j^\top) + s(e_i e_j^\top - e_j e_i^\top),$$
> 即在 $(i,j)$-平面上旋转角度 $\theta$（$c = \cos\theta$、$s = \sin\theta$），其余坐标不变。

---

## Householder 反射器的性质

> [!abstract] 性质 1
> $H = I - 2 v v^\top$ 满足：
> 1. **对称**：$H^\top = H$；
> 2. **正交**：$H^2 = I$，故 $H^{-1} = H$；
> 3. **$H v = -v$**、$H w = w$ 对一切 $w \perp v$。

**证明**：(1) 直接。(2) $H^2 = I - 4 v v^\top + 4 v (v^\top v) v^\top = I$（$v^\top v = 1$）。(3) $H v = v - 2 v (v^\top v) = -v$；$H w = w - 2 v(v^\top w) = w$。$\square$

> [!important] 几何意义
> $H$ 是关于超平面 $v^\perp$ 的**镜面反射**：$v$ 方向翻转，垂直分量不变。

---

## 构造 Householder 反射器：把向量映到坐标轴

> [!abstract] 定理（核心构造）
> 给定非零 $x \in \mathbb{R}^n$。存在 Householder 反射器 $H$ 使
> $$H x \;=\; \pm \|x\|_2\, e_1.$$
> 具体：取
> $$v \;=\; \frac{x \mp \|x\|_2\, e_1}{\|x \mp \|x\|_2\, e_1\|_2},$$
> 选择"$\mp$"中减号符号与 $x_1$ 反号（即 $\mp = -\mathrm{sgn}(x_1)$）以避免灾难性消去。

**证明**：

设 $\alpha = \mp \|x\|_2$，$u = x - \alpha e_1$（未归一化）。验证 $H = I - 2 u u^\top / \|u\|^2$ 满足 $Hx = \alpha e_1$。

$$H x \;=\; x - 2 \frac{u u^\top}{u^\top u} x \;=\; x - 2 \frac{(u^\top x)}{\|u\|^2} u.$$

计算 $u^\top x = (x - \alpha e_1)^\top x = \|x\|^2 - \alpha x_1$。

$u^\top u = \|x\|^2 - 2\alpha x_1 + \alpha^2 = 2\|x\|^2 - 2\alpha x_1 = 2(u^\top x)$.

故 $2 (u^\top x)/\|u\|^2 = 1$，
$$H x \;=\; x - u \;=\; x - (x - \alpha e_1) \;=\; \alpha e_1. \qquad \square$$

> [!warning] 符号选择避免消去
> 若 $\mp = +$ 且 $x_1 > 0$，则 $x - \|x\|_2 e_1$ 第一分量为 $x_1 - \|x\|_2$ 可能极小（灾难性消去）。约定**符号与 $x_1$ 反号**：$\alpha = -\mathrm{sgn}(x_1) \|x\|_2$，$u_1 = x_1 + \mathrm{sgn}(x_1)\|x\|_2$（同号相加，不消去）。

---

## Householder QR 算法

设 $A \in \mathbb{R}^{m\times n}$，$m \geq n$。逐列消去对角下方元素：

### 算法

对 $k = 1, 2, \ldots, n$（或 $\min(m-1, n)$）：

1. 取 $A^{(k-1)}$ 第 $k$ 列从第 $k$ 行起的子向量 $x = (a_{kk}, a_{k+1,k}, \ldots, a_{mk})^\top$；
2. 构造 Householder $H_k$（作用于 $m - k + 1$ 维子空间，扩展为 $m \times m$ 全矩阵 $\widehat H_k$）使 $H_k x = -\mathrm{sgn}(x_1) \|x\|_2 e_1$；
3. 更新 $A^{(k)} = \widehat H_k A^{(k-1)}$，把 $A$ 的第 $k$ 列对角下方清零。

$n$ 步后 $\widehat H_n \cdots \widehat H_1 A = R$（上三角），故
$$A \;=\; Q R, \qquad Q = \widehat H_1 \cdots \widehat H_n.$$

### 运算量

每步消去 $m - k + 1$ 维向量，更新右侧 $n - k$ 列。总开销 $\approx 2mn^2 - \frac{2}{3}n^3$ 浮点运算。**约为 LU 的 2 倍** —— 稳定性换计算量。

### 实现细节

- $Q$ 不显式构造，仅存储反射向量 $v_k$（**Householder 表示**）。
- $A$ 矩阵原地改写：上三角部分存 $R$，下三角部分存 $v_k$ 的非零分量（紧凑表示）。
- LAPACK `dgeqrf` 的精确实现。

---

## Givens 旋转的算法

Givens 旋转用于**精确清零单个元素**，特别适合稀疏与带状矩阵。

### 选 $(c, s)$ 把 $b$ 清零

给定 $(a, b)$，构造旋转使 $\begin{pmatrix} c & s \\ -s & c \end{pmatrix} \begin{pmatrix} a \\ b \end{pmatrix} = \begin{pmatrix} r \\ 0 \end{pmatrix}$。

$r = \sqrt{a^2 + b^2}$，$c = a/r$，$s = b/r$。

> [!info] 稳定计算 $r$
> 直接 $r = \sqrt{a^2 + b^2}$ 在 $a$ 或 $b$ 极大时溢出。稳定版（LAPACK `drotg`）：先把 $\max$ 提出来 $r = |a|\sqrt{1 + (b/a)^2}$。

### Givens QR

对方阵 $A$ 逐元清零：从下到上、从左到右扫描对角下方元素，每个用一次 Givens 清零。

总运算量 $\approx 3 m n^2$（比 Householder 多 50%），但**适合带状矩阵**：对带宽 $p$ 的 $A$，Givens QR 仅 $O(n p^2)$，远优于 Householder 的 $O(n^2 p)$。

---

## Householder vs Givens：选择指南

| 方面 | Householder | Givens |
|---|---|---|
| 一次操作清零 | 整列 | 单个元素 |
| 稠密矩阵 QR | 推荐（更快） | 慢 50% |
| 稀疏 / 带状 | 破坏结构 | 保结构 |
| 并行性 | 一列内串行 | 多元素可并行 |
| 应用 | LAPACK `dgeqrf` | Hessenberg QR、Krylov 子空间 |

---

## 具体应用

### 应用一：Householder 把 $(3, 4, 0)^\top$ 映到 $\|x\| e_1$

$x = (3, 4, 0)^\top$，$\|x\| = 5$，符号 $\mathrm{sgn}(x_1) = +$，故 $\alpha = -5$。

$u = x - \alpha e_1 = (3 + 5, 4, 0)^\top = (8, 4, 0)^\top$，$\|u\|^2 = 80$。

$$H \;=\; I - \frac{2}{80} u u^\top \;=\; I - \frac{1}{40} \begin{pmatrix} 64 & 32 & 0 \\ 32 & 16 & 0 \\ 0 & 0 & 0 \end{pmatrix} \;=\; \begin{pmatrix} -3/5 & -4/5 & 0 \\ -4/5 & 3/5 & 0 \\ 0 & 0 & 1 \end{pmatrix}.$$

验证：$Hx = (-3/5 \cdot 3 - 4/5 \cdot 4, -4/5 \cdot 3 + 3/5 \cdot 4, 0)^\top = (-9/5 - 16/5, -12/5 + 12/5, 0)^\top = (-5, 0, 0)^\top = -5 e_1 = \alpha e_1$ ✓。

### 应用二：Givens 旋转的算例

$\begin{pmatrix} 3 \\ 4 \end{pmatrix}$ 清零 $4$：$r = 5$，$c = 3/5$，$s = 4/5$。

$\begin{pmatrix} 3/5 & 4/5 \\ -4/5 & 3/5 \end{pmatrix} \begin{pmatrix} 3 \\ 4 \end{pmatrix} = \begin{pmatrix} 5 \\ 0 \end{pmatrix}$ ✓。

### 应用三：稳定的最小二乘求解

Householder QR 求解 $\min \|Ax - b\|_2$ 是 LAPACK `dgels` 的核心。比 Gram-Schmidt + 正规方程稳定一阶（$\kappa$ 而非 $\kappa^2$）。详见 [[最小二乘问题]]。

### 应用四：Hessenberg 化（QR 算法预处理）

将稠密 $A$ 化为上 Hessenberg 形（仅第一次对角下方有非零）以加速 [[QR 算法]]：

- 用 $n - 2$ 次 Householder 反射，复杂度 $O(n^3)$；
- 化后每步 QR 仅 $O(n^2)$（用 Givens 在 Hessenberg 形上 QR）；
- 此预处理使 QR 算法总开销从 $O(n^4)$ 降到 $O(n^3)$。

### 应用五：旋转 Givens 在 Krylov 方法中清零

[[Krylov 子空间与 GMRES]] 用 Givens 把上 Hessenberg 矩阵 $H_k$ 逐步化为上三角，**每步增量 $O(k)$，无需重新分解**。这是 GMRES 在线更新的核心。

---

## 算法关键点

> [!tip] 两种基本正交变换的几何
> - **Householder**：一次反射，"翻转一半空间"——适合一击清零整列；
> - **Givens**：一次旋转，"二维角度调整"——适合精确清零单元素。
>
> 二者构成正交矩阵分解算法的"两块基石"。

> [!important] 为何 Householder QR 是稳定性金标准？
> 每步 $H_k$ 是**精确正交矩阵**（浮点下也是 $\|H_k^\top H_k - I\| = O(\varepsilon)$）。$n$ 步连乘后 $\|Q^\top Q - I\| = O(n \varepsilon)$，严格机器精度。Gram-Schmidt 累积失正交可达 $O(\kappa^2 \varepsilon)$——病态时显著差距。详见 [[浮点运算与后向稳定性]]。

> [!warning] 显式构造 $Q$ 浪费内存
> Householder QR 不需要显式 $Q$：用 $v_1, \ldots, v_n$ 隐式表示，需要 $Q x$ 时按序作用反射器，仅 $O(mn)$。LAPACK 的 `dormqr` 函数即为此。**显式形成 $Q$ 仅在必要时**（如 $Q$ 本身是输出）。

> [!info] 历史与命名
> - **Householder**：Alston Householder，1958 年提出反射器 QR；
> - **Givens**：Wallace Givens，1958 年提出旋转 QR（与 Householder 同年）；
> - **Gram-Schmidt**：Jørgen Pedersen Gram（1883）& Erhard Schmidt（1907）——历史最早，但数值稳定性最差。

$\blacksquare$
