---
title: Krylov 子空间与 GMRES
date: 2026-06-06
tags:
  - 数值分析
  - 数值线性代数
  - Krylov子空间
  - GMRES
  - Arnoldi
  - 迭代法
---

# Krylov 子空间与 GMRES

## 预备定义

> [!note] Krylov 子空间
> 给定 $A \in \mathbb{R}^{n\times n}$、$v \neq 0$，称
> $$\mathcal{K}_k(A, v) \;=\; \mathrm{span}\{v, A v, A^2 v, \ldots, A^{k-1} v\}$$
> 为 $k$ 阶 **Krylov 子空间**。

> [!note] Krylov 投影方法的通用框架
> 求解 $Ax = b$ 的 Krylov 方法在 $x_0 + \mathcal{K}_k(A, r_0)$ 中选 $x_k$（$r_0 = b - A x_0$），满足某种最优/正交条件。不同条件 → 不同算法：
>
> | 算法 | 矩阵类型 | 最优性条件 |
> |---|---|---|
> | CG | SPD | $A$-范数误差极小 |
> | MINRES | 对称不定 | 残差 2-范数极小 |
> | GMRES | 一般非对称 | 残差 2-范数极小 |
> | BiCG / BiCGSTAB | 一般非对称 | 双正交残差 |

---

## Arnoldi 过程：Krylov 子空间的正交基

### 算法

构造 $\mathcal{K}_k(A, v_1)$ 的正交基 $\{v_1, v_2, \ldots, v_k\}$。

输入：$A$、初始向量 $v_1$（$\|v_1\| = 1$）。

对 $j = 1, 2, \ldots, k$：

1. $w = A v_j$；
2. 对 $i = 1, 2, \ldots, j$：$h_{ij} = v_i^\top w$；$w \leftarrow w - h_{ij} v_i$；（修正 Gram-Schmidt）
3. $h_{j+1, j} = \|w\|$；
4. 若 $h_{j+1, j} = 0$：终止（**幸运分解**，找到精确不变子空间）；
5. $v_{j+1} = w/h_{j+1, j}$。

### Arnoldi 关系

> [!abstract] 定理（Arnoldi 关系）
> $$A V_k \;=\; V_{k+1} \widetilde H_k,$$
> 其中 $V_k = [v_1, \ldots, v_k] \in \mathbb{R}^{n\times k}$ 列正交，$\widetilde H_k \in \mathbb{R}^{(k+1) \times k}$ 是**上 Hessenberg** 矩阵（仅第一次次对角下方为零）：
> $$\widetilde H_k \;=\; \begin{pmatrix} H_k \\ h_{k+1,k} e_k^\top \end{pmatrix}, \quad H_k \in \mathbb{R}^{k\times k} \text{ 上 Hessenberg}.$$

**证明**：由步骤 2-5，$A v_j = \sum_{i \leq j+1} h_{ij} v_i$，即 $A V_k$ 的第 $j$ 列恰是 $\widetilde H_k$ 第 $j$ 列与 $V_{k+1}$ 列的线性组合。$\square$

> [!important] Lanczos 是 Arnoldi 的对称特例
> 若 $A$ 对称，$H_k$ 退化为**三对角**（仅主对角与上下次对角），Arnoldi 简化为 **Lanczos 三项递推**——这是 CG 短递推的来源。

---

## GMRES 算法

### 核心思想

在 $x_0 + \mathcal{K}_k(A, r_0)$ 中找 $x_k$ 使**残差 2-范数极小**：
$$x_k \;=\; \arg\min_{x \in x_0 + \mathcal{K}_k} \|b - A x\|_2.$$

### GMRES 推导

设 $x = x_0 + V_k y$（$y \in \mathbb{R}^k$）。则
$$b - A x \;=\; r_0 - A V_k y \;=\; r_0 - V_{k+1} \widetilde H_k y.$$

设 $\beta = \|r_0\|$、$v_1 = r_0/\beta$。则 $r_0 = \beta V_{k+1} e_1$，
$$b - A x \;=\; V_{k+1} (\beta e_1 - \widetilde H_k y).$$

正交矩阵保 2-范数：
$$\|b - A x\|_2 \;=\; \|\beta e_1 - \widetilde H_k y\|_2.$$

