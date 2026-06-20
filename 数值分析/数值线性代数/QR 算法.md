---
title: QR 算法
date: 2026-06-06
tags:
  - 数值分析
  - 数值线性代数
  - QR算法
  - 特征值
  - Schur分解
  - Hessenberg
---

# QR 算法

## 预备定义

> [!note] QR 算法（基本形式）
> 设 $A \in \mathbb{R}^{n\times n}$。令 $A_0 = A$。对 $k = 0, 1, 2, \ldots$：
> 1. **QR 分解** $A_k = Q_k R_k$；
> 2. **逆序乘积** $A_{k+1} = R_k Q_k$。
>
> 序列 $\{A_k\}$ 在合适条件下收敛到上三角形（即 [[Schur分解定理|Schur 分解]] 中的 $T$）。

> [!info] 立即观察
> $A_{k+1} = R_k Q_k = Q_k^\top A_k Q_k$（用 $R_k = Q_k^\top A_k$）。**每步是正交相似变换**，故 $A_k$ 与 $A_0 = A$ 谱相同。这是 QR 算法保特征值的根本。

---

## QR 算法的收敛定理

> [!abstract] 定理（基本 QR 算法收敛性）
> 设 $A \in \mathbb{R}^{n\times n}$ 可对角化，特征值满足 $|\lambda_1| > |\lambda_2| > \cdots > |\lambda_n| > 0$（**严格分离**）。则
> $$A_k \to T, \quad T_{ii} = \lambda_i, \quad T \text{ 上三角}.$$
> 收敛速率：对角下方元 $(A_k)_{ij} = O((\lambda_i/\lambda_j)^k)$（$i > j$）。

### 证明梗概（与幂法的联系）

定义"块幂法"：$A^k$ 的前 $j$ 列张成的子空间逐步收敛到由 $v_1, \ldots, v_j$ 张成的不变子空间。

QR 算法等价于：$\widetilde Q_k = Q_0 Q_1 \cdots Q_{k-1}$ 的列向量逐步与 $A$ 的特征向量序对齐。即**所有特征向量同步幂法**。

详细论证用块 LR 分解 + 子空间迭代，参见 Golub-Van Loan 《Matrix Computations》§7.3。$\square$

> [!warning] 复数特征值
> 实矩阵的复特征值成共轭对 $\lambda, \bar\lambda$（同模），不满足"严格分离"——基本 QR 不收敛到上三角，而**收敛到块上三角（实 Schur 形）**：对角块 $1\times 1$（实特征值）或 $2\times 2$（共轭对）。

---

## 加速一：Hessenberg 化预处理

基本 QR 每步 $O(n^3)$ 太昂贵。**预先把 $A$ 化为上 Hessenberg 形**（对角下方仅第一次次对角非零）：
$$H \;=\; \begin{pmatrix} * & * & * & \cdots & * \\ * & * & * & \cdots & * \\ 0 & * & * & \cdots & * \\ \vdots & \ddots & \ddots & \ddots & \vdots \\ 0 & \cdots & 0 & * & * \end{pmatrix}.$$

### Householder 化为 Hessenberg

用 $n-2$ 次 Householder 反射，复杂度 $O(n^3)$（一次性预处理）：
- 第 $k$ 步：用 Householder 把第 $k$ 列从第 $k+2$ 行起清零；
- 类似 Householder QR，但**保留**第 $k+1$ 行（否则破坏相似性）。

详见 [[Householder 反射与 Givens 旋转]]。

### Hessenberg QR 的复杂度

上 Hessenberg 矩阵的 QR 分解仅 $O(n^2)$（用 $n-1$ 次 Givens 旋转清次对角元）。**且 Hessenberg 形在 QR 步下保持不变**（关键！）。

故每步 QR 从 $O(n^3)$ 降到 $O(n^2)$，**总开销 $O(n^3)$**（预处理 + $O(n)$ 次迭代 × $O(n^2)$ 每步）。

---

## 加速二：位移 QR 算法

### 思想

注意 QR 算法收敛速率 $|\lambda_i/\lambda_j|$。**位移** $\mu$ 把 $A_k$ 替换为 $A_k - \mu I$ 后再 QR：
- 特征值平移到 $\lambda_i - \mu$；
- 若 $\mu \approx \lambda_n$，则 $|\lambda_n - \mu|/|\lambda_{n-1} - \mu|$ 极小 → 极快收敛到 $\lambda_n$。

### 单位移 QR 算法

对 $k = 0, 1, 2, \ldots$：

1. 选位移 $\mu_k$（常取 $\mu_k = (A_k)_{nn}$ 或 Wilkinson 位移，见下）；
2. QR 分解 $A_k - \mu_k I = Q_k R_k$；
3. $A_{k+1} = R_k Q_k + \mu_k I$.

仍保正交相似：$A_{k+1} = Q_k^\top A_k Q_k$.

### Wilkinson 位移

取 $A_k$ 右下 $2\times 2$ 子块 $\begin{pmatrix} \alpha & \beta \\ \beta & \gamma \end{pmatrix}$ 的**最接近 $\gamma$ 的特征值**为 $\mu_k$。对对称矩阵保证收敛；非对称用类似策略。

### 双位移（Francis QR 算法）

