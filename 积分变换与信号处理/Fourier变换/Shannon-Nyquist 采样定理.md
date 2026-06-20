---
title: Shannon-Nyquist 采样定理
date: 2026-04-18
tags:
  - 积分变换
  - Fourier变换
  - 信号与系统
  - 采样
  - 数字信号处理
---

# Shannon-Nyquist 采样定理

## 预备定义

> [!note] Fourier 变换
> 设 $x(t) \in L^1(\mathbb{R})$。$x(t)$ 的 **Fourier 变换**定义为
> $$X(f) = \mathcal{F}\{x(t)\}(f) = \int_{-\infty}^{+\infty} x(t)\, e^{-j2\pi ft}\, dt,$$
> 其 **Fourier 逆变换**为
> $$x(t) = \mathcal{F}^{-1}\{X(f)\}(t) = \int_{-\infty}^{+\infty} X(f)\, e^{j2\pi ft}\, df.$$
> 本文采用频率变量 $f$（单位：Hz）的约定，而非角频率 $\omega = 2\pi f$。

> [!note] 带限信号
> 称信号 $x(t)$ 为**带限的**（bandlimited），带宽为 $W > 0$，若其 Fourier 变换满足
> $$X(f) = 0, \quad \forall\, |f| > W.$$
> 即 $x(t)$ 的频谱完全集中在 $[-W, W]$ 内。

> [!note] Dirac 梳状函数
> 以 $T_s > 0$ 为周期的 **Dirac 梳状函数**（Dirac comb）定义为
> $$p(t) = \sum_{n=-\infty}^{+\infty} \delta(t - nT_s),$$
> 其中 $\delta(t)$ 为 Dirac delta 分布。$p(t)$ 可视为理想采样器：$x(t) \cdot p(t) = \sum_n x(nT_s)\, \delta(t - nT_s)$。

> [!note] Sinc 函数
> **归一化 sinc 函数**定义为
> $$\operatorname{sinc}(u) = \begin{cases} \dfrac{\sin(\pi u)}{\pi u}, & u \neq 0, \\ 1, & u = 0. \end{cases}$$
> 它是 Fourier 变换的核心函数：$\mathcal{F}^{-1}\{\operatorname{rect}(f)\} = \operatorname{sinc}(t)$，其中 $\operatorname{rect}(f) = \mathbf{1}_{|f| \leq 1/2}$ 为矩形函数。

> [!abstract] 引理：Fourier 变换将时域乘法映射为频域卷积
> 设 $x(t)$ 和 $y(t)$ 的 Fourier 变换分别为 $X(f)$ 和 $Y(f)$。若 $z(t) = x(t) \cdot y(t)$，则
> $$Z(f) = (X * Y)(f) = \int_{-\infty}^{+\infty} X(\xi)\, Y(f - \xi)\, d\xi.$$
> 对于分布意义下的 Fourier 变换，此性质同样成立。

> [!abstract] 引理：Dirac 梳状函数的 Fourier 变换
> 周期为 $T_s$ 的 Dirac 梳的 Fourier 变换（在分布意义下）为
> $$\mathcal{F}\left\{\sum_{n=-\infty}^{+\infty} \delta(t - nT_s)\right\}(f) = f_s \sum_{k=-\infty}^{+\infty} \delta(f - k f_s), \quad \cdots (\dagger)$$
> 其中 $f_s = 1/T_s$ 为采样频率。即**时域的 Dirac 梳在频域仍为 Dirac 梳**，周期由 $T_s$ 变为 $f_s$，幅度缩放 $f_s$ 倍。

**证明**：$p(t) = \sum_n \delta(t - nT_s)$ 是周期为 $T_s$ 的分布，可展开为 Fourier 级数：

$$p(t) = \sum_{k=-\infty}^{+\infty} c_k\, e^{j2\pi k f_s t},$$

其中 Fourier 系数为

