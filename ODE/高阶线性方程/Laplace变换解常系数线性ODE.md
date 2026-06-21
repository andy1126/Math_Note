---
title: Laplace 变换解常系数线性 ODE
date: 2026-06-20
tags:
  - 微分方程
  - ODE
  - 高阶线性方程
  - Laplace变换
  - 初值问题
  - 脉冲响应
---

# Laplace 变换解常系数线性 ODE

## 预备定义

> [!note] Laplace 变换
> 设 $f: [0, \infty) \to \mathbb{R}$ 分段连续且指数阶增长。其 **Laplace 变换**定义为
> $$F(s) = \mathcal{L}[f](s) := \int_0^{\infty} e^{-st} f(t)\, dt, \quad \operatorname{Re}(s) > \sigma_0.$$
> 详见 [[积分变换与信号处理/]] 中的相关笔记。

> [!note] 常系数线性 IVP
> 考虑 $n$ 阶常系数线性 ODE 配初值：
> $$\begin{cases} a_n y^{(n)} + a_{n-1} y^{(n-1)} + \cdots + a_0 y = g(t), & t \geq 0, \\ y(0) = y_0,\ y'(0) = y_0',\ \ldots,\ y^{(n-1)}(0) = y_0^{(n-1)}. \end{cases} \quad \cdots (\mathrm{IVP})$$
> $a_n \neq 0$，$g$ 分段连续且指数阶增长。

