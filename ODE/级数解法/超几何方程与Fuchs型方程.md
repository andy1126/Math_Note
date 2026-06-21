---
title: 超几何方程与 Fuchs 型方程
date: 2026-06-20
tags:
  - 微分方程
  - ODE
  - 级数解法
  - 超几何方程
  - Fuchs型方程
  - 正则奇点
  - Riemann-P符号
---

# 超几何方程与 Fuchs 型方程

## 预备定义

> [!note] Fuchs 型方程
> 复平面上含**有限个正则奇点**（在 $\infty$ 处也要求正则）且在其余点均解析的二阶齐次线性 ODE 称为 **Fuchs 型方程**（Fuchsian equation）。其标准形式为
> $$y'' + \sum_{k=1}^{m} \frac{A_k}{z - a_k}\, y' + \sum_{k=1}^{m} \frac{B_k}{(z - a_k)^2}\, y + \sum_{k=1}^{m} \frac{C_k}{z - a_k}\, y = 0,$$
> 其中 $\infty$ 处正则性的条件为 $\sum A_k = 2$ 以及另两个关于 $B_k, C_k$ 的约束（Fuchs 关系）。

> [!note] 超几何方程（hypergeometric equation / Gauss 方程）
> 恰有**三个正则奇点**（分别在 $0, 1, \infty$）的最一般的 Fuchs 型方程便是 **Gauss 超几何方程**：
> $$z(1 - z)\, y'' + \big[\gamma - (\alpha + \beta + 1) z\big]\, y' - \alpha\beta\, y = 0, \quad \cdots (\mathrm{HG})$$
> 其中 $\alpha, \beta, \gamma \in \mathbb{C}$，$\gamma \notin \mathbb{Z}_{\leq 0}$（保证指标根不为零或负整数）。$z = 0, 1$ 为有限奇点，$z = \infty$ 为第三个奇点。

> [!note] Riemann $P$-符号（Riemann $P$-symbol）
> 超几何方程（更一般地任何 Fuchs 型方程）可用 Riemann $P$-符号紧凑记录：
> $$y = P\begin{Bmatrix}
> 0 & 1 & \infty & \\
> 0 & 0 & \alpha & z \\
> 1 - \gamma & \gamma - \alpha - \beta & \beta &
> \end{Bmatrix}.$$
> 三列分别对应三个奇点，每列的两个数分别是该奇点处的**两个指标根**。$P$-符号完整规定了方程在 Möbius 变换下的性状——Möbius 变换把 Fuchs 奇点集映为另一 Fuchs 奇点集，而指标根不变。

> [!abstract] 引理：Frobenius 方法在三个正则奇点处各自给出指标方程
> 对 $z = 0$（同理对 $z = 1, \infty$），指标方程为 $r(r-1) + p_0 r + q_0 = 0$。对 (HG)，$p(z) = \frac{\gamma - (\alpha+\beta+1)z}{z(1-z)}$，$q(z) = \frac{-\alpha\beta}{z(1-z)}$，在 $z = 0$ 处的指标方程给出根 $0$ 与 $1 - \gamma$。详见 [[正则奇点与Frobenius方法]]。

---

## 定理

**(i)（超几何级数）** 在 $z = 0$ 处对应较大指标根 $r = 0$ 的 Frobenius 解为 **Gauss 超几何级数**：
$${}_2F_1(\alpha, \beta; \gamma; z) = \sum_{n=0}^{\infty} \frac{(\alpha)_n (\beta)_n}{(\gamma)_n\, n!}\, z^n, \quad |z| < 1,$$
其中 $(\alpha)_n := \alpha(\alpha + 1)\cdots(\alpha + n - 1)$ 为 **Pochhammer 符号**（上阶乘）。

**(ii)（收敛半径）** 级数在 $|z| < 1$ 内收敛。$z = 1$ 为离展开点最近的奇点，故收敛半径恰为 $1$。在 $|z| \geq 1$ 处的解析延拓由超几何函数的积分表示或连接公式（Kummer 的 24 个解）给出。

**(iii)（含参特例——所有经典正交多项式与特殊函数的统一母体）** 当 $\alpha$ 或 $\beta$ 为负整数 $-n$ 时，级数截断为 $n$ 次多项式，给出 **Jacobi 多项式** $P_n^{(\gamma-1, \, \cdot)}(1 - 2z)$ 的某倍数，后者以 Legendre（$\alpha = -n,\ \beta = n+1,\ \gamma = 1$）、Chebyshev、Gegenbauer 等为特例。

---

## 证明

### 第(i)部分：递推 ⇒ 超几何级数

将 Frobenius 级数 $y = \sum_{n=0}^\infty a_n z^{n+r}$ 代入 (HG)。在 $z = 0$ 处，指标方程为 $r(r-1) + \gamma r = r(r + \gamma - 1) = 0$（由 $p_0 = \gamma,\ q_0 = 0$），根 $r = 0,\ 1 - \gamma$。

