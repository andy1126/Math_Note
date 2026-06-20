---
title: Cauchy 序列是有界的
date: 2026-04-11
tags:
  - 实分析
  - 度量空间
  - Cauchy序列
  - 有界性
---

# Cauchy 序列是有界的

## 预备定义

> [!note] Cauchy 序列
> 设 $(X, d)$ 为度量空间。称序列 $(x_n)$ 为 **Cauchy 序列**，若对任意 $\varepsilon > 0$，存在 $N \in \mathbb{N}$ 使得
> $$m, n \geq N \implies d(x_m, x_n) < \varepsilon.$$

> [!note] 有界序列
> 称序列 $(x_n)$ 在 $(X, d)$ 中**有界**，若存在 $p \in X$ 和 $M > 0$ 使得
> $$d(x_n, p) \leq M, \quad \forall\, n \in \mathbb{N}.$$

---

## 命题

设 $(X, d)$ 为度量空间，$(x_n)$ 为 $X$ 中的 Cauchy 序列。则 $(x_n)$ 有界。

---

## 证明

### 第一步：用 Cauchy 条件控制尾部

取 $\varepsilon = 1$。由 $(x_n)$ 是 Cauchy 序列，存在 $N \in \mathbb{N}$ 使得

$$m, n \geq N \implies d(x_m, x_n) < 1.$$

特别地，取 $m = N$：

$$d(x_n, x_N) < 1, \quad \forall\, n \geq N. \quad \cdots (\ast)$$

$\square$

### 第二步：合并有限初始段与尾部

令

$$M = \max\bigl(d(x_1, x_N),\; d(x_2, x_N),\; \dots,\; d(x_{N-1}, x_N),\; 1\bigr).$$

则对所有 $n \in \mathbb{N}$：

- 若 $n \geq N$：$d(x_n, x_N) < 1 \leq M$（由 $(\ast)$）；
- 若 $n < N$：$d(x_n, x_N) \leq M$（由 $M$ 的定义）。

故

$$d(x_n, x_N) \leq M, \quad \forall\, n \in \mathbb{N}.$$

$(x_n)$ 有界（以 $x_N$ 为中心，$M$ 为半径）。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 再次使用**"有限 + 尾部"论证**（与[[一致收敛的有界函数序列是一致有界的|一致收敛有界函数序列的一致有界性]]证明结构相同）：
>
> 1. **尾部**（$n \geq N$）：Cauchy 条件（取 $\varepsilon = 1$）保证所有尾部项与 $x_N$ 的距离 $< 1$；
> 2. **有限初始段**（$n < N$）：只有有限个点，直接取最大距离；
> 3. **合并**：$\max$ 统一控制全体。
>
> $\varepsilon = 1$ 的选取是任意的——任何正数都可以。
