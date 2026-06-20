---
title: Arzelà–Ascoli 定理
date: 2026-05-23
tags:
  - 实分析
  - 泛函分析
  - 函数序列
  - 紧致性
  - 等度连续
  - 一致收敛
---

# Arzelà–Ascoli 定理

## 预备定义

> [!note] 一致有界（uniformly bounded）
> 设 $\mathcal{F}$ 为定义在集合 $K$ 上的函数族，取值于 $\mathbb{R}^d$。称 $\mathcal{F}$ **一致有界**，若存在常数 $M > 0$，使得
> $$|f(x)| \leq M, \quad \forall\, f \in \mathcal{F},\; \forall\, x \in K.$$

> [!note] 等度连续（equicontinuous）
> 设 $(K, d_K)$ 为度量空间，$\mathcal{F}$ 为 $K$ 上取值于 $\mathbb{R}^d$ 的函数族。称 $\mathcal{F}$ 在 $K$ 上**等度连续**，若
> $$\forall\, \varepsilon > 0,\; \exists\, \delta > 0,\; \forall\, f \in \mathcal{F},\; \forall\, x, y \in K:\; d_K(x, y) < \delta \;\Longrightarrow\; |f(x) - f(y)| < \varepsilon.$$
>
> **关键**：$\delta$ 与 $f$ 无关。这比"$\mathcal{F}$ 中每个 $f$ 都一致连续"更强——每个 $f$ 都有同一个 $\delta$。

> [!note] 一致收敛
> 设 $f_n, f: K \to \mathbb{R}^d$。称 $f_n$ 在 $K$ 上**一致收敛**于 $f$（记作 $f_n \rightrightarrows f$），若
> $$\lim_{n \to \infty} \sup_{x \in K} |f_n(x) - f(x)| = 0.$$

> [!abstract] 引理（紧致度量空间的可分性）
> 紧致度量空间 $(K, d_K)$ 是**可分的**：存在 $K$ 的可数稠密子集 $\{x_k\}_{k \in \mathbb{N}}$。

**证明**：对每个 $n \in \mathbb{N}^*$，由紧致性，$K$ 可以被有限个半径 $\tfrac{1}{n}$ 的开球覆盖。取这些球的球心组成有限集 $D_n$。令 $D = \bigcup_{n} D_n$，则 $D$ 至多可数。

对任意 $x \in K$ 与 $\varepsilon > 0$，取 $n$ 充分大使 $\tfrac{1}{n} < \varepsilon$。$x$ 必在 $D_n$ 中某球心 $y$ 的 $\tfrac{1}{n}$ 邻域内，即 $d_K(x, y) < \tfrac{1}{n} < \varepsilon$。故 $D$ 在 $K$ 中稠密。$\square$

> [!abstract] 引理（Bolzano–Weierstrass，作为黑箱）
> $\mathbb{R}^d$ 中的有界序列存在收敛子列。

---

## 定理

设 $(K, d_K)$ 为**紧致**度量空间，$\{f_n\}_{n \in \mathbb{N}}$ 为 $K \to \mathbb{R}^d$ 的连续函数序列。若：

1. $\{f_n\}$ **一致有界**；
2. $\{f_n\}$ **等度连续**，

则 $\{f_n\}$ 存在在 $K$ 上**一致收敛**的子列。

---

## 证明

证明分为两个核心步骤：

- **第一步**：用**对角线论证**抽取在可数稠密子集上点点收敛的子列；
- **第二步**：用**等度连续性**将点点收敛升级为一致收敛。

### 第一步：用对角线论证抽取点点收敛子列

由紧致度量空间可分性引理，取 $K$ 的可数稠密子集 $D = \{x_1, x_2, x_3, \ldots\}$。

#### 第一子步：在 $x_1$ 处提取收敛子列

由一致有界性，存在 $M$ 使 $|f_n(x_1)| \leq M$ 对一切 $n$ 成立。即 $\{f_n(x_1)\}$ 为 $\mathbb{R}^d$ 中有界序列。

