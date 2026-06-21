---
title: Laplace 方程的 Green 函数
date: 2026-06-21
tags:
  - 数学物理方法
  - 偏微分方程
  - Green函数
  - Laplace方程
  - 镜像法
---

# Laplace 方程的 Green 函数

## 预备定义

> [!note] Green 函数的动机
> 对 Poisson 方程 $-\Delta u = f$ 在 $\Omega$ 内，$u|_{\partial\Omega} = 0$。若存在函数 $G(x,\xi)$ 使得对每 $\xi \in \Omega$：
> $$\begin{cases}
> -\Delta_x G(x,\xi) = \delta(x-\xi), & x \in \Omega \\
> G(x,\xi) = 0, & x \in \partial\Omega
> \end{cases}$$
> 则解可表示为 $u(x) = \int_\Omega G(x,\xi) f(\xi) d\xi$。

> [!note] Green 函数的结构
> $$G(x,\xi) = \Phi(x-\xi) - \phi(x,\xi)$$
> 其中 $\Phi(x-\xi)$ 是基本解（自由空间的 Green 函数），$\phi(x,\xi)$ 是**修正项**（corrector）：在 $\Omega$ 内调和（$\Delta_x \phi = 0$），在边界上 $\phi(x,\xi) = \Phi(x-\xi)$。
>
> 对 $\mathbb{R}^n$（$n \geq 3$）：$\Phi(r) = \dfrac{1}{n(n-2)\omega_n} r^{2-n}$（$\omega_n$ 为单位球体积）
> 对 $\mathbb{R}^2$：$\Phi(r) = -\dfrac{1}{2\pi}\ln r$

---

## Green 函数的对称性

> [!abstract] 对称性定理
> $G(x,\xi) = G(\xi,x)$ 对所有 $x,\xi \in \Omega$（$x \neq \xi$）。

**证明**：设 $v(x) = G(x,\xi_1)$，$w(x) = G(x,\xi_2)$。在 $\Omega \setminus (B_\varepsilon(\xi_1) \cup B_\varepsilon(\xi_2))$ 上应用 Green 第二恒等式：
$$\int (v \Delta w - w \Delta v) dx = 0$$

边界项在 $\partial\Omega$ 上为零（两者在边界上均为零）。令 $\varepsilon \to 0$，$v$ 在 $\xi_1$ 和 $w$ 在 $\xi_2$ 处的奇性贡献给出 $G(\xi_2,\xi_1) = G(\xi_1,\xi_2)$。$\square$

> [!important] 物理意义
> 对称性 $G(x,\xi) = G(\xi,x)$ 体现**互易原理**（reciprocity）：$\xi$ 处的单位点源在 $x$ 处产生的效应等于 $x$ 处的点源在 $\xi$ 处产生的效应。

---

## 镜像法

### 半空间 $\mathbb{R}^n_+$

对半空间 $\mathbb{R}^n_+ = \{x_n > 0\}$，Dirichlet 边界 $u(x',0) = 0$：

$$G(x,\xi) = \Phi(x-\xi) - \Phi(x-\tilde{\xi})$$

其中 $\tilde{\xi} = (\xi_1, \ldots, \xi_{n-1}, -\xi_n)$ 为 $\xi$ 关于平面 $x_n = 0$ 的反射点。

**验证**：当 $x_n = 0$ 时，$|x-\xi| = |x-\tilde{\xi}|$，故 $G(x,\xi) = 0$。$\square$

在 $\mathbb{R}^3$ 中：
$$G(x,\xi) = \frac{1}{4\pi}\left( \frac{1}{|x-\xi|} - \frac{1}{|x-\tilde{\xi}|} \right)$$

### 球 $B_R(0)$

对球 $B_R(0)$ 内的 Poisson 方程，Dirichlet 边界条件。使用**球面反演**：对 $\xi \in B_R(0)$（$\xi \neq 0$），定义 Kelvin 变换点 $\xi^* = \frac{R^2}{|\xi|^2}\xi$（在球外）。

Green 函数为：
$$G(x,\xi) = \Phi(x-\xi) - \Phi\!\left( \frac{|\xi|}{R} |x - \xi^*| \right)$$

或等价地（$\mathbb{R}^3$）：
$$G(x,\xi) = \frac{1}{4\pi}\left( \frac{1}{|x-\xi|} - \frac{R}{|\xi|\,|x-\xi^*|} \right)$$

当 $\xi = 0$ 时，$\xi^* = \infty$，有 $G(x,0) = \frac{1}{4\pi}(1/|x| - 1/R)$。

### 象限与楔形区域

对第一象限 $\{x > 0, y > 0\}$：依次对 $x$ 轴和 $y$ 轴做镜像反射（共 4 个映像）。

---

## Poisson 核与边界表示公式

对球 $B_R(0)$ 上的 Dirichlet 问题（$-\Delta u = 0$ 在球内，$u = f$ 在边界），由 Green 表示公式：
$$u(\xi) = -\int_{\partial B_R(0)} f(x) \frac{\partial G}{\partial \nu_x}(x,\xi) dS(x)$$

定义 **Poisson 核** $K(x,\xi) = -\frac{\partial G}{\partial \nu_x}(x,\xi)$：
$$K(x,\xi) = \frac{R^2 - |\xi|^2}{n\omega_n R |x-\xi|^n}$$

当 $n=2$ 时即恢复单位圆盘的 Poisson 核 $\frac{1}{2\pi}\frac{1-r^2}{1-2r\cos\theta+r^2}$。

---

## 习题

1. **$\mathbb{R}^3$ 半空间 Green 函数**：验证对 $\mathbb{R}^3_+$ 半空间，$G(x,\xi) = \frac{1}{4\pi}(1/|x-\xi| - 1/|x-\tilde{\xi}|)$ 满足 $\Delta_x G = -\delta(x-\xi)$ 和 $G|_{x_3=0} = 0$。

2. **球 Green 函数验证**：对单位球，验证当 $|x| = 1$ 时 $G(x,\xi) = \frac{1}{4\pi}(1/|x-\xi| - 1/|\xi|\,|x-\xi^*|) = 0$。提示：当 $|x|=1$ 时，由 Kelvin 变换的定义直接计算得 $|x-\xi^*| = \frac{1}{|\xi|}|x-\xi|$。

3. **二维半平面**：构造上半平面 $\{y > 0\}$ 上 Laplace 方程 Dirichlet 问题的 Green 函数。

4. **Green 表示公式**：由 $u(\xi) = \int_\Omega G(x,\xi) f(x) dx - \int_{\partial\Omega} u(x) \frac{\partial G}{\partial \nu_x} dS$ 推导：若 $-\Delta u = 0$ 在 $\Omega$ 内，则调和函数 $u$ 可由边界值 $u|_{\partial\Omega}$ 和 $\partial u/\partial \nu|_{\partial\Omega}$ 表示。

5. **对称性的应用**：用 Green 函数的对称性证明 Poisson 方程的 Dirichlet 问题解的唯一性。

> [!hint]- 部分提示
> - 3: $G(x,y;\xi,\eta) = -\frac{1}{2\pi}\ln\sqrt{(x-\xi)^2+(y-\eta)^2} + \frac{1}{2\pi}\ln\sqrt{(x-\xi)^2+(y+\eta)^2}$
> - 4: 对 $u$ 和 $G$ 使用 Green 第二恒等式

---

## 相关笔记

- [[泊松积分公式]] — 圆盘 Poisson 积分的复分析视角
- [[调和函数的极值原理]] — 解唯一性的另一证明方法
- [[圆盘Laplace方程与Poisson积分]] — 分离变量法导出同一结果
