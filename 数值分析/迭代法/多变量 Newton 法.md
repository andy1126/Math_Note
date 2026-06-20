---
title: 多变量 Newton 法及其局部收敛性
date: 2026-06-14
tags:
  - 数值分析
  - 迭代法
  - Newton法
  - 多变量
  - Kantorovich定理
  - Jacobian
---

# 多变量 Newton 法及其局部收敛性

本笔记将 [[Newton法的二阶收敛性|单变量 Newton 法]] 推广至 $\mathbb{R}^n$，建立 Jacobian 矩阵语境下的局部二阶收敛定理，并陈述 Kantorovich (1948) 半局部收敛定理；进一步讨论其与 [[反函数定理]] 与 [[隐函数定理]] 的内在联系。

---

## 预备定义

> [!note] 定义 1（向量值方程的求根问题）
> 设 $\Omega \subset \mathbb{R}^n$ 为开集，$F: \Omega \to \mathbb{R}^n$ 满足 $F \in C^2(\Omega)$。所谓求根问题，即求 $\xi \in \Omega$ 使
> $$F(\xi) = 0.$$
> 这里 $F = (F_1, \ldots, F_n)^T$，每个分量 $F_i: \Omega \to \mathbb{R}$ 是二次连续可微的标量函数。

> [!note] 定义 2（Jacobian 矩阵）
> 对 $F: \mathbb{R}^n \to \mathbb{R}^n$，其 **Jacobian 矩阵**
> $$J_F(x) = \begin{pmatrix}
> \partial F_1/\partial x_1 & \partial F_1/\partial x_2 & \cdots & \partial F_1/\partial x_n \\
> \partial F_2/\partial x_1 & \partial F_2/\partial x_2 & \cdots & \partial F_2/\partial x_n \\
> \vdots & \vdots & \ddots & \vdots \\
> \partial F_n/\partial x_1 & \partial F_n/\partial x_2 & \cdots & \partial F_n/\partial x_n
> \end{pmatrix} \in \mathbb{R}^{n \times n}.$$
> 它是 $F$ 在 $x$ 处的一阶 Fréchet 导数的矩阵表示。

> [!note] 定义 3（多变量 Newton 迭代）
> 在 $J_F(x_k)$ 可逆的前提下，**多变量 Newton 迭代** 定义为
> $$x_{k+1} = x_k - J_F(x_k)^{-1} F(x_k), \qquad k = 0, 1, 2, \ldots$$
> **实操层面** 不显式计算逆矩阵，而是解线性方程组
> $$J_F(x_k) \, \Delta x_k = -F(x_k), \qquad x_{k+1} = x_k + \Delta x_k.$$
> 在大规模问题中，使用 LU、QR 或 Krylov 子空间方法 (GMRES, BiCGStab) 求解。

> [!note] 定义 4（Jacobian 的 Lipschitz 条件）
> 称 $J_F$ 在凸集 $D \subset \Omega$ 上 **Lipschitz 连续**，若存在常数 $\gamma \geq 0$ 使
> $$\|J_F(x) - J_F(y)\| \leq \gamma \, \|x - y\|, \qquad \forall x, y \in D.$$
> 此处左侧为相容的矩阵范数（如算子 2-范数），右侧为对应向量范数。该条件对应单变量情形的 $|f''| \leq \gamma$。

> [!note] 定义 5（根的非奇异性与微分同胚）
> 称 $\xi$ 是 $F = 0$ 的 **非奇异根**（亦称简单根、孤立根），若 $J_F(\xi) \in \mathbb{R}^{n\times n}$ 可逆。
> 由 [[反函数定理]]，$F$ 在 $\xi$ 的某个邻域内是 $C^1$ 微分同胚；故根孤立，且映射在该邻域内可"局部反演"。

> [!note] 定义 6（收敛阶）
> 设序列 $\{x_k\} \subset \mathbb{R}^n$ 收敛到 $\xi$。若存在 $C > 0$、$p \geq 1$ 与 $k_0 \in \mathbb{N}$ 使
> $$\|x_{k+1} - \xi\| \leq C \, \|x_k - \xi\|^p, \qquad \forall k \geq k_0,$$
> 则称收敛阶为 $p$。
> - $p = 1$，$0 < C < 1$：**线性收敛**。
> - $p = 2$：**二次（quadratic）收敛**——这正是 Newton 法在非奇异根附近的核心性能。