由 Bolzano–Weierstrass 定理，存在子列 $\{f_n^{(1)}\} \subseteq \{f_n\}$ 使得 $\{f_n^{(1)}(x_1)\}$ 收敛。

#### 第二子步：递归提取嵌套子列

假设已构造子列 $\{f_n^{(k)}\}$ 使得 $\{f_n^{(k)}(x_j)\}$ 对一切 $j \leq k$ 收敛。由一致有界，$\{f_n^{(k)}(x_{k+1})\}$ 是 $\mathbb{R}^d$ 中有界序列，从中再抽取子列 $\{f_n^{(k+1)}\} \subseteq \{f_n^{(k)}\}$ 使得 $\{f_n^{(k+1)}(x_{k+1})\}$ 收敛。

由归纳，$\{f_n^{(k+1)}\}$ 在 $x_1, \ldots, x_{k+1}$ 处均点点收敛。

#### 第三子步：对角线序列

定义**对角线子列** $g_n := f_n^{(n)}$。则 $\{g_n\}$ 是 $\{f_n\}$ 的子列（每个 $g_n$ 是 $f_n^{(n)}$，而 $\{f_n^{(n)}\}_{n \geq k}$ 是 $\{f_n^{(k)}\}$ 的子列）。

> [!important] 对角线技巧的核心
> 对任意固定的 $k$，序列 $\{g_n\}_{n \geq k}$ 是 $\{f_n^{(k)}\}$ 的子列。而 $\{f_n^{(k)}\}$ 在 $x_k$ 处收敛，故 $\{g_n(x_k)\}$ 也收敛。

由此，$\{g_n\}$ 在 $D$ 的**每个点上**都收敛。$\square$

### 第二步：用等度连续性升级到一致收敛

**目标**：证明 $\{g_n\}$ 是关于上确界范数 $\|\cdot\|_\infty$ 的 Cauchy 序列，从而在完备空间 $C(K; \mathbb{R}^d)$ 中一致收敛。

#### 第一子步：选定参数

任给 $\varepsilon > 0$。

由等度连续性，存在 $\delta > 0$，使
$$d_K(x, y) < \delta \;\Longrightarrow\; |g_n(x) - g_n(y)| < \frac{\varepsilon}{3}, \quad \forall\, n. \quad \cdots (\star)$$

由 $K$ 紧致与 $D$ 稠密，存在有限个 $x_{k_1}, \ldots, x_{k_N} \in D$ 使得
$$K \subseteq \bigcup_{i=1}^{N} B(x_{k_i}, \delta). \quad \cdots (\dagger)$$

> [!info] 为何可以取有限个稠密点
> 开球 $\{B(y, \delta) : y \in D\}$ 是 $K$ 的开覆盖（由 $D$ 稠密）。由 $K$ 紧致，存在有限子覆盖。取该子覆盖的球心即得 $x_{k_1}, \ldots, x_{k_N}$。

#### 第二子步：在有限点集上控制下标

对每个 $i = 1, \ldots, N$，$\{g_n(x_{k_i})\}$ 收敛，故是 Cauchy 序列。存在 $N_i$ 使
$$n, m \geq N_i \;\Longrightarrow\; |g_n(x_{k_i}) - g_m(x_{k_i})| < \frac{\varepsilon}{3}.$$

取 $N_0 = \max\{N_1, \ldots, N_N\}$（仅由 $\varepsilon$ 决定，不依赖具体的 $x \in K$）。

#### 第三子步：三角不等式合成

对任意 $x \in K$，由 $(\dagger)$ 存在 $i$ 使 $d_K(x, x_{k_i}) < \delta$。

对 $n, m \geq N_0$，
$$
\begin{aligned}
|g_n(x) - g_m(x)| &\leq \underbrace{|g_n(x) - g_n(x_{k_i})|}_{\text{由 }(\star)\text{，}<\,\varepsilon/3} + \underbrace{|g_n(x_{k_i}) - g_m(x_{k_i})|}_{\text{由第二子步，}<\,\varepsilon/3} + \underbrace{|g_m(x_{k_i}) - g_m(x)|}_{\text{由 }(\star)\text{，}<\,\varepsilon/3} \\
&< \frac{\varepsilon}{3} + \frac{\varepsilon}{3} + \frac{\varepsilon}{3} = \varepsilon.
\end{aligned}
$$

