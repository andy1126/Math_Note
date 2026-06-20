---
title: 复指数信号是 LTI 系统的特征函数
date: 2026-04-19
tags:
  - 信号与系统
  - LTI系统
  - 特征函数
  - 卷积
  - 传递函数
---

# 复指数信号是 LTI 系统的特征函数

## 预备定义

> [!note] LTI 系统
> 称系统 $\mathcal{T}$ 为**线性时不变系统**（linear time-invariant system，LTI 系统），若满足：
> 1. **线性**：对任意信号 $x_1(t), x_2(t)$ 和常数 $a, b \in \mathbb{C}$，
>    $$\mathcal{T}\{a\, x_1(t) + b\, x_2(t)\} = a\, \mathcal{T}\{x_1(t)\} + b\, \mathcal{T}\{x_2(t)\}.$$
> 2. **时不变**：若 $\mathcal{T}\{x(t)\} = y(t)$，则对任意 $t_0 \in \mathbb{R}$，
>    $$\mathcal{T}\{x(t - t_0)\} = y(t - t_0).$$

> [!note] 冲激响应与卷积表示
> LTI 系统完全由其**冲激响应**（impulse response）$h(t)$ 决定。对任意输入 $x(t)$，系统输出为
> $$y(t) = (h * x)(t) = \int_{-\infty}^{\infty} h(\tau)\, x(t - \tau)\, d\tau,$$
> 其中 $*$ 表示卷积运算。此公式成立的条件是上述积分绝对收敛。

> [!note] 特征函数与特征值
> 设 $\mathcal{T}$ 为一个算子（operator）。若存在非零函数 $\varphi(t)$ 和常数 $\lambda$，使得
> $$\mathcal{T}\{\varphi(t)\} = \lambda\, \varphi(t),$$
> 则称 $\varphi(t)$ 为 $\mathcal{T}$ 的**特征函数**（eigenfunction），$\lambda$ 为对应的**特征值**（eigenvalue）。
>
> 特征函数的意义：算子仅对其作**标量缩放**，不改变其函数形式。

> [!note] 系统函数（传递函数）
> 设 LTI 系统的冲激响应为 $h(t)$，定义其**系统函数**（system function）或**传递函数**（transfer function）为
> $$H(s) = \int_{-\infty}^{\infty} h(\tau)\, e^{-s\tau}\, d\tau, \quad s \in \mathbb{C},$$
> 即 $h(t)$ 的（双边）Laplace 变换。当 $s = j\omega$ 时，$H(j\omega)$ 即为系统的**频率响应**（frequency response），是 $h(t)$ 的 Fourier 变换。
>
> $H(s)$ 仅在使积分绝对收敛的 $s$ 值（即**收敛域** ROC）上有定义。

---

## 定理

设 $\mathcal{T}$ 为冲激响应为 $h(t)$ 的 LTI 系统，$s \in \mathbb{C}$ 属于 $H(s)$ 的收敛域。则

$$\mathcal{T}\{e^{st}\} = H(s)\, e^{st}.$$

即**复指数信号 $e^{st}$ 是 LTI 系统的特征函数**，对应的**特征值为 $H(s)$**。

特别地，取 $s = j\omega$（纯虚数），有

$$\mathcal{T}\{e^{j\omega t}\} = H(j\omega)\, e^{j\omega t}.$$

---

## 证明

### 第一步：写出卷积表达式

将 $x(t) = e^{st}$ 代入卷积公式，得系统输出

$$y(t) = \int_{-\infty}^{\infty} h(\tau)\, x(t - \tau)\, d\tau = \int_{-\infty}^{\infty} h(\tau)\, e^{s(t - \tau)}\, d\tau. \quad \cdots (\ast)$$

$\square$

### 第二步：分离关于 $t$ 的因子

将 $(\ast)$ 中的指数拆分：

$$e^{s(t - \tau)} = e^{st} \cdot e^{-s\tau}.$$

其中 $e^{st}$ 不依赖于积分变量 $\tau$，可提出积分号外：

$$y(t) = e^{st} \int_{-\infty}^{\infty} h(\tau)\, e^{-s\tau}\, d\tau. \quad \cdots (\star)$$

> [!important] 提取 $e^{st}$ 的合法性
> 将 $e^{st}$ 提出积分号的前提是积分 $\displaystyle\int_{-\infty}^{\infty} h(\tau)\, e^{-s\tau}\, d\tau$ 绝对收敛，即 $s$ 处于系统函数 $H(s)$ 的收敛域内。这正是定理条件所要求的。