**变成 $(k+1) \times k$ 的小最小二乘问题**：
$$y_k \;=\; \arg\min_y \|\beta e_1 - \widetilde H_k y\|_2.$$

### GMRES 算法整体

1. $r_0 = b - A x_0$；$\beta = \|r_0\|$；$v_1 = r_0/\beta$；
2. 对 $j = 1, 2, \ldots$：
   - Arnoldi 一步生成 $v_{j+1}$ 与 $\widetilde H_j$；
   - 解小型最小二乘问题 $\min_y \|\beta e_1 - \widetilde H_j y\|$ 得 $y_j$；
   - 检查残差 $\|r_j\| = \|\beta e_1 - \widetilde H_j y_j\|$；
3. 收敛后 $x_j = x_0 + V_j y_j$.

### 高效实现：Givens 旋转

最小二乘 $\min \|\beta e_1 - \widetilde H_j y\|$ 用 [[Householder 反射与 Givens 旋转|Givens 旋转]] 逐步把 $\widetilde H_j$ 化为上三角。**关键**：每步新增一列 $v_{j+1}$ 时只需一次 Givens 旋转更新前面已分解的部分，**增量复杂度 $O(j)$**。

---

## 主定理 1：GMRES 的有限步终止

> [!abstract] 定理（GMRES 的精确终止）
> 在精确算术下，存在 $m \leq n$ 使 GMRES 在第 $m$ 步达精确解 $r_m = 0$。$m$ 等于 $A$ 的极小多项式的次数（不超过 $A$ 的不同特征值个数）。

**证明梗概**：极小多项式 $\mu(\lambda)$ 满足 $\mu(A) = 0$，$\deg \mu \leq n$。故 $A^m \in \mathrm{span}\{I, A, \ldots, A^{m-1}\}$，$\mathcal{K}_{m+1} = \mathcal{K}_m$ 不再扩张。Arnoldi 在第 $m$ 步出现 $h_{m+1, m} = 0$（幸运分解），残差为零。$\square$

> [!warning] $m \leq n$ 但浮点下不必然
> 与 CG 同理：浮点误差破坏 Krylov 正交性，$m$ 可能 $> n$。**实践把 GMRES 当迭代法用**。

---

## 主定理 2：收敛速率

> [!abstract] 定理（GMRES 收敛估计）
> 设 $A$ 可对角化 $A = X \Lambda X^{-1}$。则
> $$\frac{\|r_k\|_2}{\|r_0\|_2} \;\leq\; \kappa_2(X) \cdot \min_{p \in \mathcal{P}_k, p(0)=1} \max_{\lambda \in \sigma(A)} |p(\lambda)|,$$
> 其中 $\mathcal{P}_k$ 是 $\leq k$ 次多项式集合。

**解读**：
- **谱聚集** → 多项式可在小邻域中压低 → GMRES 快；
- **谱分散** → 多项式难以同时压低各特征值 → GMRES 慢；
- **正常 $A$**（$X$ 正交）→ $\kappa_2(X) = 1$，估计紧；
- **病态 $X$** → 估计松，实际表现可能差。

---

## 内存与重启 (Restart)

### 全 GMRES 的内存问题

完整 GMRES 需保存所有 $v_1, \ldots, v_k$ → $O(nk)$ 内存。$k$ 大时内存爆炸。

### Restarted GMRES (GMRES(m))

$m$ 步后用当前 $x_m$ 作新初值，重新启动 Arnoldi：

```
循环：
  从 x_0 跑 GMRES m 步得 x_m
  若收敛：停止；否则 x_0 ← x_m
```

**优点**：内存 $O(nm)$ 固定；**缺点**：可能**停滞**（stagnation）——某些非对称矩阵下 GMRES(m) 不收敛但全 GMRES 收敛。

实践：$m = 30, 50$ 常用；调试时尝试不同 $m$。

---

## CG vs MINRES vs GMRES 对比

| 算法 | 矩阵 | 内存 | 计算/步 | 残差最优 |
|---|---|---|---|---|
| CG | SPD | $O(n)$（短递推） | 1 MV + $O(n)$ | $A$-范数误差 |
| MINRES | 对称不定 | $O(n)$（短递推） | 1 MV + $O(n)$ | 2-范数残差 |
| GMRES | 一般 | $O(nk)$（长递推） | 1 MV + $O(nk)$ | 2-范数残差 |
| BiCGSTAB | 一般 | $O(n)$（短递推） | 2 MV + $O(n)$ | 非极小化（贪婪） |

