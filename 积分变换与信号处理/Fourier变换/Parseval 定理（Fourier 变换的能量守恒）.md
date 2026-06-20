---
title: Parseval 定理（Fourier 变换的能量守恒）
date: 2026-04-19
tags:
  - 积分变换
  - Fourier变换
  - 信号与系统
  - 能量谱
  - Parseval
---

# Parseval 定理（Fourier 变换的能量守恒）

## 预备定义

> [!note] Fourier 变换（$L^1 \cap L^2$ 上的定义）
> 设 $x(t) \in L^1(\mathbb{R}) \cap L^2(\mathbb{R})$。$x(t)$ 的 **Fourier 变换**定义为
> $$X(f) = \mathcal{F}\{x\}(f) = \int_{-\infty}^{+\infty} x(t)\, e^{-j2\pi ft}\, dt,$$
> 其 **Fourier 逆变换**为
> $$x(t) = \mathcal{F}^{-1}\{X\}(t) = \int_{-\infty}^{+\infty} X(f)\, e^{j2\pi ft}\, df.$$
>
> 在 $L^1 \cap L^2$ 上，Fourier 变换和逆变换均为普通的 Lebesgue 积分，且互为逆运算。

> [!note] 信号的能量
> 信号 $x(t)$ 的**总能量**（total energy）定义为
> $$E_x = \int_{-\infty}^{+\infty} |x(t)|^2\, dt = \|x\|_{L^2}^2.$$
> 物理上，若 $x(t)$ 为电压信号通过 $1\,\Omega$ 电阻，则 $|x(t)|^2$ 为瞬时功率，$E_x$ 为总耗散能量。
> 称 $E_x < +\infty$ 的信号为**能量有限信号**（energy signal），即 $x \in L^2(\mathbb{R})$。

> [!note] 能量谱密度
> 设 $x(t)$ 为能量有限信号，$X(f) = \mathcal{F}\{x\}(f)$。称
> $$S_x(f) = |X(f)|^2$$
> 为 $x(t)$ 的**能量谱密度**（energy spectral density）。$S_x(f)\,df$ 表示信号在频率 $[f, f+df]$ 内的能量贡献。

> [!note] $L^2$ 内积
> $L^2(\mathbb{R})$ 上的**内积**定义为
> $$\langle x, y \rangle = \int_{-\infty}^{+\infty} x(t)\, \overline{y(t)}\, dt,$$
> 其中 $\overline{y(t)}$ 表示复共轭。对应的范数为 $\|x\| = \sqrt{\langle x, x \rangle}$。

> [!abstract] 引理：Fubini 定理（积分换序）
> 设 $h(x,y)$ 在 $\mathbb{R}^2$ 上可测，且 $\iint |h(x,y)|\,dx\,dy < +\infty$，则累次积分可交换顺序。

---

## 定理

**（Parseval 定理）** 设 $x, y \in L^1(\mathbb{R}) \cap L^2(\mathbb{R})$，其 Fourier 变换分别为 $X(f)$ 和 $Y(f)$。则：

**(i)** **内积守恒**（Parseval 恒等式）：

$$\int_{-\infty}^{+\infty} x(t)\, \overline{y(t)}\, dt = \int_{-\infty}^{+\infty} X(f)\, \overline{Y(f)}\, df.$$

即 $\langle x, y \rangle_{L^2} = \langle X, Y \rangle_{L^2}$：**Fourier 变换保持 $L^2$ 内积**。

**(ii)** **能量守恒**（Rayleigh 能量定理）：

$$\int_{-\infty}^{+\infty} |x(t)|^2\, dt = \int_{-\infty}^{+\infty} |X(f)|^2\, df.$$

即 $\|x\|_{L^2} = \|X\|_{L^2}$：**信号在时域和频域中的总能量相等**。

---

## 第(i)部分的证明

### 第一步：用 Fourier 逆变换表示 $y(t)$

由逆变换公式，

