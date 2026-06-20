---
title: Floquet 定理
date: 2026-04-11
tags:
  - 常微分方程
  - 线性系统
  - 周期系数
  - Floquet理论
  - 基本矩阵
  - 稳定性
---

# Floquet 定理

## 预备定义

> [!note] 周期线性系统
> 设 $A: \mathbb{R} \to \mathbb{R}^{n \times n}$ 连续，且存在 $T > 0$ 使得
> $$A(t + T) = A(t) \quad \forall\, t \in \mathbb{R}.$$
> 称齐次线性系统 $x'(t) = A(t)\, x(t)$ 为**周期线性系统**，$T$ 为其**周期**。

> [!note] 基本矩阵与主基本矩阵
> $\Phi(t)$ 为 $x' = A(t)x$ 的**基本矩阵**，若 $\Phi' = A(t)\Phi$ 且 $\det\Phi(t) \neq 0$。
> 若进一步 $\Phi(0) = I$（单位矩阵），则称 $\Phi$ 为**主基本矩阵**（principal fundamental matrix），记为 $\Phi(t)$。

> [!note] 单值矩阵（monodromy matrix）
> 对以 $T$ 为周期的系统，**单值矩阵**定义为
> $$M = \Phi(T),$$
> 其中 $\Phi$ 为主基本矩阵。$M$ 描述了解经过一个完整周期后的"返回映射"。
> $M$ 的特征值 $\rho_1, \ldots, \rho_n$ 称为 **Floquet 乘子**（Floquet multipliers）。

> [!note] 矩阵对数
> 若 $M \in \mathbb{R}^{n \times n}$ 可逆，则存在（一般为复数）矩阵 $B \in \mathbb{C}^{n \times n}$ 使得
> $$M = e^{BT}.$$
> $B$ 的特征值 $\mu_k$（满足 $\rho_k = e^{\mu_k T}$）称为 **Floquet 指数**（Floquet exponents）。

> [!abstract] 引理：$\Phi(t + T)$ 也是基本矩阵
> 设 $\Phi(t)$ 为 $x' = A(t)x$ 的基本矩阵。则 $\Psi(t) = \Phi(t + T)$ 也是基本矩阵。

**证明**：

$$\Psi'(t) = \Phi'(t + T) = A(t + T)\, \Phi(t + T) = A(t)\, \Psi(t),$$

其中用到了 $A$ 的 $T$-周期性。且 $\det\Psi(t) = \det\Phi(t+T) \neq 0$。$\square$

---

## 定理

设 $A(t)$ 以 $T$ 为周期，$\Phi(t)$ 为主基本矩阵（$\Phi(0) = I$），$M = \Phi(T)$ 为单值矩阵。

**(i)** 存在（一般为复数）矩阵 $B \in \mathbb{C}^{n \times n}$ 和以 $T$ 为周期的可逆矩阵值函数 $P: \mathbb{R} \to \mathbb{C}^{n \times n}$，使得

$$\Phi(t) = P(t)\, e^{Bt}, \quad P(t + T) = P(t), \quad P(0) = I.$$

**(ii)** 每个解 $x(t) = \Phi(t)\, c$ 可表示为

$$x(t) = P(t)\, e^{Bt}\, c,$$

即**周期调制** $P(t)$ 乘以**指数增长/衰减** $e^{Bt}$。

**(iii)** 系统的稳定性由 Floquet 乘子决定：
- 所有 $|\rho_k| < 1$ $\Longrightarrow$ 渐近稳定；
- 某个 $|\rho_k| > 1$ $\Longrightarrow$ 不稳定。

---

## 证明

### 第(i)部分：Floquet 分解

#### 第一步：基本矩阵的周期递推关系

由引理，$\Phi(t + T)$ 是基本矩阵。任意两个基本矩阵通过右乘常数可逆矩阵相联系，故存在常数矩阵 $C$ 使得

$$\Phi(t + T) = \Phi(t)\, C. \quad \cdots (\ast)$$

令 $t = 0$：$\Phi(T) = \Phi(0)\, C = I \cdot C = C$，故

$$C = M = \Phi(T).$$

因此

$$\Phi(t + T) = \Phi(t)\, M. \quad \cdots (\star)$$

> [!important] 周期递推关系的含义
> $(\star)$ 表明经过一个周期，基本矩阵右乘单值矩阵 $M$。连续 $k$ 个周期后，$\Phi(t + kT) = \Phi(t)\, M^k$。系统的长时间行为完全由 $M$ 的谱决定。

$\square$

#### 第二步：构造矩阵 $B$

$M = \Phi(T)$ 可逆（因 $\det\Phi(t) \neq 0$）。取 $B \in \mathbb{C}^{n \times n}$ 使得

$$e^{BT} = M. \quad \cdots (1)$$

