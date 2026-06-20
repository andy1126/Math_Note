---
title: Lagrange 插值的余项公式与误差估计
date: 2026-05-28
tags:
  - 数值分析
  - 插值
  - Lagrange插值
  - 误差估计
  - Rolle定理
---

# Lagrange 插值的余项公式与误差估计

## 预备定义

> [!note] Lagrange 插值多项式
> 给定 $n + 1$ 互异节点 $x_0 < x_1 < \cdots < x_n$ 与函数值 $f(x_0), \ldots, f(x_n)$。**Lagrange 插值多项式**
> $$L_n(x) = \sum_{k=0}^n f(x_k)\, \ell_k(x),\qquad \ell_k(x) = \prod_{\substack{j = 0 \\ j \neq k}}^n \frac{x - x_j}{x_k - x_j}.$$
> 满足 $L_n(x_k) = f(x_k)$ 且 $\deg L_n \leq n$。

> [!note] 节点多项式
> 称
> $$\omega(x) = \prod_{k=0}^n (x - x_k)$$
> 为**节点多项式**。$\omega \in \mathbb{R}[x]$，$\deg \omega = n + 1$。

> [!abstract] 引理：Rolle 定理
> 设 $g \in C[a, b]$，可微于 $(a, b)$，$g(a) = g(b) = 0$。则存在 $\xi \in (a, b)$ 使 $g'(\xi) = 0$。详见 [[中值定理]]。

> [!abstract] 引理：Rolle 定理的迭代
> 若 $g \in C^{n+1}[a, b]$ 在 $n + 2$ 个不同点取值为 $0$，则存在 $\xi \in (a, b)$ 使 $g^{(n+1)}(\xi) = 0$。
>
> **证明**：对相邻两零点应用 Rolle 得 $n + 1$ 个 $g'$ 的零点；再迭代得 $n$ 个 $g''$ 零点；……；$n + 1$ 次迭代后得 $1$ 个 $g^{(n+1)}$ 零点。$\square$

---

## 定理（Lagrange 插值余项）

设 $f \in C^{n+1}[a, b]$，$x_0, \ldots, x_n \in [a, b]$ 互异。则对任意 $x \in [a, b]$，存在 $\xi = \xi(x) \in (a, b)$ 使

$$f(x) - L_n(x) = \frac{f^{(n+1)}(\xi)}{(n+1)!}\, \omega(x).$$

**误差估计**：
$$\|f - L_n\|_\infty \leq \frac{\|f^{(n+1)}\|_\infty}{(n+1)!} \cdot \|\omega\|_\infty,$$
范数取于 $[a, b]$。

---

## 证明

### 情形分析

若 $x = x_k$ 某节点，$f(x) - L_n(x) = 0$，$\omega(x) = 0$，结论平凡成立（任取 $\xi$）。**以下假设 $x \notin \{x_0, \ldots, x_n\}$，并将 $x$ 固定**。

### 第一步：构造辅助函数

定义
$$\Phi(t) := f(t) - L_n(t) - K\, \omega(t), \quad t \in [a, b],$$

其中常数 $K$ 待选。

**选取 $K$ 使 $\Phi(x) = 0$**：
$$K := \frac{f(x) - L_n(x)}{\omega(x)}. \quad \cdots (\ast)$$

（$\omega(x) \neq 0$ 因为 $x$ 不是节点。）

### 第二步：$\Phi$ 有至少 $n + 2$ 个零点

- $\Phi(x_k) = f(x_k) - L_n(x_k) - K\, \omega(x_k) = 0 - 0 = 0$，$k = 0, \ldots, n$；
- $\Phi(x) = 0$ 由 $(\ast)$ 的构造。

故 $\Phi$ 在 $n + 2$ 个互异点（$x_0, \ldots, x_n, x$）处取值 $0$。

### 第三步：应用迭代 Rolle 引理

由 $f \in C^{n+1}$，$L_n, \omega$ 为多项式（光滑），故 $\Phi \in C^{n+1}[a, b]$。

由引理（迭代 Rolle），存在 $\xi \in (a, b)$ 使 $\Phi^{(n+1)}(\xi) = 0$。

### 第四步：计算 $\Phi^{(n+1)}$

