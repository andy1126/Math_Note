---
title: Hermite 方程的级数解
date: 2026-06-20
tags:
  - 题解
  - 微分方程
  - ODE
  - 级数解法
  - Hermite方程
  - Hermite多项式
  - 量子谐振子
---

# Hermite 方程的级数解

## 题目

> 在常点 $x = 0$ 附近求 **Hermite 方程**
> $$y'' - 2x y' + \lambda y = 0, \quad \lambda \in \mathbb{R}$$
> 的幂级数解，讨论 $\lambda = 2n$（$n \in \mathbb{N}$）时级数截断为 **Hermite 多项式**的条件。

---

## 预备定义与定理

> [!note] Hermite 方程
> 标准形 $y'' + p y' + q y = 0$，$p(x) = -2x$，$q(x) = \lambda$。$p, q$ 均为多项式，在 $\mathbb{R}$ 上处处解析，故**每一点都是常点**。幂级数解的收敛半径为 $R = \infty$（整函数解）。

> [!note] Hermite 多项式 $H_n(x)$
> 当 $\lambda = 2n$（$n \in \mathbb{N}$）时，Hermite 方程有 $n$ 次多项式解——标准化后（首项系数 $2^n$）即为 **Hermite 多项式** $H_n(x)$。$H_n$ 在 $\mathbb{R}$ 上关于权函数 $w(x) = e^{-x^2}$ 正交：
> $$\int_{-\infty}^\infty H_m(x) H_n(x)\, e^{-x^2} dx = 2^n n! \sqrt{\pi}\, \delta_{mn}.$$
> 详见 [[Sturm-Liouville定理]]。

> [!abstract] 引理：常点的幂级数解
> 系数解析 $\Rightarrow$ 任意解解析于全平面（$R = \infty$）。详见 [[常点附近的幂级数解]]。

> [!abstract] 量子谐振子的联系
> 一维量子谐振子的无量纲 Schrödinger 方程为 $- \psi'' + x^2 \psi = E \psi$。作代换 $\psi(x) = e^{-x^2/2} y(x)$，得到 $y'' - 2x y' + (E - 1) y = 0$——恰为 $\lambda = E - 1$ 的 Hermite 方程。本征值 $E = 2n + 1$ 对应 $\lambda = 2n$，本征函数即 Hermite 函数 $e^{-x^2/2} H_n(x)$。

---

## 解答

### 第一步：设幂级数 $y = \sum a_k x^k$

$$y = \sum_{k=0}^{\infty} a_k x^k, \quad y' = \sum_{k=1}^{\infty} k a_k x^{k-1}, \quad y'' = \sum_{k=2}^{\infty} k(k-1) a_k x^{k-2}.$$

### 第二步：代入并移位指标

代入 $y'' - 2x y' + \lambda y = 0$。将三项化至统一的 $x^k$ 幂次：

- $y''$：$\sum_{k=0}^{\infty} (k+2)(k+1) a_{k+2} x^k$
- $-2x y'$：$-2 \sum_{k=1}^{\infty} k a_k x^k$
- $\lambda y$：$\lambda \sum_{k=0}^{\infty} a_k x^k$

合并（$k \geq 1$ 时三项均有贡献，$k = 0$ 仅一、三项）：
$$k = 0: \quad 2 a_2 + \lambda a_0 = 0 \;\Longrightarrow\; a_2 = -\frac{\lambda}{2} a_0.$$
$$k \geq 1: \quad (k+2)(k+1) a_{k+2} - 2k a_k + \lambda a_k = 0.$$

### 第三步：递推关系

对 $k \geq 1$，
$$(k+2)(k+1) a_{k+2} + (\lambda - 2k) a_k = 0,$$
即
$$a_{k+2} = \frac{2k - \lambda}{(k+2)(k+1)}\, a_k. \quad \cdots (\ast)$$

（验算：$k = 0$ 也适用此式，给出 $a_2 = -\frac{\lambda}{2} a_0$，一致。）

递推只连相差 $2$ 的指标，偶/奇独立：

- **偶次序列**：$a_0 \to a_2 \to a_4 \to \cdots$
- **奇次序列**：$a_1 \to a_3 \to a_5 \to \cdots$

### 第四步：前几项

$$a_2 = -\frac{\lambda}{2} a_0, \quad a_4 = \frac{4 - \lambda}{12} a_2 = \frac{\lambda(\lambda - 4)}{24} a_0,$$
$$a_3 = \frac{2 - \lambda}{6} a_1, \quad a_5 = \frac{6 - \lambda}{20} a_3 = \frac{(\lambda - 2)(\lambda - 6)}{120} a_1.$$

