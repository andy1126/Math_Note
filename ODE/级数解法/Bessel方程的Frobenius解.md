---
title: Bessel 方程的 Frobenius 解
date: 2026-06-20
tags:
  - 题解
  - 微分方程
  - ODE
  - 级数解法
  - Frobenius方法
  - Bessel方程
  - 特殊函数
---

# Bessel 方程的 Frobenius 解

## 题目

> 求 **Bessel 方程**
> $$x^2 y'' + x y' + (x^2 - \nu^2) y = 0, \quad \nu \geq 0$$
> 在正则奇点 $x = 0$ 处的**指标方程**，并求出较大的指标根对应的第一个 Frobenius 级数解（即 $J_\nu(x)$ 的级数表达式）。

---

## 预备定义与定理

> [!note] Bessel 方程（标准形与参数）
> $$x^2 y'' + x y' + (x^2 - \nu^2) y = 0, \quad \nu \geq 0.$$
> 写成标准形 $y'' + p(x) y' + q(x) y = 0$：
> $$p(x) = \frac{1}{x}, \qquad q(x) = \frac{x^2 - \nu^2}{x^2} = 1 - \frac{\nu^2}{x^2}.$$
> $p$ 与 $q$ 在 $x = 0$ 处不解析，故 $x = 0$ 为**奇点**。

> [!note] 正则奇点（regular singular point）
> 称 $x_0$ 为方程 $y'' + p y' + q y = 0$ 的**正则奇点**，若 $(x - x_0) p(x)$ 和 $(x - x_0)^2 q(x)$ 在 $x_0$ 处解析。
>
> 对 Bessel 方程：$x p(x) = 1$（解析），$x^2 q(x) = x^2 - \nu^2$（解析）。故 $x = 0$ 是正则奇点。详见 [[正则奇点与Frobenius方法]]。

> [!abstract] 定理：Frobenius 方法（正则奇点情形）
> 在正则奇点 $x_0 = 0$ 处，至少存在一个形如
> $$y = x^r \sum_{n=0}^{\infty} a_n x^n = \sum_{n=0}^{\infty} a_n x^{n+r}, \quad a_0 \neq 0$$
> 的 Frobenius 级数解，其中 $r$ 由**指标方程**确定。指标方程及递推关系由代入级数并对齐 $x^{n+r}$ 的最低次幂得出。详见 [[正则奇点与Frobenius方法]]。

> [!note] 指标方程（indicial equation）
> 设 $p(x) = \frac{1}{x}\sum_{n=0}^{\infty} p_n x^n$，$q(x) = \frac{1}{x^2}\sum_{n=0}^{\infty} q_n x^n$（$p_0, q_0$ 为常数项）。则指标方程为
> $$r(r-1) + p_0 r + q_0 = 0.$$
> 对 Bessel 方程：$p_0 = 1,\ q_0 = -\nu^2$，故指标方程为 $r(r-1) + r - \nu^2 = r^2 - \nu^2 = 0$，根为 $r = \pm\nu$。

> [!abstract] 定义：第一类 Bessel 函数 $J_\nu(x)$
> $J_\nu(x)$ 是 Bessel 方程对应于较大指标根 $r = \nu$（$\nu \geq 0$）的标准解，定义为
> $$J_\nu(x) = \sum_{k=0}^{\infty} \frac{(-1)^k}{k!\,\Gamma(k + \nu + 1)}\left(\frac{x}{2}\right)^{2k + \nu}.$$
> 此处 $\Gamma$ 为 Gamma 函数（$\Gamma(z+1) = z!$ 对正整数 $z$）。本文即导出此公式。

> [!abstract] 引理：Gamma 函数的递推
> $\Gamma(z+1) = z\,\Gamma(z)$。特别对 $n \in \mathbb{N}$，$\Gamma(n+1) = n!$。

---

## 解答

### 第一步：确认奇点类型

