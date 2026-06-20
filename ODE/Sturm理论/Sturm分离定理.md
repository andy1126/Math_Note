---
title: Sturm 分离定理
date: 2026-04-11
tags:
  - 常微分方程
  - 二阶线性ODE
  - Sturm理论
  - Wronskian
  - 零点
---

# Sturm 分离定理

## 预备定义

> [!note] 二阶齐次线性 ODE
> 设 $p, q: I \to \mathbb{R}$ 为开区间 $I$ 上的连续函数。**二阶齐次线性 ODE** 为
> $$y'' + p(t)\, y' + q(t)\, y = 0. \quad \cdots (E)$$
> 该方程的解空间是二维线性空间：任意两个线性无关解 $y_1, y_2$ 构成一组基。

> [!note] Wronskian（二阶情形）
> 对 $(E)$ 的两个解 $y_1, y_2$，其 **Wronskian** 为
> $$W(t) = y_1(t)\, y_2'(t) - y_1'(t)\, y_2(t) = \det \begin{pmatrix} y_1 & y_2 \\ y_1' & y_2' \end{pmatrix}.$$

> [!abstract] 引理：Abel 公式（Liouville 公式的二阶特殊情形）
> 对 $(E)$ 的任意两个解 $y_1, y_2$，其 Wronskian 满足
> $$W(t) = W(t_0) \exp\!\left(-\int_{t_0}^{t} p(s)\, ds\right).$$

**证明**：将 $(E)$ 改写为一阶系统 $\mathbf{x}' = A(t)\, \mathbf{x}$，其中

$$A(t) = \begin{pmatrix} 0 & 1 \\ -q(t) & -p(t) \end{pmatrix}, \quad \operatorname{tr}(A) = -p(t).$$

由 [[Liouville公式]]，$W(t) = W(t_0)\exp\!\left(\int_{t_0}^{t} \operatorname{tr}(A(s))\, ds\right) = W(t_0)\exp\!\left(-\int_{t_0}^{t} p(s)\, ds\right)$。$\square$

> [!important] Abel 公式的关键推论
> 由于 $\exp(\cdot) > 0$，Wronskian $W(t)$ 要么**恒为零**（$y_1, y_2$ 线性相关），要么**处处非零**（$y_1, y_2$ 线性无关）。线性无关时 $W$ 在整个 $I$ 上保持定号。

---

## 定理

设 $y_1, y_2$ 为 $(E)$ 的两个**线性无关**解。则 $y_1$ 的任意两个相邻零点之间恰好有 $y_2$ 的一个零点。

等价地：$y_1$ 和 $y_2$ 的零点在实轴上**严格交替排列**。

---

## 证明

设 $\alpha < \beta$ 为 $y_1$ 的两个**相邻**零点，即

$$y_1(\alpha) = y_1(\beta) = 0, \quad y_1(t) \neq 0 \;\;\forall\, t \in (\alpha, \beta).$$

证明分两部分：$y_2$ 在 $(\alpha, \beta)$ 内至少有一个零点，且至多有一个零点。

### 第一部分：$y_2$ 在 $(\alpha, \beta)$ 内至少有一个零点

**反证法**：假设 $y_2$ 在 $[\alpha, \beta]$ 上不变号，即 $y_2(t) \neq 0$ 对一切 $t \in (\alpha, \beta)$。不妨设 $y_2(t) > 0$ 在 $(\alpha, \beta)$ 上（否则换 $-y_2$）。

#### 第一步：确定 $y_1$ 在 $(\alpha, \beta)$ 上的符号与端点导数

$y_1$ 在 $(\alpha, \beta)$ 上不变号（因 $\alpha, \beta$ 是相邻零点）。不妨设 $y_1(t) > 0$ 在 $(\alpha, \beta)$ 上。

由 $y_1(\alpha) = 0$ 且 $y_1(t) > 0$ 在 $\alpha$ 右侧，得

$$y_1'(\alpha) \geq 0. \quad \cdots (1)$$

由 $y_1(\beta) = 0$ 且 $y_1(t) > 0$ 在 $\beta$ 左侧，得

$$y_1'(\beta) \leq 0. \quad \cdots (2)$$

> [!info] 为何不等式严格成立
> 事实上 $y_1'(\alpha) > 0$ 且 $y_1'(\beta) < 0$。若 $y_1'(\alpha) = 0$，则 $y_1(\alpha) = y_1'(\alpha) = 0$，由唯一性 $y_1 \equiv 0$，矛盾。同理排除 $y_1'(\beta) = 0$。但下文只需非严格不等式即可得到矛盾。

