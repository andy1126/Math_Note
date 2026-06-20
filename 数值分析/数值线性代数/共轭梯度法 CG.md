---
title: 共轭梯度法 CG
date: 2026-06-06
tags:
  - 数值分析
  - 数值线性代数
  - 共轭梯度法
  - CG
  - Krylov子空间
  - SPD
---

# 共轭梯度法 CG

## 预备定义

> [!note] $A$-内积与 $A$-范数
> 设 $A \in \mathbb{R}^{n\times n}$ 对称正定。称
> $$\langle x, y \rangle_A \;=\; x^\top A y, \qquad \|x\|_A \;=\; \sqrt{x^\top A x}$$
> 为 **$A$-内积**与 **$A$-范数**。

> [!note] $A$-共轭
> 两向量 $p, q$ 称 **$A$-共轭** 或 **$A$-正交**，若 $\langle p, q \rangle_A = p^\top A q = 0$。

> [!note] Krylov 子空间
> 给定 $A$、$r_0$，称
> $$\mathcal{K}_k(A, r_0) \;=\; \mathrm{span}\{r_0, A r_0, A^2 r_0, \ldots, A^{k-1} r_0\}$$
> 为 $k$ 阶 **Krylov 子空间**。

> [!info] CG 的等价定义
> CG 解 SPD 系统 $Ax = b$，等价于以下三个视角：
> 1. **二次函数极小**：$\min_x \frac{1}{2} x^\top A x - b^\top x$；
> 2. **$A$-范数误差极小**：$\min_x \|x - x^*\|_A$ 在仿射子空间 $x_0 + \mathcal{K}_k$ 上；
> 3. **正交残差**：在 $\mathcal{K}_k$ 中找 $x_k$ 使 $r_k = b - A x_k \perp \mathcal{K}_k$.

---

## 主算法：CG 的递推公式

### 算法

输入：$A$ SPD、$b$、初值 $x_0$。

1. $r_0 = b - A x_0$；$p_0 = r_0$.
2. 对 $k = 0, 1, 2, \ldots$：
   $$\alpha_k = \frac{r_k^\top r_k}{p_k^\top A p_k};$$
   $$x_{k+1} = x_k + \alpha_k p_k;$$
   $$r_{k+1} = r_k - \alpha_k A p_k;$$
   $$\beta_k = \frac{r_{k+1}^\top r_{k+1}}{r_k^\top r_k};$$
   $$p_{k+1} = r_{k+1} + \beta_k p_k.$$
3. 若 $\|r_{k+1}\| < \varepsilon \|b\|$：停止。

### 复杂度

每步：1 次矩阵向量积 $A p_k$（$O(n^2)$ 稠密、$O(\text{nnz}(A))$ 稀疏）+ 几次 $O(n)$ 向量运算。**主要开销在矩阵向量积**，故 CG 对稀疏 $A$ 极高效。

### 内存

仅需 $x_k, r_k, p_k, A p_k$ 四个向量——$O(n)$。**这是 CG 相对 GMRES 的核心优势**。

---

## 主定理 1：正交性与共轭性

> [!abstract] 定理（CG 的不变量）
> 算法生成的残差与方向向量满足：
> 1. **残差正交**：$r_i^\top r_j = 0$（$i \neq j$）；
> 2. **方向 $A$-共轭**：$p_i^\top A p_j = 0$（$i \neq j$）；
> 3. **子空间扩张**：$\mathrm{span}\{r_0, \ldots, r_k\} = \mathrm{span}\{p_0, \ldots, p_k\} = \mathcal{K}_{k+1}(A, r_0)$.

### 证明（数学归纳法）

**基础** $k = 0$：trivial。

**归纳**：设结论对 $j \leq k$ 成立。

#### 残差正交：$r_{k+1}^\top r_j = 0$（$j \leq k$）

由更新 $r_{k+1} = r_k - \alpha_k A p_k$：
$$r_{k+1}^\top r_j \;=\; r_k^\top r_j - \alpha_k (A p_k)^\top r_j.$$