$p(x) = 1/x$，$q(x) = 1 - \nu^2/x^2$。则
$$x p(x) = 1 =: P(x), \qquad x^2 q(x) = x^2 - \nu^2 =: Q(x).$$

$P, Q$ 均为多项式（常数 $1$，多项式 $x^2 - \nu^2$），在 $x = 0$ 处解析。故 $x = 0$ 是**正则奇点**，可用 Frobenius 方法。

### 第二步：设 Frobenius 级数

$$y = \sum_{n=0}^{\infty} a_n x^{n+r}, \quad a_0 \neq 0.$$

逐项求导：
$$y' = \sum_{n=0}^{\infty} (n+r) a_n x^{n+r-1},$$
$$y'' = \sum_{n=0}^{\infty} (n+r)(n+r-1) a_n x^{n+r-2}.$$

### 第三步：代入 Bessel 方程

将 $y, y', y''$ 代入 $x^2 y'' + x y' + (x^2 - \nu^2) y = 0$：

- $x^2 y'' = \sum_{n=0}^{\infty} (n+r)(n+r-1) a_n x^{n+r}$；
- $x y' = \sum_{n=0}^{\infty} (n+r) a_n x^{n+r}$；
- $(x^2 - \nu^2) y = x^2 y - \nu^2 y = \sum_{n=0}^{\infty} a_n x^{n+r+2} - \nu^2 \sum_{n=0}^{\infty} a_n x^{n+r}$。

合并前三项的 $x^{n+r}$ 部分（不含 $x^2 y$）：
$$\sum_{n=0}^{\infty} \Big[ (n+r)(n+r-1) + (n+r) - \nu^2 \Big] a_n x^{n+r} + \sum_{n=0}^{\infty} a_n x^{n+r+2} = 0.$$

化简括号内的表达式：
$$(n+r)(n+r-1) + (n+r) - \nu^2 = (n+r)\big((n+r-1) + 1\big) - \nu^2 = (n+r)^2 - \nu^2.$$

故方程化为
$$\sum_{n=0}^{\infty} \big[(n+r)^2 - \nu^2\big] a_n x^{n+r} + \sum_{n=0}^{\infty} a_n x^{n+r+2} = 0.$$

### 第四步：提取最低次幂——指标方程

对齐 $x^{n+r}$ 的系数。第二个级数的指标偏后两个单位（$x^{n+r+2}$），故最低次幂 $x^r$（对应 $n = 0$）仅来自第一级数。其系数必为零：
$$[r^2 - \nu^2]\, a_0 = 0.$$

因 $a_0 \neq 0$（首项非零约定），得到指标方程：
$$r^2 - \nu^2 = 0 \;\Longrightarrow\; r = \pm\nu.$$

> [!important] 指标根
> $r_1 = \nu$（较大根），$r_2 = -\nu$（较小根）。当 $\nu \geq 0$ 时 $r_1 \geq r_2$，两根之差为 $2\nu$。差为整数（尤其 $2\nu \in \mathbb{Z}$）的情形决定了第二个解是否含 $\ln x$ 项——此处先求 $r = \nu$ 对应的第一个解。

### 第五步：$x^{r+1}$ 项的系数

考察 $n = 1$。第一级数贡献 $[(1+r)^2 - \nu^2] a_1$；第二级数尚未出现 $x^{r+1}$ 项（其最小指数为 $r+2$，对应 $n=0$ 项的 $a_0 x^{r+2}$）。故
$$[(1+r)^2 - \nu^2]\, a_1 = 0.$$

代入 $r = \nu$：$(1+\nu)^2 - \nu^2 = 1 + 2\nu + \nu^2 - \nu^2 = 1 + 2\nu$。若 $1 + 2\nu \neq 0$（即 $\nu \neq -1/2$，$\nu \geq 0$ 时必然成立），则
$$a_1 = 0.$$

（$\nu = -1/2$ 为特殊情形，不在本文讨论范围。）

### 第六步：一般递推关系

