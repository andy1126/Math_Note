---
title: 有界区间上单调有界函数的 Riemann 可积性
date: 2026-04-11
tags:
  - 实分析
  - Riemann积分
  - 单调函数
  - Darboux和
---

# 有界区间上单调有界函数的 Riemann 可积性

## 预备定义

> [!note] Riemann 可积的判定准则
> 有界函数 $f: [a, b] \to \mathbb{R}$ 是 Riemann 可积的，当且仅当对任意 $\varepsilon > 0$，存在分划 $P = \{x_0, \dots, x_n\}$ 使得
> $$U(f, P) - L(f, P) = \sum_{k=1}^{n} (M_k - m_k)\, \Delta x_k < \varepsilon,$$
> 其中 $M_k = \sup_{[x_{k-1}, x_k]} f$，$m_k = \inf_{[x_{k-1}, x_k]} f$。

> [!abstract] 引理：有界单调函数在端点有单侧极限
> 设 $f: (a, b) \to \mathbb{R}$ 单调递增且有界。则 $\lim_{x \to a^+} f(x)$ 与 $\lim_{x \to b^-} f(x)$ 均存在且有限。

**证明**：$\{f(x) : x \in (a,b)\}$ 有下界，由确界原理 $L = \inf_{x \in (a,b)} f(x)$ 存在。对任意 $\varepsilon > 0$，存在 $x_0 \in (a,b)$ 使得 $f(x_0) < L + \varepsilon$。对任意 $x \in (a, x_0)$，由单调性 $L \leq f(x) \leq f(x_0) < L + \varepsilon$，故 $|f(x) - L| < \varepsilon$。取 $\delta = x_0 - a$ 即得 $\lim_{x \to a^+} f(x) = L$。右端极限类似。$\square$

---

## 定理

设 $I$ 为有界区间，$f: I \to \mathbb{R}$ 既是单调的又是有界的。则 $f$ 是 Riemann 可积的。

---

## 证明

### 前提准备：归结为闭区间上的单调函数

若 $I$ 退化（$\varnothing$ 或单点），结论平凡。设 $I$ 有端点 $a < b$。

不失一般性设 $f$ 单调递增（递减的情形用 $-f$ 替代即可）。

由引理，$f$ 在 $(a,b)$ 上的单侧极限存在。定义 $\tilde{f}: [a, b] \to \mathbb{R}$：

$$\tilde{f}(x) = \begin{cases} \lim_{t \to a^+} f(t), & x = a \text{ 且 } a \notin I, \\ \lim_{t \to b^-} f(t), & x = b \text{ 且 } b \notin I, \\ f(x), & x \in I. \end{cases}$$

则 $\tilde{f}$ 在 $[a, b]$ 上仍单调递增。

> [!info] 为何延拓保持单调性
> 设 $a \notin I$。令 $L = \lim_{t \to a^+} f(t) = \inf_{(a,b)} f$。对任意 $x \in (a,b)$，$\tilde{f}(a) = L \leq f(x) = \tilde{f}(x)$。类似地在 $b$ 端。故 $\tilde{f}$ 单调递增。

又 $\tilde{f}$ 与 $f$ 至多在两个端点处不同，Riemann 可积性不受影响。故不失一般性，设

$$f: [a, b] \to \mathbb{R} \text{ 单调递增}. \quad \square$$

---

### 核心证明：等距分划与伸缩求和

#### 第一步：构造等距分划

对任意正整数 $n$，取等距分划

$$P_n = \{x_0, x_1, \dots, x_n\}, \quad x_k = a + k \cdot \frac{b - a}{n}.$$

每个子区间长度 $\Delta x_k = \dfrac{b - a}{n}$。$\square$

#### 第二步：利用单调性确定极值

由 $f$ 单调递增，在 $[x_{k-1}, x_k]$ 上：

$$m_k = f(x_{k-1}), \qquad M_k = f(x_k).$$

$\square$

#### 第三步：伸缩求和

$$U(f, P_n) - L(f, P_n) = \sum_{k=1}^{n} [f(x_k) - f(x_{k-1})] \cdot \frac{b-a}{n} = \frac{b-a}{n} \sum_{k=1}^{n} [f(x_k) - f(x_{k-1})].$$

求和为伸缩和：

$$\sum_{k=1}^{n} [f(x_k) - f(x_{k-1})] = f(b) - f(a).$$

故

$$U(f, P_n) - L(f, P_n) = \frac{(b - a)[f(b) - f(a)]}{n}. \quad \cdots (\ast)$$

$\square$

#### 第四步：验证判定准则

对任意 $\varepsilon > 0$：

- 若 $f(a) = f(b)$（$f$ 为常函数），则 $(\ast) = 0 < \varepsilon$，取 $n = 1$ 即可。
- 若 $f(a) < f(b)$，由 Archimedes 性质取正整数 $n > \dfrac{(b-a)[f(b)-f(a)]}{\varepsilon}$，则

$$U(f, P_n) - L(f, P_n) = \frac{(b - a)[f(b) - f(a)]}{n} < \varepsilon.$$

由 Riemann 可积的判定准则，$f$ 在 $[a, b]$ 上 Riemann 可积。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明分两层：
>
> 1. **归结**：有界单调函数在端点有单侧极限（确界原理），故可延拓为 $[a,b]$ 上的单调函数，归结为闭区间情形（见 [[有界闭区间上的单调函数是 Riemann 可积的]]）；
> 2. **等距分划 + 伸缩求和**：单调性保证 $M_k - m_k = f(x_k) - f(x_{k-1})$，等距分划提出公因子后得到伸缩和 $f(b) - f(a)$，最终
> $$U - L = \frac{(b-a)[f(b) - f(a)]}{n} \to 0.$$
>
> 本质上，单调函数的振幅总量被锁定为 $f(b) - f(a)$，分划越细每份摊得越薄。

> [!warning] 有界性的角色
> 在闭区间 $[a,b]$ 上，单调性自动蕴含有界（$f$ 在端点取到极值）。但对一般有界区间（如开区间 $(a,b)$），单调函数可以无界（例如 $f(x) = 1/x$ 在 $(0,1)$ 上单调递减但无界）。因此"有界"这一假设在非闭区间情形下不可省略——它保证了单侧极限有限，从而延拓可行。
