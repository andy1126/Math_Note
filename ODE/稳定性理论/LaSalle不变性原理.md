---
title: LaSalle 不变性原理
date: 2026-04-11
tags:
  - 常微分方程
  - 动力系统
  - 稳定性
  - Lyapunov函数
  - 极限集
  - 不变集
---

# LaSalle 不变性原理

## 预备定义

> [!note] 自治系统与流
> 考虑自治系统 $x' = f(x)$，其中 $f: D \to \mathbb{R}^n$（$D \subseteq \mathbb{R}^n$ 为开集）局部 Lipschitz。记 $\varphi_t(x_0)$ 为初值 $x_0$ 对应的解在时刻 $t$ 的值。

> [!note] 正向不变集
> 称 $\Omega \subseteq D$ 为**正向不变的**（positively invariant），若对一切 $x_0 \in \Omega$ 和一切 $t \geq 0$，$\varphi_t(x_0) \in \Omega$。
>
> 即：从 $\Omega$ 内出发的轨道永远留在 $\Omega$ 内。

> [!note] $\omega$-极限集
> 对 $x_0 \in D$，其 $\omega$-极限集为
> $$\omega(x_0) = \bigcap_{T \geq 0} \overline{\{\varphi_t(x_0) : t \geq T\}}.$$
> 参见 [[Poincaré-Bendixson定理]] 中的定义。

> [!note] 不变集
> 称 $S \subseteq D$ 为（双向）**不变的**（invariant），若对一切 $x_0 \in S$ 和一切 $t \in \mathbb{R}$，$\varphi_t(x_0) \in S$。

> [!abstract] 引理：$\omega$-极限集的性质
> 若正半轨道 $\gamma^+(x_0)$ 包含在 $D$ 的某个紧子集中，则：
> 1. $\omega(x_0)$ 非空、紧致、连通；
> 2. $\omega(x_0)$ 关于流 $\varphi_t$ **双向不变**；
> 3. $\operatorname{dist}(\varphi_t(x_0), \, \omega(x_0)) \to 0$ 当 $t \to \infty$。

**证明概要**：(1) 同 [[Poincaré-Bendixson定理]] 引理 1。(3) 若否，存在 $\varepsilon > 0$ 和 $t_n \to \infty$ 使得 $\operatorname{dist}(\varphi_{t_n}(x_0), \omega) \geq \varepsilon$。由紧致性取收敛子列 $\varphi_{t_{n_k}}(x_0) \to p$，则 $p \in \omega(x_0)$ 但 $\operatorname{dist}(p, \omega) \geq \varepsilon$，矛盾。$\square$

---

## 定理

设 $\Omega \subset D$ 为紧致的正向不变集。设 $V: D \to \mathbb{R}$ 连续可微，且

$$\dot{V}(x) = \nabla V(x) \cdot f(x) \leq 0 \quad \forall\, x \in \Omega.$$

定义

$$E = \{x \in \Omega : \dot{V}(x) = 0\},$$

并设 $M$ 为 $E$ 中包含的**最大不变集**（即 $E$ 中所有完整轨道都在 $M$ 中的不变子集之并）。

则从 $\Omega$ 中出发的每条轨道都趋向 $M$：

$$\varphi_t(x_0) \to M \quad (t \to \infty) \quad \forall\, x_0 \in \Omega.$$

即 $\omega(x_0) \subseteq M$ 对一切 $x_0 \in \Omega$。

> [!info] 与 Lyapunov 稳定性定理的关系
> [[Lyapunov稳定性定理]] 的第(ii)部分要求 $\dot{V} < 0$ **严格**负定才能得到渐近稳定性。LaSalle 原理将此放宽为 $\dot{V} \leq 0$（半负定），代价是需要分析 $\{\dot{V} = 0\}$ 中的不变集 $M$。
>
> 特别地，若 $M = \{0\}$（即 $\dot{V} = 0$ 的集合中唯一的完整轨道是平衡点），则 $0$ 渐近稳定——即使 $\dot{V}$ 不是严格负定的。

