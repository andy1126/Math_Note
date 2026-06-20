---
title: Banach 不动点定理
date: 2026-04-11
tags:
  - 实分析
  - 度量空间
  - 压缩映射
  - 不动点
  - 完备性
  - Banach
---

# Banach 不动点定理

> [!info] 相关笔记
> 本笔记为**度量空间语境**下的版本。泛函分析语境下（含 Picard 迭代与数值应用等扩展）参见 [[Banach 不动点定理|Banach 不动点定理（压缩映射原理）]]。

## 预备定义

> [!note] 完备度量空间
> 称度量空间 $(X, d)$ 是**完备**的（complete），若 $X$ 中的每个 Cauchy 序列都收敛于 $X$ 中的某个点。

> [!note] 压缩映射
> 设 $(X, d)$ 为度量空间。称 $T: X \to X$ 为**压缩映射**（contraction mapping），若存在常数 $q \in [0, 1)$ 使得
> $$d(T(x), T(y)) \leq q \, d(x, y), \quad \forall\, x, y \in X.$$
> 常数 $q$ 称为**压缩系数**。

> [!note] 不动点
> 称 $x^\ast \in X$ 为 $T$ 的**不动点**（fixed point），若 $T(x^\ast) = x^\ast$。

---

## 定理

设 $(X, d)$ 为非空完备度量空间，$T: X \to X$ 为压缩系数 $q \in [0, 1)$ 的压缩映射。则：

**(i)** $T$ 有且仅有一个不动点 $x^\ast \in X$。

**(ii)** 对任意初始点 $x_0 \in X$，迭代序列 $x_{n+1} = T(x_n)$ 收敛于 $x^\ast$，且有误差估计

$$d(x_n, x^\ast) \leq \frac{q^n}{1 - q}\, d(x_0, x_1).$$

---

## 证明

取任意 $x_0 \in X$，定义迭代序列

$$x_0, \quad x_1 = T(x_0), \quad x_2 = T(x_1), \quad \dots, \quad x_{n+1} = T(x_n).$$

### 第一步：相邻项距离的几何递缩

对 $n \geq 1$：

$$d(x_{n+1}, x_n) = d(T(x_n), T(x_{n-1})) \leq q \, d(x_n, x_{n-1}).$$

归纳得

$$d(x_{n+1}, x_n) \leq q^n \, d(x_1, x_0). \quad \cdots (\ast)$$

$\square$

### 第二步：$(x_n)$ 是 Cauchy 序列

对 $m > n$，反复应用三角不等式并用 $(\ast)$：

$$d(x_m, x_n) \leq \sum_{k=n}^{m-1} d(x_{k+1}, x_k) \leq \sum_{k=n}^{m-1} q^k \, d(x_1, x_0).$$

用几何级数求和（$q < 1$）：

$$\sum_{k=n}^{m-1} q^k = q^n \cdot \frac{1 - q^{m-n}}{1 - q} < \frac{q^n}{1 - q}.$$

故

$$d(x_m, x_n) \leq \frac{q^n}{1 - q}\, d(x_1, x_0). \quad \cdots (\star)$$

由 $q^n \to 0$（$n \to \infty$），对任意 $\varepsilon > 0$，取 $N$ 充分大使得 $\dfrac{q^N}{1 - q}\, d(x_1, x_0) < \varepsilon$，则 $m > n \geq N$ 时 $d(x_m, x_n) < \varepsilon$。

故 $(x_n)$ 是 Cauchy 序列。$\square$

### 第三步：收敛至不动点

由 $X$ 完备，$(x_n)$ 收敛于某个 $x^\ast \in X$：$x_n \to x^\ast$。

验证 $T(x^\ast) = x^\ast$：

$$d(T(x^\ast), x^\ast) \leq d(T(x^\ast), T(x_n)) + d(T(x_n), x^\ast) \leq q\, d(x^\ast, x_n) + d(x_{n+1}, x^\ast).$$

$n \to \infty$ 时右端趋于 $0$，故 $d(T(x^\ast), x^\ast) = 0$，即 $T(x^\ast) = x^\ast$。$\square$

### 第四步：不动点的唯一性

设 $x^\ast, y^\ast$ 均为 $T$ 的不动点。则

$$d(x^\ast, y^\ast) = d(T(x^\ast), T(y^\ast)) \leq q\, d(x^\ast, y^\ast).$$

即 $(1 - q)\, d(x^\ast, y^\ast) \leq 0$。由 $1 - q > 0$ 和 $d \geq 0$，得 $d(x^\ast, y^\ast) = 0$，即 $x^\ast = y^\ast$。$\square$

### 第五步：误差估计

在 $(\star)$ 中令 $m \to \infty$，由距离函数的连续性 $d(x_m, x_n) \to d(x^\ast, x_n)$：

$$d(x^\ast, x_n) \leq \frac{q^n}{1 - q}\, d(x_1, x_0). \quad \square$$

### 结论

综合以上各步：

1. $T$ 有不动点 $x^\ast$（第三步）。 ✓
2. 不动点唯一（第四步）。 ✓
3. 迭代序列 $x_n \to x^\ast$，误差 $\leq \dfrac{q^n}{1 - q}\, d(x_1, x_0)$（第五步）。 ✓

$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明的逻辑链为：
> $$\text{压缩} \xRightarrow{(\ast)} \text{相邻项几何递缩} \xRightarrow{\text{几何级数}} \text{Cauchy 序列} \xRightarrow{\text{完备性}} \text{收敛} \xRightarrow{\text{压缩连续}} \text{极限是不动点} \xRightarrow{\text{压缩}} \text{唯一}$$
>
> 每一步都自然且不可省略：
> - **压缩**给出相邻项距离以比 $q$ 几何递缩；
> - **几何级数** $\sum q^k < \infty$（$q < 1$）保证序列是 Cauchy 的；
> - **完备性**保证 Cauchy 序列有极限；
> - **压缩映射的连续性**（Lipschitz，从而连续）保证可以对 $T(x_n) = x_{n+1}$ 取极限得 $T(x^\ast) = x^\ast$；
> - **唯一性**再次用压缩：两个不动点的距离压缩后不变，只有距离为零才可能。

> [!warning] 完备性与 $q < 1$ 均不可省略
> **完备性**：$T(x) = x/2$ 在 $(0, 1)$（不完备）上是压缩映射，但不动点 $0 \notin (0, 1)$。
>
> **严格压缩** $q < 1$：$T(x) = x + 1/x$ 在 $[1, \infty)$ 上满足 $d(T(x), T(y)) < d(x, y)$（对 $x \neq y$），但不存在 $q < 1$ 使得 $d(T(x), T(y)) \leq q\, d(x, y)$，且 $T$ 没有不动点。仅要求"严格缩短距离"不够，必须有**全局压缩系数** $q < 1$。