此估计对一切 $x \in K$ 成立，故
$$\sup_{x \in K} |g_n(x) - g_m(x)| \leq \varepsilon, \quad \forall\, n, m \geq N_0.$$

即 $\{g_n\}$ 是 $(C(K; \mathbb{R}^d), \|\cdot\|_\infty)$ 中的 Cauchy 序列。$\square$

#### 第四子步：完备性收尾

$C(K; \mathbb{R}^d)$ 在上确界范数下完备（连续函数的一致极限仍连续）。故 Cauchy 序列 $\{g_n\}$ 在 $C(K; \mathbb{R}^d)$ 中一致收敛。

### 总结

综合两步：
1. 对角线子列 $\{g_n\} \subseteq \{f_n\}$ 在 $K$ 上的可数稠密集 $D$ 上点点收敛。 ✓
2. 由等度连续性 + $K$ 紧致，$\{g_n\}$ 是上确界范数下的 Cauchy 序列，故一致收敛于某个连续函数。 ✓

故 $\{f_n\}$ 存在一致收敛的子列。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明展示了**"紧致性 = 一致有界 + 等度连续"** 在函数空间中的精确刻画。三个条件各司其职：
> 1. **一致有界** $\Longrightarrow$ 每点上的取值序列在 $\mathbb{R}^d$ 中有界 $\Longrightarrow$ Bolzano–Weierstrass 可用；
> 2. **等度连续** $\Longrightarrow$ 全局共享的 $\delta$ 让有限多个稠密点的控制传播到整个 $K$；
> 3. **$K$ 紧致** $\Longrightarrow$ 可分（保证可数稠密集）+ 有限子覆盖（让"有限"在三角不等式中起作用）。
>
> **核心技巧**：
> - **Cantor 对角线**：从一族嵌套子列中抽取一个对所有"测试点"都收敛的子列；
> - **三段 $\varepsilon/3$ 估计**：将一致估计分解为"局部连续性 + 点点收敛 + 局部连续性"。

> [!warning] 各条件均不可去
> - **去掉一致有界**：$f_n(x) = n$（常值），等度连续但无收敛子列。
> - **去掉等度连续**：$f_n(x) = \sin(nx)$ 在 $[0, 2\pi]$ 上一致有界但不等度连续，无一致收敛子列（虽有弱收敛于 $0$）。
> - **去掉 $K$ 紧致**：在 $K = \mathbb{R}$ 上，$f_n(x) = \arctan(x - n)$ 一致有界、等度连续，但仅点点收敛于 $-\pi/2$，**非一致收敛**。

> [!info] 等价表述（紧致性版本）
> 在 Banach 空间 $C(K; \mathbb{R}^d)$（$K$ 紧致）中，子集 $\mathcal{F}$ 是**相对紧致**（即闭包紧致）的充要条件为：$\mathcal{F}$ 一致有界且等度连续。
> 这一表述称为 **Arzelà–Ascoli 刻画定理**。

---

## 应用

### 应用一：Peano 存在定理（ODE 存在性，无需 Lipschitz）

考虑初值问题
$$\begin{cases} y'(t) = f(t, y(t)), \\ y(t_0) = y_0, \end{cases}$$
其中 $f$ 仅在某矩形邻域 $R = [t_0 - a, t_0 + a] \times \overline{B}(y_0, b) \subset \mathbb{R} \times \mathbb{R}^d$ 上**连续**（不假设 Lipschitz）。

#### 构造逼近序列

设 $|f| \leq M$ 于 $R$，取 $h = \min(a, b/M)$。

