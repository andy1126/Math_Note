---
title: Fourier 级数
date: 2026-06-21
tags:
  - 数学物理方法
  - Fourier分析
  - 级数展开
  - 正交函数系
  - 分离变量法
---

# Fourier 级数

## 预备定义

> [!note] 正交函数系
> 函数族 $\{\phi_n\}_{n=0}^\infty$ 在区间 $[a,b]$ 上关于权函数 $w(x) \geq 0$ **正交**，若：
> $$\int_a^b \phi_m(x) \phi_n(x) \, w(x) \, dx = 0, \quad m \neq n$$
> 若还有 $\int_a^b \phi_n^2 w \, dx = 1$ 对所有 $n$ 成立，则称为**标准正交系**（orthonormal system）。

> [!note] Fourier 级数的定义
> 设 $f(x)$ 在 $[-L, L]$ 上可积。$f$ 的**Fourier 级数**为：
> $$f(x) \sim \frac{a_0}{2} + \sum_{n=1}^\infty \left( a_n \cos\frac{n\pi x}{L} + b_n \sin\frac{n\pi x}{L} \right)$$
> 其中 **Fourier 系数**为：
> $$a_n = \frac{1}{L} \int_{-L}^L f(x) \cos\frac{n\pi x}{L} \, dx, \quad n = 0, 1, 2, \ldots$$
> $$b_n = \frac{1}{L} \int_{-L}^L f(x) \sin\frac{n\pi x}{L} \, dx, \quad n = 1, 2, 3, \ldots$$

---

## 基础引理：三角函数的正交性

> [!abstract] 引理
> 在 $[-L, L]$ 上，三角函数系 $\{1, \cos\frac{n\pi x}{L}, \sin\frac{n\pi x}{L}\}$ 关于权函数 $w(x) = 1$ 正交。

**证明**：只需验证（对所有 $m, n \geq 1$）：

**(i)** $\displaystyle\int_{-L}^L \cos\frac{m\pi x}{L} \cos\frac{n\pi x}{L} \, dx = L \delta_{mn}$

**(ii)** $\displaystyle\int_{-L}^L \sin\frac{m\pi x}{L} \sin\frac{n\pi x}{L} \, dx = L \delta_{mn}$

**(iii)** $\displaystyle\int_{-L}^L \cos\frac{m\pi x}{L} \sin\frac{n\pi x}{L} \, dx = 0$

**(iv)** $\displaystyle\int_{-L}^L 1 \cdot \cos\frac{n\pi x}{L} \, dx = \int_{-L}^L 1 \cdot \sin\frac{n\pi x}{L} \, dx = 0$

所有积分均通过积化和差公式计算。以 (i) 为例：当 $m \neq n$，
$$\int_{-L}^L \cos\frac{m\pi x}{L}\cos\frac{n\pi x}{L} dx = \frac{1}{2}\int_{-L}^L \left[\cos\frac{(m+n)\pi x}{L} + \cos\frac{(m-n)\pi x}{L}\right] dx = 0$$

当 $m=n$，$\cos^2\frac{n\pi x}{L} = \frac{1+\cos(2n\pi x/L)}{2}$，积分得 $L$。其余类似。$\square$

> [!info] 注
> 有时使用复指数形式 $\{e^{in\pi x/L}\}_{n\in\mathbb{Z}}$，正交关系为 $\frac{1}{2L}\int_{-L}^L e^{im\pi x/L} e^{-in\pi x/L} dx = \delta_{mn}$。

---

## Dirichlet 核与部分和

### 部分和的积分表示

Fourier 级数的第 $N$ 部分和为：
$$S_N f(x) = \frac{a_0}{2} + \sum_{n=1}^N \left( a_n \cos\frac{n\pi x}{L} + b_n \sin\frac{n\pi x}{L} \right)$$

将 Fourier 系数公式代入并利用积化和差，得到：
$$S_N f(x) = \frac{1}{L} \int_{-L}^L f(y) D_N\!\left(\frac{\pi(x-y)}{L}\right) dy$$

其中 $D_N(t)$ 称为 **Dirichlet 核**，具有封闭形式：
$$D_N(t) = \frac{1}{2} + \sum_{n=1}^N \cos(nt) = \frac{\sin((N+\frac{1}{2})t)}{2\sin(t/2)}, \quad t \neq 0$$

