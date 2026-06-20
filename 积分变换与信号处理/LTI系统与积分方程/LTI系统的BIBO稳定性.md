---
title: LTI 系统的 BIBO 稳定性判据
date: 2026-04-18
tags:
  - 积分变换
  - Laplace变换
  - 信号与系统
  - 稳定性
  - 传递函数
---

# LTI 系统的 BIBO 稳定性判据

## 预备定义

> [!note] 因果 LTI 系统
> **线性时不变系统**（linear time-invariant system，简称 LTI 系统）是满足以下两个性质的系统：
> 1. **线性**：若输入 $x_1(t) \mapsto y_1(t)$，$x_2(t) \mapsto y_2(t)$，则 $\alpha x_1(t) + \beta x_2(t) \mapsto \alpha y_1(t) + \beta y_2(t)$。
> 2. **时不变**：若 $x(t) \mapsto y(t)$，则 $x(t - t_0) \mapsto y(t - t_0)$。
>
> 称 LTI 系统为**因果的**（causal），若其脉冲响应 $h(t)$ 满足 $h(t) = 0,\; \forall\, t < 0$。
>
> 因果 LTI 系统的输入输出关系为**单边卷积**：
> $$y(t) = (h * x)(t) = \int_0^{+\infty} h(\tau)\, x(t - \tau)\, d\tau.$$

> [!note] 传递函数
> 因果 LTI 系统的**传递函数**（transfer function）定义为脉冲响应 $h(t)$ 的 Laplace 变换：
> $$H(s) = \mathcal{L}\{h(t)\}(s) = \int_0^{+\infty} e^{-st}\, h(t)\, dt.$$
>
> 由 [[Laplace 变换的卷积定理|卷积定理]]，输出的 Laplace 变换满足
> $$Y(s) = H(s) \cdot X(s),$$
> 其中 $X(s) = \mathcal{L}\{x(t)\}$，$Y(s) = \mathcal{L}\{y(t)\}$。

> [!note] 有理传递函数与极点
> 称传递函数 $H(s)$ 为**有理的**（rational），若它可以表示为两个多项式的比：
> $$H(s) = \frac{B(s)}{A(s)} = \frac{b_m s^m + \cdots + b_1 s + b_0}{s^n + a_{n-1} s^{n-1} + \cdots + a_1 s + a_0}, \quad m < n.$$
>
> $A(s)$ 的根 $s_1, s_2, \ldots, s_n$（含重根）称为系统的**极点**（poles）。条件 $m < n$ 确保系统是**严格真的**（strictly proper），即 $|H(s)| \to 0$ 当 $|s| \to \infty$。

> [!note] BIBO 稳定性
> 称系统为 **BIBO 稳定的**（Bounded-Input Bounded-Output stable），若对任意有界输入 $x(t)$（即 $\sup_{t \geq 0} |x(t)| < +\infty$），系统输出 $y(t)$ 亦有界（即 $\sup_{t \geq 0} |y(t)| < +\infty$）。

> [!note] 部分分式展开与 Laplace 逆变换
> 设 $H(s)$ 为严格真有理函数，极点为 $s_1, \ldots, s_r$，重数分别为 $m_1, \ldots, m_r$（$\sum m_i = n$）。则 $H(s)$ 可作**部分分式展开**：
> $$H(s) = \sum_{i=1}^{r} \sum_{k=1}^{m_i} \frac{c_{ik}}{(s - s_i)^k}.$$
>
> 对因果系统取 Laplace 逆变换，得脉冲响应：
> $$h(t) = \sum_{i=1}^{r} \sum_{k=1}^{m_i} c_{ik}\, \frac{t^{k-1}}{(k-1)!}\, e^{s_i t}, \quad t \geq 0.$$

---

## 定理

设因果 LTI 系统的传递函数 $H(s) = B(s)/A(s)$ 为严格真有理函数，极点为 $s_1, \ldots, s_r$。则以下三个条件等价：

**(i)** 系统是 BIBO 稳定的。

**(ii)** 脉冲响应绝对可积：$\displaystyle\int_0^{+\infty} |h(t)|\, dt < +\infty$。

**(iii)** 所有极点均位于开左半平面：$\operatorname{Re}(s_i) < 0$，$\forall\, i = 1, \ldots, r$。

---

## 证明

证明按 **(ii) $\Rightarrow$ (i) $\Rightarrow$ (ii) $\Rightarrow$ (iii) $\Rightarrow$ (ii)** 的顺序进行。

### 第一部分：(ii) $\Rightarrow$ (i)（绝对可积蕴含 BIBO 稳定）

**目标**：设 $\int_0^{+\infty} |h(\tau)|\, d\tau < +\infty$。对任意有界输入 $|x(t)| \leq M$，证明输出有界。

由 LTI 系统的输入输出关系：