$$\overline{y(t)} = \overline{\int_{-\infty}^{+\infty} Y(f)\, e^{j2\pi ft}\, df} = \int_{-\infty}^{+\infty} \overline{Y(f)}\, e^{-j2\pi ft}\, df. \quad \cdots (\ast)$$

$\square$

### 第二步：代入内积并交换积分顺序

将 $(\ast)$ 代入左端内积：

$$\langle x, y \rangle = \int_{-\infty}^{+\infty} x(t)\, \overline{y(t)}\, dt = \int_{-\infty}^{+\infty} x(t) \left(\int_{-\infty}^{+\infty} \overline{Y(f)}\, e^{-j2\pi ft}\, df\right) dt.$$

> [!important] 交换积分顺序的正当性
> 需要验证 Fubini 定理的条件。被积函数的绝对值为
> $$|x(t)| \cdot |\overline{Y(f)}| \cdot |e^{-j2\pi ft}| = |x(t)| \cdot |Y(f)|.$$
> 由于 $x \in L^2$，$Y \in L^2$（因为 $y \in L^1 \cap L^2$ 保证 $Y \in L^2 \cap L^\infty$），且 $x \in L^1$，故
> $$\int\!\!\int |x(t)|\,|Y(f)|\,dt\,df = \|x\|_{L^1} \cdot \|Y\|_{L^1}.$$
> 当 $Y \in L^1$（由 $y \in L^1 \cap L^2$ 在适当条件下保证）时，此量有限，Fubini 定理适用。更一般地，可用 $L^2$ 上的稠密逼近论证绕过此限制。

交换积分顺序：

$$\langle x, y \rangle = \int_{-\infty}^{+\infty} \overline{Y(f)} \left(\int_{-\infty}^{+\infty} x(t)\, e^{-j2\pi ft}\, dt\right) df. \quad \cdots (\star)$$

$\square$

### 第三步：识别 Fourier 变换

$(\star)$ 中的内层积分恰为 $x(t)$ 的 Fourier 变换：

$$\int_{-\infty}^{+\infty} x(t)\, e^{-j2\pi ft}\, dt = X(f).$$

代入 $(\star)$ 得

$$\langle x, y \rangle = \int_{-\infty}^{+\infty} \overline{Y(f)}\, X(f)\, df = \int_{-\infty}^{+\infty} X(f)\, \overline{Y(f)}\, df = \langle X, Y \rangle.$$

因此 $\langle x, y \rangle_{L^2} = \langle X, Y \rangle_{L^2}$。$\square$

---

## 第(ii)部分的证明

在第(i)部分的结论中取 $y = x$：

$$\int_{-\infty}^{+\infty} x(t)\, \overline{x(t)}\, dt = \int_{-\infty}^{+\infty} X(f)\, \overline{X(f)}\, df,$$

即

$$\int_{-\infty}^{+\infty} |x(t)|^2\, dt = \int_{-\infty}^{+\infty} |X(f)|^2\, df.$$

用能量谱密度的记号，

$$E_x = \int_{-\infty}^{+\infty} S_x(f)\, df.$$

$\square$

---

## 总结

1. Fourier 变换保持 $L^2$ 内积：$\langle x, y \rangle = \langle X, Y \rangle$。 ✓
2. 取 $y = x$ 即得能量守恒：$\|x\|_{L^2}^2 = \|X\|_{L^2}^2$。 ✓

因此 Fourier 变换是 $L^2(\mathbb{R})$ 上的**等距映射**（isometry）。$\blacksquare$

---

## 应用示例

