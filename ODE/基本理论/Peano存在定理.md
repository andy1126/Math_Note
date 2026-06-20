---
title: Peano 存在定理
date: 2026-04-11
tags:
  - 常微分方程
  - 初值问题
  - Euler折线法
  - Arzelà-Ascoli定理
  - 等度连续
---

# Peano 存在定理

## 预备定义

> [!note] 初值问题（IVP）
> 给定连续函数 $f: U \to \mathbb{R}^n$（$U \subseteq \mathbb{R} \times \mathbb{R}^n$ 为开集）和初始条件 $(t_0, y_0) \in U$，**初值问题**是求函数 $y: I \to \mathbb{R}^n$ 使得
> $$y'(t) = f(t, y(t)), \quad y(t_0) = y_0.$$

> [!note] 等度连续
> 设 $\mathcal{F} \subseteq C([a,b], \mathbb{R}^n)$ 为函数族。称 $\mathcal{F}$ **等度连续**（equicontinuous），若对任意 $\varepsilon > 0$，存在 $\delta > 0$，使得对一切 $\varphi \in \mathcal{F}$ 及一切 $s, t \in [a,b]$，
> $$|s - t| < \delta \implies \|\varphi(s) - \varphi(t)\| < \varepsilon.$$
> 关键在于 $\delta$ 对 $\mathcal{F}$ 中**所有函数统一成立**。

> [!note] 一致有界
> 函数族 $\mathcal{F} \subseteq C([a,b], \mathbb{R}^n)$ 称为**一致有界的**（uniformly bounded），若存在 $C > 0$，使得
> $$\|\varphi\|_\infty \leq C \quad \forall\, \varphi \in \mathcal{F}.$$

> [!abstract] Arzelà-Ascoli 定理
> 设 $\mathcal{F} \subseteq C([a,b], \mathbb{R}^n)$。若 $\mathcal{F}$ 一致有界且等度连续，则 $\mathcal{F}$ 的任意序列都有一致收敛的子列。
> （即 $\mathcal{F}$ 在 $(C([a,b], \mathbb{R}^n), \|\cdot\|_\infty)$ 中相对紧致。）

> [!note] Euler 折线（Euler polygonal approximation）
> 给定步长 $h > 0$，**Euler 折线**是用逐步线性逼近构造 IVP 近似解的方法：
> - 令 $t_k = t_0 + kh$；
> - 在每个节点上令 $y_{k+1} = y_k + h \, f(t_k, y_k)$；
> - 在 $[t_k, t_{k+1}]$ 上线性插值，得到分段线性的连续函数。

---

## 定理

设 $f: [t_0 - a, \, t_0 + a] \times \overline{B}(y_0, b) \to \mathbb{R}^n$ 连续。令

$$M = \max_{(t,y) \in [t_0-a, \, t_0+a] \times \overline{B}(y_0, b)} \|f(t, y)\|, \qquad \delta = \min\!\left(a, \, \frac{b}{M}\right).$$

则初值问题

$$y'(t) = f(t, y(t)), \quad y(t_0) = y_0$$

在区间 $[t_0 - \delta, \, t_0 + \delta]$ 上**至少有一个**解。

> [!info] 与 Picard-Lindelöf 定理的对比
> Picard-Lindelöf 定理要求 $f$ 关于 $y$ 满足 Lipschitz 条件，得到**存在且唯一**。Peano 定理仅要求 $f$ 连续，得到**存在但未必唯一**。代价是证明方法从 Banach 不动点定理变为 Arzelà-Ascoli 紧致性论证，且丧失了唯一性。

---

## 证明

不失一般性，仅在 $[t_0, t_0 + \delta]$ 上证明（$[t_0 - \delta, t_0]$ 上的证明完全类似，令 $\tau = -t$ 即可）。

证明分三个阶段：构造 Euler 折线近似解序列，证明该序列有收敛子列，最后验证极限是 IVP 的解。

### 第一阶段：构造 Euler 折线近似解

对每个 $m \in \mathbb{N}^+$，取步长 $h_m = \delta / m$，令 $t_k^{(m)} = t_0 + k h_m$（$k = 0, 1, \ldots, m$）。

递推定义节点值：

$$y_0^{(m)} = y_0, \qquad y_{k+1}^{(m)} = y_k^{(m)} + h_m \, f\!\left(t_k^{(m)}, \, y_k^{(m)}\right).$$