- $j = k$：$\alpha_k$ 的选择恰好使 $r_{k+1}^\top r_k = r_k^\top r_k - \alpha_k p_k^\top A r_k$，用 $r_k = p_k - \beta_{k-1} p_{k-1}$ 与 $p_{k-1}^\top A p_k = 0$（归纳）得 $p_k^\top A r_k = p_k^\top A p_k$。代入 $\alpha_k$ 定义即 $= 0$。
- $j < k$：$r_k^\top r_j = 0$（归纳），$(A p_k)^\top r_j = p_k^\top A r_j$。由 $A r_j = (r_j - r_{j+1})/\alpha_j$ 且 $\alpha_j p_j^\top A r_j = p_j^\top (r_j - r_{j+1})$，结合 $r_{j+1}^\top p_j = 0$（前一步证明）可推 $p_k^\top A r_j = 0$。

详细演算用 $p_k = r_k + \beta_{k-1} p_{k-1}$ 展开。$\square$

#### 方向 $A$-共轭

类似归纳。关键：$\beta_k$ 的选择恰好保证 $p_{k+1}^\top A p_k = 0$，再用归纳推到所有 $j < k$。

#### 子空间扩张

显然 $r_k, p_k \in \mathcal{K}_{k+1}$（由 $A p_{k-1}$ 等出现），反之亦然。$\square$

---

## 主定理 2：有限步终止

> [!abstract] 定理（CG 至多 $n$ 步终止）
> 在精确算术下，CG 至多 $n$ 步内得到精确解 $x^*$：存在 $k \leq n$ 使 $r_k = 0$、$x_k = x^*$。

**证明**：

由残差正交性，$r_0, r_1, \ldots, r_n$ 是 $\mathbb{R}^n$ 中 $n+1$ 个两两正交向量。**$n+1$ 维空间不存在**——故至少一个 $r_k = 0$，对应 $x_k = x^*$。$\square$

> [!warning] 浮点下不必然有限步
> 实际计算中浮点误差破坏正交性，CG 可能需要 $> n$ 步。**实践把 CG 当迭代法用**（早早达到精度容差就停止）。

---

## 主定理 3：误差估计

> [!abstract] 定理（CG 收敛速率）
> 设 $\kappa = \kappa_2(A) = \lambda_{\max}/\lambda_{\min}$。CG 误差满足
> $$\frac{\|x_k - x^*\|_A}{\|x_0 - x^*\|_A} \;\leq\; 2 \left(\frac{\sqrt{\kappa} - 1}{\sqrt{\kappa} + 1}\right)^k.$$

**证明梗概**：CG 在每个 $\mathcal{K}_k$ 上极小化 $\|x - x^*\|_A$。误差 $e_k = x_k - x^* \in x_0 - x^* + \mathcal{K}_k$ 可写为 $e_k = p(A) e_0$，$p$ 是 $\leq k$ 次多项式且 $p(0) = 1$。

故
$$\|e_k\|_A^2 \;\leq\; \min_{p(0)=1,\, \deg p \leq k} \max_{\lambda \in [\lambda_{\min}, \lambda_{\max}]} p(\lambda)^2 \cdot \|e_0\|_A^2.$$

这是 Chebyshev 极小化问题。取 Chebyshev 多项式（平移到 $[\lambda_{\min}, \lambda_{\max}]$）即得估计。$\square$

> [!important] 解读
> - **良态** $\kappa = O(1)$：CG 几步达机器精度；
> - **病态** $\kappa = 10^6$：$\sqrt{\kappa} - 1)/(\sqrt{\kappa} + 1) \approx 1 - 2/\sqrt{\kappa}$；达 $\varepsilon$ 精度需 $\sim \sqrt{\kappa} \log(1/\varepsilon)$ 步。
> - **比 Gauss-Seidel** ($\kappa$ 步) 与 **SOR** ($\sqrt{\kappa}$ 步) 同阶或更优，且**无超参数**。

---

## 预条件 CG (PCG)

加速 CG 的关键：找 $M \approx A$ 使 $M^{-1} A$ 谱聚集（$\kappa(M^{-1} A) \ll \kappa(A)$），且 $M^{-1} v$ 易算。

### PCG 算法

形式上对 $M^{-1} A x = M^{-1} b$ 用 CG，但需保持 $A$ 内积。算法：

1. $r_0 = b - A x_0$；$z_0 = M^{-1} r_0$；$p_0 = z_0$.
2. 每步：
   $\alpha_k = \frac{r_k^\top z_k}{p_k^\top A p_k}$;
   $x_{k+1} = x_k + \alpha_k p_k$；$r_{k+1} = r_k - \alpha_k A p_k$；
   $z_{k+1} = M^{-1} r_{k+1}$；
   $\beta_k = \frac{r_{k+1}^\top z_{k+1}}{r_k^\top z_k}$；
   $p_{k+1} = z_{k+1} + \beta_k p_k$.

