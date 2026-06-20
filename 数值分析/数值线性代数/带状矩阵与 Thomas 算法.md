---
title: 带状矩阵与 Thomas 算法
date: 2026-06-06
tags:
  - 数值分析
  - 数值线性代数
  - 带状矩阵
  - 三对角矩阵
  - Thomas算法
---

# 带状矩阵与 Thomas 算法

## 预备定义

> [!note] 带状矩阵（banded matrix）
> $A \in \mathbb{R}^{n\times n}$ 称为**带宽**（bandwidth） $p$ 的带状矩阵，若
> $$a_{ij} \;=\; 0 \quad \text{当 } |i - j| > p.$$
> 即非零元集中在主对角线及上下各 $p$ 条次对角线上。

> [!note] 三对角矩阵（tridiagonal matrix）
> 带宽 $p = 1$ 的特例：仅主对角与上下次对角非零，
> $$A \;=\; \begin{pmatrix} b_1 & c_1 & & & \\ a_2 & b_2 & c_2 & & \\ & a_3 & b_3 & \ddots & \\ & & \ddots & \ddots & c_{n-1} \\ & & & a_n & b_n \end{pmatrix}.$$

> [!note] 严格对角占优（strict diagonal dominance）
> $A$ 称为**严格对角占优**，若
> $$|a_{ii}| \;>\; \sum_{j \neq i} |a_{ij}|, \quad i = 1, \ldots, n.$$
> 对三对角阵即 $|b_i| > |a_i| + |c_i|$（约定 $a_1 = c_n = 0$）。

---

## 命题：LU 分解保持带状结构

> [!abstract] 命题
> 设带宽 $p$ 的矩阵 $A$ 满足 [[LU 分解的存在性与唯一性]] 条件（顺序主子式全非零）。则其 Doolittle 分解 $A = LU$ 中 $L$、$U$ 也都是带宽 $p$。

**证明**：对 $n$ 归纳。设结论对 $(n-1) \times (n-1)$ 带状矩阵成立。

按 LU 笔记的分块构造：
$$L \;=\; \begin{pmatrix} \widetilde L & 0 \\ \ell^\top & 1 \end{pmatrix}, \quad U \;=\; \begin{pmatrix} \widetilde U & u \\ 0 & u_{nn} \end{pmatrix},$$
其中 $\ell^\top = c^\top \widetilde U^{-1}$、$u = \widetilde L^{-1} b$，$b, c \in \mathbb{R}^{n-1}$ 是 $A$ 最后一列、行的子向量。

- $A$ 带宽 $p$ ⇒ $b$ 的前 $n - 1 - p$ 个分量为 0；$c$ 同理。
- $\widetilde L^{-1}$ 与 $\widetilde U^{-1}$ 在带状结构下仅"延展"到带宽 $p$（具体：归纳假设给出 $\widetilde L, \widetilde U$ 带宽 $p$，其逆带宽不必为 $p$，但**作用于稀疏向量** $b, c$ 后结果仍稀疏）。

逐项验证 $u_i = 0$（$i \leq n - 1 - p$）与 $\ell_j = 0$（$j \leq n - 1 - p$）：用 $\widetilde L u = b$、$\widetilde U^\top \ell = c$，由前向/后向代换 + $\widetilde L, \widetilde U$ 带宽 $p$ + $b, c$ 末段非零，可归纳得证。$\square$

> [!important] 储存与运算量
> 带宽 $p$ 的 LU 分解：储存 $O(np)$、运算 $O(np^2)$。**远优于稠密 $O(n^3)$**。

---

## Thomas 算法（三对角 LU + 前代回代）

对带宽 $p = 1$ 的三对角系统 $Ax = d$，结合上节命题，$L$、$U$ 均为双对角阵。可显式写出 LU 分解+求解的合并算法，复杂度 $O(n)$。

### 阶段一：前向消元