$$c_k = \frac{1}{T_s} \int_0^{T_s} p(t)\, e^{-j2\pi k f_s t}\, dt = \frac{1}{T_s} \cdot 1 = f_s.$$

因此 $p(t) = f_s \sum_k e^{j2\pi k f_s t}$。取 Fourier 变换，利用 $\mathcal{F}\{e^{j2\pi f_0 t}\} = \delta(f - f_0)$，得

$$\mathcal{F}\{p(t)\}(f) = f_s \sum_{k=-\infty}^{+\infty} \delta(f - k f_s). \quad \square$$

---

## 定理

**（Shannon-Nyquist 采样定理）** 设 $x(t)$ 为带限信号，带宽为 $W$（即 $X(f) = 0,\; |f| > W$）。若采样频率 $f_s \geq 2W$，则 $x(t)$ 可由其等间隔采样值 $\{x(nT_s)\}_{n \in \mathbb{Z}}$（$T_s = 1/f_s$）**精确重建**：

$$x(t) = \sum_{n=-\infty}^{+\infty} x(nT_s)\, \operatorname{sinc}\!\left(\frac{t - nT_s}{T_s}\right). \quad \cdots (\ast)$$

特别地，当 $f_s = 2W$（**Nyquist 速率**）时，

$$x(t) = \sum_{n=-\infty}^{+\infty} x\!\left(\frac{n}{2W}\right) \operatorname{sinc}(2Wt - n).$$

此公式称为 **Whittaker-Shannon 插值公式**。

---

## 证明

### 第一步：建立采样信号的数学模型

将连续信号 $x(t)$ 乘以 Dirac 梳状函数 $p(t) = \sum_n \delta(t - nT_s)$，得**理想采样信号**：

$$x_s(t) = x(t) \cdot p(t) = \sum_{n=-\infty}^{+\infty} x(nT_s)\, \delta(t - nT_s). \quad \cdots (1)$$

$(1)$ 以 Dirac delta 序列的形式精确保留了 $x(t)$ 在采样点 $t = nT_s$ 处的值。$\square$

### 第二步：计算采样信号的频谱

对 $(1)$ 取 Fourier 变换。由时域乘法对应频域卷积：

$$X_s(f) = \mathcal{F}\{x(t) \cdot p(t)\}(f) = X(f) * \mathcal{F}\{p(t)\}(f).$$

代入 $(\dagger)$：

$$X_s(f) = X(f) * \left[f_s \sum_{k=-\infty}^{+\infty} \delta(f - kf_s)\right] = f_s \sum_{k=-\infty}^{+\infty} X(f - kf_s). \quad \cdots (2)$$

> [!important] 频谱的周期延拓
> 公式 $(2)$ 揭示了采样的频域本质：**采样使原始频谱 $X(f)$ 以 $f_s$ 为周期进行无限次平移叠加**。每个平移副本 $X(f - kf_s)$ 对应一个"镜像"。这是理解采样定理的关键。

$\square$

### 第三步：无混叠条件

**目标**：证明当 $f_s \geq 2W$ 时，频谱的平移副本互不重叠。

第 $k$ 个副本 $X(f - kf_s)$ 的支撑为 $[kf_s - W,\; kf_s + W]$。相邻两个副本（$k$ 和 $k+1$）的间距为

$$\text{间距} = (k+1)f_s - W - (kf_s + W) = f_s - 2W.$$

当 $f_s \geq 2W$ 时，间距 $\geq 0$，即相邻副本不重叠。

> [!info] 混叠现象
> 若 $f_s < 2W$，则间距为负，相邻频谱副本发生重叠，称为**混叠**（aliasing）。此时不同频率分量叠加在一起，无法分离，原始信号不可恢复。$2W$ 称为 **Nyquist 速率**，是避免混叠的最低采样频率。

特别地，在 $|f| \leq W$ 的范围内，$(2)$ 中仅有 $k = 0$ 项 $X(f)$ 非零（因为其他副本的支撑不覆盖此区间）。因此

$$X_s(f) = f_s \cdot X(f), \quad |f| \leq W. \quad \cdots (3)$$