在 $[t_k^{(m)}, \, t_{k+1}^{(m)}]$ 上线性插值，定义 $\varphi_m: [t_0, t_0 + \delta] \to \mathbb{R}^n$：

$$\varphi_m(t) = y_k^{(m)} + (t - t_k^{(m)}) \, f\!\left(t_k^{(m)}, \, y_k^{(m)}\right), \quad t \in [t_k^{(m)}, \, t_{k+1}^{(m)}]. \quad \cdots (\ast)$$

#### 第一步：$\varphi_m$ 的值落在 $\overline{B}(y_0, b)$ 内

对 $t \in [t_k^{(m)}, \, t_{k+1}^{(m)}]$，由 $(\ast)$ 递推得

$$\|\varphi_m(t) - y_0\| \leq \|y_k^{(m)} - y_0\| + h_m M \leq k h_m M + h_m M = (k+1) h_m M \leq m h_m M = \delta M \leq b.$$

> [!info] 归纳细节
> 上述估计用到归纳：$\|y_k^{(m)} - y_0\| \leq k h_m M$。基础情形 $k=0$ 显然；归纳步骤由 $\|y_{k+1}^{(m)} - y_0\| \leq \|y_k^{(m)} - y_0\| + h_m \|f(t_k^{(m)}, y_k^{(m)})\| \leq kh_mM + h_mM$ 得到。

故 $\varphi_m$ 的构造是良定义的（每步的 $f$ 值都在定义域内取到）。$\square$

#### 第二步：$\varphi_m$ 是 Lipschitz 连续的

对任意 $s, t \in [t_0, t_0 + \delta]$，

$$\|\varphi_m(t) - \varphi_m(s)\| \leq M |t - s|. \quad \cdots (\star)$$

**证明**：在每段 $[t_k^{(m)}, t_{k+1}^{(m)}]$ 上，$\varphi_m$ 的斜率为 $f(t_k^{(m)}, y_k^{(m)})$，其范数 $\leq M$。对跨越多段的 $s < t$，由三角不等式逐段累加即得。$\square$

### 第二阶段：提取一致收敛的子列

#### 第一步：$\{\varphi_m\}$ 一致有界

由第一阶段第一步，$\|\varphi_m(t) - y_0\| \leq b$ 对一切 $m$ 和一切 $t$ 成立，故

$$\|\varphi_m\|_\infty \leq \|y_0\| + b \quad \forall\, m. \quad \square$$

#### 第二步：$\{\varphi_m\}$ 等度连续

由 $(\star)$，对任意 $\varepsilon > 0$，取 $\delta_0 = \varepsilon / M$，则

$$|t - s| < \delta_0 \implies \|\varphi_m(t) - \varphi_m(s)\| \leq M \cdot \delta_0 = \varepsilon \quad \forall\, m.$$

故 $\{\varphi_m\}$ 等度连续。$\square$

#### 第三步：应用 Arzelà-Ascoli 定理

由一致有界性和等度连续性，Arzelà-Ascoli 定理保证存在子列 $\{\varphi_{m_j}\}$ 和连续函数 $y: [t_0, t_0+\delta] \to \mathbb{R}^n$，使得

$$\varphi_{m_j} \to y \quad \text{一致收敛} \quad (j \to \infty). \quad \cdots (\dagger)$$

由 $\|\varphi_m(t) - y_0\| \leq b$，极限函数亦满足 $\|y(t) - y_0\| \leq b$。$\square$

### 第三阶段：验证极限函数是 IVP 的解

**目标**：证明 $y$ 满足积分方程

$$y(t) = y_0 + \int_{t_0}^{t} f(s, y(s)) \, ds. \quad \cdots (\ddagger)$$

由微积分基本定理，$(\ddagger)$ 蕴含 $y'(t) = f(t, y(t))$ 且 $y(t_0) = y_0$。

#### 第一步：Euler 折线满足的近似积分方程

由 $(\ast)$，$\varphi_m$ 在每段上的导数（除节点外处处存在）为

$$\varphi_m'(t) = f\!\left(t_k^{(m)}, \, y_k^{(m)}\right) \quad \text{当 } t \in (t_k^{(m)}, t_{k+1}^{(m)}).$$

对 $[t_0, t]$ 积分：

$$\varphi_m(t) = y_0 + \int_{t_0}^{t} f\!\left(\tau_m(s), \, \varphi_m(\tau_m(s))\right) ds, \quad \cdots (\S)$$

