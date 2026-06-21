---
title: Bessel 函数
date: 2026-06-21
tags:
  - 数学物理方法
  - 特殊函数
  - Bessel函数
  - 柱坐标
  - 分离变量法
  - Sturm-Liouville
---

# Bessel 函数

## 预备定义

> [!note] Bessel 方程
> $$\nu \text{ 阶 Bessel 方程：} \quad x^2 y'' + x y' + (x^2 - \nu^2)y = 0$$
> 其中 $\nu \geq 0$ 为阶数。该方程在 $x=0$ 处有正则奇点。

> [!note] 第一类 Bessel 函数 $J_\nu(x)$
> $$J_\nu(x) = \sum_{k=0}^\infty \frac{(-1)^k}{k! \, \Gamma(k+\nu+1)} \left(\frac{x}{2}\right)^{2k+\nu}$$
> $J_\nu(x)$ 在 $x=0$ 处有限（当 $\nu \geq 0$），并随 $x \to \infty$ 振荡衰减。

> [!note] 第二类 Bessel 函数 $Y_\nu(x)$（Neumann 函数）
> $$Y_\nu(x) = \frac{J_\nu(x)\cos(\nu\pi) - J_{-\nu}(x)}{\sin(\nu\pi)}$$
> $Y_\nu(x)$ 在 $x=0$ 处有对数奇性（$\nu=0$ 时）或 $x^{-\nu}$ 型奇性（$\nu>0$ 时）。

---

## 柱坐标分离变量

### Laplace 方程在柱坐标下的分离

三维 Laplace 方程 $\Delta u = 0$ 在柱坐标 $(r,\theta,z)$ 下：
$$\frac{1}{r}\frac{\partial}{\partial r}\left(r\frac{\partial u}{\partial r}\right) + \frac{1}{r^2}\frac{\partial^2 u}{\partial \theta^2} + \frac{\partial^2 u}{\partial z^2} = 0$$

取 $u(r,\theta,z) = R(r)\Theta(\theta)Z(z)$，分离得：
$$\Theta'' + \nu^2 \Theta = 0 \quad \Rightarrow \quad \Theta(\theta) = A\cos(\nu\theta) + B\sin(\nu\theta), \quad \nu = 0,1,2,\ldots$$
$$Z'' - k^2 Z = 0 \quad \text{（或 } Z'' + k^2 Z = 0 \text{ 取决于符号选择）}$$
$$r^2 R'' + r R' + (k^2 r^2 - \nu^2)R = 0 \quad \text{（Bessel 方程，变量 } kr \text{）}$$

### Helmholtz 方程在柱坐标下的分离

对 $u_{tt} = c^2\Delta u$，时间分离 $u = T(t)v(r,\theta)$ 后，$v$ 满足 Helmholtz 方程 $\Delta v + \lambda v = 0$。空间分离同上，得 $R$ 满足：
$$r^2 R'' + r R' + (\lambda r^2 - \nu^2)R = 0$$

令 $x = \sqrt{\lambda}r$，即得标准 Bessel 方程。

---

## Bessel 函数的正交性

### S-L 形式

Bessel 方程可写为 Sturm-Liouville 形式：
$$\frac{d}{dr}\left( r \frac{dJ_\nu}{dr} \right) + \left( \lambda r - \frac{\nu^2}{r} \right) J_\nu = 0$$

其中 $p(r) = r$，$w(r) = r$，$q(r) = \nu^2/r$。注意 $p(0) = 0$：这是**奇异 S-L 问题**。

### 正交性定理

> [!abstract] Fourier-Bessel 正交性
> 设 $\alpha_{n}$ 为 $J_\nu(x)$ 的第 $n$ 个正零点（$J_\nu(\alpha_n) = 0$，$n=1,2,\ldots$）。则在 $[0,a]$ 上：
> $$\int_0^a J_\nu\!\left(\frac{\alpha_m r}{a}\right) J_\nu\!\left(\frac{\alpha_n r}{a}\right) r \, dr = \frac{a^2}{2} [J_{\nu+1}(\alpha_n)]^2 \, \delta_{mn}$$

**证明思路**：对两个不同零点 $\alpha_m \neq \alpha_n$ 对应的函数 $\phi_m(r) = J_\nu(\alpha_m r/a)$，$\phi_n(r) = J_\nu(\alpha_n r/a)$，应用 S-L 正交性理论（或直接分部积分）。$\square$

### Fourier-Bessel 级数

任意（适当光滑的）函数 $f(r)$ 在 $[0,a]$ 上可展开为 Fourier-Bessel 级数：
$$f(r) = \sum_{n=1}^\infty c_n J_\nu\!\left(\frac{\alpha_n r}{a}\right), \quad c_n = \frac{2}{a^2 [J_{\nu+1}(\alpha_n)]^2} \int_0^a f(r) J_\nu\!\left(\frac{\alpha_n r}{a}\right) r \, dr$$

---

## 渐近行为