---

## 证明

取任意 $x_0 \in \Omega$。由 $\Omega$ 正向不变且紧致，正半轨道 $\gamma^+(x_0) \subseteq \Omega$（紧集），故 $\omega(x_0)$ 非空、紧致、不变（引理）。

**目标**：证明 $\omega(x_0) \subseteq M$。

### 第一步：$V$ 沿轨道单调不增且有极限

由 $\dot{V} \leq 0$ 在 $\Omega$ 上，

$$\frac{d}{dt}V(\varphi_t(x_0)) = \dot{V}(\varphi_t(x_0)) \leq 0,$$

故 $t \mapsto V(\varphi_t(x_0))$ 单调不增。又 $V$ 在紧集 $\Omega$ 上有下界，由**单调有界定理**，

$$c = \lim_{t \to \infty} V(\varphi_t(x_0)) \quad \text{存在}. \quad \cdots (\ast)$$

$\square$

### 第二步：$V$ 在 $\omega(x_0)$ 上恒等于 $c$

任取 $p \in \omega(x_0)$。由定义，存在 $t_n \to \infty$ 使得 $\varphi_{t_n}(x_0) \to p$。由 $V$ 的连续性和 $(\ast)$，

$$V(p) = \lim_{n \to \infty} V(\varphi_{t_n}(x_0)) = c.$$

由 $p \in \omega(x_0)$ 的任意性，

$$V(q) = c \quad \forall\, q \in \omega(x_0). \quad \cdots (\star)$$

> [!important] $V$ 在 $\omega$-极限集上为常数
> 这是本证明最关键的观察。$V$ 沿轨道单调递减，但在极限集上必须取到同一个值——因为极限集是不变的，轨道在其上既要"前进"又要"停留"，唯一的可能是 $V$ 保持恒定。

$\square$

### 第三步：$\dot{V} = 0$ 在 $\omega(x_0)$ 上

由 $\omega(x_0)$ 的不变性，对任意 $q \in \omega(x_0)$，完整轨道 $\varphi_t(q) \in \omega(x_0)$ 对一切 $t \in \mathbb{R}$。由 $(\star)$，

$$V(\varphi_t(q)) = c \quad \forall\, t \in \mathbb{R}.$$

对 $t$ 求导：

$$\dot{V}(\varphi_t(q)) = \frac{d}{dt}V(\varphi_t(q)) = 0 \quad \forall\, t \in \mathbb{R}.$$

特别地，令 $t = 0$：

$$\dot{V}(q) = 0 \quad \forall\, q \in \omega(x_0).$$

故 $\omega(x_0) \subseteq E = \{\dot{V} = 0\}$。$\square$

### 第四步：$\omega(x_0) \subseteq M$

由第三步，$\omega(x_0) \subseteq E$。又 $\omega(x_0)$ 关于流双向不变（引理），故 $\omega(x_0)$ 是 $E$ 中的不变子集。由 $M$ 的定义（$E$ 中的最大不变集），

$$\omega(x_0) \subseteq M. \quad \square$$

### 第五步：轨道趋向 $M$

由引理第(3)条，$\operatorname{dist}(\varphi_t(x_0), \omega(x_0)) \to 0$。由 $\omega(x_0) \subseteq M$，

$$\operatorname{dist}(\varphi_t(x_0), M) \leq \operatorname{dist}(\varphi_t(x_0), \omega(x_0)) \to 0 \quad (t \to \infty).$$

$\blacksquare$

---

## 应用示例