令 $c_1' = c_1/b_1$，$d_1' = d_1/b_1$，并对 $i = 2, \ldots, n$ 递推：
$$m_i \;=\; b_i - a_i c_{i-1}', \qquad c_i' \;=\; \frac{c_i}{m_i}, \qquad d_i' \;=\; \frac{d_i - a_i d_{i-1}'}{m_i}.$$

$m_i$ 即等价 $U$ 的第 $i$ 个对角元。注意末步 $c_n' $ 不需要（$U$ 最后一行只有对角）。

### 阶段二：回代

$$x_n \;=\; d_n', \qquad x_i \;=\; d_i' - c_i' x_{i+1}, \quad i = n-1, \ldots, 1.$$

### 运算量

每步常数次乘除：前向 $n$ 步 + 回代 $n$ 步 $\Rightarrow$ $O(n)$ 浮点运算。**比一般 LU 优 $n^2$ 倍**。

---

## 稳定性

> [!abstract] 定理（严格对角占优 ⇒ Thomas 稳定）
> 若 $A$ 三对角严格对角占优（$|b_i| > |a_i| + |c_i|$），则 Thomas 算法所有 $m_i \neq 0$ 且 $|c_i'| < 1$，无需主元交换。

**证明**：对 $i$ 归纳证 $|c_i'| < 1$。

**基础**：$|c_1'| = |c_1|/|b_1| < 1$（由 $|b_1| > |c_1|$）。

**归纳**：设 $|c_{i-1}'| < 1$。则
$$|m_i| \;=\; |b_i - a_i c_{i-1}'| \;\geq\; |b_i| - |a_i|\,|c_{i-1}'| \;>\; |b_i| - |a_i| \;\geq\; |c_i| \;\geq\; 0.$$
故 $m_i \neq 0$ 且 $|c_i'| = |c_i|/|m_i| < |c_i|/|c_i| = 1$（若 $c_i \neq 0$；若 $c_i = 0$ 则 $c_i' = 0$）。$\square$

> [!important] 何时严格对角占优？
> - 有限差分离散 Poisson 方程：$2 > 1 + 1$（等号边界，称为**弱对角占优**），但加边界条件后退化为严格对角占优；
> - 三次自然样条的系数矩阵：明确严格对角占优；
> - M-矩阵、椭圆 PDE 的离散——一大类应用都满足。

---

## 具体应用

### 应用一：4×4 数值算例（1D Poisson）

求解
$$A x \;=\; d, \quad A \;=\; \begin{pmatrix} 2 & -1 & 0 & 0 \\ -1 & 2 & -1 & 0 \\ 0 & -1 & 2 & -1 \\ 0 & 0 & -1 & 2 \end{pmatrix}, \quad d \;=\; \begin{pmatrix} 1 \\ 0 \\ 0 \\ 1 \end{pmatrix}.$$

#### 前向

$i = 1$: $m_1 = 2$, $c_1' = -1/2$, $d_1' = 1/2$.
$i = 2$: $m_2 = 2 - (-1)(-1/2) = 3/2$, $c_2' = -1/(3/2) = -2/3$, $d_2' = (0 - (-1)(1/2))/(3/2) = 1/3$.
$i = 3$: $m_3 = 2 - (-1)(-2/3) = 4/3$, $c_3' = -1/(4/3) = -3/4$, $d_3' = (0 - (-1)(1/3))/(4/3) = 1/4$.
$i = 4$: $m_4 = 2 - (-1)(-3/4) = 5/4$, $d_4' = (1 - (-1)(1/4))/(5/4) = 1$.

#### 回代

$x_4 = 1$；$x_3 = 1/4 - (-3/4)(1) = 1$；$x_2 = 1/3 - (-2/3)(1) = 1$；$x_1 = 1/2 - (-1/2)(1) = 1$.

解 $x = (1, 1, 1, 1)^\top$。**验证**：$Ax = (2 - 1, -1 + 2 - 1, -1 + 2 - 1, -1 + 2)^\top = (1, 0, 0, 1)^\top = d$ ✓。

### 应用二：一维 Poisson 方程的有限差分

