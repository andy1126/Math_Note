---
title: 矩形 Laplace 方程的分离变量法
date: 2026-06-21
tags:
  - 数学物理方法
  - 偏微分方程
  - Laplace方程
  - 分离变量法
  - Fourier级数
  - Dirichlet问题
---

# 矩形 Laplace 方程的分离变量法

## 预备定义

> [!note] 矩形区域上的 Dirichlet 问题
> 求函数 $u(x,y)$ 满足：
> $$\begin{cases}
> u_{xx} + u_{yy} = 0, & 0 < x < a, \; 0 < y < b \\[4pt]
> u(0,y) = u(a,y) = 0, & 0 < y < b \\[4pt]
> u(x,0) = 0, & 0 < x < a \\[4pt]
> u(x,b) = f(x), & 0 < x < a
> \end{cases}$$

> [!note] 物理背景
> 矩形薄板稳态温度分布：底面和三边保持零温度，顶边指定温度分布 $f(x)$。

---

## 四步法求解

### 第一步：分离假设与特征值问题（齐次方向）

设 $u(x,y) = X(x) Y(y)$，代入 $\Delta u = 0$：
$$X''(x) Y(y) + X(x) Y''(y) = 0$$

分离变量：
$$\frac{X''(x)}{X(x)} = -\frac{Y''(y)}{Y(y)} = -\lambda$$

得到：
$$X''(x) + \lambda X(x) = 0, \quad Y''(y) - \lambda Y(y) = 0$$

**关键选择**：先在**两个齐次边界**的方向解特征值问题。这里 $x$ 方向有两个齐次边界条件：$u(0,y) = u(a,y) = 0 \Rightarrow X(0) = X(a) = 0$。

与一维热/波方程相同的特征值问题：
$$\lambda_n = \left(\frac{n\pi}{a}\right)^2, \quad X_n(x) = \sin\frac{n\pi x}{a}, \quad n = 1, 2, 3, \ldots$$

### 第二步：求解 $y$ 方向的方程

对每个 $\lambda_n$，$Y''(y) - \lambda_n Y(y) = 0$。由于 $\lambda_n > 0$，通解为双曲函数：
$$Y_n(y) = C_n \cosh\frac{n\pi y}{a} + D_n \sinh\frac{n\pi y}{a}$$

### 第三步：利用底面齐次边界

$u(x,0) = 0 \Rightarrow Y_n(0) = 0 \Rightarrow C_n = 0$。故：
$$Y_n(y) = D_n \sinh\frac{n\pi y}{a}$$

叠加得到通解：
$$u(x,y) = \sum_{n=1}^\infty D_n \sin\frac{n\pi x}{a} \sinh\frac{n\pi y}{a}$$

### 第四步：匹配顶面非齐次边界

代入 $u(x,b) = f(x)$：
$$f(x) = \sum_{n=1}^\infty D_n \sinh\frac{n\pi b}{a} \sin\frac{n\pi x}{a}$$

这是 $f(x)$ 的正弦 Fourier 级数：
$$D_n \sinh\frac{n\pi b}{a} = \frac{2}{a} \int_0^a f(x) \sin\frac{n\pi x}{a} \, dx$$

因此：
$$u(x,y) = \sum_{n=1}^\infty \left( \frac{2}{a} \int_0^a f(\xi) \sin\frac{n\pi \xi}{a} \, d\xi \right) \frac{\sinh(n\pi y/a)}{\sinh(n\pi b/a)} \sin\frac{n\pi x}{a}$$

---

## 一般边界条件处理策略

### 策略：叠加原理分解

当多个边界有非齐次条件时，将问题分解为若干子问题之和：

$$\begin{cases}
\Delta u = 0, & \text{在矩形内} \\
u|_{\partial\Omega} = \text{给定}
\end{cases}$$

写 $u = u_1 + u_2 + u_3 + u_4$，其中每个 $u_k$ 仅在一个边界上有非齐次条件，其余三边界为零。每个子问题用上述方法处理。

