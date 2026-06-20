---
title: Lyapunov 稳定性定理（第二方法）
date: 2026-04-11
tags:
  - 常微分方程
  - 稳定性
  - Lyapunov函数
  - 动力系统
  - 平衡点
---

# Lyapunov 稳定性定理

## 预备定义

> [!note] 自治系统与平衡点
> **自治系统**（autonomous system）为
> $$x' = f(x), \quad x \in \mathbb{R}^n,$$
> 其中 $f: D \to \mathbb{R}^n$（$D \subseteq \mathbb{R}^n$ 为包含原点的开集）局部 Lipschitz。
> 称 $x^\ast$ 为**平衡点**（equilibrium），若 $f(x^\ast) = 0$。不失一般性设 $x^\ast = 0$。

> [!note] Lyapunov 稳定性
> 平衡点 $x^\ast = 0$ 称为 **Lyapunov 稳定的**（stable in the sense of Lyapunov），若对任意 $\varepsilon > 0$，存在 $\delta > 0$，使得
> $$\|x(0)\| < \delta \implies \|x(t)\| < \varepsilon \quad \forall\, t \geq 0.$$
> 直观含义：初值足够近则轨道永远留在任意小的邻域内。

> [!note] 渐近稳定性
> 平衡点 $x^\ast = 0$ 称为**渐近稳定的**（asymptotically stable），若：
> 1. 它是 Lyapunov 稳定的；
> 2. 存在 $\delta_0 > 0$，使得 $\|x(0)\| < \delta_0 \implies x(t) \to 0$（$t \to \infty$）。

> [!note] 正定函数
> 连续可微函数 $V: D \to \mathbb{R}$ 称为**正定的**（positive definite），若
> 1. $V(0) = 0$；
> 2. $V(x) > 0$ 对一切 $x \in D \setminus \{0\}$。
>
> 典型例子：$V(x) = x^\top P x$，其中 $P$ 为正定对称矩阵。

> [!note] 沿轨道的导数（Lie 导数）
> 对 $V: D \to \mathbb{R}$ 可微，定义其沿 $x' = f(x)$ 的**轨道导数**为
> $$\dot{V}(x) = \nabla V(x) \cdot f(x) = \sum_{i=1}^{n} \frac{\partial V}{\partial x_i}(x)\, f_i(x).$$
> 这是 $V$ 沿解曲线的变化率：若 $x(t)$ 是解，则 $\frac{d}{dt}V(x(t)) = \dot{V}(x(t))$。
> 关键优势：计算 $\dot{V}$ **不需要求解 ODE**，只需 $V$ 和 $f$ 的表达式。

---

## 定理

设 $x^\ast = 0$ 为 $x' = f(x)$ 的平衡点，$D \subseteq \mathbb{R}^n$ 为包含原点的开集。设 $V: D \to \mathbb{R}$ 连续可微。

**(i)**（**稳定性**）若 $V$ 正定且 $\dot{V}(x) \leq 0$ 对一切 $x \in D$，则 $0$ 是 **Lyapunov 稳定的**。

**(ii)**（**渐近稳定性**）若 $V$ 正定且 $\dot{V}(x) < 0$ 对一切 $x \in D \setminus \{0\}$（即 $\dot{V}$ 负定），则 $0$ 是**渐近稳定的**。

满足上述条件的 $V$ 称为 **Lyapunov 函数**。

---

## 第(i)部分的证明：稳定性

**目标**：对任意 $\varepsilon > 0$，找 $\delta > 0$ 使得 $\|x(0)\| < \delta \implies \|x(t)\| < \varepsilon$ 对一切 $t \geq 0$。

### 第一步：构造 $V$ 的下界

取 $\varepsilon > 0$ 足够小使得 $\overline{B}(0, \varepsilon) \subset D$。令

$$\alpha = \min_{\|x\| = \varepsilon} V(x).$$

> [!important] $\alpha > 0$
> $\{x : \|x\| = \varepsilon\}$ 是紧集，$V$ 连续，故最小值存在。由 $V$ 正定，$V(x) > 0$ 在此集上，故 $\alpha > 0$。

$\square$

### 第二步：由 $V(0) = 0$ 和连续性选取 $\delta$

$V$ 在 $0$ 处连续且 $V(0) = 0$，故存在 $\delta \in (0, \varepsilon)$ 使得

$$\|x\| < \delta \implies V(x) < \alpha. \quad \cdots (\ast)$$

$\square$

### 第三步：证明轨道不穿越 $\|x\| = \varepsilon$

设 $x(t)$ 为满足 $\|x(0)\| < \delta$ 的解。由 $\dot{V} \leq 0$，

$$V(x(t)) \leq V(x(0)) < \alpha \quad \forall\, t \geq 0. \quad \cdots (\star)$$

> [!info] $V$ 沿轨道单调不增
> $\frac{d}{dt}V(x(t)) = \dot{V}(x(t)) \leq 0$，故 $t \mapsto V(x(t))$ 是不增函数。这就是"$V$ 是能量函数，能量不增"的精确含义。

**反证法**：假设存在 $t_1 > 0$ 使得 $\|x(t_1)\| \geq \varepsilon$。由连续性和 $\|x(0)\| < \delta < \varepsilon$，存在 $t^\ast \in (0, t_1]$ 使得 $\|x(t^\ast)\| = \varepsilon$（中值定理）。则

$$V(x(t^\ast)) \geq \min_{\|x\| = \varepsilon} V(x) = \alpha,$$

与 $(\star)$ 矛盾。故 $\|x(t)\| < \varepsilon$ 对一切 $t \geq 0$。$\square$