$\square$

#### 第二步：利用 Wronskian 得到矛盾

在 $t = \alpha$ 处：

$$W(\alpha) = y_1(\alpha)\, y_2'(\alpha) - y_1'(\alpha)\, y_2(\alpha) = -y_1'(\alpha)\, y_2(\alpha).$$

由 $y_1'(\alpha) > 0$（见上注）和 $y_2(\alpha) \geq 0$，得

$$W(\alpha) \leq 0. \quad \cdots (3)$$

在 $t = \beta$ 处：

$$W(\beta) = y_1(\beta)\, y_2'(\beta) - y_1'(\beta)\, y_2(\beta) = -y_1'(\beta)\, y_2(\beta).$$

由 $y_1'(\beta) < 0$ 和 $y_2(\beta) \geq 0$，得

$$W(\beta) \geq 0. \quad \cdots (4)$$

但由 Abel 公式，$W$ 在 $I$ 上保持定号（$y_1, y_2$ 线性无关故 $W$ 处处非零）。

$(3)$ 与 $(4)$ 合在一起要求 $W(\alpha) \leq 0$ 且 $W(\beta) \geq 0$，而 $W$ 不变号且不为零——**矛盾！**

故假设不成立，$y_2$ 在 $(\alpha, \beta)$ 内至少有一个零点。$\square$

### 第二部分：$y_2$ 在 $(\alpha, \beta)$ 内至多有一个零点

**反证法**：假设 $y_2$ 在 $(\alpha, \beta)$ 内有两个零点 $\gamma_1 < \gamma_2$。

交换 $y_1$ 和 $y_2$ 的角色：$\gamma_1, \gamma_2$ 是 $y_2$ 的两个零点（未必相邻，但无妨）。由第一部分的论证（对 $y_2$ 的**任意**两个零点之间应用），$y_1$ 在 $(\gamma_1, \gamma_2) \subseteq (\alpha, \beta)$ 内至少有一个零点。

> [!important] 对称性论证
> 第一部分的证明对 $y_1$ 和 $y_2$ 是完全对称的：只要一个解有两个零点，另一个解在其间必有零点。这里我们对 $y_2$ 的两个零点应用同样的结论。

但 $\alpha, \beta$ 是 $y_1$ 的**相邻**零点，$y_1$ 在 $(\alpha, \beta)$ 上无零点——**矛盾！**

故 $y_2$ 在 $(\alpha, \beta)$ 内至多有一个零点。$\square$

### 总结

综合两部分：
1. $y_2$ 在 $(\alpha, \beta)$ 内至少有一个零点。 ✓
2. $y_2$ 在 $(\alpha, \beta)$ 内至多有一个零点。 ✓

因此 $y_1$ 的任意两个相邻零点之间**恰好**有 $y_2$ 的一个零点，即两组零点严格交替排列。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明的两个核心工具：
> 1. **Wronskian 的定号性**（由 Abel/Liouville 公式）：$W$ 处处非零且不变号，这是线性无关性的"刚性"体现；
> 2. **端点处 Wronskian 的符号分析**：在 $y_1$ 的零点处，$W = -y_1' \cdot y_2$，于是 $y_2$ 的符号被 $W$ 的定号性所约束。
>
> 第二部分巧妙地利用了**对称性**：第一部分的结论对任意一对线性无关解都成立，将 $y_1, y_2$ 角色互换即得上界。
>
> 直观图景：两个线性无关解像两条"交替穿越零轴"的波——当一个在零轴上方时，另一个必须穿越一次零轴，形成严格的交错格局。

> [!warning] 推广与限制
> - **Sturm 比较定理**是分离定理的推广：若 $q_1(t) \leq q_2(t)$，则 $y'' + q_2\, y = 0$ 的解的零点比 $y'' + q_1\, y = 0$ 的解"更密集"。分离定理是 $q_1 = q_2$ 的特殊情形。
> - **高阶方程**：Sturm 分离定理**不能**直接推广到三阶及以上的 ODE。三阶方程的两个线性无关解的零点可以不交替排列。
> - **奇异端点**：当 $I$ 为无界区间时，零点可能积聚于无穷远处（如 $y'' + y = 0$ 的解 $\sin t, \cos t$，零点以 $\pi$ 为间距交替排列直至 $\pm\infty$）。