故两独立解：
$$y_{\text{even}} = a_0 \left(1 - \frac{\lambda}{2} x^2 + \frac{\lambda(\lambda - 4)}{24} x^4 - \frac{\lambda(\lambda - 4)(\lambda - 8)}{720} x^6 + \cdots \right),$$
$$y_{\text{odd}} = a_1 \left(x - \frac{\lambda - 2}{6} x^3 + \frac{(\lambda - 2)(\lambda - 6)}{120} x^5 - \cdots \right).$$

### 第五步：本征值截断 ⇒ 多项式

递推 $(\ast)$ 的分子 $2k - \lambda$。若 $\lambda = 2n$（$n \in \mathbb{N}$），则当 $k = n$ 时分子为零，$a_{n+2} = 0$，进而 $a_{n+4} = a_{n+6} = \cdots = 0$——**级数截断为 $n$ 次多项式**。

- $n$ 偶：偶次序列截断，奇次序列仍为无穷级数（$x \to \infty$ 时 $\sim e^{x^2}$ 发散）；
- $n$ 奇：奇次序列截断。

取非截断序列的 $a_0$（$n$ 奇）或 $a_1$（$n$ 偶）为 $0$，得多项式解。标准化使首项系数为 $2^n$，得 **Hermite 多项式**：
$$H_0 = 1,\ H_1 = 2x,\ H_2 = 4x^2 - 2,\ H_3 = 8x^3 - 12x,\ H_4 = 16x^4 - 48x^2 + 12.$$

### 第六步：收敛半径

对一般的 $\lambda \neq 2n$，$|a_{k+2}/a_k| \sim 2/k \to 0$，比值判别法给出 $R = \infty$。解为整函数。但 $x \to \infty$ 时解的渐近行为为 $y \sim C_1 e^{x^2} + C_2 x e^{x^2}$（当 $\lambda$ 非本征值时两个独立解都发散如 $e^{x^2}$）。仅在 $\lambda = 2n$ 时，截断支给出多项式的温和增长（乘以 $e^{-x^2/2}$ 后成为 $L^2$ 的 Hermite 函数）。$\blacksquare$

---

## 答案

$$\boxed{ y_{\text{even}} = a_0 \sum_{m=0}^{\infty} \frac{(-\lambda)(4-\lambda)\cdots(4m-4-\lambda)}{(2m)!}\, x^{2m} }$$
$$\boxed{ y_{\text{odd}} = a_1 \sum_{m=0}^{\infty} \frac{(2-\lambda)(6-\lambda)\cdots(4m-2-\lambda)}{(2m+1)!}\, x^{2m+1} }$$

当 $\lambda = 2n$（$n \in \mathbb{N}$）时，其中一支截断为 $n$ 次 Hermite 多项式 $H_n(x)$。

---

## 变形与延伸

> [!info] 变形 1（Rodrigues 公式与生成函数）
> $H_n(x) = (-1)^n e^{x^2} \frac{d^n}{dx^n} e^{-x^2}$（Rodrigues 公式）。生成函数：$\exp(2xt - t^2) = \sum_{n=0}^\infty H_n(x) \frac{t^n}{n!}$。
>
> **提示**：从生成函数可得递推 $H_{n+1} = 2x H_n - 2n H_{n-1}$ 和 $H_n' = 2n H_{n-1}$，均优于直接处理级数。

> [!info] 变形 2（量子谐振子的能级与零点能）
> 量子谐振子能量 $E_n = \hbar \omega (n + 1/2)$。讨论 Hermite 多项式截断条件 $\lambda = 2n$ 如何对应能量量子化，以及基态 $n = 0$ 的零点能 $\hbar\omega/2$。
>
> **提示**：边界条件 $\psi \in L^2(\mathbb{R})$ 要求 $\psi = e^{-x^2/2} y$ 平方可积，这排除了发散如 $e^{x^2}$ 的无穷级数解——本征值条件由此逼迫出来。这是 Sturm-Liouville 理论在无界域上的范本，见 [[Sturm-Liouville定理]]。

> [!info] 延伸（Hermite 函数与 Fourier 变换的不动点）
> $\phi_n(x) = \frac{1}{\sqrt{2^n n! \sqrt{\pi}}} e^{-x^2/2} H_n(x)$ 是 Fourier 变换的特征函数：$\mathcal{F}[\phi_n] = (-i)^n \phi_n$。
>
> **提示**：这源于量子谐振子的 Hamilton 量 $\hat{H} = \frac{1}{2}(\hat{x}^2 + \hat{p}^2)$ 在 Fourier 变换下的对称性。Hermite 函数是所有 $C^\infty \cap L^2$ 中"在 Fourier 对偶中最规整"的基底。