对 $n \geq 2$，对齐 $x^{n+r}$ 的系数。第二级数以 $n-2$ 的项贡献 $a_{n-2} x^{(n-2)+r+2} = a_{n-2} x^{n+r}$。故：
$$[(n+r)^2 - \nu^2]\, a_n + a_{n-2} = 0, \qquad n \geq 2.$$

即
$$a_n = -\frac{a_{n-2}}{(n+r)^2 - \nu^2}. \quad \cdots (\ast)$$

> [!important] 递推结构的特征
> $(\ast)$ 只连接指标相差 $2$ 的系数。与 Airy 方程（模 $3$）类似，系数按指标奇偶分为两个独立序列。由于 $a_1 = 0$，递推得**所有奇次系数均为零**：$a_1 = a_3 = a_5 = \cdots = 0$。

### 第七步：求解偶次系数序列（$r = \nu$）

令 $n = 2k$（$k \geq 1$）。代入 $(\ast)$，$r = \nu$：
$$a_{2k} = -\frac{a_{2k-2}}{(2k + \nu)^2 - \nu^2} = -\frac{a_{2k-2}}{4k^2 + 4k\nu} = -\frac{a_{2k-2}}{4k(k + \nu)}.$$

改写成从 $a_{2(k-1)}$ 到 $a_{2k}$ 的递推：
$$a_{2k} = -\frac{a_{2(k-1)}}{2^2\, k\, (k + \nu)}, \qquad k \geq 1.$$

**展开前几项**（$a_0$ 自由）：
$$\begin{aligned}
a_2 &= -\frac{a_0}{2^2 \cdot 1 \cdot (1 + \nu)}, \\
a_4 &= -\frac{a_2}{2^2 \cdot 2 \cdot (2 + \nu)} = \frac{a_0}{2^4 \cdot 1 \cdot 2 \cdot (1+\nu)(2+\nu)}, \\
a_6 &= -\frac{a_4}{2^2 \cdot 3 \cdot (3 + \nu)} = -\frac{a_0}{2^6 \cdot 1 \cdot 2 \cdot 3 \cdot (1+\nu)(2+\nu)(3+\nu)}.
\end{aligned}$$

### 第八步：导出 $J_\nu(x)$ 的级数

**通项**（归纳可得）：
$$a_{2k} = \frac{(-1)^k\, a_0}{2^{2k}\, k!\, (\nu+1)(\nu+2)\cdots(\nu+k)}.$$

用 Gamma 函数改写分母：$(\nu+1)(\nu+2)\cdots(\nu+k) = \dfrac{\Gamma(\nu+k+1)}{\Gamma(\nu+1)}$。

取标准归一化 $a_0 = \dfrac{1}{2^\nu\,\Gamma(\nu+1)}$，则
$$a_{2k} = \frac{(-1)^k}{2^{2k+\nu}\, k!\, \Gamma(k + \nu + 1)}.$$

于是第一个 Frobenius 解为
$$y = \sum_{k=0}^{\infty} a_{2k} x^{2k+\nu} = \sum_{k=0}^{\infty} \frac{(-1)^k}{k!\,\Gamma(k+\nu+1)} \left(\frac{x}{2}\right)^{2k+\nu}.$$

这恰为**第一类 Bessel 函数 $J_\nu(x)$**。$\blacksquare$

### 第九步：级数前几项

$$J_\nu(x) = \frac{1}{\Gamma(\nu+1)}\left(\frac{x}{2}\right)^\nu \left[ 1 - \frac{1}{1!\,(\nu+1)}\left(\frac{x}{2}\right)^2 + \frac{1}{2!\,(\nu+1)(\nu+2)}\left(\frac{x}{2}\right)^4 - \cdots \right].$$

**半整数阶特例**（$\nu = 1/2$）：
$$J_{1/2}(x) = \frac{1}{\Gamma(3/2)}\left(\frac{x}{2}\right)^{1/2} \left[ 1 - \frac{x^2}{6} + \cdots \right].$$

