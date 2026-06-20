---
title: 二重积分与Fubini定理
date: 2026-06-18
tags:
  - 多元微积分
  - 二重积分
  - Fubini定理
  - 累次积分
  - Riemann和
  - 矩形分割
---

# 二重积分与Fubini定理

## 预备定义

> [!note] 矩形的分割与Riemann和
> 设 $R = [a, b] \times [c, d]$ 为一有界闭矩形。$R$ 的一个**分割**（partition）$P$ 由 $x$ 和 $y$ 两个方向的分割组成：
> $$P_x: a = x_0 < x_1 < \cdots < x_n = b, \qquad P_y: c = y_0 < y_1 < \cdots < y_m = d.$$
> 子矩形记作
> $$R_{ij} = [x_{i-1}, x_i] \times [y_{j-1}, y_j], \quad \Delta x_i = x_i - x_{i-1},\; \Delta y_j = y_j - y_{j-1},\; \Delta A_{ij} = \Delta x_i \Delta y_j.$$
> 分割的**细度**（mesh）为 $\|P\| = \max_{i,j}\{\Delta x_i, \Delta y_j\}$。
>
> 在每个子矩形中任取样本点 $\boldsymbol{\xi}_{ij} \in R_{ij}$，构造 **Riemann 和**：
> $$S(f, P, \boldsymbol{\xi}) = \sum_{i=1}^{n} \sum_{j=1}^{m} f(\boldsymbol{\xi}_{ij}) \, \Delta A_{ij}.$$
> 若存在数 $I \in \mathbb{R}$，使对任意 $\varepsilon > 0$，存在 $\delta > 0$，只要 $\|P\| < \delta$（且 $\boldsymbol{\xi}_{ij}$ 任意选取），就有
> $$|S(f, P, \boldsymbol{\xi}) - I| < \varepsilon,$$
> 则称 $f$ 在 $R$ 上 **Riemann 可积**，记
> $$\iint_R f = \iint_R f(x,y)\,dA = I.$$

> [!note] 零延拓与一般有界区域上的二重积分
> 设 $D \subseteq \mathbb{R}^2$ 为有界区域，$f: D \to \mathbb{R}$ 有界。取一矩形 $R \supset D$，定义 $f$ 的**零延拓**：
> $$\widetilde{f}(x,y) = \begin{cases} f(x,y), & (x,y) \in D, \\ 0, & (x,y) \in R \setminus D. \end{cases}$$
> 若 $\widetilde{f}$ 在 $R$ 上 Riemann 可积，则称 $f$ 在 $D$ 上**可积**，定义
> $$\iint_D f = \iint_R \widetilde{f}.$$
> 可以证明此定义与包络矩形 $R$ 的选取无关（只要 $R \supset D$）。

> [!note] I 型区域与 II 型区域
> - **I 型区域**（$x$-simple）：存在连续函数 $g_1, g_2: [a,b] \to \mathbb{R}$ 使
>   $$D = \{\, (x,y) \mid a \le x \le b,\; g_1(x) \le y \le g_2(x) \,\}.$$
> - **II 型区域**（$y$-simple）：存在连续函数 $h_1, h_2: [c,d] \to \mathbb{R}$ 使
>   $$D = \{\, (x,y) \mid c \le y \le d,\; h_1(y) \le x \le h_2(y) \,\}.$$
> 许多常见区域既是 I 型又是 II 型；此时 Fubini 定理提供两种累次积分次序。

> [!note] 零测集
> 称 $E \subseteq \mathbb{R}^2$ 为**（二维 Lebesgue）零测集**，若对任意 $\varepsilon > 0$，存在可数个矩形覆盖 $E$ 且其总面积之和 $< \varepsilon$。有限条光滑曲线（例如区域的边界 $\partial D$）均为零测集。

---

## 可积性条件

> [!abstract] 定理（Riemann可积的Lebesgue准则）
> 有界函数 $f$ 在矩形 $R$ 上 Riemann 可积，当且仅当 $f$ 的间断点集为（二维 Lebesgue）零测集。

> [!important] 两个常用推论
> 1. 若 $f$ 在 $D$ 上**连续**，则 $f$ 在 $D$ 上可积（连续 ⇒ 无间断点 ⇒ 间断集为空 ⇒ 零测）。
> 2. 若 $f$ 在 $D$ 上有界且间断点仅落在有限条光滑曲线上，则 $f$ 仍可积（光滑曲线为零测集）。换言之，**“几乎处处连续”的有界函数可积**。
>
> 这条准则在应用中的价值在于：我们通常遇到的函数（连续、分段连续）都自动满足可积条件，从而可以放心使用下述 Fubini 定理。

