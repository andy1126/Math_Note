---
title: Poincaré-Bendixson 定理
date: 2026-04-11
tags:
  - 常微分方程
  - 动力系统
  - 平面系统
  - 极限集
  - 周期轨道
  - Jordan曲线定理
---

# Poincaré-Bendixson 定理

## 预备定义

> [!note] 平面自治系统
> 考虑 $\mathbb{R}^2$ 上的自治系统
> $$x' = f(x), \quad x \in \mathbb{R}^2,$$
> 其中 $f: D \to \mathbb{R}^2$（$D \subseteq \mathbb{R}^2$ 为开集）连续可微。记 $\varphi_t(x_0)$ 为初值 $x_0$ 对应的解在时刻 $t$ 的值（流映射）。

> [!note] $\omega$-极限集
> 对轨道 $\{\varphi_t(x_0) : t \geq 0\}$，其 **$\omega$-极限集**定义为
> $$\omega(x_0) = \bigcap_{T \geq 0} \overline{\{\varphi_t(x_0) : t \geq T\}}.$$
> 等价地，$p \in \omega(x_0)$ 当且仅当存在序列 $t_n \to +\infty$ 使得 $\varphi_{t_n}(x_0) \to p$。
>
> 直观含义：$\omega(x_0)$ 是轨道在 $t \to +\infty$ 时"趋向"的集合。

> [!note] 横截线段（transversal）
> 设 $p$ 为非平衡点（$f(p) \neq 0$）。过 $p$ 作一条短线段 $\Sigma$，使得 $f$ 在 $\Sigma$ 上处处与 $\Sigma$ 横截（不相切）。称 $\Sigma$ 为**横截线段**。
>
> 横截线段的存在性由 $f(p) \neq 0$ 和连续性保证：取 $\Sigma$ 垂直于 $f(p)$ 即可。

> [!abstract] 引理 1：$\omega$-极限集的基本性质
> 若正半轨道 $\{\varphi_t(x_0) : t \geq 0\}$ 包含在 $D$ 的某个紧子集中，则 $\omega(x_0)$ 是非空、紧致、连通的，且关于流 $\varphi_t$ **正向和反向不变**（即 $\varphi_t(\omega(x_0)) = \omega(x_0)$ 对一切 $t \in \mathbb{R}$）。

**证明概要**：非空性由紧集中序列必有收敛子列；紧致性由闭集套定义中的交集为闭集，包含在紧集中故紧致；连通性由递减闭集套的交集连通（每个 $\overline{\{\varphi_t(x_0) : t \geq T\}}$ 是轨道弧的闭包，连通）；不变性由流的连续性和极限的交换。$\square$

> [!abstract] 引理 2：轨道穿越横截线段的单调性
> 设 $\Sigma$ 为过非平衡点 $p$ 的横截线段。若轨道 $\varphi_t(x_0)$ 在时刻 $t_1 < t_2 < t_3$ 依次穿越 $\Sigma$ 于点 $p_1, p_2, p_3$，则 $p_2$ 位于 $p_1$ 和 $p_3$ 之间（在 $\Sigma$ 的线性序下）。
>
> 即：轨道对 $\Sigma$ 的连续穿越点沿 $\Sigma$ **单调排列**。

**证明概要**：由 $\varphi_{[t_1, t_2]}(x_0)$（从 $p_1$ 到 $p_2$ 的轨道弧）与 $\Sigma$ 上从 $p_2$ 到 $p_1$ 的线段围成一个 Jordan 曲线 $\Gamma$。由 **Jordan 曲线定理**，$\Gamma$ 将平面分为内部和外部。

> [!important] Jordan 曲线定理的核心作用
> 这是 Poincaré-Bendixson 定理本质上依赖于**二维**的地方。Jordan 曲线定理在 $\mathbb{R}^3$ 中不成立（闭曲线不分割空间），故整个论证在三维及以上失效。

由流的连续性和 $\Sigma$ 的横截性，$\varphi_{t_2}(x_0) = p_2$ 之后的轨道从 $\Gamma$ 的一侧出发。下一次穿越 $\Sigma$ 时，轨道必须从 $\Gamma$ 的同一侧穿越，故 $p_3$ 位于 $p_1$ 和 $p_2$ 之间的同一侧——即 $p_2$ 介于 $p_1$ 和 $p_3$ 之间。

