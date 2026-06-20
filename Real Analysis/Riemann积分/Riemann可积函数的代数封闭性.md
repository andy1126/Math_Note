---
title: Riemann 可积函数的代数封闭性
date: 2026-04-11
tags:
  - 实分析
  - Riemann积分
  - Darboux和
  - 代数运算
  - 振幅
---

# Riemann 可积函数的代数封闭性

## 预备定义

> [!note] Riemann 可积
> 有界函数 $f: [a, b] \to \mathbb{R}$ 是 **Riemann 可积**的，若对任意 $\varepsilon > 0$，存在分划 $P$ 使得 $U(f, P) - L(f, P) < \varepsilon$。

> [!note] 振幅
> 设 $f: [a, b] \to \mathbb{R}$ 有界，$J \subseteq [a, b]$ 为子区间。$f$ 在 $J$ 上的**振幅**为
> $$\omega(f, J) = \sup_J f - \inf_J f.$$
> 则 $U(f, P) - L(f, P) = \sum_k \omega(f, J_k)\, \Delta x_k$。

> [!abstract] 引理：Riemann 可积的等价判据
> 有界函数 $f: [a, b] \to \mathbb{R}$ Riemann 可积，当且仅当对任意 $\varepsilon > 0$，存在分划 $P$ 使得
> $$\sum_{k=1}^n \omega(f, J_k)\, \Delta x_k < \varepsilon.$$

> [!abstract] 引理：分划加细不增大上下和之差
> 若 $P'$ 是 $P$ 的加细（$P \subseteq P'$），则 $U(f, P') - L(f, P') \leq U(f, P) - L(f, P)$。
> 特别地，若 $P_1, P_2$ 为两个分划，令 $P = P_1 \cup P_2$（公共加细），则
> $$U(f, P) - L(f, P) \leq \min\{U(f, P_1) - L(f, P_1),\; U(f, P_2) - L(f, P_2)\}.$$

---

## 定理

设 $f, g: [a, b] \to \mathbb{R}$ 均为 Riemann 可积的。则：

**(i)** $f + g$ Riemann 可积。

**(ii)** $cf$ Riemann 可积（$c \in \mathbb{R}$）。

**(iii)** $fg$ Riemann 可积。

**(iv)** $|f|$ Riemann 可积。

**(v)** $\max(f, g)$ 和 $\min(f, g)$ Riemann 可积。

---

## 证明

### 第(i)部分：$f + g$ Riemann 可积

#### 关键振幅估计

对任意子区间 $J$：

$$\omega(f + g, J) \leq \omega(f, J) + \omega(g, J). \quad \cdots (\ast)$$

> [!info] 为何 $(\ast)$ 成立
> 对 $x, y \in J$：
> $$|(f+g)(x) - (f+g)(y)| \leq |f(x) - f(y)| + |g(x) - g(y)| \leq \omega(f, J) + \omega(g, J).$$
> 对左端取 $\sup_{x, y \in J}$ 即得 $\omega(f+g, J) \leq \omega(f, J) + \omega(g, J)$。

#### 验证判据

给定 $\varepsilon > 0$。由 $f, g$ Riemann 可积，存在分划 $P_f, P_g$ 使得

$$\sum_k \omega(f, J_k^f)\, \Delta x_k < \frac{\varepsilon}{2}, \qquad \sum_k \omega(g, J_k^g)\, \Delta x_k < \frac{\varepsilon}{2}.$$

取公共加细 $P = P_f \cup P_g$。由加细不增大上下和之差，$P$ 对 $f$ 和 $g$ 同时满足上述不等式。由 $(\ast)$：

$$\sum_k \omega(f+g, J_k)\, \Delta x_k \leq \sum_k \omega(f, J_k)\, \Delta x_k + \sum_k \omega(g, J_k)\, \Delta x_k < \frac{\varepsilon}{2} + \frac{\varepsilon}{2} = \varepsilon.$$

$\square$

---

### 第(ii)部分：$cf$ Riemann 可积

对任意子区间 $J$：$\omega(cf, J) = |c| \cdot \omega(f, J)$。

若 $c = 0$，$cf = 0$ 是常函数，显然可积。若 $c \neq 0$，对 $f$ 可积给出的分划 $P$（使得 $\sum \omega(f, J_k) \Delta x_k < \varepsilon / |c|$）：

$$\sum_k \omega(cf, J_k)\, \Delta x_k = |c| \sum_k \omega(f, J_k)\, \Delta x_k < \varepsilon.$$

$\square$

---

### 第(iv)部分：$|f|$ Riemann 可积

> [!important] 先证 (iv)，因为 (iii) 和 (v) 以它为基础。

#### 关键振幅估计

对任意子区间 $J$：

$$\omega(|f|, J) \leq \omega(f, J). \quad \cdots (\star)$$

> [!info] 为何 $(\star)$ 成立
> 由逆三角不等式：对 $x, y \in J$，
> $$\bigl||f(x)| - |f(y)|\bigr| \leq |f(x) - f(y)| \leq \omega(f, J).$$
> 对左端取 $\sup$ 即得 $\omega(|f|, J) \leq \omega(f, J)$。