$\square$

### 第四步：用理想低通滤波器恢复原始频谱

由 $(3)$，可通过**理想低通滤波器**提取 $X(f)$：

$$X(f) = \frac{1}{f_s}\, X_s(f) \cdot H_{LP}(f), \quad \cdots (4)$$

其中理想低通滤波器的传递函数为

$$H_{LP}(f) = \begin{cases} 1, & |f| \leq W, \\ 0, & |f| > W \end{cases} = \operatorname{rect}\!\left(\frac{f}{2W}\right).$$

> [!important] 低通滤波器的作用
> $H_{LP}(f)$ 的作用是"窗口化" — 它保留 $|f| \leq W$ 内的主副本 $f_s \cdot X(f)$，同时完全消除所有高频的平移副本。由第三步的无混叠条件，这一操作是无损的。

$\square$

### 第五步：推导时域重建公式

将 $(4)$ 展开。首先，由 $(1)$ 直接计算 $X_s(f)$：

$$X_s(f) = \mathcal{F}\left\{\sum_n x(nT_s)\, \delta(t - nT_s)\right\}(f) = \sum_{n=-\infty}^{+\infty} x(nT_s)\, e^{-j2\pi f n T_s}. \quad \cdots (5)$$

将 $(5)$ 代入 $(4)$：

$$X(f) = \frac{1}{f_s} \sum_{n=-\infty}^{+\infty} x(nT_s)\, e^{-j2\pi f n T_s} \cdot \operatorname{rect}\!\left(\frac{f}{2W}\right).$$

取 Fourier 逆变换恢复 $x(t)$：

$$x(t) = \int_{-\infty}^{+\infty} X(f)\, e^{j2\pi ft}\, df = \frac{1}{f_s} \sum_{n=-\infty}^{+\infty} x(nT_s) \int_{-W}^{W} e^{j2\pi f(t - nT_s)}\, df. \quad \cdots (6)$$

（交换求和与积分的顺序在带限信号的条件下成立。）$\square$

### 第六步：计算核积分，得到 sinc 插值

计算 $(6)$ 中的积分。令 $\tau = t - nT_s$：

$$\int_{-W}^{W} e^{j2\pi f\tau}\, df = \frac{e^{j2\pi W\tau} - e^{-j2\pi W\tau}}{j2\pi\tau} = \frac{2\sin(2\pi W\tau)}{2\pi\tau} = 2W \cdot \operatorname{sinc}(2W\tau).$$

> [!info] 推导细节
> 直接积分：$\displaystyle\int_{-W}^{W} e^{j2\pi f\tau}\, df = \left[\frac{e^{j2\pi f\tau}}{j2\pi\tau}\right]_{-W}^{W} = \frac{e^{j2\pi W\tau} - e^{-j2\pi W\tau}}{j2\pi\tau} = \frac{2j\sin(2\pi W\tau)}{j2\pi\tau}$。
> 利用 $\operatorname{sinc}(u) = \dfrac{\sin(\pi u)}{\pi u}$，代入 $u = 2W\tau$ 即得 $2W \cdot \operatorname{sinc}(2W\tau)$。
> 当 $\tau = 0$ 时，积分值为 $2W$，与 $\operatorname{sinc}(0) = 1$ 一致。

代入 $(6)$：

$$x(t) = \frac{1}{f_s} \sum_{n=-\infty}^{+\infty} x(nT_s) \cdot 2W \cdot \operatorname{sinc}(2W(t - nT_s)).$$

取 $f_s = 2W$（即 $T_s = 1/(2W)$），则 $\dfrac{2W}{f_s} = 1$，得到

$$x(t) = \sum_{n=-\infty}^{+\infty} x\!\left(\frac{n}{2W}\right) \operatorname{sinc}(2Wt - n). \quad \cdots (\ast)$$

更一般地，对 $f_s \geq 2W$，有