其中 $\tau_m(s) = t_k^{(m)}$ 当 $s \in [t_k^{(m)}, t_{k+1}^{(m)})$（即 $\tau_m$ 将 $s$ 向左取到最近的网格点）。

注意 $|\tau_m(s) - s| \leq h_m = \delta/m \to 0$。$\square$

#### 第二步：被积函数一致收敛于 $f(s, y(s))$

需证

$$f\!\left(\tau_{m_j}(s), \, \varphi_{m_j}(\tau_{m_j}(s))\right) \to f(s, y(s)) \quad \text{一致于 } s \in [t_0, t_0+\delta].$$

**论证**：

- $\tau_{m_j}(s) \to s$ 一致收敛（因 $|\tau_{m_j}(s) - s| \leq h_{m_j} \to 0$）；
- 由 $(\star)$，$\|\varphi_{m_j}(\tau_{m_j}(s)) - \varphi_{m_j}(s)\| \leq M h_{m_j} \to 0$ 一致于 $s$；
- 由 $(\dagger)$，$\varphi_{m_j}(s) \to y(s)$ 一致收敛；
- 故 $\varphi_{m_j}(\tau_{m_j}(s)) \to y(s)$ 一致收敛；
- $f$ 在紧集 $[t_0 - a, t_0 + a] \times \overline{B}(y_0, b)$ 上连续，因而一致连续。

> [!important] 一致连续性的核心运用
> $f$ 在紧集上连续 $\Rightarrow$ $f$ 一致连续。这使得 $(\tau_{m_j}(s), \varphi_{m_j}(\tau_{m_j}(s))) \to (s, y(s))$ 的一致收敛可以"穿过" $f$，得到被积函数的一致收敛。

综合以上，$f(\tau_{m_j}(s), \varphi_{m_j}(\tau_{m_j}(s))) \to f(s, y(s))$ 一致于 $s$。$\square$

#### 第三步：取极限得到积分方程

在 $(\S)$ 中令 $m = m_j \to \infty$。左边由 $(\dagger)$ 得 $\varphi_{m_j}(t) \to y(t)$。右边由第二步的一致收敛，积分与极限可交换：

$$\int_{t_0}^{t} f\!\left(\tau_{m_j}(s), \, \varphi_{m_j}(\tau_{m_j}(s))\right) ds \to \int_{t_0}^{t} f(s, y(s)) \, ds.$$

故

$$y(t) = y_0 + \int_{t_0}^{t} f(s, y(s)) \, ds,$$

即 $y$ 满足积分方程 $(\ddagger)$，从而 $y$ 是 IVP 在 $[t_0, t_0 + \delta]$ 上的解。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明的核心是**构造逼近 + 紧致性提取极限**的经典分析范式：
> 1. **Euler 折线**：用分段线性函数 $\varphi_m$ 逼近 ODE 的解，每步沿当前点的方向场走一小段；
> 2. **统一估计**：所有 $\varphi_m$ 都以 $M$ 为 Lipschitz 常数，值域落在 $\overline{B}(y_0, b)$ 中；
> 3. **Arzelà-Ascoli**：一致有界 + 等度连续 $\Rightarrow$ 存在一致收敛的子列；
> 4. **极限传递**：$f$ 在紧集上的一致连续性保证被积函数的一致收敛可穿过积分号。
>
> 对比 Picard-Lindelöf 定理：
> | | Picard-Lindelöf | Peano |
> |---|---|---|
> | 条件 | $f$ 连续 + Lipschitz | $f$ 连续 |
> | 结论 | 存在 + **唯一** | 仅存在 |
> | 方法 | Banach 不动点（压缩映射） | Arzelà-Ascoli（紧致性） |
> | 构造性 | Picard 迭代收敛于唯一解 | 子列收敛，但不知收敛到哪个解 |

> [!warning] 唯一性的丧失
> Peano 定理**不保证唯一性**，经典反例：
> $$y' = \sqrt{|y|}, \quad y(0) = 0.$$
> $f(t,y) = \sqrt{|y|}$ 连续但在 $y = 0$ 处不满足 Lipschitz 条件。该 IVP 有无穷多解（参见 [[Picard-Lindelöf定理]] 中的讨论）。
>
> 事实上，缺乏唯一性并非病态现象：Peano 定理的解集在适当拓扑下构成一个紧致连通集（Kneser 定理），具有丰富的结构。
