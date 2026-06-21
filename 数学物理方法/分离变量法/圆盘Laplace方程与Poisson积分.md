---
title: 圆盘 Laplace 方程与 Poisson 积分
date: 2026-06-21
tags:
  - 数学物理方法
  - 偏微分方程
  - Laplace方程
  - 分离变量法
  - 极坐标
  - Poisson积分
---

# 圆盘 Laplace 方程与 Poisson 积分

## 预备定义

> [!note] 圆盘上的 Dirichlet 问题
> 求函数 $u(r,\theta)$ 在单位圆盘内调和，在边界上等于给定函数：
> $$\begin{cases}
> \Delta u = 0, & 0 \leq r < 1, \; 0 \leq \theta < 2\pi \\[4pt]
> u(1,\theta) = f(\theta), & 0 \leq \theta < 2\pi
> \end{cases}$$
> 其中 $f$ 为 $2\pi$ 周期连续函数。

> [!note] 极坐标下的 Laplace 算子
> $$\Delta u = \frac{1}{r}\frac{\partial}{\partial r}\left(r\frac{\partial u}{\partial r}\right) + \frac{1}{r^2}\frac{\partial^2 u}{\partial \theta^2} = 0$$

---

## 四步法求解

### 第一步：分离假设

设 $u(r,\theta) = R(r) \Theta(\theta)$，代入极坐标 Laplace 方程：
$$\frac{1}{r}(rR')' \Theta + \frac{1}{r^2} R \Theta'' = 0$$

乘以 $r^2 / (R\Theta)$，分离变量：
$$\frac{r(rR')'}{R} = -\frac{\Theta''}{\Theta} = \lambda$$

得到两个 ODE：
$$\Theta'' + \lambda \Theta = 0 \quad \cdots (1)$$
$$r^2 R'' + r R' - \lambda R = 0 \quad \cdots (2)$$

### 第二步：角向特征值问题

由于 $u(r,\theta)$ 必须为 $\theta$ 的 $2\pi$ 周期函数（物理上单值），$\Theta$ 需满足周期性边界条件：
$$\Theta(0) = \Theta(2\pi), \quad \Theta'(0) = \Theta'(2\pi)$$

解 $\Theta'' + \lambda \Theta = 0$：
- $\lambda < 0$：通解为实指数函数，不满足周期性（除平凡解）
- $\lambda = 0$：$\Theta_0(\theta) = \text{常数}$（特征函数）
- $\lambda > 0$：通解 $\Theta(\theta) = A\cos(\sqrt{\lambda}\theta) + B\sin(\sqrt{\lambda}\theta)$。周期 $2\pi$ 要求 $\sqrt{\lambda} = n$（$n = 1, 2, \ldots$）

因此：
$$\lambda_n = n^2, \quad \Theta_n(\theta) = A_n \cos(n\theta) + B_n \sin(n\theta), \quad n = 0, 1, 2, \ldots$$

注意：$\lambda_0 = 0$ 的几何重数为 $1$（仅常数），$\lambda_n$（$n \geq 1$）的几何重数为 $2$（$\cos$ 与 $\sin$ 线性无关）。

### 第三步：径向方程求解

方程 (2) 为 Euler 方程：$r^2 R'' + r R' - n^2 R = 0$。

设 $R(r) = r^\alpha$，代入得 $\alpha(\alpha-1) + \alpha - n^2 = 0$，即 $\alpha^2 = n^2$，$\alpha = \pm n$。

- 当 $n = 0$：$r^2 R'' + r R' = 0$，通解 $R_0(r) = C_0 + D_0 \ln r$。由于解需要在 $r = 0$ 处有限（物理上温度在盘心有限），$D_0 = 0$。故 $R_0(r) = C_0$。
- 当 $n \geq 1$：$R_n(r) = C_n r^n + D_n r^{-n}$。$r^{-n}$ 在 $r = 0$ 处发散，故 $D_n = 0$。得 $R_n(r) = C_n r^n$。

### 第四步：叠加与边界匹配

叠加得到通解：
$$u(r,\theta) = \frac{A_0}{2} + \sum_{n=1}^\infty r^n \big( A_n \cos(n\theta) + B_n \sin(n\theta) \big)$$

代入边界条件 $u(1,\theta) = f(\theta)$：
$$f(\theta) = \frac{A_0}{2} + \sum_{n=1}^\infty \big( A_n \cos(n\theta) + B_n \sin(n\theta) \big)$$

这正是 $f$ 的 Fourier 级数：
$$A_n = \frac{1}{\pi} \int_0^{2\pi} f(t) \cos(nt) \, dt, \quad B_n = \frac{1}{\pi} \int_0^{2\pi} f(t) \sin(nt) \, dt$$

---

## 从级数到 Poisson 积分

将系数代入解：
$$u(r,\theta) = \frac{1}{2\pi} \int_0^{2\pi} f(t) \, dt + \frac{1}{\pi} \sum_{n=1}^\infty r^n \int_0^{2\pi} f(t) \big( \cos(nt)\cos(n\theta) + \sin(nt)\sin(n\theta) \big) dt$$

利用 $\cos(nt)\cos(n\theta) + \sin(nt)\sin(n\theta) = \cos(n(\theta-t))$：
$$u(r,\theta) = \frac{1}{2\pi} \int_0^{2\pi} f(t) \left[ 1 + 2\sum_{n=1}^\infty r^n \cos(n(\theta-t)) \right] dt$$

括号内的级数是**Poisson 核的 Fourier 展开**：
$$1 + 2\sum_{n=1}^\infty r^n \cos(n\phi) = \frac{1 - r^2}{1 - 2r\cos\phi + r^2} = P_r(\phi)$$

> [!info] Poisson 核的级数推导
> 利用 $r^n e^{in\phi}$ 的几何级数：
> $$\sum_{n=0}^\infty (r e^{i\phi})^n = \frac{1}{1 - r e^{i\phi}}$$
> 取实部：$\operatorname{Re}\frac{1}{1-re^{i\phi}} = \frac{1-r\cos\phi}{1-2r\cos\phi+r^2}$
> 故 $1 + 2\sum_{n=1}^\infty r^n \cos(n\phi) = 2\operatorname{Re}\frac{1}{1-re^{i\phi}} - 1 = \frac{1-r^2}{1-2r\cos\phi+r^2}$

最终得到 **Poisson 积分公式**：
$$u(r,\theta) = \frac{1}{2\pi} \int_0^{2\pi} \frac{1 - r^2}{1 - 2r\cos(\theta-t) + r^2} \, f(t) \, dt$$

---

## 圆环上的 Dirichlet 问题

对圆环 $a < r < b$，径向解同时包含 $r^n$ 和 $r^{-n}$ 项（无 $r=0$ 处的正则性限制）：
$$u(r,\theta) = \frac{A_0 + B_0 \ln r}{2} + \sum_{n=1}^\infty \big[ (A_n r^n + B_n r^{-n}) \cos(n\theta) + (C_n r^n + D_n r^{-n}) \sin(n\theta) \big]$$

由内外边界的 Dirichlet 条件确定所有系数。

---

## 例题

> [!example] 边界恒温一半圆
> 设 $f(\theta) = \begin{cases} 1, & 0 < \theta < \pi \\ 0, & \pi < \theta < 2\pi \end{cases}$
> 
> $$A_0 = \frac{1}{\pi}\int_0^\pi 1\,d\theta = 1$$
> $$A_n = \frac{1}{\pi}\int_0^\pi \cos(n\theta)d\theta = 0$$
> $$B_n = \frac{1}{\pi}\int_0^\pi \sin(n\theta)d\theta = \frac{1 - \cos(n\pi)}{n\pi} = \begin{cases} \frac{2}{n\pi}, & n \text{ 奇数} \\ 0, & n \text{ 偶数} \end{cases}$$
> 
> $$u(r,\theta) = \frac{1}{2} + \frac{2}{\pi}\sum_{k=0}^\infty \frac{r^{2k+1}}{2k+1} \sin((2k+1)\theta)$$

---

## 习题

1. **基本 Dirichlet 问题**：用分离变量法求单位圆盘内的调和函数，边界值 $f(\theta) = \cos(3\theta)$。

2. **Poisson 积分的均值性质**：在 Poisson 积分公式中令 $r = 0$，直接导出调和函数的均值性质。

3. **圆环问题**：求圆环 $1 < r < 2$ 内的调和函数，边界条件为 $u(1,\theta) = 0$，$u(2,\theta) = \sin\theta$。

4. **扇形区域**：求扇形区域 $\{0 < r < 1, 0 < \theta < \alpha\}$ 上的 Dirichlet 问题，边界条件 $u(r,0) = u(r,\alpha) = 0$，$u(1,\theta) = f(\theta)$。特征函数与 $\alpha$ 的关系是什么？

5. **Neumann 问题**：对单位圆盘上的 Neumann 问题 $\partial u/\partial r(1,\theta) = g(\theta)$，分离变量法需要什么兼容性条件？写出解的表达式。

6. **Poisson 核性质**：直接从分离变量级数证明 $P_r(\theta) > 0$（$0 \leq r < 1$）和 $\frac{1}{2\pi}\int_0^{2\pi} P_r(\theta)d\theta = 1$。

7. **外域问题**：求单位圆外 $r > 1$ 的调和函数，边界条件 $u(1,\theta) = f(\theta)$，且 $u$ 在无穷远处有界。注意径向解的选择不同。

> [!hint]- 部分提示
> - 1: $u(r,\theta) = r^3 \cos(3\theta)$
> - 3: $u(r,\theta) = \frac{2}{3}(r - r^{-1})\sin\theta$
> - 4: 特征函数为 $\sin(n\pi\theta/\alpha)$，特征值 $\lambda_n = (n\pi/\alpha)^2$
> - 5: 兼容性条件 $\int_0^{2\pi} g(\theta)d\theta = 0$
> - 7: 取 $R_n(r) = r^{-n}$（$n \geq 1$）以确保 $r \to \infty$ 时有界

---

## 相关笔记

- [[泊松积分公式]] — 复分析方法导出的同一公式
- [[Fourier级数]] — 级数展开的数学基础
- [[矩形Laplace方程的分离变量法]] — 直角坐标分离
- [[调和函数的均值性质]] — 均值性质的深层含义