---

## 基本性质

> [!abstract] 命题（二重积分的基本性质）
> 设 $f, g$ 在 $D$ 上可积。
>
> **线性**：
> $$\iint_D (\alpha f + \beta g) = \alpha \iint_D f + \beta \iint_D g \quad (\alpha, \beta \in \mathbb{R}).$$
>
> **区域可加性**：若 $D = D_1 \cup D_2$ 且 $D_1, D_2$ 的内部不交（至多边界重叠），则
> $$\iint_D f = \iint_{D_1} f + \iint_{D_2} f.$$
>
> **单调性**：若 $f \ge g$ 在 $D$ 上，则
> $$\iint_D f \ge \iint_D g.$$
> 特别地，$f \ge 0 \Rightarrow \iint_D f \ge 0$。
>
> **估值不等式**：若 $m \le f(x,y) \le M$ 对一切 $(x,y) \in D$，则
> $$m \cdot \operatorname{Area}(D) \le \iint_D f \le M \cdot \operatorname{Area}(D).$$
> 其中 $\operatorname{Area}(D) = \iint_D 1$ 为 $D$ 的面积。

这些性质均可从 Riemann 和的定义直接导出：线性来自和的线性，单调性来自每项非负，估值来自 $m \Delta A_{ij} \le f \Delta A_{ij} \le M \Delta A_{ij}$ 逐项放缩。

---

## 定理：Fubini 定理

> [!abstract] 定理（Fubini，矩形情形）
> 设 $f$ 在矩形 $R = [a, b] \times [c, d]$ 上可积。若对每个固定的 $x \in [a, b]$，一元函数 $y \mapsto f(x, y)$ 在 $[c, d]$ 上可积，则
> $$\iint_R f = \int_a^b \left( \int_c^d f(x,y)\,dy \right) dx. \quad \cdots (1)$$
> 对称地，若对每个固定的 $y \in [c, d]$，$x \mapsto f(x,y)$ 在 $[a,b]$ 上可积，则
> $$\iint_R f = \int_c^d \left( \int_a^b f(x,y)\,dx \right) dy. \quad \cdots (2)$$
> 若两种次序的内层单变量可积性均成立，则两种累次积分相等。

> [!abstract] 定理（Fubini，I 型/II 型区域）
> 设 $D$ 为 I 型区域 $D = \{\, (x,y) \mid a \le x \le b,\; g_1(x) \le y \le g_2(x) \,\}$，$f$ 在 $D$ 上可积且对每个 $x$，$y \mapsto f(x,y)$ 在 $[g_1(x), g_2(x)]$ 上可积。则
> $$\iint_D f = \int_a^b \int_{g_1(x)}^{g_2(x)} f(x,y)\,dy\,dx. \quad \cdots (\ast)$$
> 对称地，若 $D$ 为 II 型区域 $D = \{\, (x,y) \mid c \le y \le d,\; h_1(y) \le x \le h_2(y) \,\}$，则
> $$\iint_D f = \int_c^d \int_{h_1(y)}^{h_2(y)} f(x,y)\,dx\,dy.$$

> [!important] Tonelli 定理（非负函数的便利版本）
> 若 $f \ge 0$ 可测（特别地，若 $f \ge 0$ 且 Riemann 可积），则**无须验证内层可积性**：累次积分直接等于二重积分。这也是为什么许多计算题可以“直接迭代”而不担心可积性——被积函数非负（或取绝对值后用 Tonelli 验证可积）。

---

## 证明

### Fubini 定理（矩形情形）的证明

设 $R = [a, b] \times [c, d]$，$f$ 在 $R$ 上可积，记 $I = \iint_R f$。

#### 第一步：将累次积分视为一元函数的积分

对每个 $x \in [a, b]$，由假设 $F(x) := \displaystyle\int_c^d f(x, y)\,dy$ 存在。目标：证 $F$ 在 $[a,b]$ 上可积且 $\int_a^b F(x)\,dx = I$。

#### 第二步：用 Riemann 和的三角不等式建立联系

取 $R$ 的分割 $P = P_x \times P_y$，对 $x$ 方向在子区间 $[x_{i-1}, x_i]$ 中取样本点 $x_i^*$，对 $y$ 方向在 $[y_{j-1}, y_j]$ 中取样本点 $y_j^*$。