> [!abstract] 引理：导数的 Laplace 变换
> $$\mathcal{L}[y'](s) = s Y(s) - y(0),$$
> $$\mathcal{L}[y''](s) = s^2 Y(s) - s y(0) - y'(0),$$
> 一般地 $\mathcal{L}[y^{(k)}](s) = s^k Y(s) - \sum_{j=0}^{k-1} s^{k-1-j} y^{(j)}(0)$。
> 详见 [[Laplace变换的微分性质]]。

> [!abstract] 引理：逆 Laplace 变换与部分分式
> 有理函数可通过部分分式分解还原为指数 × 多项式 × 三角的组合。基本对应：
> $$\mathcal{L}^{-1}\!\left[\frac{1}{s - a}\right] = e^{at}, \quad \mathcal{L}^{-1}\!\left[\frac{1}{(s - a)^k}\right] = \frac{t^{k-1}}{(k-1)!} e^{at},$$
> $$\mathcal{L}^{-1}\!\left[\frac{s - a}{(s - a)^2 + \beta^2}\right] = e^{at} \cos\beta t, \quad \mathcal{L}^{-1}\!\left[\frac{\beta}{(s - a)^2 + \beta^2}\right] = e^{at} \sin\beta t.$$

---

## 定理

**(i)（代数化）** 对 (IVP) 两端作 Laplace 变换，微分方程化为 $Y(s)$ 的**代数方程**
$$P(s)\, Y(s) = Q(s) + G(s),$$
其中 $P(s) = a_n s^n + \cdots + a_0$ 为特征多项式，$Q(s)$ 为由初值决定的多项式（次数 $< n$），$G(s) = \mathcal{L}[g](s)$。于是
$$Y(s) = \frac{Q(s) + G(s)}{P(s)}.$$

**(ii)（IVP 的解）** $y(t) = \mathcal{L}^{-1}[Y(s)](t)$ 是 (IVP) 的唯一解。Laplace 变换法**一次性同时给出齐次解和特解**，初值自动入账。

**(iii)（传递函数与脉冲响应）** 当所有初值为零时，$Y(s) = G(s)/P(s) =: H(s) G(s)$。其中 $H(s) = 1/P(s)$ 称为系统的**传递函数**（transfer function）。其逆变换 $h(t) = \mathcal{L}^{-1}[1/P(s)]$ 称为**脉冲响应**（impulse response）——即 $g(t) = \delta(t)$ 时的解。

**(iv)（对间断 / 脉冲强迫的优越性）** 当 $g$ 含阶跃 $H(t - a)$、脉冲 $\delta(t - a)$、或分段函数时，Laplace 变换通过平移定理直接处理，而待定系数法需分段拼接。

---

## 证明

### 第(i)部分：代数化

对 (IVP) 两端逐项作 Laplace 变换。利用导数的 Laplace 变换公式：
$$\mathcal{L}[a_k y^{(k)}] = a_k \big(s^k Y(s) - s^{k-1} y(0) - \cdots - y^{(k-1)}(0)\big).$$

将所有 $k = 0, \ldots, n$ 的项相加。$Y(s)$ 的系数收集为 $P(s) = a_n s^n + \cdots + a_0$。与初值有关的项不含 $Y(s)$，收集为多项式 $Q(s)$（次数 $\leq n-1$）。右端 $g(t)$ 的变换记为 $G(s)$。故
$$P(s)\, Y(s) - Q(s) = G(s) \;\Longrightarrow\; Y(s) = \frac{Q(s) + G(s)}{P(s)}. \quad \square$$

### 第(ii)部分：逆变换即解

$Y(s)$ 为有理函数（若 $G(s)$ 也是有理函数或至多含指数因子 $e^{-as}$）。作部分分式分解后逐项逆变换即得表达式中各项。由 Laplace 变换的唯一性（Lerch 定理），所得 $y(t)$ 是满足 (IVP) 的唯一连续解。初值已由 $Q(s)$ 自动满足。$\square$

### 第(iii)部分：传递函数

当初值全为零，$Q(s) \equiv 0$，故 $Y(s) = G(s)/P(s) = H(s) G(s)$。在时域中，由卷积定理（详见 [[Laplace 变换的卷积定理]]）：
$$y(t) = (h * g)(t) = \int_0^t h(t - \tau)\, g(\tau)\, d\tau, \quad h(t) = \mathcal{L}^{-1}[1/P(s)](t).$$

$h(t)$ 的物理意义：当输入为 Dirac $\delta$（单位瞬时脉冲），$G(s) = 1$，$Y(s) = H(s)$，$y = h$。故 $h$ = 脉冲响应。$\square$

### 第(iv)部分：间断强迫

设 $g(t) = H(t - a) f(t - a)$（$a \geq 0$）。由平移定理 $\mathcal{L}[g](s) = e^{-as} F(s)$。此时 $Y(s) = (Q(s) + e^{-as} F(s))/P(s)$，逆变换直接给出含阶梯的显式解——无需在 $t = a$ 处拼接。对含 $\delta$ 的强迫项（如 $g(t) = \delta(t - a)$），$G(s) = e^{-as}$，$y$ 即为平移后的脉冲响应 $h(t - a)$。$\blacksquare$

---

## 一般解法（算法流程）

> [!tip] 用 Laplace 变换解 IVP
> 1. 对方程两端取 Laplace 变换；
> 2. 代入初值，解出代数方程 $Y(s) = (Q(s) + G(s))/P(s)$；
> 3. 将 $Y(s)$ 部分分式分解；
> 4. 查表逆变换得 $y(t)$。
>
> 优势：初值在步骤 2 自动处理；对 $g$ 含 $H(t-a)$、$\delta(t-a)$、分段函数时仍统一。

---

## 例：$y'' + y = H(t - \pi),\ y(0) = 0,\ y'(0) = 1$

Laplace 变换：$(s^2 + 1) Y(s) - 1 = \dfrac{e^{-\pi s}}{s}$。故
$$Y(s) = \frac{1}{s^2 + 1} + \frac{e^{-\pi s}}{s(s^2 + 1)}.$$
逆变换：$\mathcal{L}^{-1}[1/(s^2+1)] = \sin t$，
$$\mathcal{L}^{-1}\!\left[\frac{e^{-\pi s}}{s(s^2+1)}\right] = H(t - \pi) \cdot (1 - \cos(t - \pi)) = H(t - \pi)(1 + \cos t).$$
故 $y(t) = \sin t + H(t - \pi)(1 + \cos t)$。$\blacksquare$

> [!info] 对比待定系数法
> 用 [[待定系数法]] 需在 $[0, \pi)$ 与 $[\pi, \infty)$ 上分别求解，再在 $t = \pi$ 处施加连续性条件拼接。Laplace 变换一次给出全局解，且 $H(t - \pi)$ 的衔接自动满足。

---

## 证明思路总结

> [!tip] 关键思想
> Laplace 变换将**微分方程变成代数方程**：
> $$\text{求导} \;\xrightarrow{\mathcal{L}}\; \text{乘 } s\ \text{并减去初值}.$$
> 初值在变换中自动入账（而非事后确定积分常数），这是 Laplace 变换法最强的地方。
>
> 系统论视角：$P(s) Y(s) = Q(s) + G(s)$ 即
> $$\text{响应} = \text{零输入响应}\;(Q(s)/P(s)) + \text{零状态响应}\;(G(s)/P(s)).$$
> 传递函数 $H(s) = 1/P(s)$ 完整刻画系统的输入–输出关系，特征根即 $H(s)$ 的极点。

> [!info] 与算子法、特征方程法的关系
> - Laplace 变换法 = 特征方程法的**积分变换实现**：$P(s) = 0$ 正是特征方程；
> - 多项式 $Q(s)$ 的构造与 [[待定系数法]] 的齐次解初值确定等价；
> - 传递函数 $H(s) = 1/P(s)$ 与 [[算子法与逆算子分解]] 中的 $1/p(D)$（逆算子）对应：$s$ 复变量 vs $D$ 微分算子。