取 $r = 0$。代入方程对齐 $z^n$ 系数得递推
$$\frac{a_{n+1}}{a_n} = \frac{(n + \alpha)(n + \beta)}{(n + 1)(n + \gamma)}, \quad n \geq 0.$$

**验证**：代入 Frobenius 级数，$y = \sum a_n z^n$，$y' = \sum n a_n z^{n-1}$，$y'' = \sum n(n-1) a_n z^{n-2}$。对齐最低次幂 $z^{n-1}$（来自 $y''$ 和 $y'$ 项）与 $z^n$（来自 $y$ 项），整理得递推。此处的关键结构是 $z=0$ 处 $p_0 = \gamma, q_0 = 0$ 使指标根的 $0$ 分支递推无奇性。

由递推（$a_0 = 1$）：
$$a_n = \frac{(\alpha)_n (\beta)_n}{(\gamma)_n\, n!}.$$

故 $y = {}_2F_1(\alpha, \beta; \gamma; z)$。$\square$

### 第(ii)部分：收敛半径

由比值判别法，$|a_{n+1}/a_n| = |\frac{(n+\alpha)(n+\beta)}{(n+1)(n+\gamma)}| \sim 1 + O(1/n)$，故 $R = 1$。这是 Fuchs 定理的精确体现：$0$ 与最近的另两个奇点（$1$ 或 $\infty$）的距离均为 $1$。

在 $z = 1$ 处作 Möbius 变换 $w = 1 - z$ 可得第二个 Frobenius 解；在 $z = \infty$ 处作 $w = 1/z$ 亦同。超几何方程共有 24 个 Kummer 解（不同奇点展开 + 不同指标根组合的线性变换关系）。$\square$

### 第(iii)部分：截断为多项式

若 $\alpha = -n$（$n \in \mathbb{N}$），则 $(\alpha)_{n+1} = 0$，递推在 $n$ 处截断，${}_2F_1(-n, \beta; \gamma; z)$ 退化为次数 $\leq n$ 的多项式。标准化后与 Jacobi 多项式 $P_n^{(\gamma-1, \beta-\gamma-n)}(1 - 2z)$ 成正比。取具体参数 $\gamma$ 和 $\beta$ 即得各类经典正交多项式。$\blacksquare$

---

## 超几何函数的涵盖范围

| 特殊函数 | 参数对应 |
|---|---|
| Legendre $P_n(x)$ | ${}_2F_1(-n, n+1; 1; \frac{1-x}{2})$ |
| Chebyshev $T_n(x)$ | ${}_2F_1(-n, n; \frac{1}{2}; \frac{1-x}{2})$ |
| Gegenbauer $C_n^{(\lambda)}(x)$ | ${}_2F_1(-n, n+2\lambda; \lambda+\frac{1}{2}; \frac{1-x}{2})$ |
| Jacobi $P_n^{(\alpha, \beta)}(x)$ | ${}_2F_1(-n, n+\alpha+\beta+1; \alpha+1; \frac{1-x}{2})$ |
| Bessel $J_\nu(x)$ | $\frac{(x/2)^\nu}{\Gamma(\nu+1)} {}_0F_1(; \nu+1; -x^2/4)$（合流超几何，$z \to \infty$ 退化） |
| Kummer 合流超几何 | $\infty$ 与 $0$ 合并：$z y'' + (\gamma - z) y' - \alpha y = 0$ |

---

## 证明思路总结

> [!tip] 关键思想
> 超几何方程是**"三个正则奇点的 Fuchs 型方程"**的具体实现——参数 $\alpha, \beta, \gamma$ 分别控制三个奇点处的两个指标根之差。它的威力在于**普遍性**：通过取不同的 $\alpha, \beta, \gamma$ 和不同的 Möbius 变换，几乎所有在数学物理中出现的二阶线性 ODE（至多三个正则奇点）都可以化为超几何方程的特例或合流极限。
>
> 高观点下：超几何方程 = $\mathbb{CP}^1 \setminus \{0, 1, \infty\}$ 上的平坦联络的 Fuchs 型 ODE 实现；Pochhammer 符号 = 指标方程根之差在递推中的代数表现；24 个 Kummer 解 = 基本群表示中不同基底的线性变换。

> [!info] 与 Frobenius 理论、SL 理论的关系
> - Frobenius 方法的三个情形（根差非整数/零/整数）在超几何方程中全部出现，分别对应 $1 - \gamma \notin \mathbb{Z}$、$\gamma = 1$、$\gamma \in \mathbb{Z}$；
> - 截断为多项式的条件（$\alpha$ 或 $\beta = -n$）实质上是从连续谱中挑出 $L^2_w$ 可归一化的多项式解——这是 [[Sturm-Liouville定理]] 在复域的前奏；
> - Legendre、Hermite、Laguerre 均为超几何方程的特例或合流极限，详见各独立笔记。
