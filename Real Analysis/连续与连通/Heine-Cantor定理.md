---
title: Heine-Cantor 定理
date: 2026-04-11
tags:
  - 实分析
  - 度量空间
  - 紧致性
  - 一致连续
  - Heine-Cantor
---

# Heine-Cantor 定理

## 预备定义

> [!note] 一致连续
> 设 $(X, d_X)$, $(Y, d_Y)$ 为度量空间。称 $f: X \to Y$ 是**一致连续**的（uniformly continuous），若对任意 $\varepsilon > 0$，存在 $\delta > 0$ 使得
> $$d_X(x_1, x_2) < \delta \implies d_Y(f(x_1), f(x_2)) < \varepsilon, \quad \forall\, x_1, x_2 \in X.$$
> 关键：$\delta$ 仅依赖于 $\varepsilon$，不依赖于点 $x_1, x_2$ 的选取。

> [!note] 紧致度量空间
> 度量空间 $(X, d)$ 是**紧致**的（compact），若 $X$ 中的每个序列都有收敛子列（列紧性）。
>
> 等价地，$X$ 的每个开覆盖都有有限子覆盖。（证明见 [[度量空间中紧致性与列紧性的等价]]。）

---

## 定理

设 $(X, d_X)$ 为紧致度量空间，$(Y, d_Y)$ 为度量空间，$f: X \to Y$ 连续。则 $f$ 一致连续。

---

## 证明

### 反证法

假设 $f$ 不是一致连续的。则存在 $\varepsilon_0 > 0$，使得对任意 $\delta > 0$，存在 $x_1, x_2 \in X$ 满足

$$d_X(x_1, x_2) < \delta \quad \text{但} \quad d_Y(f(x_1), f(x_2)) \geq \varepsilon_0.$$

### 第一步：构造序列对

取 $\delta = 1/n$（$n = 1, 2, 3, \dots$）。对每个 $n$，存在 $p_n, q_n \in X$ 使得

$$d_X(p_n, q_n) < \frac{1}{n} \quad \text{且} \quad d_Y(f(p_n), f(q_n)) \geq \varepsilon_0. \quad \cdots (\ast)$$

$\square$

### 第二步：利用紧致性提取收敛子列

由 $X$ 紧致，$(p_n)$ 有收敛子列 $p_{n_k} \to p$（$p \in X$）。

对子列 $(q_{n_k})$ 再次用紧致性，提取收敛子列。但实际上无需二次提取——由 $(\ast)$：

$$d_X(q_{n_k}, p) \leq d_X(q_{n_k}, p_{n_k}) + d_X(p_{n_k}, p) < \frac{1}{n_k} + d_X(p_{n_k}, p) \to 0.$$

故 $q_{n_k} \to p$。$\square$

### 第三步：推出矛盾

由 $f$ 在 $p$ 处连续：

$$p_{n_k} \to p \implies f(p_{n_k}) \to f(p),$$
$$q_{n_k} \to p \implies f(q_{n_k}) \to f(p).$$

因此

$$d_Y(f(p_{n_k}), f(q_{n_k})) \leq d_Y(f(p_{n_k}), f(p)) + d_Y(f(p), f(q_{n_k})) \to 0.$$

但由 $(\ast)$，$d_Y(f(p_{n_k}), f(q_{n_k})) \geq \varepsilon_0 > 0$ 对所有 $k$ 成立。**矛盾！**

### 结论

假设不成立，故 $f$ 是一致连续的。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明是**反证法 + 紧致性提取子列**的经典配合：
>
> 1. **否定一致连续**：得到"见证序列对" $(p_n, q_n)$——它们越来越近（$d < 1/n$），但像的距离始终 $\geq \varepsilon_0$；
> 2. **紧致性**：从 $(p_n)$ 中提取收敛子列 $p_{n_k} \to p$。由 $d(q_{n_k}, p_{n_k}) < 1/n_k \to 0$，$q_{n_k}$ 也趋于 $p$；
> 3. **连续性的矛盾**：$f$ 在 $p$ 处连续使得 $f(p_{n_k})$ 和 $f(q_{n_k})$ 都趋于 $f(p)$，与像的距离 $\geq \varepsilon_0$ 矛盾。
>
> 紧致性的作用是**将"对一切 $\delta$"的全局对手转化为一个具体极限点**，在该点处连续性产生矛盾。

> [!warning] 紧致性不可省略
> $f(x) = \sin(1/x)$ 在 $(0, 1)$ 上连续但不一致连续：在 $x \to 0^+$ 时振荡越来越密。$(0, 1)$ 不紧致（不是闭集）。更简单地，$f(x) = x^2$ 在 $\mathbb{R}$ 上连续但不一致连续：$\mathbb{R}$ 不紧致（不有界）。