因 $\Gamma(3/2) = \dfrac{\sqrt{\pi}}{2}$，$J_{1/2}(x) = \sqrt{\dfrac{2}{\pi x}}\, \sin x$。

---

## 答案

Bessel 方程 $x^2 y'' + x y' + (x^2 - \nu^2) y = 0$ 在 $x = 0$ 处的：
- **指标方程**：$r^2 - \nu^2 = 0$，根为 $r = \pm\nu$；
- **第一个 Frobenius 解**（$r = \nu \geq 0$）：
$$\boxed{\,J_\nu(x) = \sum_{k=0}^{\infty} \frac{(-1)^k}{k!\,\Gamma(k+\nu+1)} \left(\frac{x}{2}\right)^{2k+\nu}\,}$$

---

## 变形与延伸

> [!info] 变形 1（第二个解：$J_{-\nu}$ 与 $Y_\nu$）
> 当 $2\nu \notin \mathbb{Z}$ 时，$J_{-\nu}(x)$ 是与 $J_\nu(x)$ 线性独立的第二个 Frobenius 解。但当 $\nu$ 为整数 $n$ 时，$J_{-n}(x) = (-1)^n J_n(x)$（线性相关），此时第二个解含 $\ln x$ 项，即**第二类 Bessel 函数 $Y_\nu(x)$**（又称 Neumann 函数）：
> $$Y_n(x) = \frac{2}{\pi} J_n(x) \ln\frac{x}{2} - \frac{1}{\pi} \sum_{k=0}^{n-1} \frac{(n-k-1)!}{k!} \left(\frac{x}{2}\right)^{2k-n} - \frac{1}{\pi} \sum_{k=0}^{\infty} (\cdots).$$
> **提示**：用 Frobenius 第二情形（根差整数）或降阶法从 $J_n$ 构造 $Y_n$，详见 [[正则奇点与Frobenius方法]]。

> [!info] 变形 2（Bessel 方程在本征值问题中的角色）
> Bessel 方程出现在圆域 / 柱坐标下 Laplace 算子的分离变量中。方程 $x^2 y'' + x y' + (\lambda x^2 - \nu^2) y = 0$ 在 $[0, R]$ 上配合边条件 $y(R) = 0$ 构成 Sturm-Liouville 本征值问题，本征值为 $J_\nu(\sqrt{\lambda} R) = 0$ 的根。
>
> **提示**：权函数为 $x$，Bessel 函数的正交性 $\int_0^R x J_\nu(\alpha_{m} x/R) J_\nu(\alpha_n x/R) dx = 0$（$m \neq n$）来自 [[Sturm-Liouville定理]]。

> [!info] 变形 3（修正 Bessel 方程）
> 解 $x^2 y'' + x y' - (x^2 + \nu^2) y = 0$（修正 Bessel 方程），其解为 $I_\nu(x), K_\nu(x)$。
>
> **提示**：作代换 $x \mapsto ix$，Bessel 方程变为修正形；$I_\nu(x) = i^{-\nu} J_\nu(ix)$。指标方程相同，级数仅符号变化（所有 $(-1)^k$ 变为 $+1$）。

> [!info] 延伸（Bessel 函数的渐近行为与生成函数）
> $x \to \infty$ 时 $J_\nu(x) \sim \sqrt{\frac{2}{\pi x}} \cos\!\left(x - \frac{\nu\pi}{2} - \frac{\pi}{4}\right)$。Bessel 函数有生成函数 $\exp\!\big(\frac{x}{2}(t - 1/t)\big) = \sum_{n=-\infty}^\infty J_n(x) t^n$，由此可得所有整数阶 Bessel 函数的统一表达式。
>
> **提示**：将生成函数展为 Laurent 级数，比较 $t^n$ 系数即得 $J_n$ 的级数——这比直接解 Frobenius 递推更快捷（对整数阶）。