### 常见预条件子

- **Jacobi**：$M = D$。简单但效果有限；
- **SSOR**：$M = (D + L) D^{-1} (D + L^\top)$。常用；
- **不完全 Cholesky (IC)**：$A = L L^\top + R$ 中保留 $L$ 的稀疏模式。SPD 系统的标准选择；
- **代数多重网格 (AMG)**：对 PDE 离散最强效，$O(N)$ 收敛。

---

## 具体应用

### 应用一：3×3 CG 算例

$A = \begin{pmatrix} 4 & 1 & 0 \\ 1 & 3 & 1 \\ 0 & 1 & 2 \end{pmatrix}$（SPD），$b = (1, 1, 1)^\top$，$x_0 = 0$。

**步 0**：$r_0 = (1, 1, 1)^\top$、$p_0 = (1, 1, 1)^\top$.
$A p_0 = (5, 5, 3)^\top$、$p_0^\top A p_0 = 13$、$r_0^\top r_0 = 3$、$\alpha_0 = 3/13$.
$x_1 = (3/13, 3/13, 3/13)^\top$、$r_1 = r_0 - (3/13)(5, 5, 3)^\top = (-2/13, -2/13, 4/13)^\top$.

**步 1**：$r_1^\top r_1 = 24/169$、$\beta_0 = (24/169)/3 = 8/169$.
$p_1 = r_1 + \beta_0 p_0 = (-2/13 + 8/169, -2/13 + 8/169, 4/13 + 8/169)^\top$.
…（继续算）。3 步内收敛到精确解（$n = 3$）。

### 应用二：Poisson 方程的 CG

[[带状矩阵与 Thomas 算法|1D Poisson 离散]] 或 2D 离散，$\kappa = O(1/h^2)$，$\sqrt{\kappa} = O(1/h)$。CG 步数 $\sim 1/h$。

加预条件后（AMG），步数降到 $O(1)$——**总复杂度 $O(N)$ 解 Poisson**。

### 应用三：与最小二乘的联系

求解最小二乘 $\min \|Ax - b\|_2$（$A$ 任意）等价于正规方程 $A^\top A x = A^\top b$。$A^\top A$ SPD，可用 CG，称 **CGLS** 或 **CGNR**。

但 $\kappa(A^\top A) = \kappa(A)^2$ → 收敛慢。改用 **LSQR**（基于 Lanczos 双对角化），更稳定。

详见 [[最小二乘问题]]、[[Krylov 子空间与 GMRES]]。

### 应用四：科学计算的主力

CG（带各种预条件）是椭圆 PDE 求解器的工业标准：
- 结构力学有限元；
- 电磁学（Maxwell 方程稳态）；
- 量子化学的 Hartree-Fock 自洽场迭代。

LAPACK 不含 CG（CG 用于稀疏问题），用 PETSc、Trilinos、SciPy `cg` 等。

---

## 算法关键点

> [!tip] CG 的"奇迹"
> 每步只需一次矩阵向量积 + 几次向量运算，却能在 $O(\sqrt{\kappa})$ 步内解出方程。**短递推 + Krylov 子空间最优性 + SPD 共轭**三者合一的产物。1952 年 Hestenes-Stiefel 提出，被 SIAM 评为 20 世纪十大算法之一。

> [!important] 短递推的关键
> CG 仅用 $p_{k-1}, p_k$ 两个方向向量递推 $p_{k+1}$——**仅靠 SPD 才可能**。一般矩阵需 GMRES 长递推（保留所有前期向量），内存 $O(nk)$。

> [!warning] 仅适用 SPD
> CG 要求 $A$ SPD。非 SPD 系统：
> - 对称不定 → MINRES；
> - 一般非对称 → BiCG / BiCGSTAB / GMRES。

> [!info] CG 与梯度下降
> CG 的二次函数视角 $\min \frac{1}{2}x^\top A x - b^\top x$ 让它与梯度下降同源。但每步**沿 $A$-共轭方向**而非最速下降方向——避免了"锯齿"轨迹，是最优的二次梯度法。详见 Nocedal-Wright《Numerical Optimization》。

$\blacksquare$