$$|y(t)| = \left|\int_0^{+\infty} h(\tau)\, x(t - \tau)\, d\tau\right| \leq \int_0^{+\infty} |h(\tau)|\, |x(t - \tau)|\, d\tau \leq M \int_0^{+\infty} |h(\tau)|\, d\tau < +\infty.$$

因此 $\sup_{t \geq 0} |y(t)| \leq M \cdot \|h\|_{L^1}$，系统 BIBO 稳定。$\square$

### 第二部分：(i) $\Rightarrow$ (ii)（BIBO 稳定蕴含绝对可积）

**目标**：设系统 BIBO 稳定。证明 $h \in L^1[0, +\infty)$。

**策略**：构造法 — 构造一个特殊的有界输入，使输出值恰好等于 $\int_0^T |h(\tau)|\, d\tau$，再利用 BIBO 稳定性得出此积分有界。

#### 第一步：构造有界输入

固定 $t_0 > 0$，定义

$$x_0(\xi) = \begin{cases} +1, & \text{若 } h(t_0 - \xi) > 0, \\ -1, & \text{若 } h(t_0 - \xi) < 0, \\ 0, & \text{若 } h(t_0 - \xi) = 0. \end{cases}$$

即 $x_0(\xi) = \operatorname{sgn}(h(t_0 - \xi))$。

显然 $|x_0(\xi)| \leq 1$，故 $x_0$ 是有界输入。$\square$

#### 第二步：计算对应的输出

在 $t = t_0$ 处，

$$y(t_0) = \int_0^{+\infty} h(\tau)\, x_0(t_0 - \tau)\, d\tau = \int_0^{+\infty} h(\tau)\, \operatorname{sgn}(h(\tau))\, d\tau = \int_0^{+\infty} |h(\tau)|\, d\tau.$$

> [!info] 关键等式
> 由 $x_0$ 的定义，$x_0(t_0 - \tau) = \operatorname{sgn}(h(\tau))$。因此 $h(\tau) \cdot x_0(t_0 - \tau) = h(\tau) \cdot \operatorname{sgn}(h(\tau)) = |h(\tau)|$。这个构造的巧妙之处在于输入信号与脉冲响应"完美对齐"，使卷积积分恰好提取出 $|h|$。

$\square$

#### 第三步：利用 BIBO 稳定性得出结论

由 BIBO 稳定性，$|y(t_0)| \leq C$ 对某常数 $C$ 成立。因此

$$\int_0^{+\infty} |h(\tau)|\, d\tau = y(t_0) \leq C < +\infty.$$

故 $h \in L^1[0, +\infty)$。$\square$

---

### 第三部分：(ii) $\Leftrightarrow$ (iii)（绝对可积等价于极点在开左半平面）

#### 方向 (iii) $\Rightarrow$ (ii)：所有极点在开左半平面蕴含绝对可积

**目标**：设所有极点满足 $\operatorname{Re}(s_i) < 0$。证明 $h \in L^1[0, +\infty)$。

由部分分式展开，脉冲响应为

$$h(t) = \sum_{i=1}^{r} \sum_{k=1}^{m_i} c_{ik}\, \frac{t^{k-1}}{(k-1)!}\, e^{s_i t}, \quad t \geq 0. \quad \cdots (\ast)$$

记 $\sigma_i = \operatorname{Re}(s_i) < 0$。对 $(\ast)$ 中的每一项，

$$\left|c_{ik}\, \frac{t^{k-1}}{(k-1)!}\, e^{s_i t}\right| = \frac{|c_{ik}|}{(k-1)!}\, t^{k-1}\, e^{\sigma_i t}, \quad t \geq 0.$$

由于 $\sigma_i < 0$，指数衰减支配多项式增长：

$$\int_0^{+\infty} t^{k-1}\, e^{\sigma_i t}\, dt = \frac{(k-1)!}{|\sigma_i|^k} < +\infty. \quad \cdots (\star)$$

> [!info] 公式 $(\star)$ 的来源
> 这是 Gamma 函数的特殊情形。令 $u = |\sigma_i| t$，则
> $$\int_0^{+\infty} t^{k-1} e^{\sigma_i t}\, dt = \frac{1}{|\sigma_i|^k} \int_0^{+\infty} u^{k-1} e^{-u}\, du = \frac{\Gamma(k)}{|\sigma_i|^k} = \frac{(k-1)!}{|\sigma_i|^k}.$$

由三角不等式和 $(\star)$，

$$\int_0^{+\infty} |h(t)|\, dt \leq \sum_{i=1}^{r} \sum_{k=1}^{m_i} \frac{|c_{ik}|}{(k-1)!} \cdot \frac{(k-1)!}{|\sigma_i|^k} = \sum_{i=1}^{r} \sum_{k=1}^{m_i} \frac{|c_{ik}|}{|\sigma_i|^k} < +\infty.$$

故 $h \in L^1[0, +\infty)$。$\square$

#### 方向 (ii) $\Rightarrow$ (iii)：绝对可积蕴含所有极点在开左半平面