$$x(t) = \sum_{n=-\infty}^{+\infty} x(nT_s)\, \operatorname{sinc}\!\left(\frac{t - nT_s}{T_s}\right). \quad \square$$

### 第七步：验证插值的精确性

**目标**：验证公式 $(\ast)$ 在采样点处精确还原原始值。

在 $t = mT_s$（$m \in \mathbb{Z}$）处：

$$\operatorname{sinc}\!\left(\frac{mT_s - nT_s}{T_s}\right) = \operatorname{sinc}(m - n) = \begin{cases} 1, & m = n, \\ 0, & m \neq n, \end{cases}$$

因为 $\operatorname{sinc}(k) = 0$ 对一切非零整数 $k$ 成立（$\sin(k\pi) = 0$），而 $\operatorname{sinc}(0) = 1$。

因此 $(\ast)$ 式在 $t = mT_s$ 处化简为

$$x(mT_s) = \sum_{n} x(nT_s) \cdot \operatorname{sinc}(m - n) = x(mT_s) \cdot 1 = x(mT_s). \quad \checkmark$$

公式不仅在采样点处精确，由前述推导它在**一切** $t \in \mathbb{R}$ 处均精确。$\square$

---

### 总结

1. 采样 = 时域乘以 Dirac 梳，频域产生频谱的周期延拓。 ✓
2. 当 $f_s \geq 2W$ 时，平移副本不重叠（无混叠）。 ✓
3. 理想低通滤波器可无损提取原始频谱。 ✓
4. 逆变换得到 sinc 插值重建公式。 ✓
5. sinc 函数的正交性保证采样点处精确还原。 ✓

因此带限信号可由 Nyquist 速率以上的等间隔采样精确重建。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明在**时域**与**频域**之间反复切换，核心链条为：
>
> $$\underbrace{x(t) \cdot p(t)}_{\text{时域采样}} \;\xrightarrow{\;\mathcal{F}\;}\; \underbrace{f_s \sum_k X(f - kf_s)}_{\text{频谱周期延拓}} \;\xrightarrow{\;H_{LP}\;}\; \underbrace{X(f)}_{\text{恢复原谱}} \;\xrightarrow{\;\mathcal{F}^{-1}\;}\; \underbrace{\sum_n x(nT_s)\,\operatorname{sinc}(\cdots)}_{\text{sinc 插值重建}}$$
>
> 三个 Fourier 变换性质支撑了整个论证：
> 1. **时域乘法 = 频域卷积**：将采样操作转化为频谱的平移叠加。
> 2. **Dirac 梳的自对偶性**：时域的脉冲列在频域仍为脉冲列。
> 3. **矩形窗 $\leftrightarrow$ sinc 函数**：理想低通滤波器的逆变换给出 sinc 插值核。
>
> 带限条件 $X(f) = 0,\; |f| > W$ 是定理的**充分必要前提** — 它保证频谱副本间的"安全距离"，使低通滤波能无损分离原始频谱。

> [!warning] 实际应用中的局限
> 1. **严格带限信号在时域上无紧支撑**：由 Paley-Wiener 定理，若 $X(f)$ 有紧支撑，则 $x(t)$ 是一个整函数（entire function），不可能在某个时刻之后恒为零。因此现实中的有限持续时间信号**不可能严格带限**。
> 2. **理想低通滤波器不可物理实现**：$\operatorname{sinc}$ 函数在时域上双侧无穷延伸且非因果，理想低通滤波器违反因果性。实际系统必须用近似滤波器（如 Butterworth、Chebyshev）。
> 3. **无穷求和不可实现**：$(\ast)$ 中的求和遍及所有 $n \in \mathbb{Z}$，实际只能取有限项截断，引入截断误差。
>
> 尽管如此，Shannon-Nyquist 定理作为**理论基石**，为模拟-数字转换设定了根本性的界限，一切数字音频（CD 采样率 44.1 kHz 对应 $W \approx 22$ kHz 的人耳听觉带宽）、数字通信和数字图像处理都建立在这一定理之上。
