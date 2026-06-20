---
title: Jacobi 与 Gauss-Seidel 迭代
date: 2026-06-06
tags:
  - 数值分析
  - 数值线性代数
  - 迭代法
  - Jacobi迭代
  - Gauss-Seidel迭代
  - 对角占优
---

# Jacobi 与 Gauss-Seidel 迭代

## 预备定义

> [!note] 矩阵的标准分解
> 设 $A \in \mathbb{R}^{n\times n}$。把 $A$ 分解为
> $$A \;=\; D - L - U,$$
> 其中 $D = \mathrm{diag}(a_{11}, \ldots, a_{nn})$ 为对角部分，$-L$ 为严格下三角部分（$L \geq 0$ 处使用，注意符号约定），$-U$ 为严格上三角部分。

> [!note] Jacobi 迭代
> 由 $D x = (L + U) x + b$ 移项，得
> $$x^{(k+1)} \;=\; D^{-1}(L + U) x^{(k)} + D^{-1} b.$$
> 迭代矩阵 $B_J = D^{-1}(L + U) = I - D^{-1} A$。

> [!note] Gauss-Seidel 迭代
> 由 $(D - L) x = U x + b$ 移项，得
> $$x^{(k+1)} \;=\; (D - L)^{-1} U x^{(k)} + (D - L)^{-1} b.$$
> 迭代矩阵 $B_{GS} = (D - L)^{-1} U$。

> [!info] 算法层的实现
> Jacobi（**逐分量、全用旧值**）：
> $$x_i^{(k+1)} \;=\; \frac{1}{a_{ii}}\bigl(b_i - \sum_{j \neq i} a_{ij} x_j^{(k)}\bigr).$$
> Gauss-Seidel（**逐分量、立即用新值**）：
> $$x_i^{(k+1)} \;=\; \frac{1}{a_{ii}}\bigl(b_i - \sum_{j < i} a_{ij} x_j^{(k+1)} - \sum_{j > i} a_{ij} x_j^{(k)}\bigr).$$

---

## 收敛性定理

由 [[线性迭代法收敛性的谱半径准则]]：迭代 $x^{(k+1)} = B x^{(k)} + c$ 收敛 $\Leftrightarrow$ $\rho(B) < 1$。

### Jacobi 的充分条件

> [!abstract] 定理 1（严格对角占优 ⇒ Jacobi 收敛）
> 设 $A$ **严格行对角占优**：$|a_{ii}| > \sum_{j \neq i} |a_{ij}|$（$i = 1, \ldots, n$）。则 $\|B_J\|_\infty < 1$，从而 Jacobi 收敛。

**证明**：

$$\|B_J\|_\infty \;=\; \max_i \sum_{j \neq i} \left|\frac{a_{ij}}{a_{ii}}\right| \;=\; \max_i \frac{\sum_{j \neq i} |a_{ij}|}{|a_{ii}|} \;<\; 1.$$

由[[向量范数与矩阵范数]]：$\rho(B_J) \leq \|B_J\|_\infty < 1$。$\square$

> [!info] 列对角占优亦同
> 类似可证，**严格列对角占优** ⇒ $\|B_J\|_1 < 1$ ⇒ Jacobi 收敛。

### Gauss-Seidel 的充分条件

> [!abstract] 定理 2（严格对角占优 ⇒ Gauss-Seidel 收敛）
> 设 $A$ 严格行对角占优。则 $\rho(B_{GS}) < 1$，Gauss-Seidel 收敛。

**证明**：

设 $\lambda$ 是 $B_{GS}$ 的特征值，$x \neq 0$ 满足 $B_{GS} x = \lambda x$，即 $U x = \lambda (D - L) x$。取分量 $i$：
$$\sum_{j > i} a_{ij} x_j \cdot (-1) \;=\; -\lambda \bigl(a_{ii} x_i + \sum_{j < i} a_{ij} x_j\bigr).$$