**目标**：证明逆否命题 — 若存在极点 $s_0$ 使得 $\operatorname{Re}(s_0) \geq 0$，则 $h \notin L^1[0, +\infty)$。

**反证法**：假设存在极点 $s_0$，重数为 $m_0$，使得 $\sigma_0 = \operatorname{Re}(s_0) \geq 0$。

##### 情形一：$\sigma_0 > 0$

脉冲响应 $h(t)$ 中包含项

$$\varphi(t) = c\, t^{m_0 - 1} e^{s_0 t}, \quad c \neq 0.$$

其模为 $|c|\, t^{m_0 - 1} e^{\sigma_0 t}$，当 $t \to +\infty$ 时指数增长。因此

$$\int_0^{+\infty} |h(t)|\, dt \geq |c| \int_T^{+\infty} t^{m_0-1} e^{\sigma_0 t}\, dt - C_0 = +\infty,$$

其中 $C_0$ 为其余有限项在 $[T, +\infty)$ 上的积分绝对值（取 $T$ 充分大使指数增长项支配），故 $h \notin L^1$。$\square$

##### 情形二：$\sigma_0 = 0$（即极点在虚轴上）

此时 $s_0 = j\omega_0$（$\omega_0 \in \mathbb{R}$），脉冲响应中包含项

$$\varphi(t) = c\, t^{m_0 - 1} e^{j\omega_0 t}, \quad c \neq 0.$$

**子情形 2a**：若 $m_0 \geq 2$，则 $|\varphi(t)| = |c|\, t^{m_0-1} \to +\infty$，显然 $\varphi \notin L^1$。$\square$

**子情形 2b**：若 $m_0 = 1$，则 $\varphi(t) = c\, e^{j\omega_0 t}$，其模为常数 $|c|$。

$$\int_0^{T} |\varphi(t)|\, dt = |c|\, T \to +\infty \quad (T \to +\infty).$$

> [!important] 虚轴上简单极点的不可积性
> 即使极点是虚轴上的简单极点（$\sigma_0 = 0$，$m_0 = 1$），对应的脉冲响应项 $c\, e^{j\omega_0 t}$ 虽然有界（不发散），但**不绝对可积**。直观地说，一个永不衰减的振荡信号的"总能量"是无穷的。特别地，当 $\omega_0 = 0$ 时即为常数 $c \neq 0$，同样不可积。

因此 $h \notin L^1[0, +\infty)$。$\square$

---

### 总结

综合三个部分：

1. (ii) $\Rightarrow$ (i)：$h \in L^1$ 蕴含 BIBO 稳定（卷积的 $L^1$ 估计）。 ✓
2. (i) $\Rightarrow$ (ii)：BIBO 稳定蕴含 $h \in L^1$（构造符号输入）。 ✓
3. (ii) $\Leftrightarrow$ (iii)：$h \in L^1$ 等价于所有极点在开左半平面（指数衰减 vs. 不衰减）。 ✓

因此 (i)、(ii)、(iii) 三者等价。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本定理建立了 LTI 系统稳定性的三重刻画：
>
> $$\boxed{\text{BIBO 稳定} \;\Longleftrightarrow\; h \in L^1[0,+\infty) \;\Longleftrightarrow\; \text{所有极点在开左半平面}}$$
>
> 证明的核心分为两层：
>
> **第一层（时域）**：BIBO $\Leftrightarrow$ $L^1$
> - 正方向用**卷积的 $L^1$ 估计**（Young 不等式的特殊情形）；
> - 反方向用**符号函数构造法** — 构造 $x(\xi) = \operatorname{sgn}(h(t_0 - \xi))$，使卷积积分恰好提取出 $|h|$。
>
> **第二层（频域）**：$L^1$ $\Leftrightarrow$ 极点位置
> - 正方向用**部分分式展开** + **Gamma 函数**积分公式；
> - 反方向对虚轴极点和右半平面极点**分类讨论**，逐一排除。
>
> Laplace 变换在此扮演了**桥梁**的角色：它将时域中难以直接判断的 $L^1$ 可积性条件，转化为频域中极点位置的**简单代数判据**。这正是 Laplace 变换在工程中如此重要的原因 — 系统稳定性可以通过检查特征多项式的根来判定，而无需显式计算脉冲响应。

> [!warning] 边界情形：虚轴上的极点
> 虚轴上的极点（$\operatorname{Re}(s_i) = 0$）导致系统**临界不稳定**（marginally unstable）：
> - **简单极点**（$m_i = 1$）：脉冲响应包含永不衰减的振荡项 $e^{j\omega t}$，有界但不绝对可积，系统非 BIBO 稳定。典型例子：理想振荡器 $H(s) = \dfrac{1}{s^2 + \omega_0^2}$。
> - **重极点**（$m_i \geq 2$）：脉冲响应包含发散项 $t^{m_i - 1} e^{j\omega t}$，系统更明确地不稳定。
>
> 因此，**极点必须严格位于左半平面**，虚轴上不行。这一区分在控制系统设计中至关重要。