考虑双指标 Riemann 和与累次 Riemann 和的差：
$$\left|\sum_i \sum_j f(x_i^*, y_j^*) \Delta x_i \Delta y_j - \sum_i F(x_i^*) \Delta x_i\right|.$$

对于固定的 $i$，内层和 $\sum_j f(x_i^*, y_j^*) \Delta y_j$ 是 $F(x_i^*) = \int_c^d f(x_i^*, y)\,dy$ 的 Riemann 和。由于 $f$ 在 $R$ 上可积，存在精细分割使两者之差受控。

> [!info] 为何 $y$ 方向的可积性对每个 $x$ 不需要？
> 矩形情形定理的假设中包含“对每个 $x$，$y \mapsto f(x,y)$ 可积”——但在应用中，$f$ 连续便自动满足这一条件。证明中最关键的步骤是控制两个极限（二重积分极限与累次积分极限）的交换，实质等同于“二重 Riemann 和的极限 = 先对 $y$ 后对 $x$ 的累次极限”。

#### 第三步：利用可积性的 $\varepsilon$-$\delta$ 刻画

由 $f$ 在 $R$ 上可积：$\forall \varepsilon > 0$，$\exists \delta > 0$，当 $\|P\| < \delta$ 时，对**任意**选取的样本点，
$$\left|\iint_R f - \sum_{i,j} f(x_i^*, y_j^*) \Delta x_i \Delta y_j\right| < \varepsilon.$$

对于 $F(x_i^*)$ 的每个 Riemann 和，任给 $\varepsilon > 0$，可取足够精细的 $y$-分割使
$$\left|\sum_j f(x_i^*, y_j^*) \Delta y_j - F(x_i^*)\right| < \varepsilon.$$

将两者组合：
$$\left|\iint_R f - \sum_i F(x_i^*) \Delta x_i\right| \le \left|\iint_R f - \sum_{i,j} f(x_i^*, y_j^*) \Delta x_i \Delta y_j\right| + \sum_i \left|\sum_j f(x_i^*, y_j^*) \Delta y_j - F(x_i^*)\right| \Delta x_i < \varepsilon + \varepsilon(b-a).$$

这说明 $\sum_i F(x_i^*) \Delta x_i$ 是 $\iint_R f$ 的 Riemann 和逼近，即 $\int_a^b F(x)\,dx = \iint_R f$。$\blacksquare$

### 一般区域情形的推导

设 $D$ 为 I 型区域，$D \subseteq R = [a,b] \times [c,d]$，其中 $c = \min g_1$，$d = \max g_2$。

对 $f$ 做零延拓得到 $\widetilde{f}$，它在 $R$ 上可积。对固定 $x \in [a,b]$：
$$\int_c^d \widetilde{f}(x,y)\,dy = \int_{g_1(x)}^{g_2(x)} f(x,y)\,dy,$$
因为在 $[c, g_1(x)]$ 和 $[g_2(x), d]$ 上 $\widetilde{f} = 0$。

对 $\widetilde{f}$ 应用矩形情形的 Fubini 定理：
$$\iint_D f = \iint_R \widetilde{f} = \int_a^b \left( \int_c^d \widetilde{f}(x,y)\,dy \right) dx = \int_a^b \int_{g_1(x)}^{g_2(x)} f(x,y)\,dy\,dx.$$

即得 $(\ast)$。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> Fubini 定理的实质是**将二维 Riemann 和的极限分解为两次一维 Riemann 和的极限**：
> $$\iint_R f = \lim_{\|P_x\| \to 0} \sum_i \left( \lim_{\|P_y\| \to 0} \sum_j f(x_i^*, y_j^*) \Delta y_j \right) \Delta x_i.$$
> 核心困难在于**交换极限次序**——先取 $y$ 方向的 Riemann 和极限（得到 $F(x_i^*)$），再取 $x$ 方向的 Riemann 和极限。可积性（二重极限的存在性）保证了两种次序的极限相等。
>
> 从矩形推广到一般区域的关键技巧是**零延拓**：把任意有界区域“嵌入”到一个矩形中，边界之外被积函数为 $0$，从而将一般区域的积分转化为矩形积分。

> [!warning] 不可随意换序
> Fubini 定理的前提（二重积分的存在性 + 内层单变量可积性）是实质性的。存在这样的函数：两种累次积分存在且相等，但二重积分本身**不存在**。详见 [[交换二重积分次序]] 的“变形与延伸”部分。计算时通常先确保 $f$ 连续（或分段连续），即可安全应用 Fubini。

---

## 例题

