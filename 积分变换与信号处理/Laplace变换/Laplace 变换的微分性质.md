---
title: Laplace 变换的微分性质
date: 2026-04-19
tags:
  - 积分变换
  - Laplace变换
  - 信号与系统
  - 微分方程
  - RC电路
---

# Laplace 变换的微分性质

## 预备定义

> [!note] 单边 Laplace 变换
> 设 $f: [0^-, +\infty) \to \mathbb{R}$。$f$ 的**单边 Laplace 变换**定义为
> $$F(s) = \mathcal{L}\{f(t)\}(s) = \int_{0^-}^{+\infty} e^{-st}\, f(t)\, dt,$$
> 其中积分下限取 $0^-$（即从 $0$ 的左侧开始），以纳入 $t = 0$ 处可能出现的 Dirac delta。

> [!note] 指数阶函数
> 称 $f(t)$ 为**指数阶**的，若存在 $M > 0$，$\sigma_0 \geq 0$，使得 $|f(t)| \leq M\,e^{\sigma_0 t}$ 对充分大的 $t$ 成立。此条件保证 $\lim_{t \to +\infty} f(t)\, e^{-st} = 0$（当 $\operatorname{Re}(s) > \sigma_0$ 时）。

> [!note] 单位阶跃函数
> **单位阶跃函数**（unit step function）$u(t)$ 定义为
> $$u(t) = \begin{cases} 1, & t \geq 0, \\ 0, & t < 0. \end{cases}$$
> 其 Laplace 变换为 $\mathcal{L}\{u(t)\} = \dfrac{1}{s}$（$\operatorname{Re}(s) > 0$）。

> [!info] 本节用到的 Laplace 变换对
>
> | $f(t)$（$t \geq 0$） | $F(s)$ |
> |--------|--------|
> | $1$（即 $u(t)$） | $\dfrac{1}{s}$ |
> | $e^{at}$ | $\dfrac{1}{s - a}$ |

---

## 定理

**(i)** **一阶微分性质**：设 $f(t)$ 在 $t \geq 0$ 上连续可微且为指数阶。则