归纳应用，穿越点沿 $\Sigma$ 单调排列。$\square$

---

## 定理

设 $x' = f(x)$ 为 $\mathbb{R}^2$ 上的连续可微自治系统。设正半轨道 $\gamma^+ = \{\varphi_t(x_0) : t \geq 0\}$ 包含在某个紧集 $K \subset D$ 中。则 $\omega(x_0)$ 恰为以下三种情形之一：

**(i)** 单个平衡点；

**(ii)** 一条周期轨道；

**(iii)** 由有限个平衡点和连接它们的轨道（同宿轨道或异宿轨道）构成的图。

**特别地**（最常用的形式）：若 $\omega(x_0)$ 不含平衡点，则 $\omega(x_0)$ 是一条**周期轨道**。

---

## 证明（不含平衡点的情形）

以下证明定理的核心特殊情形：

**假设 $\omega(x_0)$ 不含平衡点。证明 $\omega(x_0)$ 是一条周期轨道。**

### 第一步：$\omega$-极限集中取一点并构造横截线段

取 $p \in \omega(x_0)$。由假设 $f(p) \neq 0$，过 $p$ 作横截线段 $\Sigma$（足够短，使得 $\Sigma$ 上无平衡点且 $f$ 与 $\Sigma$ 处处横截）。

由 $p \in \omega(x_0)$ 的定义，存在序列 $t_n \to +\infty$ 使得 $\varphi_{t_n}(x_0) \to p$。当 $n$ 足够大时，$\varphi_{t_n}(x_0)$ 落在 $\Sigma$ 的邻域内。由流的横截性，轨道在 $t_n$ 附近穿越 $\Sigma$，记穿越点为 $q_n \in \Sigma$。

> [!info] 穿越点 vs 逼近点
> $q_n$ 是轨道实际穿越 $\Sigma$ 的点，与 $\varphi_{t_n}(x_0)$ 略有不同但 $q_n \to p$（因 $\varphi_{t_n}(x_0) \to p$ 且流横截于 $\Sigma$）。

$\square$

### 第二步：穿越点的单调性与收敛

由引理 2，穿越点 $q_1, q_2, q_3, \ldots$ 沿 $\Sigma$ 单调排列。

$\Sigma$ 是 $\mathbb{R}$ 中的有界区间（将 $\Sigma$ 参数化后），单调有界序列必收敛：

$$q_n \to q^\ast \in \Sigma \quad (n \to \infty). \quad \cdots (\ast)$$

$\square$

### 第三步：证明 $q^\ast = p$

由 $q_n \to p$（第一步）和 $q_n \to q^\ast$（第二步），极限的唯一性给出

$$q^\ast = p. \quad \cdots (\star)$$

$\square$

### 第四步：$p$ 的轨道是周期轨道

由 $\omega(x_0)$ 的不变性（引理 1），$p \in \omega(x_0)$ 意味着过 $p$ 的完整轨道 $\{\varphi_t(p) : t \in \mathbb{R}\}$ 包含在 $\omega(x_0)$ 中。

**证明 $\varphi_t(p)$ 是周期的**：

考虑 $p$ 自身的轨道 $\varphi_t(p)$。由 $p \in \omega(x_0)$，$p$ 也是自身轨道的 $\omega$-极限点（因为 $\omega(x_0)$ 是不变闭集，$\varphi_t(p)$ 的 $\omega$-极限集 $\subseteq \omega(x_0)$）。

> [!important] 关键论证
> 实际上可以更直接地证明：$p$ 的轨道也必须穿越 $\Sigma$。由于 $p \in \Sigma$ 且 $f(p)$ 与 $\Sigma$ 横截，$\varphi_t(p)$ 从 $p$ 出发后立即离开 $\Sigma$。轨道 $\varphi_t(p)$ 包含在紧集 $\omega(x_0)$ 中，故有界。类似第一步和第二步的论证，$\varphi_t(p)$ 必须在某个时刻 $\tau > 0$ 回到 $\Sigma$。