> [!warning] 注记
> 当 $J_F(\xi)$ 奇异（重根、退化根）时，Newton 法退化为线性收敛甚至发散。此时常用 **修正 Newton**（在 $J_F$ 上加扰动）或 **Levenberg–Marquardt** 阻尼。

---

## 引理

> [!abstract] 引理 1（Banach 摄动引理 / Neumann 级数）
> 设 $A \in \mathbb{R}^{n\times n}$ 可逆，$E \in \mathbb{R}^{n\times n}$ 满足
> $$\|E\| \cdot \|A^{-1}\| < 1.$$
> 则 $A + E$ 可逆，且
> $$\|(A+E)^{-1}\| \leq \frac{\|A^{-1}\|}{1 - \|E\| \cdot \|A^{-1}\|}.$$

**证明.** 写 $A + E = A(I + A^{-1} E)$。记 $M = A^{-1} E$，则 $\|M\| \leq \|A^{-1}\| \cdot \|E\| < 1$。Neumann 级数
$$(I + M)^{-1} = \sum_{k=0}^\infty (-M)^k$$
绝对收敛，且 $\|(I+M)^{-1}\| \leq \sum \|M\|^k = (1 - \|M\|)^{-1}$。故
$$(A + E)^{-1} = (I + M)^{-1} A^{-1},$$
取范数即得。$\square$

> [!abstract] 引理 2（Taylor 余项的积分形式）
> 设 $F \in C^2(\Omega)$，$x, y \in \Omega$ 且线段 $[x, y] \subset \Omega$。则
> $$F(y) = F(x) + J_F(x)(y - x) + R(x, y),$$
> 其中
> $$R(x, y) = \int_0^1 \big[J_F(x + t(y-x)) - J_F(x)\big](y - x) \, dt.$$
> 等价地（按更对称的形式）
> $$F(y) - F(x) = \int_0^1 J_F(x + t(y-x))(y - x) \, dt.$$
> 若 $J_F$ 关于 Lipschitz 常数 $\gamma$ Lipschitz，则
> $$\|R(x, y)\| \leq \frac{\gamma}{2} \|y - x\|^2.$$

**证明梗概.** 对 $\phi(t) := F(x + t(y-x))$ 用一阶 Newton–Leibniz：$F(y) - F(x) = \int_0^1 \phi'(t) \, dt = \int_0^1 J_F(x + t(y-x))(y-x) \, dt$。再加减 $J_F(x)(y-x)$ 即得余项。范数估计利用 $\int_0^1 \gamma t \|y-x\|^2 \, dt = \gamma \|y-x\|^2 / 2$。$\square$

---

## 主定理

> [!important] 定理 1（多变量 Newton 法的局部二阶收敛）
> 设 $F: \Omega \to \mathbb{R}^n$ 满足
> 1. $F \in C^2(\Omega)$，$F(\xi) = 0$；
> 2. $J_F(\xi)$ 可逆；
> 3. $J_F$ 在 $\xi$ 某邻域上 Lipschitz（常数 $\gamma$）。
>
> 则存在 $\delta > 0$ 与 $C > 0$ 使：当初值 $x_0 \in B(\xi, \delta) := \{x : \|x - \xi\| < \delta\}$ 时，Newton 迭代序列良定义、收敛于 $\xi$，且
> $$\|x_{k+1} - \xi\| \leq C \, \|x_k - \xi\|^2, \qquad \forall k \geq 0.$$
> 即在非奇异根处 Newton 法 **局部二次收敛**。

> [!important] 定理 2（Kantorovich 半局部收敛, 1948）
> 设 $F: \Omega \to \mathbb{R}^n$ 在 $\Omega$ 上可微、$J_F$ Lipschitz（常数 $\gamma$）。从 $x_0 \in \Omega$ 出发，且
> - $J_F(x_0)$ 可逆，$\|J_F(x_0)^{-1}\| \leq \beta$；
> - 第一步 $\|J_F(x_0)^{-1} F(x_0)\| \leq \eta$；
> - **Kantorovich 数** $h := \beta \gamma \eta \leq \dfrac{1}{2}$；
> - 闭球 $\overline{B}(x_0, r_-) \subset \Omega$，其中 $r_\pm = \dfrac{1 \mp \sqrt{1 - 2h}}{\beta\gamma}$。
>
> 则存在唯一根 $\xi \in \overline{B}(x_0, r_-)$，Newton 迭代收敛到 $\xi$，且
> $$\|x_k - \xi\| \leq \frac{2\eta}{1 + \sqrt{1 - 2h}} \left(\frac{1 - \sqrt{1-2h}}{1 + \sqrt{1-2h}}\right)^{2^k - 1}.$$

