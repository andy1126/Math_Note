---
title: Fatou 引理
date: 2026-05-28
tags:
  - 实分析
  - 测度论
  - Lebesgue积分
  - Fatou引理
  - liminf
---

# Fatou 引理

## 预备定义

> [!note] 非负可测函数的积分
> 见 [[单调收敛定理]] 中的定义：$\int_X f\,d\mu = \sup\{\int_X \varphi\,d\mu : 0 \leq \varphi \leq f,\ \varphi \text{ 简单}\}$。

> [!note] liminf 的定义
> 对实数序列 $\{a_n\}$，
> $$\liminf_n a_n := \sup_{N \geq 1} \inf_{n \geq N} a_n = \lim_{N \to \infty} \left(\inf_{n \geq N} a_n\right).$$
> 内层 $\inf_{n \geq N} a_n$ 关于 $N$ 单增，故极限存在（允许 $\pm\infty$）。

> [!abstract] 引理：$\liminf$ 的可测性
> 设 $\{f_n\}$ 为可测函数列。则 $\liminf_n f_n$ 可测。证明见 [[可测函数的逐点极限仍可测]]。

> [!abstract] 引理：单调收敛定理（MCT）
> 设 $\{g_N\}$ 为非负可测函数列且 $g_N \uparrow g$，则 $\int g_N\,d\mu \uparrow \int g\,d\mu$。详见 [[单调收敛定理]]。

---

## 定理（Fatou 引理）

设 $(X, \mathcal{M}, \mu)$ 为测度空间，$\{f_n\}_{n=1}^\infty$ 为 $X$ 上的**非负**可测函数列。则

$$\int_X \liminf_n f_n\,d\mu \leq \liminf_n \int_X f_n\,d\mu.$$

---

## 证明

### 第一步：构造单增辅助函数列

令
$$g_N(x) := \inf_{n \geq N} f_n(x), \quad N \geq 1.$$

由 $\inf$ 的可测性（[[可测函数的逐点极限仍可测]]），$g_N$ 可测且非负。

**单调性**：
$$\{f_n\}_{n \geq N+1} \subseteq \{f_n\}_{n \geq N} \Longrightarrow \inf_{n \geq N+1} f_n \geq \inf_{n \geq N} f_n,$$

即 $g_N \leq g_{N+1}$。$\square$

### 第二步：$g_N \uparrow \liminf_n f_n$

由 $\liminf$ 的定义，
$$\liminf_n f_n(x) = \sup_N g_N(x) = \lim_N g_N(x).$$

结合第一步的单增性，$g_N \uparrow \liminf_n f_n$ 在 $X$ 上逐点。$\square$

### 第三步：应用 MCT

由 MCT（针对 $\{g_N\}$）：
$$\int_X \liminf_n f_n\,d\mu = \lim_N \int_X g_N\,d\mu. \quad \cdots (\ast)$$

### 第四步：用 $g_N \leq f_n$（$n \geq N$）作积分比较

固定 $N$。对一切 $n \geq N$，$g_N \leq f_n$。由积分单调性：
$$\int_X g_N\,d\mu \leq \int_X f_n\,d\mu, \quad \forall\, n \geq N.$$

> [!important] 关键步：在右端取 inf
> 上式对一切 $n \geq N$ 成立，故对右端取 inf：
> $$\int_X g_N\,d\mu \leq \inf_{n \geq N} \int_X f_n\,d\mu. \quad \cdots (\dagger)$$

### 第五步：$N \to \infty$

$(\dagger)$ 中左端 $N \to \infty$（由 $(\ast)$）→ $\int \liminf_n f_n$；右端 $N \to \infty$ → $\sup_N \inf_{n \geq N} \int f_n = \liminf_n \int f_n$。

故
$$\int_X \liminf_n f_n\,d\mu \leq \liminf_n \int_X f_n\,d\mu. \quad \blacksquare$$

---

## 证明思路总结

> [!tip] 关键思想
> Fatou 引理是 MCT 的**直接推论**，关键在于构造**单增的下包络** $g_N = \inf_{n \geq N} f_n$，把"非单调极限"问题化归为"单调极限"问题：
> $$\underbrace{\liminf_n f_n}_{\text{非单调}} = \underbrace{\sup_N g_N}_{\text{单增}} = \lim_N g_N.$$
> 一旦化归为单增，MCT 即给出积分与极限交换；再用 $g_N \leq f_n$（$n \geq N$）的逐点不等式翻译到积分上，并对右端取 inf 即得结论。
>
> 直观上：$\liminf$ 是"最终落到的最低点"，积分对"局部最低"作平均时会损失，因此左端 $\leq$ 右端。

> [!warning] 不等式可能严格
> 反例 1（**质量逃逸到无穷**）：$X = \mathbb{R}$，Lebesgue 测度，$f_n = \mathbf{1}_{[n, n+1]}$。$\liminf f_n = 0$，$\int \liminf = 0$；但 $\int f_n = 1$，$\liminf \int = 1$。
>
> 反例 2（**质量集中**）：$X = \mathbb{R}$，$f_n = n \mathbf{1}_{[0, 1/n]}$。$\liminf f_n = 0$（$x = 0$ 处 $f_n = n \to \infty$，但 $x = 0$ 是零测集），$\int \liminf = 0$；$\int f_n = 1$，$\liminf \int = 1$。

> [!warning] 非负性不可省
> 反例：$f_n = -\mathbf{1}_{[n, n+1]}$。$\liminf f_n = 0$，$\int \liminf = 0$；$\int f_n = -1$，$\liminf \int = -1$。不等号方向反了。
>
> 一般实值函数的版本须假设 $|f_n| \leq g$ 且 $g$ 可积（此即 [[Lebesgue控制收敛定理]] 中的设定）。

> [!info] Fatou 引理的对偶：上极限
> 若 $f_n \leq g$ 且 $g$ 可积，可对 $g - f_n \geq 0$ 用 Fatou 得
> $$\int \limsup_n f_n\,d\mu \geq \limsup_n \int f_n\,d\mu.$$
> 这是 DCT 证明中的关键中间步骤。