---

## 第(ii)部分的证明：渐近稳定性

### 第一步：Lyapunov 稳定性已成立

由第(i)部分（$\dot{V} < 0$ 蕴含 $\dot{V} \leq 0$），$0$ 是 Lyapunov 稳定的。取 $\delta_0$ 对应 $\varepsilon_0$（使 $\overline{B}(0, \varepsilon_0) \subset D$），则

$$\|x(0)\| < \delta_0 \implies \|x(t)\| < \varepsilon_0 \quad \forall\, t \geq 0.$$

故轨道 $\{x(t) : t \geq 0\}$ 包含在 $\overline{B}(0, \varepsilon_0) \subset D$ 中，解全局存在（$t^+ = +\infty$，参见 [[解的最大延伸定理]]）。$\square$

### 第二步：$V(x(t))$ 有极限

$V(x(t))$ 沿轨道严格递减且有下界 $0$（由 $V$ 正定）。由单调有界定理，

$$\ell = \lim_{t \to \infty} V(x(t)) \geq 0 \quad \text{存在}. \quad \cdots (\dagger)$$

$\square$

### 第三步：证明 $\ell = 0$

**反证法**：假设 $\ell > 0$。

由 $V(x(t)) \geq \ell > 0 = V(0)$ 及 $V$ 的连续性，轨道 $x(t)$ 远离原点：存在 $r > 0$ 使得

$$\|x(t)\| \geq r \quad \forall\, t \geq 0. \quad \cdots (1)$$

> [!info] 为何 $\|x(t)\| \geq r$
> 若存在 $t_k$ 使得 $\|x(t_k)\| \to 0$，则 $V(x(t_k)) \to V(0) = 0$。由 $V(x(t))$ 单调不增，这迫使 $V(x(t)) \to 0$，即 $\ell = 0$，矛盾。故存在 $r > 0$ 使 $(1)$ 成立。

轨道包含在紧环形区域 $K = \{x : r \leq \|x\| \leq \varepsilon_0\}$ 中。由 $\dot{V}$ 在 $K$ 上连续且 $\dot{V}(x) < 0$ 对 $x \neq 0$，而 $K$ 不含原点，故

$$\beta = \max_{x \in K} \dot{V}(x) < 0. \quad \cdots (2)$$

于是对一切 $t \geq 0$，

$$\frac{d}{dt}V(x(t)) = \dot{V}(x(t)) \leq \beta < 0.$$

积分得

$$V(x(t)) \leq V(x(0)) + \beta\, t.$$

当 $t$ 足够大时右边为负，与 $V \geq 0$ **矛盾！**

故 $\ell = 0$。$\square$

### 第四步：$\ell = 0$ 蕴含 $x(t) \to 0$

需证 $V(x(t)) \to 0 \implies x(t) \to 0$。

**反证法**：假设存在 $\eta > 0$ 和序列 $t_k \to \infty$ 使得 $\|x(t_k)\| \geq \eta$。令

$$\gamma = \min_{\eta \leq \|x\| \leq \varepsilon_0} V(x) > 0$$

（正定性 + 紧集上的最小值）。则 $V(x(t_k)) \geq \gamma > 0$，与 $V(x(t)) \to 0$ 矛盾。

故 $x(t) \to 0$。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> Lyapunov 第二方法的精髓是**用能量替代轨道**：
> 1. **稳定性**：$V$ 正定 + $\dot{V} \leq 0$ $\Rightarrow$ $V$ 是轨道不可穿越的"等高线围墙"。$V(x(0)) < \alpha$ 意味着轨道永远被困在 $\{V < \alpha\}$ 的子水平集内。
> 2. **渐近稳定性**：$\dot{V} < 0$ 意味着能量**严格递减**。由单调有界定理极限存在；若极限 $\ell > 0$，则轨道被困在 $\{V \geq \ell\}$ 的紧集上，$\dot{V}$ 有一致负上界 $\beta < 0$，能量线性下降至负值——矛盾。
>
> 核心不等式链：
> $$\dot{V} \leq 0 \;\Longrightarrow\; V(x(t)) \text{ 不增} \;\Longrightarrow\; x(t) \text{ 被困在子水平集} \;\Longrightarrow\; \text{稳定.}$$
> $$\dot{V} < 0 \;\Longrightarrow\; V(x(t)) \text{ 严格递减} \;\xrightarrow{\text{反证}} \; V \to 0 \;\Longrightarrow\; x \to 0 \;\Longrightarrow\; \text{渐近稳定.}$$

> [!warning] 局限性与推广
> - **构造 Lyapunov 函数是一门艺术**：定理的威力取决于能否找到合适的 $V$。对线性系统 $x' = Ax$，$V(x) = x^\top P x$（其中 $P$ 解 Lyapunov 方程 $A^\top P + PA = -Q$）给出系统性构造。对非线性系统，没有一般性方法。
> - **LaSalle 不变性原理**：当 $\dot{V} \leq 0$（半负定）但不严格负定时，仍可能得到渐近稳定性——只需 $\dot{V} = 0$ 的集合中不包含非平凡的完整轨道。这大大放宽了第(ii)部分的条件。
> - **不稳定性判据**（Chetaev 定理）：若存在 $V$ 使得 $V(0) = 0$，在原点任意邻域中 $V > 0$ 的区域非空，且在此区域上 $\dot{V} > 0$，则 $0$ 不稳定。
> - **Lyapunov 函数的物理来源**：在力学系统中，总能量（动能 + 势能）常是自然的 Lyapunov 函数；耗散力（摩擦）使 $\dot{V} < 0$。