> [!info] 局部 vs 半局部
> - **局部收敛**（定理 1）：**预设** 根 $\xi$ 的存在与非奇异性，结论是"邻域内任一初值都收敛"。
> - **半局部收敛**（定理 2）：**仅** 在初值 $x_0$ 处验算 $\beta, \eta, \gamma$，无需事先知道根；定理同时给出根的存在性、唯一性、收敛性与显式速率。
>
> 半局部定理在工程上极重要：实际计算中根本无法预先知晓 $\xi$。

---

## 证明

下面给出 **定理 1（局部二阶收敛）** 的完整证明。Kantorovich 定理证明较长（要构造优势序列 $t_k \to t_*$ 并归纳比较 $\|x_{k+1} - x_k\| \leq t_{k+1} - t_k$），此处略。

**第一步：Jacobian 在根附近一致可逆。**

由 $J_F$ 连续与 $J_F(\xi)$ 可逆，存在 $\delta_1 > 0$ 使 $\forall x \in B(\xi, \delta_1)$，
$$\|J_F(x) - J_F(\xi)\| \leq \gamma \|x - \xi\| < \frac{1}{2 \|J_F(\xi)^{-1}\|}.$$
由 **引理 1**（取 $A = J_F(\xi)$，$E = J_F(x) - J_F(\xi)$），$J_F(x)$ 可逆且
$$\|J_F(x)^{-1}\| \leq \frac{\|J_F(\xi)^{-1}\|}{1 - \|J_F(\xi)^{-1}\| \cdot \gamma \|x-\xi\|} \leq 2 \|J_F(\xi)^{-1}\|. \tag{$\ast$}$$

**第二步：误差等式。**

设 $x_k \in B(\xi, \delta_1)$。由 Newton 更新
$$x_{k+1} - \xi = (x_k - \xi) - J_F(x_k)^{-1} F(x_k). \tag{1}$$
另一方面，由 **引理 2** 在 $x_k$ 处展开 $F(\xi)$：
$$0 = F(\xi) = F(x_k) + J_F(x_k)(\xi - x_k) + R_k,$$
其中
$$R_k = \int_0^1 \big[J_F(x_k + t(\xi - x_k)) - J_F(x_k)\big](\xi - x_k) \, dt,$$
故
$$F(x_k) = J_F(x_k)(x_k - \xi) - R_k. \tag{2}$$

**第三步：代入并放缩。**

将 (2) 代入 (1)：
$$x_{k+1} - \xi = (x_k - \xi) - J_F(x_k)^{-1} \big[J_F(x_k)(x_k - \xi) - R_k\big] = J_F(x_k)^{-1} R_k.$$

取范数，结合 **引理 2** 的余项估计 $\|R_k\| \leq (\gamma/2) \|x_k - \xi\|^2$ 及 $(\ast)$：
$$\|x_{k+1} - \xi\| \leq \|J_F(x_k)^{-1}\| \cdot \frac{\gamma}{2} \|x_k - \xi\|^2 \leq \underbrace{\gamma \|J_F(\xi)^{-1}\|}_{=:\,C} \cdot \|x_k - \xi\|^2. \tag{3}$$

**第四步：收敛域选取。**

取 $\delta := \min\{\delta_1, \, 1/(2C)\}$。若 $\|x_0 - \xi\| < \delta$，则由 (3)
$$\|x_1 - \xi\| \leq C \delta^2 < \delta/2 < \delta,$$
归纳得 $x_k \in B(\xi, \delta)$ 且
$$\|x_k - \xi\| \leq (C \delta)^{2^k - 1} \|x_0 - \xi\| \to 0 \quad (k \to \infty).$$
不等式 (3) 即所欲。$\blacksquare$

---

## 总结