> [!info] 矩阵对数的存在性
> 任意可逆复矩阵都有对数：将 $M$ 化为 Jordan 标准形 $M = S\, J\, S^{-1}$，对每个 Jordan 块取对数（利用 $\ln(I + N) = N - N^2/2 + \cdots$ 的有限截断，因 $N$ 幂零），再令 $B = \frac{1}{T} S\, \ln J\, S^{-1}$。对数不唯一（差一个 $2\pi i k/T$ 的整数倍），但存在性足够。
>
> 当 $M$ 有负实特征值时，$B$ 必须取复值。若将周期替换为 $2T$，则 $M^2$ 的特征值均为正，可取实矩阵 $B$。

$\square$

#### 第三步：构造周期矩阵 $P(t)$

定义

$$P(t) = \Phi(t)\, e^{-Bt}. \quad \cdots (2)$$

**验证 $P$ 以 $T$ 为周期**：

$$P(t + T) = \Phi(t + T)\, e^{-B(t+T)} = \Phi(t)\, M \, e^{-BT}\, e^{-Bt}.$$

由 $(1)$，$M\, e^{-BT} = e^{BT}\, e^{-BT} = I$，故

$$P(t + T) = \Phi(t)\, e^{-Bt} = P(t). \quad \square$$

**验证 $P(0) = I$**：

$$P(0) = \Phi(0)\, e^{0} = I \cdot I = I. \quad \square$$

**验证 $P(t)$ 可逆**：

$$\det P(t) = \det\Phi(t) \cdot \det(e^{-Bt}) = \det\Phi(t) \cdot e^{-\operatorname{tr}(B)\, t} \neq 0.$$

$\square$

由 $(2)$，$\Phi(t) = P(t)\, e^{Bt}$，第(i)部分证毕。$\square$

### 第(ii)部分：解的表示

直接由第(i)部分：一般解 $x(t) = \Phi(t)\, c = P(t)\, e^{Bt}\, c$。$\square$

### 第(iii)部分：稳定性判据

#### 第一步：$\|x(t+kT)\|$ 的增长由 $M^k$ 控制

由 $(\star)$，$x(t + kT) = \Phi(t + kT)\, c = \Phi(t)\, M^k\, c$。

在 $t \in [0, T]$ 上 $\Phi(t)$ 连续且可逆，故存在常数 $c_1, c_2 > 0$ 使得

$$c_1 \|M^k c\| \leq \|x(t + kT)\| \leq c_2 \|M^k c\|. \quad \cdots (\dagger)$$

$\square$

#### 第二步：$M^k$ 的增长由谱半径决定

$M^k \to 0$（$k \to \infty$）当且仅当 $M$ 的所有特征值满足 $|\rho_j| < 1$，即谱半径 $\rho(M) < 1$。

- 若所有 $|\rho_j| < 1$，则 $M^k \to 0$，由 $(\dagger)$ 得 $x(t) \to 0$：**渐近稳定**。
- 若某个 $|\rho_j| > 1$，取 $c$ 为对应的（广义）特征向量方向，则 $\|M^k c\| \to \infty$：**不稳定**。

$\square$

### 总结

1. $\Phi(t) = P(t)\, e^{Bt}$，$P$ 以 $T$ 为周期。 ✓
2. 一般解 $x(t) = P(t)\, e^{Bt}\, c$。 ✓
3. 稳定性由 Floquet 乘子 $\rho_j = \sigma(M)$ 的模决定。 ✓

$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明的核心是一个简洁的代数观察：
> 1. **周期性 $\Rightarrow$ 递推关系**：$A(t+T) = A(t)$ 蕴含 $\Phi(t+T) = \Phi(t) M$；
> 2. **矩阵对数**：将 $M = e^{BT}$ "展开"为连续时间的指数增长；
> 3. **分离变量**：$P(t) = \Phi(t) e^{-Bt}$ 自动继承周期性——这是因为 $\Phi$ 每过一个周期右乘 $M$，而 $e^{Bt}$ 每过一个周期也右乘 $e^{BT} = M$，两者恰好抵消。
>
> 直观图景：周期系统的解是"**在周期轨道上骑行的指数波**"——$P(t)$ 描述每个周期内的振荡细节，$e^{Bt}$ 描述周期间的包络增长或衰减。

> [!warning] 注意事项与应用
> - **$B$ 不唯一**：矩阵对数有无穷多个分支（$B$ 可替换为 $B + \frac{2\pi i k}{T} I$），但 Floquet 乘子 $\rho_j = e^{\mu_j T}$ 是唯一确定的。
> - **$B$ 可能为复矩阵**：即使 $A(t)$ 为实矩阵，$B$ 也可能为复数（当 $M$ 有负实特征值时）。此时可改用周期 $2T$，使 $B$ 取实值。
> - **经典应用**：
>   - **Mathieu 方程** $y'' + (a + b\cos 2t)\, y = 0$：参数 $(a,b)$ 平面中的稳定/不稳定区域由 Floquet 乘子是否穿越单位圆决定。
>   - **Hill 方程**：一般周期势下的 Schrödinger 方程，Floquet 理论给出能带结构。
>   - **参数共振**：当 Floquet 乘子恰好在单位圆上时，微小扰动可导致不稳定——这是秋千"泵"的数学原理。