> [!note] $x \to 0^+$ 时
> $$J_\nu(x) \sim \frac{1}{\Gamma(\nu+1)}\left(\frac{x}{2}\right)^\nu$$

> [!note] $x \to \infty$ 时
> $$J_\nu(x) \sim \sqrt{\frac{2}{\pi x}} \cos\!\left(x - \frac{\nu\pi}{2} - \frac{\pi}{4}\right)$$
> $$Y_\nu(x) \sim \sqrt{\frac{2}{\pi x}} \sin\!\left(x - \frac{\nu\pi}{2} - \frac{\pi}{4}\right)$$

---

## 应用一：圆柱 Dirichlet 问题

> [!example] 有限高圆柱的稳态温度
> 圆柱 $\{0 \leq r < a, 0 < \theta < 2\pi, 0 < z < h\}$，侧面和底面零温度，顶面 $u(r,\theta,h) = f(r)$。
> 
> 分离变量后（$\nu = 0$，轴对称），径向得 $R(r) = J_0(\alpha_n r/a)$（$J_0(\alpha_n) = 0$），竖向得 $Z(z) = \sinh(\alpha_n z/a)$。
> $$u(r,z) = \sum_{n=1}^\infty c_n J_0\!\left(\frac{\alpha_n r}{a}\right) \sinh\!\left(\frac{\alpha_n z}{a}\right)$$
> $c_n$ 由 $z=h$ 边界用 Fourier-Bessel 系数公式确定。

## 应用二：圆膜振动

> [!example] 圆膜振动特征频率
> 圆膜 $0 \leq r < a$ 满足 $u_{tt} = c^2 \Delta u$，固定边界 $u(a,\theta,t) = 0$。
> 
> 分离 $u = T(t)v(r,\theta)$，时间部分 $T'' + c^2\lambda T = 0$，空间部分 $\Delta v + \lambda v = 0$。
> 
> $v(r,\theta) = J_\nu(\sqrt{\lambda}r)(A\cos(\nu\theta) + B\sin(\nu\theta))$。边界条件 $J_\nu(\sqrt{\lambda}a) = 0$。
> 
> 令 $\alpha_{\nu,n}$ 为 $J_\nu$ 的第 $n$ 个零点，则特征频率：
> $$\omega_{\nu,n} = \frac{c \alpha_{\nu,n}}{a}$$
> 
> 基频对应于 $J_0$ 的第一个零点 $\alpha_{0,1} \approx 2.4048$。

---

## 习题

1. **级数验证**：用 $J_0(x)$ 的级数定义验证 $J_0(0) = 1$，$J_0'(0) = 0$，$J_0''(0) = -1/2$。

2. **递推关系**：证明 $\frac{d}{dx}[x^\nu J_\nu(x)] = x^\nu J_{\nu-1}(x)$ 和 $\frac{d}{dx}[x^{-\nu} J_\nu(x)] = -x^{-\nu} J_{\nu+1}(x)$。提示：从级数逐项求导。

3. **柱面波**：三维波动方程的柱对称解可写为 $u(r,t) = \int_0^\infty A(k) J_0(kr) \cos(kct) k \, dk$（Fourier-Bessel 积分）。取初值 $u(r,0) = e^{-r^2}$，$u_t(r,0) = 0$，求 $A(k)$。

4. **圆膜基频**：半径为 $a$ 的圆膜，张力 $T$，面密度 $\rho$。证明基频 $f_1 = \frac{\alpha_{0,1}}{2\pi a}\sqrt{\frac{T}{\rho}}$。若 $a$ 减半，基频如何变化？

5. **圆柱 Dirichlet 问题**：无限高圆柱 $0 \leq r < a$，侧面温度 $u(a,z) = f(z)$（$0 < z < \infty$），求 $u(r,z)$。提示：$z$ 方向用 Fourier 积分。

6. **Bessel 函数的振荡性**：利用渐近公式 $J_0(x) \sim \sqrt{2/(\pi x)}\cos(x - \pi/4)$ 证明 $J_0$ 有无穷多个零点，且 $\alpha_n \sim \pi(n - 1/4)$（$n \to \infty$）。

> [!hint]- 部分提示
> - 2: 逐项求导后重组级数
> - 3: 这是 Hankel 变换（$n=0$），$A(k) = \frac{1}{2}e^{-k^2/4}$
> - 4: $\alpha_{0,1} \approx 2.4048$，$f_1$ 与 $1/a$ 成正比（小鼓音调高）
> - 6: $\alpha_1 \approx 2.4048$，$\alpha_2 \approx 5.5201$，$\alpha_3 \approx 8.6537$，验证渐近式 $\alpha_n \approx \pi(n + 1/4)$

---

## 相关笔记

- [[Sturm-Liouville特征函数正交性]] — S-L 正交性的一般理论
- [[Legendre多项式的正交性]] — 球坐标下出现的特殊函数
- [[圆盘Laplace方程与Poisson积分]] — 二维圆盘上的分离变量法
- [[一维波动方程的分离变量法]] — 分离变量法的基本步骤