### 混合边界条件

若一边为 Dirichlet，对边为 Neumann（例如 $u(0,y)=0$，$u_x(a,y)=0$），特征值问题变为：
$$\lambda_n = \left(\frac{(n-\frac12)\pi}{a}\right)^2, \quad X_n(x) = \sin\frac{(n-\frac12)\pi x}{a}$$

---

## 角点奇性

> [!warning] 角点处的正则性
> 若边界条件在角点处不兼容（如 $u(0,0)$ 被相邻两边指定了不同温度），解在角点处可能出现对数级奇性或 $r^\alpha$ 型奇性（$0 < \alpha < 1$）。此时 Fourier 级数在角点附近收敛缓慢。

**例**：若 $u(0,0) = 0$（由 $x=0$ 边）但 $u(0,b) = 1$（由 $y=b$ 边），级数在 $(0,0)$ 附近以 $O(1/n)$ 衰减而非 $O(1/n^2)$。

---

## 例题

> [!example] 顶面均匀加热
> 设 $f(x) = T_0$（常数）。计算 Fourier 系数：
> $$D_n \sinh\frac{n\pi b}{a} = \frac{2}{a} \int_0^a T_0 \sin\frac{n\pi x}{a} dx = \frac{2T_0}{n\pi}(1 - \cos(n\pi))$$
> 
> 仅奇数项非零。令 $n = 2k+1$：
> $$u(x,y) = \frac{4T_0}{\pi} \sum_{k=0}^\infty \frac{1}{2k+1} \frac{\sinh((2k+1)\pi y/a)}{\sinh((2k+1)\pi b/a)} \sin\frac{(2k+1)\pi x}{a}$$

---

## 习题

1. **基本问题**：求解 $\Delta u = 0$，$0 < x < \pi$，$0 < y < \pi$，边界条件 $u(0,y) = u(\pi,y) = 0$，$u(x,0) = 0$，$u(x,\pi) = \sin(2x)$。

2. **两边非齐次**：求解 $\Delta u = 0$，$0 < x < 1$，$0 < y < 1$，$u(0,y) = u(1,y) = 0$，$u(x,0) = x(1-x)$，$u(x,1) = 0$。

3. **两方向交替**：若改为 $u(0,y) = u(1,y) = 0$，$u(x,0) = 0$，$u(x,1) = x$。重新求解（1、2 对调角色）。

4. **Neumann 混合**：求解 $\Delta u = 0$，$0 < x < \pi$，$0 < y < 1$，$u(0,y) = u(\pi,y) = 0$，$u_y(x,0) = 0$（Neumann），$u(x,1) = f(x)$。解释特征函数的变化。

5. **唯一性验证**：用调和函数的极值原理证明上述矩形 Dirichlet 问题解的唯一性。

6. **兼容性条件**：对矩形 Laplace 问题，边界数据在角点需要满足什么条件才能保证解在整个闭矩形上连续？若条件不满足会发生什么？

7. **分离方向的选择**：为什么先在有两个齐次边界的方向进行特征展开？若四个边界均非齐次，如何处理？写出算法步骤。

> [!hint]- 部分提示
> - 1: $u(x,y) = \frac{\sinh(2y)}{\sinh(2\pi)}\sin(2x)$
> - 2: 需要计算 $B_n = \frac{2}{1}\int_0^1 x(1-x)\sin(n\pi x)dx$
> - 6: 相邻边界的值在角点必须相等（连续性条件）
> - 7: 将问题分解为 $u_1 + u_2 + u_3 + u_4$，每个子问题仅一边非齐次

---

## 相关笔记

- [[Fourier级数]] — 正弦展开的数学基础
- [[调和函数的极值原理]] — 解的唯一性的理论基础
- [[调和函数的均值性质]] — 调和函数的内在性质
- [[一维热方程的分离变量法]] — 方法上的直接类比
