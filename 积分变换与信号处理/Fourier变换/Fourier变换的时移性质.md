---
title: Fourier 变换的时移性质
date: 2026-04-19
tags:
  - 积分变换
  - Fourier变换
  - 信号与系统
  - 时移
---

# Fourier 变换的时移性质

## 预备定义

> [!note] Fourier 变换
> 设 $x(t)$ 为绝对可积信号，即 $x \in L^1(\mathbb{R})$。其 **Fourier 变换**（Fourier transform）定义为
> $$X(j\omega) = \mathcal{F}\{x(t)\} = \int_{-\infty}^{\infty} x(t)\, e^{-j\omega t}\, dt,$$
> 其中 $\omega \in \mathbb{R}$ 为角频率，$j = \sqrt{-1}$ 为虚数单位。
>
> 对应的 **Fourier 逆变换**为
> $$x(t) = \mathcal{F}^{-1}\{X(j\omega)\} = \frac{1}{2\pi} \int_{-\infty}^{\infty} X(j\omega)\, e^{j\omega t}\, d\omega.$$

> [!note] 时移信号
> 设 $x(t)$ 为信号，$t_0 \in \mathbb{R}$ 为常数。称 $x(t - t_0)$ 为 $x(t)$ 的**时移信号**（time-shifted signal）。
>
> - 当 $t_0 > 0$ 时，信号向**右**（未来方向）平移，称为**延迟**（delay）。
> - 当 $t_0 < 0$ 时，信号向**左**（过去方向）平移，称为**超前**（advance）。
>
> 时移不改变信号的形状，仅改变其在时间轴上的位置。

> [!note] 复指数的模
> 对任意实数 $\theta$，复指数 $e^{j\theta}$ 满足
> $$|e^{j\theta}| = 1.$$
> 因此 $e^{j\theta}$ 仅贡献**相位**，不改变**幅度**。

---

## 定理

设 $x(t) \in L^1(\mathbb{R})$，其 Fourier 变换为 $X(j\omega)$。则对任意 $t_0 \in \mathbb{R}$，

$$\mathcal{F}\{x(t - t_0)\} = e^{-j\omega t_0}\, X(j\omega).$$

等价地，用变换对记号表示：

$$x(t) \longleftrightarrow X(j\omega) \quad \Longrightarrow \quad x(t - t_0) \longleftrightarrow e^{-j\omega t_0}\, X(j\omega).$$

---

## 证明

### 第一步：写出时移信号的 Fourier 变换

由 Fourier 变换的定义，

$$\mathcal{F}\{x(t - t_0)\} = \int_{-\infty}^{\infty} x(t - t_0)\, e^{-j\omega t}\, dt. \quad \cdots (\ast)$$

$\square$

### 第二步：换元化简

在 $(\ast)$ 中作变量替换。令

$$\tau = t - t_0, \qquad d\tau = dt.$$

当 $t \to -\infty$ 时 $\tau \to -\infty$；当 $t \to +\infty$ 时 $\tau \to +\infty$。且 $t = \tau + t_0$。

代入得

$$\mathcal{F}\{x(t - t_0)\} = \int_{-\infty}^{\infty} x(\tau)\, e^{-j\omega(\tau + t_0)}\, d\tau. \quad \cdots (\star)$$

$\square$

### 第三步：分离常数相位因子

将 $(\star)$ 中的指数拆分：

$$e^{-j\omega(\tau + t_0)} = e^{-j\omega \tau} \cdot e^{-j\omega t_0}.$$

注意 $e^{-j\omega t_0}$ 不依赖于积分变量 $\tau$，因此可以提到积分号外：

$$\mathcal{F}\{x(t - t_0)\} = e^{-j\omega t_0} \int_{-\infty}^{\infty} x(\tau)\, e^{-j\omega \tau}\, d\tau.$$

$\square$

### 第四步：识别 Fourier 变换

上式中的积分恰好就是 $x(t)$ 的 Fourier 变换（以 $\tau$ 为积分变量）：

$$\int_{-\infty}^{\infty} x(\tau)\, e^{-j\omega \tau}\, d\tau = X(j\omega).$$

因此

$$\mathcal{F}\{x(t - t_0)\} = e^{-j\omega t_0}\, X(j\omega). \quad \blacksquare$$

---

## 推论

> [!abstract] 推论一：时移不改变幅度谱
> 由时移性质，
> $$|\mathcal{F}\{x(t - t_0)\}| = |e^{-j\omega t_0}| \cdot |X(j\omega)| = |X(j\omega)|.$$
> 因此时移信号 $x(t - t_0)$ 与原信号 $x(t)$ 具有**相同的幅度谱**（magnitude spectrum）。

> [!abstract] 推论二：时移仅引入线性相移
> 设 $X(j\omega) = |X(j\omega)|\, e^{j\varphi(\omega)}$，其中 $\varphi(\omega)$ 为 $x(t)$ 的相位谱。则
> $$\mathcal{F}\{x(t - t_0)\} = |X(j\omega)|\, e^{j[\varphi(\omega) - \omega t_0]}.$$
> 时移信号的相位谱为 $\varphi(\omega) - \omega t_0$，即在原相位谱上叠加了一个关于 $\omega$ 的**线性项** $-\omega t_0$。

---

## 证明思路总结

> [!tip] 关键思想
> 本证明的核心是一个**简单的换元**：令 $\tau = t - t_0$。
>
> 换元后，指数项 $e^{-j\omega t}$ 变为 $e^{-j\omega(\tau + t_0)}$，自然分裂为：
> - **与 $\tau$ 有关的部分** $e^{-j\omega\tau}$ —— 留在积分内，恢复为原信号的 Fourier 变换 $X(j\omega)$；
> - **与 $\tau$ 无关的部分** $e^{-j\omega t_0}$ —— 作为常数因子提出积分号。
>
> 这体现了 Fourier 变换的一个核心直觉：**时域的平移对应频域的相位旋转**。信号在时间轴上滑动 $t_0$，等价于给每个频率分量乘以一个大小为 1 的复数 $e^{-j\omega t_0}$，即旋转了角度 $-\omega t_0$。幅度谱完全不变，只有相位谱发生线性偏移。

> [!warning] 与频移性质的对偶
> 时移性质有一个**对偶**（dual）命题——**频移性质**（frequency shifting property）：
> $$e^{j\omega_0 t}\, x(t) \longleftrightarrow X(j(\omega - \omega_0)).$$
> 时域乘以复指数 $\leftrightarrow$ 频域平移。这与时移性质（时域平移 $\leftrightarrow$ 频域乘以复指数）形成完美的对称。两者都源于 Fourier 变换和逆变换在形式上的对称性。