设 $|x_k| = \max_j |x_j|$ 在第 $k$ 行成立。从 $\lambda a_{kk} x_k = -\sum_{j>k} a_{kj} x_j - \lambda \sum_{j<k} a_{kj} x_j$：
$$|\lambda|\, |a_{kk}|\, |x_k| \;\leq\; \sum_{j>k} |a_{kj}|\, |x_k| + |\lambda| \sum_{j<k} |a_{kj}|\, |x_k|.$$

除 $|x_k|$ 后整理：
$$|\lambda| \;\leq\; \frac{\sum_{j>k} |a_{kj}|}{|a_{kk}| - \sum_{j<k} |a_{kj}|} \;<\; \frac{\sum_{j>k} |a_{kj}|}{|a_{kk}| - \sum_{j<k} |a_{kj}|}.$$

由严格对角占优，$|a_{kk}| > \sum_{j<k}|a_{kj}| + \sum_{j>k}|a_{kj}|$，分子 $<$ 分母，故 $|\lambda| < 1$。

任取特征值 $\Rightarrow \rho(B_{GS}) < 1$。$\square$

### 对称正定情形

> [!abstract] 定理 3（SPD ⇒ Gauss-Seidel 收敛）
> 设 $A$ 对称正定。则 $\rho(B_{GS}) < 1$，Gauss-Seidel 收敛。

证明用 Stein-Rosenberg 或直接基于 Lyapunov 方程；详细见 Varga《Matrix Iterative Analysis》。

> [!warning] Jacobi 对 SPD **不必然**收敛
> $A = \begin{pmatrix} 1 & 2 \\ 2 & 5 \end{pmatrix}$ 对称正定，但 $B_J = \begin{pmatrix} 0 & -2 \\ -2/5 & 0 \end{pmatrix}$，$\rho(B_J) = \sqrt{4/5} \approx 0.89 < 1$ 此例巧合收敛；但**一般 SPD 不保证**。

---

## Jacobi vs Gauss-Seidel 的比较

> [!abstract] 命题（对一致对角占优 / 三对角 SPD 情形）
> Stein-Rosenberg 定理：对 $A$ 满足 $B_J \geq 0$（如 M 矩阵），$\rho(B_J)$ 与 $\rho(B_{GS})$ 同时小于 1 或同时大于等于 1；且当两者均 $< 1$ 时
> $$\rho(B_{GS}) \;=\; \rho(B_J)^2.$$
> 即 **Gauss-Seidel 收敛速度是 Jacobi 的平方**。

> [!important] 加速因子
> 若 $\rho(B_J) = 0.9$，则 $\rho(B_{GS}) = 0.81$。每步 Gauss-Seidel 等效 2 步 Jacobi——**通常意义上 Gauss-Seidel 是 Jacobi 的 2 倍速**。

> [!warning] 例外：失败情形
> 存在矩阵 Jacobi 收敛但 Gauss-Seidel 不收敛，反之亦然。Stein-Rosenberg 仅对 $B_J \geq 0$（如 M 矩阵）保证。

---

## 实现细节

### Jacobi 的并行性

$x_i^{(k+1)}$ 只依赖 $x^{(k)}$ 的旧值——**每个 $i$ 完全独立**，可完美并行（GPU 友好）。

### Gauss-Seidel 的串行性

$x_i^{(k+1)}$ 依赖 $x_1^{(k+1)}, \ldots, x_{i-1}^{(k+1)}$——**强串行**，难并行。

**Red-Black GS**：把节点 $\{1, \ldots, n\}$ 染色（如棋盘的红黑）。同色节点之间无依赖（$A$ 是 2-邻接矩阵时），可同色并行更新。重要的多重网格预条件构件。

### 内存

两者均 $O(n)$ 额外内存（仅需 $x^{(k)}$ 与 $x^{(k+1)}$ 双缓冲；Gauss-Seidel 可原地）。

---

## 具体应用

### 应用一：3×3 数值算例

$A = \begin{pmatrix} 4 & 1 & 1 \\ 1 & 5 & 1 \\ 1 & 1 & 6 \end{pmatrix}$，$b = (6, 7, 8)^\top$。真解 $x = (1, 1, 1)^\top$。

#### Jacobi

