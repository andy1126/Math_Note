---
title: Laplace 变换的初值定理与终值定理
date: 2026-04-19
tags:
  - 积分变换
  - Laplace变换
  - 信号与系统
  - 初值定理
  - 终值定理
---

# Laplace 变换的初值定理与终值定理

## 预备定义

> [!note] 单边 Laplace 变换
> $$F(s) = \mathcal{L}\{f(t)\}(s) = \int_{0^-}^{+\infty} e^{-st}\, f(t)\, dt.$$

> [!abstract] Laplace 变换的微分性质
> 设 $f(t)$ 连续可微且为指数阶，则
> $$\mathcal{L}\{f'(t)\}(s) = s\,F(s) - f(0^-).$$
>
> 详见 [[Laplace 变换的微分性质|Laplace 变换的微分性质]]。

---

## 定理

设 $f(t)$（$t \geq 0$）为指数阶的分段连续函数，$F(s) = \mathcal{L}\{f\}(s)$。

**(i)** **初值定理**（Initial Value Theorem）：若 $f'(t)$ 在 $(0, +\infty)$ 上分段连续且为指数阶，则

$$\lim_{t \to 0^+} f(t) = \lim_{s \to +\infty} s\,F(s).$$

**(ii)** **终值定理**（Final Value Theorem）：若 $\lim_{t \to +\infty} f(t)$ 存在且有限，则

$$\lim_{t \to +\infty} f(t) = \lim_{s \to 0^+} s\,F(s).$$

---

## 第(i)部分的证明：初值定理

### 第一步：从微分性质出发

由微分性质，

$$s\,F(s) - f(0^-) = \int_{0^-}^{+\infty} e^{-st}\, f'(t)\, dt. \quad \cdots (\ast)$$

$\square$

### 第二步：令 $s \to +\infty$，计算右端极限

当 $s \to +\infty$ 时，对任意固定的 $t > 0$，$e^{-st} \to 0$。

将 $(\ast)$ 右端的积分拆成两部分：在 $t = 0$ 处的跳跃贡献和 $t > 0$ 的连续部分。

若 $f$ 在 $t = 0$ 处有跳跃 $f(0^+) - f(0^-)$，则 $f'$ 在分布意义下包含项 $[f(0^+) - f(0^-)]\,\delta(t)$，其 Laplace 变换为 $f(0^+) - f(0^-)$（对所有 $s$ 均成立）。

对 $t > 0$ 上的连续部分 $f'_c(t)$（分段连续且指数阶），

$$\left|\int_{0^+}^{+\infty} e^{-st}\, f'_c(t)\, dt\right| \leq \int_{0^+}^{+\infty} e^{-\operatorname{Re}(s)\,t}\, |f'_c(t)|\, dt.$$

由于 $|f'_c(t)| \leq M\,e^{\sigma_0 t}$，当 $s \to +\infty$ 时，

$$\int_{0^+}^{+\infty} e^{-st}\, |f'_c(t)|\, dt \leq \frac{M}{s - \sigma_0} \to 0.$$

> [!info] 直观理解
> 当 $s \to +\infty$ 时，$e^{-st}$ 变成一个越来越集中在 $t = 0$ 附近的"窗口"。积分只"看到" $t = 0$ 处的信息，其余部分被指数衰减压制为零。

因此 $(\ast)$ 右端的极限为 $f(0^+) - f(0^-)$。$\square$

### 第三步：得出结论

$$\lim_{s \to +\infty} [s\,F(s) - f(0^-)] = f(0^+) - f(0^-),$$

即

$$\lim_{s \to +\infty} s\,F(s) = f(0^+). \quad \square$$

---

## 第(ii)部分的证明：终值定理

### 第一步：从微分性质出发

同样由 $(\ast)$，

$$s\,F(s) - f(0^-) = \int_{0^-}^{+\infty} e^{-st}\, f'(t)\, dt. \quad \cdots (\star)$$

$\square$

### 第二步：令 $s \to 0^+$，计算右端极限

当 $s \to 0^+$ 时，$e^{-st} \to 1$ 对一切 $t \geq 0$。

由于 $\lim_{t \to +\infty} f(t)$ 存在且有限，$f'(t)$ 在 $[0, +\infty)$ 上的反常积分收敛：

$$\int_{0^-}^{+\infty} f'(t)\, dt = \lim_{T \to +\infty} f(T) - f(0^-) = \lim_{t \to +\infty} f(t) - f(0^-).$$

对 $(\star)$ 右端取 $s \to 0^+$ 的极限。被积函数 $|e^{-st} f'(t)| \leq |f'(t)|$（因为 $0 < e^{-st} \leq 1$），且 $|f'(t)|$ 可积。由**控制收敛定理**（dominated convergence theorem），可以将极限移入积分：

$$\lim_{s \to 0^+} \int_{0^-}^{+\infty} e^{-st}\, f'(t)\, dt = \int_{0^-}^{+\infty} \lim_{s \to 0^+} e^{-st}\, f'(t)\, dt = \int_{0^-}^{+\infty} f'(t)\, dt.$$

> [!important] 控制收敛定理的适用条件
> 需要一个与 $s$ 无关的可积控制函数。这里 $|e^{-st} f'(t)| \leq |f'(t)|$，而 $|f'(t)|$ 可积的条件由 $\lim_{t \to +\infty} f(t)$ 存在且有限来保证（$f'$ 的反常积分收敛）。

$\square$

### 第三步：得出结论

$$\lim_{s \to 0^+} [s\,F(s) - f(0^-)] = \lim_{t \to +\infty} f(t) - f(0^-),$$

即

$$\lim_{s \to 0^+} s\,F(s) = \lim_{t \to +\infty} f(t). \quad \square$$

---

## 总结

1. 初值定理：$s \to +\infty$ 时 $e^{-st}$ 集中在 $t = 0$，提取初始值。 ✓
2. 终值定理：$s \to 0^+$ 时 $e^{-st} \to 1$，积分还原为 $f' $ 的全积分，给出终值。 ✓

两个定理均建立在微分性质 $\mathcal{L}\{f'\} = sF - f(0^-)$ 之上，分别对 $s$ 取两个极端方向的极限。$\blacksquare$

---

## 应用示例

> [!info] 应用：不做逆变换，直接读出系统响应的初始值和稳态值
> 设 RC 电路的阶跃响应（见 [[Laplace 变换的微分性质|微分性质]]）为
> $$V_C(s) = \frac{V_0}{s(s + \alpha)}, \quad \alpha = \frac{1}{RC}.$$
>
> **初始值**（$t = 0^+$）：
> $$v_C(0^+) = \lim_{s \to +\infty} s \cdot V_C(s) = \lim_{s \to +\infty} \frac{V_0}{s + \alpha} = 0. \quad \checkmark$$
> （电容电压不能突变，与 $v_C(0^-) = 0$ 一致。）
>
> **稳态值**（$t \to +\infty$）：
> $$v_C(+\infty) = \lim_{s \to 0^+} s \cdot V_C(s) = \lim_{s \to 0^+} \frac{V_0}{s + \alpha} = \frac{V_0}{\alpha} \cdot \alpha = V_0. \quad \checkmark$$
> （电容最终充满至输入电压。）
>
> 两个值均无需计算逆变换即可得到。

> [!info] 应用：快速判断系统的直流增益
> 对 LTI 系统 $H(s) = \dfrac{Y(s)}{X(s)}$，若输入为单位阶跃 $X(s) = \dfrac{1}{s}$，则
> $$y(\infty) = \lim_{s \to 0^+} s \cdot H(s) \cdot \frac{1}{s} = H(0).$$
> 即系统传递函数在 $s = 0$ 处的值就是**直流增益**（DC gain）。

---

## 证明思路总结

> [!tip] 关键思想
> 两个定理的出发点相同 — 微分性质 $s F(s) - f(0^-) = \mathcal{L}\{f'\}$ — 然后分别让 $s$ 走向两个极端：
>
> | | 初值定理 | 终值定理 |
> |---|---|---|
> | **$s$ 的方向** | $s \to +\infty$ | $s \to 0^+$ |
> | **$e^{-st}$ 的行为** | 集中在 $t = 0$ 附近 | $\to 1$（均匀） |
> | **积分提取的信息** | $f(0^+)$ | $\int_0^\infty f'(t)\,dt = f(\infty) - f(0^-)$ |
> | **数学工具** | 指数阶的直接估计 | 控制收敛定理 |
>
> 直观地说：**$s$ 大 = 看近处（初始时刻），$s$ 小 = 看远处（稳态）**。这与 Laplace 变换中 $s$ 作为"频率"参数的角色一致 — 高频分量决定信号的瞬态行为，低频分量决定信号的长期趋势。

> [!warning] 终值定理的适用条件
> 终值定理**要求 $\lim_{t \to +\infty} f(t)$ 存在且有限**。若该极限不存在（例如 $f(t) = \sin t$），则定理不适用，即使 $\lim_{s \to 0^+} sF(s)$ 形式上可以计算。
>
> 经典反例：$f(t) = \sin t$，$F(s) = \dfrac{1}{s^2+1}$。
> $$\lim_{s \to 0^+} s \cdot \frac{1}{s^2+1} = 0,$$
> 但 $\lim_{t \to +\infty} \sin t$ 不存在。$0$ 并不是 $\sin t$ 的"终值"。
>
> 在实际应用中，检查终值定理是否适用的简便方法是验证 $sF(s)$ 的所有极点是否都在**开左半平面**（$s = 0$ 处的单极点除外）。若 $sF(s)$ 在虚轴或右半平面有极点，则终值定理不成立。