- $f^{(n+1)}$ 由假设光滑；
- $L_n^{(n+1)} \equiv 0$（$\deg L_n \leq n$）；
- $\omega(t) = t^{n+1} - (\sum x_k) t^n + \cdots$，故 $\omega^{(n+1)}(t) \equiv (n+1)!$。

所以
$$\Phi^{(n+1)}(t) = f^{(n+1)}(t) - 0 - K \cdot (n+1)!.$$

### 第五步：代入 $\xi$

$0 = \Phi^{(n+1)}(\xi) = f^{(n+1)}(\xi) - K\,(n+1)!$，即
$$K = \frac{f^{(n+1)}(\xi)}{(n+1)!}.$$

代回 $(\ast)$：
$$\frac{f(x) - L_n(x)}{\omega(x)} = \frac{f^{(n+1)}(\xi)}{(n+1)!},$$

即
$$f(x) - L_n(x) = \frac{f^{(n+1)}(\xi)}{(n+1)!}\, \omega(x). \quad \square$$

### 第六步：误差估计

对一切 $x \in [a, b]$：
$$|f(x) - L_n(x)| = \frac{|f^{(n+1)}(\xi)|}{(n+1)!} \cdot |\omega(x)| \leq \frac{\|f^{(n+1)}\|_\infty}{(n+1)!} \cdot |\omega(x)|.$$

取上界：
$$\|f - L_n\|_\infty \leq \frac{\|f^{(n+1)}\|_\infty}{(n+1)!} \cdot \|\omega\|_\infty. \quad \blacksquare$$

---

## 证明思路总结

> [!tip] 关键思想
> 余项公式的证明是**精心构造 + 迭代 Rolle** 的典范：
> 1. 构造 $\Phi(t) = f(t) - L_n(t) - K \omega(t)$，把待估计的余项 $f(x) - L_n(x)$ 与节点零塞进同一个函数；
> 2. $K$ 的选取使 $\Phi$ 有 $n + 2$ 个零点；
> 3. Rolle 迭代 $n + 1$ 次把零点"提升"到导数 $\Phi^{(n+1)}$；
> 4. $\Phi^{(n+1)} = f^{(n+1)} - K(n+1)!$，由 $\Phi^{(n+1)}(\xi) = 0$ 解出 $K$。
>
> 这种"**辅助函数 + 多次 Rolle**"的套路在 Taylor 余项、数值积分误差估计中反复出现。

> [!info] $\omega$ 的最优化（Chebyshev 节点）
> 误差估计的上界含两个因子：$\|f^{(n+1)}\|_\infty/(n+1)!$（由 $f$ 决定，无法控制）与 $\|\omega\|_\infty$（由节点 $x_k$ 决定）。
>
> **最小化 $\|\omega\|_\infty$ 的节点选择**：在 $[-1, 1]$ 上，使 $\|\omega\|_\infty$ 最小的节点为 **Chebyshev 节点**
> $$x_k = \cos\!\left(\frac{2k + 1}{2(n + 1)}\pi\right), \quad k = 0, \ldots, n,$$
> 此时 $\|\omega\|_\infty = 2^{-n}$，远好于等距节点。这是 Chebyshev 多项式 $T_{n+1}$ 极值性质的体现。

> [!warning] Runge 现象
> 等距节点 + 高阶插值可能**误差不减反增**。经典反例（Runge 1901）：
> $$f(x) = \frac{1}{1 + 25x^2}, \quad x \in [-1, 1].$$
> 用等距 $n + 1$ 节点的 $L_n$，$\|f - L_n\|_\infty \to \infty$（$n \to \infty$）。
>
> **原因**：$f$ 的解析延拓在复平面上 $\pm i/5$ 有极点，太靠近实轴 $[-1, 1]$；$f^{(n+1)}$ 增长太快。
>
> **解决**：Chebyshev 节点；或改用分段低阶（如样条）插值。

> [!info] 衔接其他笔记
> - **Rolle 定理** → [[中值定理]]（实分析基础）；
> - **Newton 法收敛分析** → [[Newton法的二阶收敛性]] 中用到 Taylor 余项，与本笔记同一证法套路；
> - **RK4 局部截断误差** → `Runge-Kutta方法的收敛性`（待写）中将再次出现 Taylor 多次截断 + 误差余项；
> - **数值积分（Newton-Cotes 公式）**：由插值多项式 $L_n$ 积分得到，其误差由本余项公式逐节点估计。