$x^{(0)} = 0$。
$x_1^{(1)} = 6/4 = 1.5$，$x_2^{(1)} = 7/5 = 1.4$，$x_3^{(1)} = 8/6 \approx 1.333$.

$x_1^{(2)} = (6 - 1.4 - 1.333)/4 \approx 0.817$；$x_2^{(2)} = (7 - 1.5 - 1.333)/5 \approx 0.833$；$x_3^{(2)} = (8 - 1.5 - 1.4)/6 \approx 0.85$.

误差从 $\|x - x^{(1)}\|_\infty \approx 0.5$ 降到 $\approx 0.2$。$\rho(B_J) = ?$（可数值算约 $0.45$）。

#### Gauss-Seidel

$x_1^{(1)} = 6/4 = 1.5$；$x_2^{(1)} = (7 - 1.5)/5 = 1.1$；$x_3^{(1)} = (8 - 1.5 - 1.1)/6 \approx 0.9$.

$x_1^{(2)} = (6 - 1.1 - 0.9)/4 = 1.0$；$x_2^{(2)} = (7 - 1.0 - 0.9)/5 = 1.02$；$x_3^{(2)} = (8 - 1.0 - 1.02)/6 \approx 0.997$.

**仅 2 步**已收敛到 3 位精度。Gauss-Seidel 比 Jacobi 显著快。

### 应用二：Poisson 方程的离散化

[[带状矩阵与 Thomas 算法|1D Poisson]] 有限差分 $-u'' = f$：
$$A \;=\; \frac{1}{h^2} \begin{pmatrix} 2 & -1 & \\ -1 & 2 & -1 \\ & \ddots & \ddots & \ddots \\ & & -1 & 2 \end{pmatrix}.$$

$\rho(B_J) = \cos(\pi h)$，$\rho(B_{GS}) = \cos^2(\pi h)$。$n = 100$（$h = 1/101$）：$\rho(B_J) \approx 0.9995$、$\rho(B_{GS}) \approx 0.999$。**极慢**——需 $\sim n^2$ 步达到 $h^2$ 精度。

> [!important] 大规模 PDE 应优先选 [[共轭梯度法 CG]] 或多重网格
> Jacobi/GS 对 Poisson 实际不实用，但作为多重网格的"平滑器"必不可少（高频误差衰减快）。

### 应用三：作为预条件子

Jacobi 预条件 $M = D$，Gauss-Seidel 预条件 $M = D - L$。用于 [[共轭梯度法 CG]]、[[Krylov 子空间与 GMRES]] 加速：
$$M^{-1} A x \;=\; M^{-1} b.$$

实用中：**Jacobi PCG**（对角预条件 + CG）是最简单有效的稀疏迭代法启动器。

### 应用四：与 SOR 的关系

[[SOR 方法]] 是 Gauss-Seidel 的加权改进：
$$x_i^{(k+1)} \;=\; (1 - \omega) x_i^{(k)} + \omega \cdot \text{(GS 公式)}.$$

$\omega = 1$ 即 GS。选最优 $\omega^* \in (1, 2)$ 可显著加速。

---

## 算法关键点

> [!tip] 两种迭代的哲学差异
> - **Jacobi**：保守、对称、并行——但慢；
> - **Gauss-Seidel**：贪婪、串行、单步用新信息——快但难并行。
>
> 现代大规模计算（GPU、分布式）反而青睐 Jacobi 与 Red-Black GS。

> [!important] 何时选哪种？
> | 情形 | 推荐 |
> |---|---|
> | 串行 CPU、对角占优中等问题 | Gauss-Seidel |
> | GPU/并行、大规模问题 | Jacobi |
> | 配合多重网格 | Jacobi（平滑性好） |
> | 极病态/收敛太慢 | 转 [[共轭梯度法 CG]]、[[SOR 方法]] |

> [!warning] 收敛性不保证求解效率
> 即使 $\rho(B) < 1$ 但接近 1，迭代步数巨大。**保证收敛 ≠ 实际可用**。这是 Krylov 子空间方法（CG/GMRES）兴起的原因——见 [[共轭梯度法 CG]]、[[Krylov 子空间与 GMRES]]。

$\blacksquare$
