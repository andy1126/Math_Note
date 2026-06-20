---
title: 辐角原理与 Rouché 定理
date: 2026-05-30
tags:
  - 复分析
  - 辐角原理
  - Rouché定理
  - 零点计数
  - 留数定理
---

# 辐角原理与 Rouché 定理

## 预备定义

> [!note] 亚纯函数
> 设 $\Omega \subset \mathbb{C}$ 开。称 $f$ 在 $\Omega$ **亚纯**（meromorphic），若 $f$ 在 $\Omega$ 上除孤立点（极点）外全纯，且每个孤立点处展开有有限主部。$f$ 的零点与极点均孤立。

> [!note] 零点与极点的阶
> 设 $f$ 在 $z_0$ 处有 $n$ 阶零点：$f(z) = (z - z_0)^n g(z)$，$g(z_0) \neq 0$，$g$ 在 $z_0$ 邻域全纯。
>
> $f$ 在 $z_0$ 处有 $m$ 阶极点：$f(z) = (z - z_0)^{-m} h(z)$，$h(z_0) \neq 0$，$h$ 在 $z_0$ 邻域全纯。

> [!note] 简单闭曲线与回路指标
> 设 $\gamma$ 为 $\mathbb{C}$ 中**正向**（逆时针）的简单可求长闭曲线，$\operatorname{int}(\gamma)$ 为其所围有界区域。对 $z_0 \notin \gamma$，**回路指标**
> $$n(\gamma, z_0) := \frac{1}{2\pi i} \oint_\gamma \frac{dz}{z - z_0}.$$
> 正向简单闭曲线对内部点 $n = 1$，对外部点 $n = 0$。

> [!abstract] 引理：留数定理
> 设 $f$ 在含 $\overline{\operatorname{int}(\gamma)}$ 的开集中亚纯，在 $\gamma$ 上无极点。则
> $$\frac{1}{2\pi i} \oint_\gamma f(z)\,dz = \sum_{k} \operatorname{Res}(f; a_k),$$
> 求和取遍 $\operatorname{int}(\gamma)$ 内的所有极点 $a_k$。详见 [[留数定理]]。