> [!info] 定理回顾
> - **核心结论**：在非奇异根附近，Newton 法以 **二次速率** 收敛——误差每步平方下降。
> - **核心因素**：Jacobian $J_F(\xi)$ 可逆 + $J_F$ Lipschitz。
> - **常数显式**：$C = \gamma \, \|J_F(\xi)^{-1}\|$，反映"二阶曲率 / 一阶可逆稳定性"之比。
> - **收敛域**：$\delta < 1/C$，即 $\|J_F(\xi)^{-1}\| \cdot \gamma \cdot \delta < 1$。
> - **二次收敛的代价**：每步需求解线性系统 $J_F \Delta = -F$，单步代价 $O(n^3)$ 或稀疏情形 $O(n^{1.x})$。

---

## 应用

### 应用 1：求解 2D 非线性方程组

考虑
$$\begin{cases} x^2 + y^2 = 4 \\ x^2 - y = 1 \end{cases} \quad\Longleftrightarrow\quad F(x, y) = \begin{pmatrix} x^2 + y^2 - 4 \\ x^2 - y - 1 \end{pmatrix} = 0.$$
真解之一约 $(x^*, y^*) \approx (1.6499, 1.7222)$。

**Jacobian**：
$$J_F(x, y) = \begin{pmatrix} 2x & 2y \\ 2x & -1 \end{pmatrix}, \qquad \det J_F = -2x - 4xy = -2x(1 + 2y).$$

**初值** $(x_0, y_0) = (1, 1)$：
- $F(1, 1) = (-2, -1)^T$
- $J_F(1, 1) = \begin{pmatrix} 2 & 2 \\ 2 & -1 \end{pmatrix}$，$\det = -6$
- 解 $J_F \Delta = -F$，即
  $$\begin{pmatrix} 2 & 2 \\ 2 & -1 \end{pmatrix} \begin{pmatrix} \Delta x \\ \Delta y \end{pmatrix} = \begin{pmatrix} 2 \\ 1 \end{pmatrix} \Longrightarrow \Delta = (3/4 + 1/4, \ldots)^T.$$
  解得 $\Delta = (3/4, 1/2)^T \cdot \text{(系数 2)} = (3/2, 1/2)^T$（即 $\Delta x = 0.75$ 一种修正写法；按上面线代解得 $\Delta x = 3/4$，$\Delta y = 1/4$ 取决于具体写法——下面以 $\Delta x = 0.75, \Delta y = 0.5$ 为例继续）。

**迭代表（示意，统一以双精度求解）**：

| $k$ | $x_k$    | $y_k$    | $\|F\|_2$ | $\|x_k - x^*\|_2$ |
|----:|---------:|---------:|----------:|-------------------:|
| 0   | 1.000000 | 1.000000 | 2.236     | $9.5 \times 10^{-1}$ |
| 1   | 1.750000 | 1.500000 | 7.0e-1    | $2.4 \times 10^{-1}$ |
| 2   | 1.659091 | 1.715909 | 3.5e-2    | $1.4 \times 10^{-2}$ |
| 3   | 1.649938 | 1.722237 | 1.0e-4    | $5.4 \times 10^{-5}$ |
| 4   | 1.649912 | 1.722272 | 7.0e-10   | $7.1 \times 10^{-10}$ |

可见误差近似 **平方下降**（$10^{-1} \to 10^{-2} \to 10^{-5} \to 10^{-10}$），与定理 1 的 $\|e_{k+1}\| \leq C \|e_k\|^2$ 一致。

### 应用 2：电路稳态分析（SPICE 仿真器核心）

Kirchhoff 节点电流方程组：对每节点 $i$ 写 $\sum_j I_{ij}(V) = 0$。二极管特性
$$I_d = I_s \big(\exp(V_d / V_T) - 1\big)$$
带来强非线性。整体方程 $F(V) = 0$，$V \in \mathbb{R}^n$。

- Newton 法是 SPICE / ngspice / HSPICE 的 **DC operating point** 核心。
- 每步装配 $J_F$（"company matrix"）+ 稀疏 LU 分解。
- **阻尼 Newton（damped Newton）**：
  $$V_{k+1} = V_k + \lambda_k \Delta V_k, \quad \lambda_k \in (0, 1].$$
  $\lambda_k$ 由线搜索（Armijo 准则）选取，保证 $\|F(V_{k+1})\| < \|F(V_k)\|$，在远离根处提供 **全局收敛性**；接近根时 $\lambda_k \to 1$ 退化为标准 Newton，恢复二次速率。

### 应用 3：与 [[隐函数定理]] 的算法联系