对每个 $n$，构造 **Euler 折线** $y_n: [t_0, t_0 + h] \to \mathbb{R}^d$：将 $[t_0, t_0 + h]$ $n$ 等分，令 $t_k = t_0 + kh/n$，递推
$$y_n(t_0) = y_0, \quad y_n(t_{k+1}) = y_n(t_k) + f(t_k, y_n(t_k)) \cdot (t_{k+1} - t_k),$$
在区间 $[t_k, t_{k+1}]$ 上线性插值。

#### 验证 Arzelà–Ascoli 的条件

- **一致有界**：因 $|y_n(t) - y_0| \leq M \cdot h \leq b$，故 $\{y_n\}$ 取值始终在 $\overline{B}(y_0, b)$ 内，进而 $|y_n| \leq |y_0| + b$ 一致界。
- **等度连续**：$|y_n(t) - y_n(s)| \leq M |t - s|$（折线斜率有界），故 $\{y_n\}$ Lipschitz 等度连续，取 $\delta = \varepsilon/M$ 即可。

由 Arzelà–Ascoli，存在子列 $y_{n_k} \rightrightarrows y$。

#### 验证 $y$ 是积分方程的解

通过对 $y_{n_k}(t) = y_0 + \int_{t_0}^{t} f_{n_k}(s) ds$ 取极限（其中 $f_{n_k}$ 是 $f(t, y_{n_k})$ 的阶梯近似），利用 $f$ 的一致连续性，可证
$$y(t) = y_0 + \int_{t_0}^{t} f(s, y(s)) \, ds.$$

即 $y$ 为 ODE 的解。

> [!important] 与 Picard–Lindelöf 的本质对比
> | | Picard–Lindelöf | Peano |
> |---|---|---|
> | 工具 | Banach 不动点定理 | Arzelà–Ascoli 定理 |
> | $f$ 的条件 | 连续 + Lipschitz | 仅连续 |
> | 解的性质 | 存在**唯一** | 存在（**可能不唯一**） |
> | 方法 | Picard 迭代（构造性） | Euler 折线 + 紧致抽取（**非构造性**） |
>
> **不唯一性反例**：$y' = 2\sqrt{|y|}$，$y(0) = 0$，有 $y \equiv 0$ 与 $y = t^2 \mathrm{sgn}(t)$ 等无穷多个解。$f(y) = 2\sqrt{|y|}$ 在 $0$ 附近非 Lipschitz。

---

### 应用二：Montel 定理（复变函数论）

> [!abstract] Montel 定理
> 设 $\Omega \subseteq \mathbb{C}$ 为开集，$\mathcal{F}$ 为 $\Omega$ 上全纯函数族。若 $\mathcal{F}$ 在 $\Omega$ 的每个紧子集上一致有界，则 $\mathcal{F}$ 是**正规族**（normal family），即每个序列都有在 $\Omega$ 紧子集上一致收敛的子列。

#### 与 Arzelà–Ascoli 的连接

关键观察：**全纯函数族的一致有界自动蕴含其等度连续**。

由 Cauchy 积分公式，对任意紧子集 $K \subset \Omega$，存在更大的紧集 $K' \supset K$ 与常数 $C$ 使得
$$|f'(z)| \leq C \|f\|_{K'}, \quad \forall\, z \in K,\; \forall\, f \in \mathcal{F}.$$

由 $\mathcal{F}$ 一致有界，$|f'|$ 在 $K$ 上一致有界，故 $\mathcal{F}$ 在 $K$ 上 Lipschitz 等度连续。

应用 Arzelà–Ascoli 定理于 $K$ 即得一致收敛子列。

> [!tip] Montel 是 Arzelà–Ascoli 的"复变特化"
> 在复变中，全纯性自动让"有界 $\Rightarrow$ 等度连续"，这一桥梁在实变情形中是没有的。Montel 定理是单连通区域上 Riemann 映射定理证明的关键工具。

---

### 应用三：变分法中极小化序列的紧致性

考虑泛函极小化问题：在某容许函数类 $\mathcal{A} \subset C(K)$ 中极小化 $J: \mathcal{A} \to \mathbb{R}$。