> [!example] 例 1（矩形上的二重积分）
> 计算 $\displaystyle\iint_{[0,2] \times [0,1]} (x^2 + y)\,dA$。

**解**：令 $R = [0,2] \times [0,1]$。被积函数为多项式，连续，满足 Fubini 的条件。先对 $y$ 后对 $x$ 积分：

$$\iint_R (x^2 + y)\,dA = \int_0^2 \int_0^1 (x^2 + y)\,dy\,dx.$$

内层积分（$x$ 视作常数）：
$$\int_0^1 (x^2 + y)\,dy = \left[ x^2 y + \frac{y^2}{2} \right]_{y=0}^{y=1} = x^2 + \frac12.$$

外层积分：
$$\int_0^2 \left(x^2 + \frac12\right) dx = \left[ \frac{x^3}{3} + \frac{x}{2} \right]_0^2 = \frac{8}{3} + 1 = \frac{11}{3}.$$

换序验算（先 $x$ 后 $y$）：
$$\int_0^1 \int_0^2 (x^2 + y)\,dx\,dy = \int_0^1 \left[ \frac{x^3}{3} + xy \right]_{x=0}^{x=2} dy = \int_0^1 \left( \frac{8}{3} + 2y \right) dy = \left[ \frac{8}{3}y + y^2 \right]_0^1 = \frac{11}{3}.$$

两种次序结果一致。$\square$

> [!example] 例 2（I 型区域上的二重积分）
> 设 $D$ 是以 $(0,0)$, $(2,0)$, $(0,1)$ 为顶点的三角形区域。计算 $\displaystyle\iint_D (x + y)\,dA$。

**解**：三角形可视为 I 型区域。斜边方程为 $y = 1 - \dfrac{x}{2}$（两点式：过 $(2,0)$ 与 $(0,1)$）。故
$$D = \{\, (x,y) \mid 0 \le x \le 2,\; 0 \le y \le 1 - \tfrac{x}{2} \,\}.$$

应用 Fubini 定理（I 型形式 $(\ast)$）：
$$\iint_D (x+y)\,dA = \int_0^2 \int_0^{1 - x/2} (x+y)\,dy\,dx.$$

内层积分：
$$\int_0^{1 - x/2} (x+y)\,dy = \left[ xy + \frac{y^2}{2} \right]_{y=0}^{y=1 - x/2} = x\!\left(1 - \frac{x}{2}\right) + \frac{(1 - x/2)^2}{2}.$$

展开：
$$x - \frac{x^2}{2} + \frac{1 - x + x^2/4}{2} = x - \frac{x^2}{2} + \frac12 - \frac{x}{2} + \frac{x^2}{8} = \frac{x}{2} - \frac{3x^2}{8} + \frac12.$$

外层积分：
$$\int_0^2 \left( \frac{x}{2} - \frac{3x^2}{8} + \frac12 \right) dx = \left[ \frac{x^2}{4} - \frac{x^3}{8} + \frac{x}{2} \right]_0^2 = \frac{4}{4} - \frac{8}{8} + \frac{2}{2} = 1 - 1 + 1 = 1.$$

**另解（II 型视角）**：该三角形也是 II 型区域：
$$D = \{\, (x,y) \mid 0 \le y \le 1,\; 0 \le x \le 2(1-y) \,\}.$$
则
$$\iint_D (x+y)\,dA = \int_0^1 \int_0^{2(1-y)} (x+y)\,dx\,dy = \int_0^1 \left[ \frac{x^2}{2} + xy \right]_{x=0}^{x=2-2y} dy = \int_0^1 \left( \frac{(2-2y)^2}{2} + (2-2y)y \right) dy.$$
化简得 $1$（与 I 型结果一致）。$\square$

---

## 相关笔记

- [[极限与连续]] — 可积定义中 Riemann 和的极限；可积性条件的理论基础
- [[格林公式]] — 其核心证明将环路积分转化为二重积分
- [[三重积分]] — 三维区域的类比理论：三重积分与 Fubini 定理的三次迭代
- [[变量替换公式]] — 二重积分的变量替换（极坐标、一般坐标变换）
- [[交换二重积分次序]] — Fubini 定理的典型应用：通过换序化不可能积分为可能
- [[偏导数与方向导数]] — 积分上限含参数时需要偏导
- [[含参量常义积分]] — 矩形 Fubini 是含参量积分"积分号下积分"的理论依据
- [[含参量反常积分]] — 反常情形换序需要一致收敛
- [[Gamma函数与Beta函数]] — Γ(p)Γ(q) 化为二重积分依赖 Fubini 换序