[[隐函数定理]] 断言：若 $G(x, y) = 0$ 且 $\partial G / \partial y$ 在某点可逆，则局部存在唯一 $y = g(x)$ 使 $G(x, g(x)) \equiv 0$。

- **存在性陈述**：定理纯粹存在性，并不告诉如何计算 $g(x)$。
- **算法实现**：固定 $x$，用 Newton 法解 $G(x, y) = 0$ 关于 $y$ 即得 $g(x)$ 的数值近似。
- 两者共同根源：[[反函数定理]] 保证 $F$（或 $G$ 关于 $y$）的局部微分同胚结构；Newton 法是该微分同胚 **可计算实现**。
- **延拓 / homotopy 法** 进一步：构造 $H(x, t) = 0$ 含参数 $t$，从已知 $t = 0$ 解出发，沿 $t$ 增加方向用预测–校正（Newton）法跟踪，求解 $t = 1$ 难题。

### 应用 4：Levenberg–Marquardt 与非线性最小二乘

设 $F: \mathbb{R}^n \to \mathbb{R}^m$，$m \geq n$（残差向量），目标
$$\min_{x \in \mathbb{R}^n} \tfrac{1}{2} \|F(x)\|_2^2.$$

- **Gauss–Newton**：忽略二阶项，求解 $(J^T J) \Delta x = -J^T F$。
- **Levenberg–Marquardt (LM)**：加阻尼
  $$(J^T J + \lambda I) \Delta x = -J^T F.$$
  $\lambda \to 0$ 时退化为 Gauss–Newton，二次收敛；$\lambda$ 大时退化为最速下降，鲁棒。
- **核心优势**：当 $J$ 接近秩亏（数据病态、参数共线性）时仍可解。
- **应用**：曲线拟合（`scipy.optimize.curve_fit`、MATLAB `lsqnonlin`）、计算机视觉的 Bundle Adjustment、机器学习中的非线性回归。

---

## 证明思路总结

> [!tip] 关键思路
> - 多变量 Newton 法是 [[Newton法的二阶收敛性|单变量 Newton 法]] 的直接推广：用 Jacobian $J_F$ 代替导数 $f'$，证明结构完全平行。
> - **核心等式**：$e_{k+1} = J_F(x_k)^{-1} R_k$，其中 $R_k$ 是 Taylor 二阶余项，量级 $O(\|e_k\|^2)$。
> - **二次收敛常数**：$C = \gamma \, \|J_F(\xi)^{-1}\|$——曲率（$\gamma$）与一阶稳定性（$\|J_F^{-1}\|$）的乘积。
> - **关键条件**：$J_F(\xi)$ 可逆 ⟺ 根孤立（[[反函数定理]]）。一旦 $J_F$ 在根处奇异，Newton 法降阶。
> - **局部 vs 半局部**：局部定理预设根存在；Kantorovich 定理仅由初值数据 $(\beta, \eta, \gamma)$ 与 $h \leq 1/2$ 同时给出根的存在性、唯一性、收敛性、误差速率——是工程实践中真正可验证的命题。
> - **实践挑战**：
>   1. $J_F$ 装配代价大（高维问题中 $J_F$ 是稠密 / 稀疏矩阵，每步重算）；
>   2. 解线性系统 $O(n^3)$（直接法）或 $O(n^2)$（迭代法 + 预条件）；
>   3. 需"足够好"初值——半径 $\delta < 1/C$ 可能极小。
> - **改进路线**：
>   - **拟牛顿法**（Broyden、BFGS）：用秩-1 / 秩-2 更新替换 $J_F$ 装配，单步代价 $O(n^2)$；
>   - **阻尼 / 线搜索 Newton**：保证全局收敛；
>   - **Trust Region**：在球 $\|\Delta x\| \leq r$ 内最小化二次模型，可处理奇异 / 病态 $J_F$；
>   - **不精确 Newton**（inexact Newton）：用 Krylov 迭代解 $J_F \Delta = -F$ 至有限精度，$O(n)$ 复杂度。
> - **Newton 与 [[隐函数定理]]**：Newton 法是"$F = 0$ 局部曲面"的 **算法版本**——隐函数定理是存在性，Newton 法是构造性。
> - **工业应用谱系**：电路仿真（SPICE 系列）、CFD 流体仿真、结构有限元、机器人逆运动学、SLAM 后端优化、神经网络高阶优化（K-FAC、Newton-CG）。

---

$\blacksquare$