> [!abstract] Dirichlet 核的基本性质
> 1. $\displaystyle\frac{1}{L}\int_{-L}^L D_N\!\left(\frac{\pi x}{L}\right) dx = 1$（积分恒为 $1$）
> 2. $D_N(t)$ 在 $t=0$ 附近高度 $\approx N + \frac{1}{2}$，但振荡剧烈
> 3. $D_N$ 不是非负核（与热核不同），这是 Gibbs 现象的根源

---

## 收敛性定理

### 逐点收敛

> [!abstract] Dirichlet 定理（逐点收敛）
> 设 $f$ 在 $[-L, L]$ 上分段光滑（分段连续可微，且左右极限存在）。则在每点 $x$，Fourier 级数收敛到：
> $$\frac{f(x^+) + f(x^-)}{2}$$
> 特别地，在 $f$ 的连续点处，级数收敛到 $f(x)$。

**注**：本笔记陈述结论但不给出完整证明。证明依赖于 Riemann-Lebesgue 引理和 Dirichlet 核的局部化性质。

### $L^2$ 收敛

> [!abstract] $L^2$ 收敛定理
> 设 $f \in L^2(-L, L)$（即 $\int_{-L}^L |f|^2 < \infty$），则 Fourier 级数在 $L^2$ 范数下收敛到 $f$：
> $$\lim_{N\to\infty} \int_{-L}^L |f(x) - S_N f(x)|^2 \, dx = 0$$
> 这意味着三角函数系在 $L^2(-L, L)$ 中是**完备的**。

### Parseval 等式

> [!abstract] 推论：Parseval 等式
> $$\frac{1}{L} \int_{-L}^L |f(x)|^2 \, dx = \frac{a_0^2}{2} + \sum_{n=1}^\infty (a_n^2 + b_n^2)$$

---

## 正弦级数与余弦级数

### 奇延拓 → 正弦级数

若 $f(x)$ 在 $[0, L]$ 上定义，将其**奇延拓**至 $[-L, L]$：
$$f_{\text{odd}}(x) = \begin{cases} f(x), & x \in [0, L] \\ -f(-x), & x \in [-L, 0) \end{cases}$$

则所有 $a_n = 0$（奇函数 $\times$ 偶函数 = 奇函数），得到**正弦级数**：
$$f(x) \sim \sum_{n=1}^\infty b_n \sin\frac{n\pi x}{L}, \quad b_n = \frac{2}{L} \int_0^L f(x) \sin\frac{n\pi x}{L} \, dx$$

### 偶延拓 → 余弦级数

类似地，**偶延拓**使得所有 $b_n = 0$，得到**余弦级数**：
$$f(x) \sim \frac{a_0}{2} + \sum_{n=1}^\infty a_n \cos\frac{n\pi x}{L}, \quad a_n = \frac{2}{L} \int_0^L f(x) \cos\frac{n\pi x}{L} \, dx$$

> [!info] 物理意义
> - 正弦级数满足 $f(0) = f(L) = 0$（Dirichlet 边界条件）
> - 余弦级数满足 $f'(0) = f'(L) = 0$（Neumann 边界条件）
> 
> 这正是分离变量法中边界条件决定特征函数类型的根源。

---

## Gibbs 现象

> [!note] Gibbs 现象
> 若 $f$ 有跳跃间断点，Fourier 级数在间断点附近出现**过冲**（overshoot）。当 $N \to \infty$，过冲幅度趋于跳跃幅度的约 $9\%$：
> $$\text{过冲} \approx \left( \frac{1}{\pi} \int_0^\pi \frac{\sin t}{t} dt - \frac{1}{2} \right) \times \text{跳跃量} \approx 0.0895 \times \text{跳跃量}$$
> 
> 这不是数值误差——即使 $N \to \infty$，过冲依然存在。

---

## 例题