**MV = 矩阵向量积**。SPD 用 CG、对称用 MINRES、非对称尽量用 GMRES（精度高）或 BiCGSTAB（内存少）。

---

## 具体应用

### 应用一：3×3 GMRES 算例

$A = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \\ 1 & 0 & 1 \end{pmatrix}$（非对称），$b = (3, 2, 2)^\top$。真解 $x^* = (1, 1, 1)^\top$。

$x_0 = 0$，$r_0 = b$，$\beta = 3$（设 $\|b\| = \sqrt{17}$ 后 normalize）...

逐步演算（一般 3 步内得精确解，因 $n = 3$）。

### 应用二：Navier-Stokes 方程的求解

CFD 中 Navier-Stokes 离散得到大型非对称稀疏系统。GMRES + 多重网格预条件是工业 CFD 软件（ANSYS Fluent、OpenFOAM）的核心求解器。

### 应用三：电磁学的 Maxwell 方程

Maxwell 方程的有限元离散给出复对称（非 Hermite）系统。**复 GMRES** 或 **QMR / TFQMR** 是标准选择。

### 应用四：与 Schur 分解的关系

Arnoldi 过程在第 $k$ 步给出 $A$ 在 $\mathcal{K}_k$ 上的限制矩阵 $H_k$。$H_k$ 的特征值 (**Ritz 值**) 收敛到 $A$ 谱的端点。这是稀疏矩阵特征值计算的 **Arnoldi 方法**（[[QR 算法]] 的稀疏版本）。

### 应用五：作为预条件子

对 $Ax = b$ 加预条件 $M \approx A$，求解 $M^{-1} A x = M^{-1} b$（**左预条件**）或 $A M^{-1} y = b$、$x = M^{-1} y$（**右预条件**）。$M^{-1} A$ 谱聚集 → GMRES 快收敛。

常见 $M$：
- **不完全 LU** (ILU)：$A \approx \tilde L \tilde U$ 中保留稀疏模式；
- **代数多重网格** (AMG)：对 PDE 离散极强；
- **物理基础预条件**：如 SIMPLE（CFD）、Schur 补预条件（鞍点问题）。

---

## 算法关键点

> [!tip] Krylov 方法的统一视角
> Krylov 方法把高维 $Ax = b$ 投影到 $k$ 维 Krylov 子空间，化为**小规模** $\widetilde H_k y = $ 子问题。规模 $k$ 远小于 $n$，但 $k$ 选择恰当时投影信息足够准确。**降维 + 投影 + 最优**三步法。

> [!important] GMRES 是非对称的"金标准"
> Saad-Schultz 1986 年提出，是 Krylov 方法的里程碑。**残差严格单调递减**（不像 BiCG 可能振荡）；理论分析与实践效果俱佳。

> [!warning] 长递推的内存代价
> GMRES 必须保存所有前面 Arnoldi 向量——非对称下**不可避免**。这是为何 CG 的短递推（仅 $p_{k-1}, p_k$）是"奇迹"。**Faber-Manteuffel 定理**（1984）证明：仅当 $A$ 正规（normal）时才有短递推 Krylov 方法。

> [!info] 现代 Krylov 方法的研究
> - **Block Krylov 方法**：同时多右端 $AX = B$；
> - **Recycling Krylov**：跨多次求解复用 Krylov 子空间；
> - **Communication-avoiding Krylov**：减少分布式通信轮次；
> - **GPU 适配的 BiCGSTAB 与 IDR(s) 方法**：现代异构计算下的研究热点。

> [!important] 与 [[共轭梯度法 CG]] 的家族关系
> | 算法 | 主要原理 |
> |---|---|
> | CG | 对称 Lanczos + $A$-共轭方向 |
> | MINRES | 对称 Lanczos + QR 极小残差 |
> | GMRES | Arnoldi + QR 极小残差 |
> | Arnoldi 特征值法 | Arnoldi + $H_k$ 特征值 |
>
> 同一棵 Krylov 树上的不同分支——是数值线性代数最丰饶的子领域。

$\blacksquare$