#### 验证判据

$|f|$ 有界（$\||f|\|_\infty = \|f\|_\infty$）。由 $f$ Riemann 可积，对任意 $\varepsilon > 0$，存在分划 $P$ 使得 $\sum \omega(f, J_k) \Delta x_k < \varepsilon$。由 $(\star)$：

$$\sum_k \omega(|f|, J_k)\, \Delta x_k \leq \sum_k \omega(f, J_k)\, \Delta x_k < \varepsilon.$$

$\square$

---

### 第(iii)部分：$fg$ Riemann 可积

#### 关键振幅估计

设 $M = \max(\|f\|_\infty, \|g\|_\infty)$。对任意子区间 $J$：

$$\omega(fg, J) \leq M\, \omega(f, J) + M\, \omega(g, J). \quad \cdots (\diamond)$$

> [!info] 为何 $(\diamond)$ 成立
> 对 $x, y \in J$：
> $$|f(x)g(x) - f(y)g(y)| = |f(x)g(x) - f(x)g(y) + f(x)g(y) - f(y)g(y)|$$
> $$\leq |f(x)| \cdot |g(x) - g(y)| + |g(y)| \cdot |f(x) - f(y)| \leq M\, \omega(g, J) + M\, \omega(f, J).$$

#### 验证判据

$fg$ 有界（$\|fg\|_\infty \leq M^2$）。若 $M = 0$，则 $f = g = 0$，$fg = 0$ 平凡可积。设 $M > 0$。

由 $f, g$ Riemann 可积，取公共加细 $P$ 使得 $\sum \omega(f, J_k) \Delta x_k < \varepsilon/(2M)$ 且 $\sum \omega(g, J_k) \Delta x_k < \varepsilon/(2M)$。由 $(\diamond)$：

$$\sum_k \omega(fg, J_k)\, \Delta x_k \leq M \sum_k \omega(f, J_k)\, \Delta x_k + M \sum_k \omega(g, J_k)\, \Delta x_k < M \cdot \frac{\varepsilon}{2M} + M \cdot \frac{\varepsilon}{2M} = \varepsilon.$$

$\square$

---

### 第(v)部分：$\max(f, g)$ 和 $\min(f, g)$ Riemann 可积

利用恒等式：

$$\max(f, g) = \frac{(f + g) + |f - g|}{2}, \qquad \min(f, g) = \frac{(f + g) - |f - g|}{2}.$$

由 (i)，$f - g$ Riemann 可积；由 (iv)，$|f - g|$ Riemann 可积；再由 (i) 和 (ii)，$\max(f,g)$ 和 $\min(f,g)$ Riemann 可积。$\square$

---

### 结论

1. $f + g$ Riemann 可积。 ✓
2. $cf$ Riemann 可积。 ✓
3. $fg$ Riemann 可积。 ✓
4. $|f|$ Riemann 可积。 ✓
5. $\max(f,g)$ 和 $\min(f,g)$ Riemann 可积。 ✓

$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 所有五个部分的证明遵循同一模板：
>
> 1. **建立振幅不等式**：$\omega(\varphi(f, g), J) \leq$ 某个关于 $\omega(f, J)$ 和 $\omega(g, J)$ 的线性组合；
> 2. **取公共加细**使 $\sum \omega(f, J_k) \Delta x_k$ 和 $\sum \omega(g, J_k) \Delta x_k$ 同时小；
> 3. **代入**振幅不等式，得到 $\sum \omega(\varphi, J_k) \Delta x_k < \varepsilon$。
>
> 振幅不等式的来源各不相同：
> - **加法**：三角不等式 $|(f+g)(x) - (f+g)(y)| \leq |f(x)-f(y)| + |g(x)-g(y)|$；
> - **绝对值**：逆三角不等式 $\bigl||f(x)| - |f(y)|\bigr| \leq |f(x) - f(y)|$；
> - **乘法**：拆分 $fg(x) - fg(y) = f(x)[g(x)-g(y)] + g(y)[f(x)-f(y)]$ + 有界性；
> - **$\max$/$\min$**：归结为 $|f-g|$，即绝对值情形。

> [!warning] $f/g$ 和 $f \circ g$ 不一定保持可积性
> **除法**：若 $g$ 在 $[a, b]$ 上不离开零，$f/g$ 可能无界从而不 Riemann 可积。但若 $|g| \geq \delta > 0$（$g$ 有下界远离零），则 $1/g$ 可积（用 $\omega(1/g, J) \leq \omega(g, J)/\delta^2$），从而 $f/g = f \cdot (1/g)$ 可积。
>
> **复合**：Riemann 可积函数的复合不一定可积。但若 $f$ Riemann 可积且 $\varphi$ 在 $f$ 的值域上 **Lipschitz 连续**，则 $\varphi \circ f$ Riemann 可积（因为 $\omega(\varphi \circ f, J) \leq L \cdot \omega(f, J)$）。这统一解释了 $|f|$（$\varphi = |\cdot|$，Lipschitz 常数 $L=1$）的可积性。