设 $\varphi_\tau(p) = p' \in \Sigma$ 为轨道首次回到 $\Sigma$ 的点。

**断言 $p' = p$**：

轨道弧 $\{\varphi_t(p) : 0 \leq t \leq \tau\}$ 与 $\Sigma$ 上从 $p'$ 到 $p$ 的线段（若 $p' \neq p$）构成 Jordan 曲线。由引理 2 的单调性论证，$x_0$ 的轨道的后续穿越点必须落在 $p$ 和 $p'$ 之间。但 $q_n \to p$，而单调序列的极限是端点，故 $p' = p$。

因此 $\varphi_\tau(p) = p$，即 $\varphi_t(p)$ 是周期为 $\tau$ 的周期轨道。$\square$

### 第五步：$\omega(x_0)$ 恰好等于这条周期轨道

记 $\Gamma = \{\varphi_t(p) : 0 \leq t \leq \tau\}$ 为过 $p$ 的周期轨道。已知 $\Gamma \subseteq \omega(x_0)$。

**证明 $\omega(x_0) \subseteq \Gamma$**：

任取 $q \in \omega(x_0)$。由 $f(q) \neq 0$，过 $q$ 作横截线段 $\Sigma'$。重复第一步至第四步的论证：$x_0$ 的轨道穿越 $\Sigma'$ 的点单调收敛至某个 $q^\ast \in \omega(x_0) \cap \Sigma'$，且过 $q^\ast$ 的轨道为周期轨道。

由 $\omega(x_0)$ 的连通性（引理 1），$\omega(x_0)$ 中不能包含两条不相交的周期轨道（它们各自为闭集，不相交则 $\omega(x_0)$ 不连通）。故过 $q^\ast$ 的周期轨道就是 $\Gamma$，即 $q^\ast \in \Gamma$。

由 $q \in \omega(x_0)$ 的任意性，$\omega(x_0) \subseteq \Gamma$。

### 总结

$$\omega(x_0) = \Gamma = \{\varphi_t(p) : 0 \leq t \leq \tau\},$$

即 $\omega(x_0)$ 是一条周期轨道。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明的三大支柱：
>
> 1. **横截线段上的单调性**（引理 2）：轨道每次穿越横截线段的交点沿 $\Sigma$ 单调排列——这是 **Jordan 曲线定理**（平面拓扑）的直接推论；
> 2. **单调有界序列收敛**（实分析）：穿越点 $\{q_n\}$ 在有界线段上单调 $\Rightarrow$ 收敛至极限 $q^\ast = p$；
> 3. **不变性 + 连通性**（动力系统）：$\omega(x_0)$ 关于流不变且连通，故其中的周期轨道是唯一的。
>
> 核心逻辑链：
> $$\text{轨道有界} \xrightarrow{\text{紧致性}} \omega \neq \varnothing \xrightarrow{\text{横截 + Jordan}} \text{穿越点单调} \xrightarrow{\text{收敛}} \text{回到同一点} \xrightarrow{} \text{周期轨道}$$
>
> 本质上，这是**平面拓扑对动力学的刚性约束**：在二维中，轨道无法"绕开"自己之前走过的路（Jordan 曲线定理），被迫回到起点形成闭合。

> [!warning] 维数限制与混沌
> - **三维及以上 Poincaré-Bendixson 定理不成立**。经典反例：Lorenz 系统
> $$\dot{x} = \sigma(y-x), \quad \dot{y} = x(\rho-z)-y, \quad \dot{z} = xy - \beta z$$
> 的轨道被困在紧集中但 $\omega$-极限集既不是平衡点也不是周期轨道——它是**奇异吸引子**（strange attractor），具有分形结构。
> - **推论：平面自治系统中不存在混沌**。Poincaré-Bendixson 定理将平面流的长时间行为限制为平衡点或周期振荡，排除了任何更复杂的非游荡行为。混沌至少需要三个维度。
> - **离散情形**：平面上的离散动力系统（迭代映射）**可以**产生混沌（如 Hénon 映射），因为 Jordan 曲线定理的论证不适用于离散轨道。