$$\mathcal{L}\{f'(t)\}(s) = s\,F(s) - f(0^-).$$

**(ii)** **$n$ 阶微分性质**：设 $f(t)$ 在 $t \geq 0$ 上 $n$ 次连续可微且 $f, f', \ldots, f^{(n-1)}$ 均为指数阶。则

$$\mathcal{L}\{f^{(n)}(t)\}(s) = s^n F(s) - s^{n-1} f(0^-) - s^{n-2} f'(0^-) - \cdots - f^{(n-1)}(0^-),$$

即

$$\mathcal{L}\{f^{(n)}(t)\}(s) = s^n F(s) - \sum_{k=0}^{n-1} s^{n-1-k}\, f^{(k)}(0^-).$$

---

## 第(i)部分的证明

### 第一步：写出定义并分部积分

由 Laplace 变换的定义，

$$\mathcal{L}\{f'(t)\} = \int_{0^-}^{+\infty} e^{-st}\, f'(t)\, dt.$$

对此积分施行**分部积分**（integration by parts），令

$$u = e^{-st}, \quad dv = f'(t)\, dt,$$

则 $du = -s\, e^{-st}\, dt$，$v = f(t)$。得

$$\int_{0^-}^{+\infty} e^{-st}\, f'(t)\, dt = \Big[e^{-st}\, f(t)\Big]_{0^-}^{+\infty} - \int_{0^-}^{+\infty} (-s)\, e^{-st}\, f(t)\, dt. \quad \cdots (\ast)$$

$\square$

### 第二步：处理边界项

$(\ast)$ 右端的边界项为

$$\Big[e^{-st}\, f(t)\Big]_{0^-}^{+\infty} = \lim_{t \to +\infty} e^{-st}\, f(t) - e^{-s \cdot 0^-}\, f(0^-).$$

由 $f(t)$ 为指数阶的假设，$|f(t)| \leq M\, e^{\sigma_0 t}$。当 $\operatorname{Re}(s) > \sigma_0$ 时，

$$|e^{-st}\, f(t)| \leq M\, e^{-(\operatorname{Re}(s) - \sigma_0)\, t} \to 0 \quad (t \to +\infty).$$

因此

$$\Big[e^{-st}\, f(t)\Big]_{0^-}^{+\infty} = 0 - f(0^-) = -f(0^-). \quad \square$$

### 第三步：合并得出结论

将第二步的结果代入 $(\ast)$：

$$\mathcal{L}\{f'(t)\} = -f(0^-) + s \int_{0^-}^{+\infty} e^{-st}\, f(t)\, dt = s\, F(s) - f(0^-). \quad \square$$

---

## 第(ii)部分的证明

用**数学归纳法**证明。

### 基础情形：$n = 1$

即第(i)部分，已证。$\square$

### 归纳步骤

**归纳假设**：假设对 $n - 1$ 阶导数，命题成立：

$$\mathcal{L}\{f^{(n-1)}(t)\} = s^{n-1} F(s) - \sum_{k=0}^{n-2} s^{n-2-k}\, f^{(k)}(0^-). \quad \cdots (\star)$$

#### 第一步：将 $f^{(n)}$ 视为 $f^{(n-1)}$ 的一阶导数

令 $g(t) = f^{(n-1)}(t)$，则 $f^{(n)}(t) = g'(t)$。由第(i)部分的一阶微分性质：

$$\mathcal{L}\{f^{(n)}(t)\} = \mathcal{L}\{g'(t)\} = s\, G(s) - g(0^-), \quad \cdots (1)$$

其中 $G(s) = \mathcal{L}\{g(t)\} = \mathcal{L}\{f^{(n-1)}(t)\}$，$g(0^-) = f^{(n-1)}(0^-)$。$\square$

#### 第二步：代入归纳假设

将 $(\star)$ 代入 $(1)$：

$$\mathcal{L}\{f^{(n)}(t)\} = s \left[s^{n-1} F(s) - \sum_{k=0}^{n-2} s^{n-2-k}\, f^{(k)}(0^-)\right] - f^{(n-1)}(0^-).$$

展开：

$$= s^n F(s) - \sum_{k=0}^{n-2} s^{n-1-k}\, f^{(k)}(0^-) - f^{(n-1)}(0^-).$$

注意最后一项恰为求和中 $k = n-1$ 时的项（此时 $s^{n-1-(n-1)} = s^0 = 1$）。因此

$$= s^n F(s) - \sum_{k=0}^{n-1} s^{n-1-k}\, f^{(k)}(0^-). \quad \square$$

### 总结

1. 基础情形（$n = 1$）成立：$\mathcal{L}\{f'\} = sF(s) - f(0^-)$。 ✓
2. 归纳步骤成立：$n-1 \Rightarrow n$。 ✓

由数学归纳法，命题对一切 $n \geq 1$ 成立。$\blacksquare$

---

## 应用示例：RC 低通电路的阶跃响应

> [!info] 问题
> 一阶 RC 电路中，电容电压 $v_C(t)$ 满足 ODE：
> $$RC\, \frac{dv_C}{dt} + v_C(t) = v_{in}(t),$$
> 其中 $v_{in}(t) = V_0\, u(t)$（在 $t = 0$ 时刻施加阶跃电压），初始条件 $v_C(0^-) = 0$（电容初始未充电）。求 $v_C(t)$。

### 第一步：对 ODE 两端取 Laplace 变换

设 $V_C(s) = \mathcal{L}\{v_C(t)\}$。由**微分性质**，

$$\mathcal{L}\left\{\frac{dv_C}{dt}\right\} = s\, V_C(s) - v_C(0^-) = s\, V_C(s) - 0 = s\, V_C(s).$$

对右端，$\mathcal{L}\{V_0\, u(t)\} = \dfrac{V_0}{s}$。

因此 ODE 变为代数方程：

$$RC \cdot s\, V_C(s) + V_C(s) = \frac{V_0}{s}.$$

### 第二步：解代数方程

提取公因子：

$$V_C(s)\,(RCs + 1) = \frac{V_0}{s}.$$

$$V_C(s) = \frac{V_0}{s\,(RCs + 1)} = \frac{V_0}{RC} \cdot \frac{1}{s\,(s + \frac{1}{RC})}.$$

### 第三步：部分分式展开

令 $\alpha = \dfrac{1}{RC}$，则

$$V_C(s) = \frac{V_0 \alpha}{s(s + \alpha)} = V_0 \left(\frac{1}{s} - \frac{1}{s + \alpha}\right).$$

> [!info] 部分分式的推导
> 设 $\dfrac{\alpha}{s(s+\alpha)} = \dfrac{A}{s} + \dfrac{B}{s+\alpha}$。
> 令 $s = 0$：$A = 1$。令 $s = -\alpha$：$B = -1$。

### 第四步：取 Laplace 逆变换

由已知变换对，$\mathcal{L}^{-1}\left\{\dfrac{1}{s}\right\} = u(t)$，$\mathcal{L}^{-1}\left\{\dfrac{1}{s + \alpha}\right\} = e^{-\alpha t}\, u(t)$。

$$v_C(t) = V_0\left(1 - e^{-t/(RC)}\right) u(t).$$

> [!important] 物理解读
> - $t = 0$ 时：$v_C(0) = 0$（电容未充电），与初始条件一致。
> - $t \to +\infty$ 时：$v_C \to V_0$（电容充满，电压等于输入）。
> - **时间常数** $\tau = RC$：经过 $t = \tau$ 后，$v_C(\tau) = V_0(1 - e^{-1}) \approx 0.632\, V_0$，即充电至 $63.2\%$。
> - 经过 $5\tau$ 后，$v_C(5\tau) \approx 0.993\, V_0$，工程上视为充电完成。

---

## 证明思路总结

> [!tip] 关键思想
> 微分性质的证明只用了一个工具：**分部积分**。
>
> $$\int_{0^-}^{\infty} \underbrace{e^{-st}}_{u}\, \underbrace{f'(t)\, dt}_{dv} = \underbrace{\Big[e^{-st} f(t)\Big]_{0^-}^{\infty}}_{\to\; -f(0^-)} + s \underbrace{\int_{0^-}^{\infty} e^{-st} f(t)\, dt}_{= F(s)}$$
>
> 本质上，分部积分将 $f'$ 上的"微分"转移到了 $e^{-st}$ 上，而 $e^{-st}$ 的导数只是自身乘以 $-s$ — 微分变成了乘以 $s$。这就是 Laplace 变换的核心威力：
>
> $$\text{微分方程（时域）} \;\xrightarrow{\;\mathcal{L}\;}\; \text{代数方程（频域）} \;\xrightarrow{\;\text{解代数}}\; F(s) \;\xrightarrow{\;\mathcal{L}^{-1}\;}\; f(t)$$
>
> 每做一次微分，频域中只是多乘一个 $s$，同时"释放"出一个初始条件 $f^{(k)}(0^-)$。初始条件自然地编码在代数方程中，无需像经典方法那样先求通解再定常数。

> [!warning] 初始条件 $0^-$ 与 $0^+$ 的区别
> 单边 Laplace 变换的积分下限取 $0^-$，因此公式中出现的是 $f(0^-)$（跳跃之前的值）。当系统在 $t = 0$ 有冲激输入（如电容上的初始电荷跳变）时，$f(0^-)$ 和 $f(0^+)$ 可能不同。选取 $0^-$ 的约定使得初始条件可以独立于输入来指定，这在分析含冲激信号的系统时尤为重要。
