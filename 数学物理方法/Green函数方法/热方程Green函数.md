---
title: 热方程的 Green 函数
date: 2026-06-21
tags:
  - 数学物理方法
  - 偏微分方程
  - Green函数
  - 热方程
  - 镜像法
---

# 热方程的 Green 函数

## 预备定义

> [!note] 热方程 Green 函数的定义
> 对区域 $\Omega \subset \mathbb{R}^n$，热方程 Green 函数 $G(x,t; \xi,\tau)$ 满足：
> $$\begin{cases}
> \partial_t G - \Delta_x G = \delta(x-\xi)\delta(t-\tau), & x \in \Omega, \; t > \tau \\
> G(x,t; \xi,\tau) = 0, & x \in \partial\Omega \\
> G(x,\tau; \xi,\tau) = \delta(x-\xi)
> \end{cases}$$
> 由于方程在时间平移下不变，通常记 $G(x,\xi,t-\tau)$。
>
> 初边值问题 $u_t = \Delta u + f$，$u|_{\partial\Omega} = g$，$u(x,0) = u_0(x)$ 的解可表示为：
> $$u(x,t) = \int_\Omega G(x,\xi,t) u_0(\xi) d\xi + \int_0^t \int_\Omega G(x,\xi,t-s) f(\xi,s) d\xi ds - \int_0^t \int_{\partial\Omega} \frac{\partial G}{\partial \nu_\xi} g(\xi,s) dS ds$$

> [!note] 与自由空间基本解的关系
> $$G(x,\xi,t) = \Phi(x-\xi,t) - \phi(x,\xi,t)$$
> 其中 $\Phi(x,t) = (4\pi t)^{-n/2} e^{-|x|^2/4t}$ 为热核（全空间基本解），$\phi$ 在 $\Omega$ 内满足齐次热方程，初始条件为零，边界条件为 $\phi(x,\xi,t) = \Phi(x-\xi,t)$（$x \in \partial\Omega$）。

---

## 半空间的 Green 函数（镜像法）

### $\mathbb{R}^n_+$ 上半空间 Dirichlet 边界

对 $\mathbb{R}^n_+ = \{x_n > 0\}$，边界 $u(x',0,t) = 0$。使用**奇反射法**：
$$G(x,\xi,t) = \Phi(x-\xi,t) - \Phi(x-\tilde{\xi},t)$$

其中 $\tilde{\xi} = (\xi_1, \ldots, \xi_{n-1}, -\xi_n)$。

**验证**：当 $x_n = 0$ 时，$|x-\xi| = |x-\tilde{\xi}|$，故 $G = 0$。在 $\mathbb{R}^n_+$ 内，两项分别满足热方程，故 $G$ 满足热方程。初始条件：$t \to 0^+$ 时 $\Phi(x-\xi,t) \to \delta(x-\xi)$，$\Phi(x-\tilde{\xi},t) \to \delta(x-\tilde{\xi})$。由于 $\tilde{\xi} \notin \mathbb{R}^n_+$（当 $\xi_n > 0$），第二项在积分意义下无贡献。$\square$

### 半直线上的 Neumann 边界

对 $x > 0$ 上 $u_x(0,t) = 0$（绝热边界），使用**偶反射法**：
$$G(x,\xi,t) = \Phi(x-\xi,t) + \Phi(x+\xi,t) \quad (n=1)$$

---

## 有界区间上的 Green 函数（特征展开法）

对区间 $(0,L)$ 上齐次 Dirichlet 边界的热方程，用分离变量法构造 Green 函数：
$$G(x,\xi,t) = \frac{2}{L} \sum_{n=1}^\infty \sin\frac{n\pi x}{L} \sin\frac{n\pi \xi}{L} \exp\!\left(-\left(\frac{n\pi}{L}\right)^2 t\right)$$

**推导**：此即 $-\partial_x^2$ 在 Dirichlet 边界下的特征函数展开。Heaviside 函数 $\delta(x-\xi)$ 的 Fourier 正弦级数为 $\frac{2}{L}\sum \sin(n\pi x/L)\sin(n\pi \xi/L)$。热方程的时间演化作用即乘以 $e^{-\lambda_n t}$。

类似地，对 Neumann 边界 $u_x(0,t) = u_x(L,t) = 0$：
$$G(x,\xi,t) = \frac{1}{L} + \frac{2}{L} \sum_{n=1}^\infty \cos\frac{n\pi x}{L} \cos\frac{n\pi \xi}{L} \exp\!\left(-\left(\frac{n\pi}{L}\right)^2 t\right)$$

---

## Green 函数方法的优势

> [!tip] 镜像法 vs 特征展开法
> | 方法 | 适用场景 | 优点 | 缺点 |
> |------|---------|------|------|
> | **镜像法** | 特殊对称区域（半空间、球、象限） | 闭式解，计算快捷 | 仅适用于少数几何 |
> | **特征展开法** | 一般有界区域 | 通用性强 | 级数收敛可能慢（$t$ 小时需很多项） |
> | **Laplace 变换法** | 随时间演化的问题 | 将 PDE 化为椭圆问题 | 逆变换可能困难 |

---

## 习题

1. **半空间基本公式**：写出 $\mathbb{R}^3_+$（$z > 0$）上 Dirichlet 边界热方程 Green 函数的显式。

2. **Neumann 边界验证**：验证 $n=1$ 时偶反射 Green 函数 $G(x,\xi,t) = \Phi(x-\xi,t) + \Phi(x+\xi,t)$ 在 $x=0$ 处满足 $\partial_x G = 0$。

3. **级数形式**：对 $[0,\pi]$ 上 Dirichlet 热方程，求 $G(x,\xi,t)$ 的特征展开。当 $t \to \infty$ 时，主导项是什么？

4. **初边值问题**：半空间 $x > 0$ 上 $u_t = u_{xx}$，$u(0,t) = 0$，$u(x,0) = f(x)$。用 Green 函数的积分表示写出解。

5. **特征展开与镜像法的等价性**：对 $[0,\pi]$ 的 Dirichlet 热方程，证明特征展开与全空间公式（奇周期延拓）的一致性。提示：奇周期延拓后的 Fourier 变换与正弦级数是一对 Poisson 求和公式的两面。

> [!hint]- 部分提示
> - 1: $G = \frac{1}{(4\pi t)^{3/2}} [e^{-|x-\xi|^2/4t} - e^{-|x-\tilde{\xi}|^2/4t}]$
> - 3: 主导项为 $n=1$ 项，$G \sim \frac{2}{\pi}\sin x \sin\xi \, e^{-t}$（$t \to \infty$）
> - 4: $u(x,t) = \int_0^\infty G(x,\xi,t) f(\xi) d\xi$

---

## 相关笔记

- [[热方程基本解]] — 全空间热核 $\Phi$ 的详细性质
- [[一维热方程的分离变量法]] — 有界区域的特征展开
- [[Laplace方程Green函数]] — 椭圆方程的 Green 函数方法