$\square$

### 第三步：识别系统函数

$(\star)$ 中的积分恰好就是 $H(s)$ 的定义：

$$\int_{-\infty}^{\infty} h(\tau)\, e^{-s\tau}\, d\tau = H(s).$$

因此

$$y(t) = H(s)\, e^{st}.$$

输出 $y(t)$ 与输入 $e^{st}$ 仅差一个常数因子 $H(s)$，函数形式完全不变。这正是特征函数的定义。$\blacksquare$

---

## 推论

> [!abstract] 推论一：正弦信号通过 LTI 系统的稳态响应
> 设实信号 $x(t) = A\cos(\omega_0 t + \phi)$ 输入一个稳定的 LTI 系统。利用 Euler 公式将 $\cos$ 拆为两个复指数，由线性性和特征函数性质，稳态输出为
> $$y(t) = A\,|H(j\omega_0)|\,\cos\!\big(\omega_0 t + \phi + \angle H(j\omega_0)\big).$$
> 即：
> - **频率不变**：输出仍为频率 $\omega_0$ 的正弦信号；
> - **幅度被缩放**：缩放因子为 $|H(j\omega_0)|$；
> - **相位被偏移**：偏移量为 $\angle H(j\omega_0)$。

**证明**：将 $x(t)$ 用 Euler 公式展开：

$$x(t) = \frac{A}{2}\, e^{j(\omega_0 t + \phi)} + \frac{A}{2}\, e^{-j(\omega_0 t + \phi)} = \frac{A}{2}\, e^{j\phi}\, e^{j\omega_0 t} + \frac{A}{2}\, e^{-j\phi}\, e^{-j\omega_0 t}.$$

由系统的线性性和特征函数定理：

$$y(t) = \frac{A}{2}\, e^{j\phi}\, H(j\omega_0)\, e^{j\omega_0 t} + \frac{A}{2}\, e^{-j\phi}\, H(-j\omega_0)\, e^{-j\omega_0 t}. \quad \cdots (1)$$

由于 $h(t)$ 为实函数，$H(j\omega)$ 具有**共轭对称性**：$H(-j\omega_0) = \overline{H(j\omega_0)}$。

设 $H(j\omega_0) = |H(j\omega_0)|\, e^{j\theta}$，其中 $\theta = \angle H(j\omega_0)$。则 $H(-j\omega_0) = |H(j\omega_0)|\, e^{-j\theta}$。代入 $(1)$：

$$y(t) = \frac{A\,|H(j\omega_0)|}{2}\left(e^{j(\omega_0 t + \phi + \theta)} + e^{-j(\omega_0 t + \phi + \theta)}\right) = A\,|H(j\omega_0)|\,\cos(\omega_0 t + \phi + \theta). \quad \square$$

> [!abstract] 推论二：特征函数性质赋予传递函数物理意义
> 对于频率为 $\omega$ 的正弦输入，$|H(j\omega)|$ 是该频率分量的**增益**（gain），$\angle H(j\omega)$ 是该频率分量的**相移**（phase shift）。
>
> 这正是为什么 $H(j\omega)$ 被称为"频率响应"——它逐频率地描述系统对每个正弦分量的幅度缩放和相位旋转。

---

## 证明思路总结

> [!tip] 关键思想
> 证明的核心极其简洁：将 $e^{st}$ 代入卷积积分后，指数函数的**可分离性**
> $$e^{s(t-\tau)} = e^{st} \cdot e^{-s\tau}$$
> 使得 $e^{st}$ 可以整体从积分中提出，剩余部分恰好构成 $H(s)$ 的定义式。
>
> 这个结果揭示了一个深刻的事实：**复指数是唯一一类通过任意 LTI 系统后形式不变的信号**。正因如此，将任意信号分解为复指数的叠加（即 Fourier 变换 / Laplace 变换）才成为分析 LTI 系统的自然工具——每个分量独立通过系统，只被缩放和旋转，互不干扰。
>
> 这可以说是**信号与系统整个频域方法论的逻辑起点**。

> [!warning] 稳定性与收敛域
> 定理要求 $s$ 位于 $H(s)$ 的收敛域内。对于因果且稳定的系统，收敛域包含虚轴 $s = j\omega$，因此 $e^{j\omega t}$ 一定是特征函数。但对于不稳定系统，虚轴可能不在收敛域内，此时 $e^{j\omega t}$ 通过系统后的输出可能不收敛，特征函数关系不再成立。