> [!info] 应用：利用 Parseval 定理计算困难积分
> 计算 $\displaystyle I = \int_{-\infty}^{+\infty} \operatorname{sinc}^2(t)\, dt$。
>
> 直接计算此积分不易。但注意 $\operatorname{sinc}(t) = \dfrac{\sin(\pi t)}{\pi t}$，且
> $$\mathcal{F}\{\operatorname{sinc}(t)\}(f) = \operatorname{rect}(f) = \begin{cases} 1, & |f| \leq \tfrac{1}{2}, \\ 0, & |f| > \tfrac{1}{2}. \end{cases}$$
>
> 由 Parseval 定理（能量守恒），
> $$I = \int_{-\infty}^{+\infty} |\operatorname{sinc}(t)|^2\, dt = \int_{-\infty}^{+\infty} |\operatorname{rect}(f)|^2\, df = \int_{-1/2}^{1/2} 1\, df = 1.$$
>
> 即 $\displaystyle\int_{-\infty}^{+\infty} \frac{\sin^2(\pi t)}{\pi^2 t^2}\, dt = 1$，等价于经典结果 $\displaystyle\int_{-\infty}^{+\infty} \frac{\sin^2 u}{u^2}\, du = \pi$。

> [!info] 应用：LTI 系统的输出能量
> 设 LTI 系统传递函数为 $H(f)$，输入信号 $x(t)$ 的能量谱密度为 $S_x(f) = |X(f)|^2$。
> 由 $Y(f) = H(f) \cdot X(f)$，输出能量为
> $$E_y = \int_{-\infty}^{+\infty} |Y(f)|^2\, df = \int_{-\infty}^{+\infty} |H(f)|^2 \cdot |X(f)|^2\, df = \int_{-\infty}^{+\infty} |H(f)|^2\, S_x(f)\, df.$$
>
> 这说明 $|H(f)|^2$ 作为**能量增益函数**，决定了每个频率分量的能量缩放比例。滤波器设计的本质就是塑造 $|H(f)|^2$ 的形状。

---

## 证明思路总结

> [!tip] 关键思想
> 证明仅用了一个核心操作：**在内积中用 Fourier 逆变换展开其中一个函数，然后交换积分顺序**。
>
> $$\langle x, y \rangle = \int x(t)\,\overline{y(t)}\,dt \;\xrightarrow{\;y = \mathcal{F}^{-1}\{Y\}\;}\; \int\!\!\int x(t)\,\overline{Y(f)}\,e^{-j2\pi ft}\,df\,dt \;\xrightarrow{\;\text{Fubini}\;}\; \int \overline{Y(f)} \underbrace{\left(\int x(t)\,e^{-j2\pi ft}\,dt\right)}_{= X(f)} df = \langle X, Y \rangle$$
>
> 从更高的视角看，Parseval 定理表明 **Fourier 变换是 $L^2(\mathbb{R})$ 上的酉算子**（unitary operator）：
> - **等距性**：$\|x\| = \|\mathcal{F}\{x\}\|$（能量守恒）；
> - **保内积性**：$\langle x, y \rangle = \langle \mathcal{F}\{x\}, \mathcal{F}\{y\} \rangle$；
> - **满射性**：$\mathcal{F}: L^2 \to L^2$ 是双射（Plancherel 定理）。
>
> 在信号处理中，这意味着**时域和频域是对同一信号的两种等价描述** — 不仅信息量相同（双射），而且"几何结构"（内积、能量、正交性）完全一致。

> [!warning] 从 $L^1 \cap L^2$ 到 $L^2$ 的推广
> 本文在 $L^1 \cap L^2$ 上给出了证明，此时 Fourier 变换由普通积分定义。对一般的 $L^2$ 函数（可能不在 $L^1$ 中），Fourier 变换不能用 Lebesgue 积分直接定义，需要通过 $L^1 \cap L^2$ 上的稠密逼近和等距延拓来构造。这就是 **Plancherel 定理**的内容：
>
> > $\mathcal{F}$ 在 $L^1 \cap L^2$ 上的定义可以唯一地延拓为 $L^2(\mathbb{R})$ 上的酉算子。
>
> 此推广保证了 Parseval 定理对一切 $L^2$ 信号成立，而不仅限于同时属于 $L^1$ 的信号。