> [!abstract] 引理：对数导数的局部行为
> 若 $f(z) = (z - z_0)^n g(z)$，$g$ 在 $z_0$ 邻域全纯且 $g(z_0) \neq 0$。则
> $$\frac{f'(z)}{f(z)} = \frac{n}{z - z_0} + \frac{g'(z)}{g(z)},$$
> 其中 $g'/g$ 在 $z_0$ 全纯。**故 $\operatorname{Res}(f'/f; z_0) = n$**（零点阶数）。
>
> 对极点 $f(z) = (z - z_0)^{-m} h(z)$ 类似得 $\operatorname{Res}(f'/f; z_0) = -m$。

---

## 定理 A（辐角原理 / Argument Principle）

设 $\Omega$ 开，$\gamma \subset \Omega$ 为正向简单闭曲线，$\overline{\operatorname{int}(\gamma)} \subset \Omega$。$f$ 在 $\Omega$ 中亚纯，且在 $\gamma$ 上既无零点也无极点。记

- $N$ = $f$ 在 $\operatorname{int}(\gamma)$ 中**零点总数**（按阶计重）；
- $P$ = $f$ 在 $\operatorname{int}(\gamma)$ 中**极点总数**（按阶计重）。

则

$$\frac{1}{2\pi i} \oint_\gamma \frac{f'(z)}{f(z)}\,dz = N - P.$$

等价地，"$\arg f$ 沿 $\gamma$ 的总变化量除以 $2\pi$ 等于 $N - P$"：

$$N - P = \frac{1}{2\pi} \Delta_\gamma \arg f = n(f \circ \gamma,\ 0).$$

---

## 证明 A

### 第一步：列举内部的零点与极点

由 $f$ 亚纯且 $\overline{\operatorname{int}(\gamma)}$ 紧致，$f$ 在 $\operatorname{int}(\gamma)$ 中零点 $\{z_j\}$ 与极点 $\{w_k\}$ **有限**（孤立集与紧集相交有限）。设 $z_j$ 阶 $n_j$，$w_k$ 阶 $m_k$。则

$$N = \sum_j n_j, \quad P = \sum_k m_k.$$

### 第二步：对数导数的留数

$f'/f$ 在 $\operatorname{int}(\gamma)$ 中的极点恰为 $\{z_j\} \cup \{w_k\}$。由对数导数引理：

$$\operatorname{Res}(f'/f; z_j) = n_j, \quad \operatorname{Res}(f'/f; w_k) = -m_k.$$

### 第三步：应用留数定理

$f'/f$ 在 $\gamma$ 上全纯（因 $f$ 在 $\gamma$ 上无零点、无极点）。由留数定理：

$$\frac{1}{2\pi i} \oint_\gamma \frac{f'(z)}{f(z)}\,dz = \sum_j n_j - \sum_k m_k = N - P. \quad \square$$

### 第四步：辐角变化的几何含义

形式上 $f'/f = (\log f)'$。沿 $\gamma$ 积分 $\log f = \log|f| + i \arg f$：
- 实部 $\log|f|$ 单值（沿闭曲线起止值相同），积分为 $0$；
- 虚部 $\arg f$ 多值，沿闭曲线累积**总变化量** $\Delta_\gamma \arg f$。

故

$$\oint_\gamma \frac{f'}{f}\,dz = i \Delta_\gamma \arg f \Longrightarrow N - P = \frac{1}{2\pi} \Delta_\gamma \arg f.$$

**几何**：$f \circ \gamma$ 是 $\mathbb{C} \setminus \{0\}$ 中的闭曲线，其绕原点的圈数即 $N - P$。$\blacksquare$

---

## 定理 B（Rouché 定理）

设 $\Omega$、$\gamma$ 如定理 A。$f, g$ 在含 $\overline{\operatorname{int}(\gamma)}$ 的开集上**全纯**。若

$$|f(z) - g(z)| < |f(z)| \quad (\text{或等价地 } < |g(z)|), \quad \forall\, z \in \gamma, \quad \cdots (\mathrm{R})$$

则 $f$ 与 $g$ 在 $\operatorname{int}(\gamma)$ 中**零点总数相同**（按阶计重）。

---

## 证明 B

### 第一步：$f, g$ 在 $\gamma$ 上无零点

由 (R)，对 $z \in \gamma$：若 $f(z) = 0$，则 $|g(z)| = |f(z) - g(z)| < |f(z)| = 0$，矛盾。同理 $g$ 在 $\gamma$ 上无零点。

### 第二步：构造单参数族

对 $t \in [0, 1]$，定义
$$h_t(z) := (1 - t) f(z) + t g(z) = f(z) + t (g(z) - f(z)).$$

$h_t$ 全纯于含 $\overline{\operatorname{int}(\gamma)}$ 的开集。

**$h_t$ 在 $\gamma$ 上无零点**：对 $z \in \gamma$，
$$|h_t(z)| = |f(z) + t(g(z) - f(z))| \geq |f(z)| - t |g(z) - f(z)| > |f(z)| - |f(z)| \cdot 1 = 0$$

（用 (R) 的 $|g - f| < |f|$ 与 $t \leq 1$）。

### 第三步：零点数关于 $t$ 连续

记 $N(t)$ 为 $h_t$ 在 $\operatorname{int}(\gamma)$ 中零点总数。由辐角原理（$h_t$ 全纯故 $P = 0$）：

$$N(t) = \frac{1}{2\pi i} \oint_\gamma \frac{h_t'(z)}{h_t(z)}\,dz.$$

**关键**：被积函数 $h_t'/h_t$ 关于 $(t, z) \in [0, 1] \times \gamma$ **连续**（分母无零点，分子连续）。故 $t \mapsto N(t)$ 关于 $t$ **连续**。

### 第四步：整值连续 $\Rightarrow$ 常数

$N: [0, 1] \to \mathbb{Z}$ 连续 + 整值 $\Rightarrow$ 常数。故 $N(0) = N(1)$，即 $f$ 与 $g$ 零点数相同。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> **辐角原理** = **对数导数留数 + 留数定理**：
> 1. $f'/f$ 的留数等于零点/极点的阶（带号）；
> 2. 留数定理把内部计数翻译为边界积分；
> 3. 几何上 $\oint f'/f\,dz / (2\pi i)$ 就是 $f \circ \gamma$ 绕原点圈数 $= N - P$。
>
> **Rouché 定理** = **辐角原理 + 同伦不变性**：
> 1. 单参数线性插值 $h_t = (1-t) f + tg$ 把 $f$ "连续变形"为 $g$；
> 2. (R) 保证插值过程边界无零点；
> 3. 零点数是整值连续函数 $\Rightarrow$ 常数。
>
> 哲学：**全纯函数的零点数是"边界数据"的拓扑不变量**（辐角的卷绕数）。

> [!important] (R) 条件的几何意义
> $|f - g| < |f|$ 于 $\gamma$ 表示 $g(z)$ 落在以 $f(z)$ 为中心、半径 $|f(z)|$ 的开盘内——这个盘不含原点。所以 $f$ 与 $g$ 沿 $\gamma$ 的辐角差始终 $< \pi/2$（不能"绕原点不同圈数"），故卷绕数相同。
>
> **同伦视角**：在 $\mathbb{C}^\ast = \mathbb{C} \setminus \{0\}$ 中，曲线 $f \circ \gamma$ 与 $g \circ \gamma$ 通过 $h_t \circ \gamma$ 连续同伦，故同伦类相同 $\Rightarrow$ 卷绕数相同。

> [!info] 经典应用
>
> **(1) 代数基本定理**：考虑 $p(z) = z^n + a_{n-1} z^{n-1} + \cdots + a_0$。取 $f(z) = z^n$，$g(z) = p(z)$，$\gamma = \{|z| = R\}$ 充分大。
> $$|g(z) - f(z)| = |a_{n-1} z^{n-1} + \cdots + a_0| \leq C R^{n-1} < R^n = |f(z)|$$
> 当 $R$ 大。Rouché $\Rightarrow$ $g$ 与 $z^n$ 零点数相同 $= n$。**$p$ 恰有 $n$ 个零点**。
>
> **(2) Hurwitz 定理**：若 $f_n \to f$ 一致收敛于紧集，$f_n$ 在 $\Omega$ 上全纯无零点，则 $f$ 要么恒为 $0$ 要么无零点。证明用 Rouché。
>
> **(3) 隐函数定理（全纯版）**：解析方程 $F(z, w) = 0$ 在 $(z_0, w_0)$ 处的解 $w = w(z)$ 局部存在唯一的证明用辐角原理。

> [!info] $\arg$ 变化计算的几何技巧
> 对许多简单函数，$\Delta_\gamma \arg f$ 可几何直接读出。例如 $f(z) = z$、$\gamma = $ 单位圆：$\Delta \arg z = 2\pi$ 故 $N - P = 1$（一阶零点在原点）。
>
> 对多项式 $p(z)$ 沿大圆 $|z| = R$（$R \to \infty$）：$p \sim z^n$，故 $\Delta \arg p \to 2\pi n$。重新证明代数基本定理。

> [!warning] 边界条件不可省
> 辐角原理与 Rouché 都要求**边界 $\gamma$ 上无零点/极点**。若 $f$ 在 $\gamma$ 上有零点：
> - $f'/f$ 在 $\gamma$ 上不连续，积分发散；
> - 内部零点数无法明确定义（边界零点算"内"还是"外"？）。
>
> 实际计算中常通过**扰动 $\gamma$**（取小邻域）规避。

> [!info] 衔接其他笔记
> - **留数定理** ← [[留数定理]]：本笔记的核心工具；
> - **柯西积分公式** ← [[柯西积分公式]]：与辐角原理同源；
> - **最大模原理** ← [[最大模原理与Schwarz引理]]：互补——后者控制 $|f|$，本笔记控制 $f$ 的零点；
> - **Riemann 映射定理** → [[Riemann映射定理]]：单射性证明用辐角原理（双射对应 $\Delta \arg = 2\pi$）；
> - **Nyquist 稳定性判据** → 控制论中，开环传递函数沿 Nyquist 围线的 $\arg$ 变化决定闭环极点数，本质即辐角原理。