实矩阵的复特征值用单实位移无法逼近。**Francis 双位移**：选共轭对 $\mu, \bar\mu$，做 $(A_k - \mu I)(A_k - \bar\mu I)$ 隐式 QR——保持实算术，仍能逼近复特征值。

LAPACK `dhseqr`（双隐式位移 Francis QR）是工业标准。

---

## 收敛速率比较

| 算法 | 收敛速率 | 每步 |
|---|---|---|
| 基本 QR | $\|\lambda_i/\lambda_j\|^k$（线性） | $O(n^3)$ |
| Hessenberg QR | 同上 | $O(n^2)$ |
| 单位移 Hessenberg QR | $(\|\lambda_n - \mu_k\|/\|\lambda_{n-1} - \mu_k\|)^k$（局部超线性） | $O(n^2)$ |
| Wilkinson 位移 QR | **局部二次（对称三次）** | $O(n^2)$ |
| Francis 双位移 QR | 同上，处理复特征值 | $O(n^2)$ |

实际 LAPACK 实现每个特征值平均需 $\approx 2$ 次迭代（位移收敛极快），**找全部 $n$ 个特征值总开销 $\sim 10 n^3$ 浮点运算**。

---

## 具体应用

### 应用一：3×3 基本 QR 算法演示

$A_0 = \begin{pmatrix} 2 & -1 & 0 \\ -1 & 2 & -1 \\ 0 & -1 & 2 \end{pmatrix}$（已三对角，对称，特征值 $2 - \sqrt{2}, 2, 2 + \sqrt{2}$）。

**步 1**：$A_0 = Q_0 R_0$（Givens 或 Householder），然后 $A_1 = R_0 Q_0 \approx \begin{pmatrix} 3 & -0.71 & 0 \\ -0.71 & 1.67 & -0.41 \\ 0 & -0.41 & 1.33 \end{pmatrix}$.

**步 2**：再 QR，$A_2$ 对角逐步显出特征值 $3.41, 2, 0.59$ 即 $2 \pm \sqrt{2}, 2$。

10 步内收敛到机器精度。

### 应用二：求所有特征值（LAPACK 实践）

```python
import numpy as np
A = np.random.randn(100, 100)
eigvals = np.linalg.eigvals(A)  # 调用 LAPACK dhseqr
```

LAPACK 内部：
1. Householder 化为 Hessenberg（$O(n^3)$）；
2. Francis 双位移 QR 迭代（$O(n^3)$）；
3. 从实 Schur 形中读出对角块的特征值。

### 应用三：对称矩阵的特殊处理

对称 $A$：
1. Householder 化为**对称三对角**形（带宽 $1$）；
2. 三对角 QR 算法（仅 $O(n)$ 每步）；
3. 总 $O(n^3)$ 但常数小 6 倍——LAPACK `dsyev`。

> [!info] 替代算法
> 对称三对角的特征值可用**分治法**（divide-and-conquer，`dsyevd`）或 **MRRR**（multiple relatively robust representations，`dsyevr`）求解，对大 $n$ 更快。

### 应用四：与 Schur 分解的对接

QR 算法**就是** [[Schur分解定理|Schur 分解]] 的算法实现：极限 $T_\infty$ 即 Schur 形，累积正交变换 $Q_\infty = Q_0 Q_1 \cdots$ 即 Schur 矩阵 $Q$，故
$$A \;=\; Q_\infty T_\infty Q_\infty^\top.$$

定理（存在性）保证收敛目标存在；算法（QR）保证可计算。

### 应用五：特征向量的恢复

QR 算法计算特征值后，特征向量用**反幂法**+Wilkinson 位移恢复：每个 $\lambda_i$ 一次反幂法迭代（已知位移极接近）即可。详见 [[幂法与反幂法]]。

---

## 算法关键点

> [!tip] QR 算法的"奇迹"
> QR 算法看似仅是"分解-逆乘"的简单递推，却能在 $O(n^3)$ 内找出所有特征值。**关键奇迹**：
> 1. 正交相似 → 谱不变；
> 2. Hessenberg 形在 QR 下不变 → 每步 $O(n^2)$；
> 3. 位移 → 局部超线性收敛；
> 4. 双位移 → 处理实矩阵的复特征值且保实算术。
>
> 缺一不可。**1959 年 Francis 和 Kublanovskaya 同年独立发现**，被 SIAM 评为 20 世纪十大算法之一。

> [!important] 与子空间迭代的关系
> QR 算法 ≡ 同步幂法。具体：累积 $Q_0 Q_1 \cdots Q_{k-1}$ 的前 $j$ 列张成的子空间，等于 $A^k$ 把"标准 $j$-维子空间"映出的子空间。

> [!warning] 不能处理非对角化矩阵的特征向量
> 若 $A$ 有非平凡 Jordan 块，QR 算法仍能找到特征值（重数计入），但特征向量是奇异的（需广义特征向量）。LAPACK 给出 Schur 形，不强求 Jordan 形（数值不稳定）。

> [!info] 现代替代
> - **稠密大规模**：QR 算法是金标准；
> - **稀疏大规模少数特征值**：Lanczos / Arnoldi（[[Krylov 子空间与 GMRES]] 同族）；
> - **GPU 加速**：QR 算法的并行化仍是活跃研究方向（位移选择难并行）。

$\blacksquare$