> [!info] 示例：带摩擦的非线性摆
> 考虑非线性摆方程 $\theta'' + c\,\theta' + \sin\theta = 0$（$c > 0$），改写为系统
> $$x_1' = x_2, \quad x_2' = -\sin x_1 - c\, x_2.$$
>
> 取能量函数 $V(x_1, x_2) = 1 - \cos x_1 + \frac{1}{2}x_2^2$（势能 + 动能）。则 $V$ 正定（在 $|x_1| < \pi$ 附近），且
> $$\dot{V} = x_2 \sin x_1 + x_2(-\sin x_1 - cx_2) = -c\, x_2^2 \leq 0.$$
>
> $\dot{V}$ **不是严格负定的**（当 $x_2 = 0$ 时 $\dot{V} = 0$），故 [[Lyapunov稳定性定理]] 的第(ii)部分不能直接使用。
>
> 但 $E = \{(x_1, x_2) : x_2 = 0\}$。在 $E$ 上，$x_2 = 0$ 且 $x_2' = -\sin x_1$。要使轨道始终留在 $E$ 中，需 $x_2' = 0$，即 $\sin x_1 = 0$，即 $x_1 = 0$。故 $M = \{(0, 0)\}$。
>
> 由 LaSalle 不变性原理，所有从 $\Omega$ 内出发的轨道趋向 $(0,0)$：**渐近稳定**。

---

## 证明思路总结

> [!tip] 关键思想
> LaSalle 原理的证明仅用了三个要素：
>
> 1. **单调有界定理**：$\dot{V} \leq 0$ $\Rightarrow$ $V(\varphi_t(x_0))$ 单调不增且有下界 $\Rightarrow$ 极限 $c$ 存在；
> 2. **$\omega$-极限集的不变性**：轨道在 $\omega(x_0)$ 上双向存在；
> 3. **$V$ 恒等于 $c$ + 不变性 $\Rightarrow$ $\dot{V} \equiv 0$**：在不变集上 $V$ 必须恒定，对 $t$ 求导即得 $\dot{V} = 0$。
>
> 逻辑链：
> $$\dot{V} \leq 0 \;\xrightarrow{\text{单调有界}}\; V|_\omega \equiv c \;\xrightarrow{\text{不变性}}\; \dot{V}|_\omega \equiv 0 \;\Rightarrow\; \omega \subseteq E \;\xrightarrow{\text{不变性}}\; \omega \subseteq M.$$
>
> 本质上，LaSalle 原理表明：**解只能停留在 $V$ 保持恒定的地方**，而 $\dot{V} \leq 0$ 保证解无法离开 $\{V = c\}$。这比要求 $\dot{V} < 0$ 弱得多，但结论几乎一样强。

> [!warning] 注意事项与推广
> - **紧致性假设是必需的**：若 $\Omega$ 不紧致，正半轨道可能逃逸至无穷，$\omega$-极限集可能为空。实践中常取 $\Omega = \{x : V(x) \leq c_0\}$（$V$ 的子水平集）；当 $\dot{V} \leq 0$ 时，子水平集自动正向不变。
> - **径向无界条件**：若 $V(x) \to \infty$ 当 $\|x\| \to \infty$（即 $V$ 径向无界），则每个子水平集 $\{V \leq c_0\}$ 紧致，且所有轨道有界——此时可取 $\Omega = \mathbb{R}^n$ 而无需显式指定紧集。
> - **非自治推广**（Barbalat 引理）：对非自治系统 $x' = f(t,x)$，LaSalle 原理不直接适用（$\omega$-极限集的不变性依赖自治性）。Barbalat 引理提供了替代方案：若 $V(x(t))$ 有下界且 $\dot{V}$ 一致连续，则 $\dot{V}(x(t)) \to 0$。
> - **寻找 $M$ 的方法**：在 $E = \{\dot{V} = 0\}$ 上代入 ODE，求哪些解能永远留在 $E$ 中。通常逐步求导：$\dot{V} = 0$ $\Rightarrow$ $\ddot{V} = 0$ $\Rightarrow$ $\cdots$ 不断收紧约束，直到确定 $M$。