**经典策略**：取极小化序列 $\{u_n\} \subset \mathcal{A}$ 使 $J(u_n) \to \inf_\mathcal{A} J$。

#### 若 $\mathcal{A}$ 一致有界且等度连续

由 Arzelà–Ascoli，存在子列 $u_{n_k} \rightrightarrows u^*$。

若 $\mathcal{A}$ 是 $C(K)$ 闭子集，则 $u^* \in \mathcal{A}$；若 $J$ 关于一致收敛下半连续，则
$$J(u^*) \leq \liminf_{k \to \infty} J(u_{n_k}) = \inf_\mathcal{A} J.$$

故 $u^*$ 实现极小值。

> [!info] 直接方法的精神
> 变分法的"直接方法"（direct method）的标准三步就是：**紧致性 + 下半连续性 = 极小元存在**。Arzelà–Ascoli 是经典情形下提供紧致性的核心工具；现代框架中更多用弱紧致性（Banach–Alaoglu）。

---

### 应用四：连续函数空间中相对紧致集的刻画

**结论**：在 $C(K; \mathbb{R}^d)$（$K$ 紧致度量空间）中，子集 $\mathcal{F}$ 相对紧致（其闭包紧致）当且仅当：

1. $\mathcal{F}$ 一致有界；
2. $\mathcal{F}$ 等度连续。

#### 必要性

设 $\overline{\mathcal{F}}$ 紧致。则 $\overline{\mathcal{F}}$ 在 $\|\cdot\|_\infty$ 下有界（紧致集有界），即 $\mathcal{F}$ 一致有界。

任给 $\varepsilon > 0$，由紧致性 $\overline{\mathcal{F}}$ 可被有限个半径 $\varepsilon/3$ 的球 $B(g_i, \varepsilon/3)$（$i = 1, \ldots, N$）覆盖。每个 $g_i$ 单独连续，因 $K$ 紧致而一致连续，存在 $\delta_i$。取 $\delta = \min_i \delta_i$。

对任意 $f \in \mathcal{F}$，存在 $i$ 使 $\|f - g_i\|_\infty < \varepsilon/3$。当 $d_K(x, y) < \delta$ 时，
$$|f(x) - f(y)| \leq |f(x) - g_i(x)| + |g_i(x) - g_i(y)| + |g_i(y) - f(y)| < \varepsilon.$$

故 $\mathcal{F}$ 等度连续。

#### 充分性

即 Arzelà–Ascoli 定理本身——任意序列有一致收敛子列，故 $\overline{\mathcal{F}}$ 列紧，在度量空间中即紧致。

---

## 总结表：Arzelà–Ascoli 在各领域的扮演

| 应用领域 | 函数族 $\mathcal{F}$ | 一致有界的来源 | 等度连续的来源 | 结论 |
|---------|-------------------|--------------|--------------|-----|
| Peano 存在定理 | Euler 折线 $\{y_n\}$ | $|f| \leq M$ | Lipschitz 斜率界 | ODE 解存在 |
| Montel 定理 | 全纯函数族 | 直接假设 | Cauchy 估计自动给出 | 全纯函数正规族 |
| 变分法 | 极小化序列 | 容许类性质 | 容许类性质 | 极小元存在 |
| $C(K)$ 紧致刻画 | 一般子集 | 充要条件 | 充要条件 | 相对紧致 ⟺ 二条件 |

> [!tip] Arzelà–Ascoli 的哲学意义
> 该定理回答了一个根本问题：**"在无穷维函数空间 $C(K)$ 中，哪些集合是紧致的？"**
>
> 在有限维 $\mathbb{R}^d$ 中，紧致 ⟺ 有界 + 闭（Heine–Borel）。
> 在无穷维 $C(K)$ 中，仅有界 + 闭**远远不够**，必须额外要求等度连续——这种"协调一致的局部行为"才是无穷维紧致性的实质。
>
> 这是从有限维分析进入无穷维分析时必须建立的新直觉。
