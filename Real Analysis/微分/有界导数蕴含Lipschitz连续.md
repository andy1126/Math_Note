---
title: 有界导数蕴含 Lipschitz 连续
date: 2026-04-11
tags:
  - 实分析
  - 微分
  - Lipschitz连续
  - 中值定理
---

# 有界导数蕴含 Lipschitz 连续

## 预备定义

> [!note] Lipschitz 连续
> 设 $f: I \to \mathbb{R}$（$I$ 为区间）。称 $f$ 是 **Lipschitz 连续**的，若存在常数 $M \geq 0$ 使得
> $$|f(x) - f(y)| \leq M\,|x - y|, \quad \forall\, x, y \in I.$$
> 最小的这样的 $M$ 称为 $f$ 的 **Lipschitz 常数**。

> [!abstract] [[中值定理|中值定理]]（Mean Value Theorem）
> 设 $f: [a, b] \to \mathbb{R}$ 在 $[a, b]$ 上连续，在 $(a, b)$ 上可微。则存在 $c \in (a, b)$ 使得
> $$f(b) - f(a) = f'(c)\,(b - a).$$

---

## 定理

设 $f: I \to \mathbb{R}$ 在区间 $I$ 上可微，且导数有界：存在 $M \geq 0$ 使得

$$|f'(x)| \leq M, \quad \forall\, x \in I.$$

则 $f$ 是 Lipschitz 连续的，Lipschitz 常数不超过 $M$。

---

## 证明

设 $x, y \in I$，不失一般性设 $x < y$。则 $f$ 在 $[x, y]$ 上连续、在 $(x, y)$ 上可微。由中值定理，存在 $c \in (x, y)$ 使得

$$f(y) - f(x) = f'(c)\,(y - x).$$

取绝对值：

$$|f(y) - f(x)| = |f'(c)| \cdot |y - x| \leq M\,|y - x|.$$

由 $x, y$ 的任意性，$f$ 是 Lipschitz 连续的，常数不超过 $M$。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 中值定理将两点间的增量差**精确地**归结为某中间点的导数值乘以距离：
> $$|f(y) - f(x)| = |f'(c)| \cdot |y - x|.$$
> 导数有界 $|f'| \leq M$ 直接给出 Lipschitz 条件。证明本质上是一步。

> [!warning] 反向不成立
> Lipschitz 连续不蕴含可微。经典反例：$f(x) = |x|$ 在 $\mathbb{R}$ 上 Lipschitz 连续（常数 $M = 1$），但在 $x = 0$ 处不可微。

> [!info] Lipschitz 连续蕴含一致连续
> Lipschitz 连续是比一致连续更强的条件：取 $\delta = \varepsilon / M$ 即得一致连续性。因此，有界导数的函数自动一致连续。但反之不然——$f(x) = \sqrt{x}$ 在 $[0, 1]$ 上一致连续，但不是 Lipschitz 连续的（$f'(x) = 1/(2\sqrt{x})$ 在 $x \to 0^+$ 时无界）。