> [!example] 例 1：方波的 Fourier 级数
> 设 $f(x) = \begin{cases} 1, & 0 < x < \pi \\ -1, & -\pi < x < 0 \end{cases}$，周期 $2\pi$。
> 
> $f$ 是奇函数，故 $a_n = 0$。计算 $b_n$：
> $$b_n = \frac{1}{\pi}\int_{-\pi}^\pi f(x)\sin(nx)dx = \frac{2}{\pi}\int_0^\pi \sin(nx)dx = \frac{2}{n\pi}(1 - \cos(n\pi))$$
> 
> 当 $n$ 为偶数时 $b_n = 0$，$n$ 为奇数时 $b_n = \frac{4}{n\pi}$。故：
> $$f(x) \sim \frac{4}{\pi} \sum_{k=0}^\infty \frac{\sin((2k+1)x)}{2k+1}$$

> [!example] 例 2：$f(x) = x^2$ 在 $[-\pi, \pi]$ 上的余弦展开
> 由于 $x^2$ 是偶函数，$b_n = 0$。
> $$a_0 = \frac{1}{\pi}\int_{-\pi}^\pi x^2 dx = \frac{2\pi^2}{3}$$
> $$a_n = \frac{2}{\pi}\int_0^\pi x^2\cos(nx)dx = (-1)^n\frac{4}{n^2}$$
> 故：
> $$x^2 = \frac{\pi^2}{3} + 4\sum_{n=1}^\infty \frac{(-1)^n}{n^2}\cos(nx), \quad x \in [-\pi, \pi]$$
> 取 $x = \pi$ 可得著名恒等式 $\sum_{n=1}^\infty \frac{1}{n^2} = \frac{\pi^2}{6}$。

---

## 习题

1. **基本计算**：计算 $f(x) = x$ 在 $[-\pi, \pi]$ 上的 Fourier 级数。

2. **正弦/余弦展开**：将 $f(x) = x$ 在 $[0, \pi]$ 上分别展开为 (a) 正弦级数，(b) 余弦级数。解释两者在端点处的行为差异。

3. **Parseval 应用**：利用 $f(x) = x$ 在 $[-\pi, \pi]$ 上的 Fourier 级数和 Parseval 等式，求 $\sum_{n=1}^\infty \frac{1}{n^2}$。

4. **收敛性**：方波 $f(x) = \operatorname{sgn}(x)$（$x \in [-\pi,\pi]$）的 Fourier 级数在 $x = 0$ 处收敛到什么值？在 $x = \pi$ 处呢？

5. **Dirichlet 核验证**：利用三角恒等式验证 Dirichlet 核的封闭形式：
   $$D_N(t) = \frac{1}{2} + \sum_{n=1}^N \cos(nt) = \frac{\sin((N+\frac{1}{2})t)}{2\sin(t/2)}$$

6. **正交性应用**：证明 $\{1, \cos\frac{n\pi x}{L}\}$（$n=1,2,\ldots$）在 $[0, L]$ 上关于权函数 $w(x)=1$ 正交，并计算各函数的模方。

7. **Gibbs 现象**：用计算机（或手算 $N=3,5,11,51$ 的部分和）验证方波 Fourier 级数在 $x=0$ 附近的过冲约为 $9\%$ 的跳跃量。

8. **复 Fourier 级数**：写出 $f(x)$ 在 $[-L, L]$ 上的复 Fourier 级数 $f(x) \sim \sum_{n=-\infty}^\infty c_n e^{in\pi x/L}$，给出 $c_n$ 的表达式，并说明 $c_n$ 与 $a_n, b_n$ 的关系。

> [!hint]- 部分提示
> - 1: $b_n = (-1)^{n+1}\frac{2}{n}$，$a_n = 0$
> - 3: $\sum_{n=1}^\infty 1/n^2 = \pi^2/6$
> - 4: 在 $x=0$ 收敛到 $0$，在 $x=\pi$ 收敛到 $0$（周期延拓后该处也是跳跃）
> - 8: $c_n = \frac{1}{2L}\int_{-L}^L f(x) e^{-in\pi x/L}dx$，$c_0 = a_0/2$，$c_n = (a_n - i b_n)/2$（$n>0$）

---

## 相关笔记

- [[一维热方程的分离变量法]] — Fourier 级数方法的第一个应用
- [[一维波动方程的分离变量法]] — 驻波展开
- [[Sturm-Liouville特征函数正交性]] — 正交函数系的推广