$-u''(x) = f(x)$ 在 $[0, 1]$ 上，$u(0) = u(1) = 0$。等距剖分 $x_i = ih$，$h = 1/(n+1)$，$i = 0, 1, \ldots, n+1$。二阶中心差分：
$$\frac{-u_{i-1} + 2u_i - u_{i+1}}{h^2} \;=\; f(x_i), \quad i = 1, \ldots, n.$$

得到三对角系统
$$\frac{1}{h^2} \begin{pmatrix} 2 & -1 & & \\ -1 & 2 & \ddots & \\ & \ddots & \ddots & -1 \\ & & -1 & 2 \end{pmatrix} \begin{pmatrix} u_1 \\ \vdots \\ u_n \end{pmatrix} \;=\; \begin{pmatrix} f(x_1) \\ \vdots \\ f(x_n) \end{pmatrix}.$$

严格对角占优（$2 > 1$ 在边界行；内部行 $2 = 1 + 1$ 弱对角占优，但结合**不可约性**仍保证 Thomas 稳定，可参 Varga 经典结果）。$O(n)$ 求解，**比一般 LU 的 $O(n^3)$ 在 $n = 10^6$ 量级问题上是百万倍加速**。

### 应用三：三次样条插值的三对角系统

给定数据 $(x_i, y_i)$，$i = 0, \ldots, n$，构造三次自然样条。设二阶导 $M_i = S''(x_i)$，由连续性得三对角系统
$$h_{i-1} M_{i-1} + 2(h_{i-1} + h_i) M_i + h_i M_{i+1} \;=\; 6\left(\frac{y_{i+1} - y_i}{h_i} - \frac{y_i - y_{i-1}}{h_{i-1}}\right),$$
其中 $h_i = x_{i+1} - x_i$，$i = 1, \ldots, n-1$。

主对角 $2(h_{i-1} + h_i)$ 严格大于次对角和 $h_{i-1} + h_i$ ⇒ 严格对角占优 ⇒ Thomas 算法 $O(n)$ 求解。

与 [[Lagrange插值误差估计]] 对比：Lagrange 插值无需解方程组但易振荡（Runge 现象）；样条更稳定，代价是解一次三对角系统——Thomas 让代价微不足道。

### 应用四：二维 Poisson 与五对角系统

二维网格离散 $-\Delta u = f$ 得到五对角矩阵（带宽 $\sqrt{N}$，$N = n^2$ 是总未知数）。带状 LU 复杂度 $O(N \cdot \sqrt{N}^2) = O(N^2)$，已不再线性。

> [!info] 何时改用迭代法
> 二维及更高维 Poisson 类系统，带宽随网格规模增长，带状直接法失去优势。**改用迭代法**：[[Jacobi 与 Gauss-Seidel 迭代]]、[[共轭梯度法 CG]]、多重网格等。

---

## 算法关键点

> [!tip] 为何 Thomas 算法快？
> 它本质是 LU 分解专用于带宽 $1$ 的实现——LU 保持带状结构使运算从 $O(n^3)$ 降到 $O(n)$。**没有任何新数学，只有结构利用**。这是数值代数中"稀疏结构的代数代价"原则的最朴素例证。

> [!warning] 非对角占优时可能失败
> $\begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$ 不能用 Thomas（主元为零），与 [[LU 分解的存在性与唯一性]] 失败原因相同。补救：主元交换，但**破坏带状结构**——交换后非零元可能跑到带外，新算法需用 PLU 并接受 $O(np)$ → $O(n p^2)$ 退化。
>
> 实际：若已知系数矩阵严格对角占优（如 Poisson、样条），直接用 Thomas；否则用 [[PLU 分解的存在性]]。

> [!important] 工程实现
> LAPACK 的 `dgtsv`（general tridiagonal solver）即 Thomas + 部分主元；`dptsv`（positive definite tridiagonal）即 Cholesky 版本，更快。SciPy `scipy.linalg.solve_banded`、MATLAB 三对角直接用 `\`（自动识别稀疏带状）。

$\blacksquare$
