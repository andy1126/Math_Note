---
title: 有界区间上分段连续有界函数的 Riemann 可积性
date: 2026-04-11
tags:
  - 实分析
  - Riemann积分
  - 分段连续
  - 一致连续
  - Darboux和
---

# 有界区间上分段连续有界函数的 Riemann 可积性

## 预备定义

> [!note] 分段连续
> 设 $f: [a, b] \to \mathbb{R}$。称 $f$ 是**分段连续**的（piecewise continuous），若存在分划
> $$a = c_0 < c_1 < \cdots < c_N = b,$$
> 使得 $f$ 在每个开区间 $(c_{j-1}, c_j)$（$j = 1, \dots, N$）上连续。
> 换言之，$f$ 至多在有限个点处不连续。

> [!note] 振幅
> 设 $f: S \to \mathbb{R}$ 为有界函数，$J \subseteq S$。$f$ 在 $J$ 上的**振幅**（oscillation）定义为
> $$\omega(f, J) = \sup_J f - \inf_J f.$$

> [!abstract] 引理：Riemann 可积的判定准则
> 有界函数 $f: [a, b] \to \mathbb{R}$ 是 Riemann 可积的，当且仅当对任意 $\varepsilon > 0$，存在分划 $P = \{x_0, \dots, x_n\}$ 使得
> $$U(f, P) - L(f, P) = \sum_{k=1}^{n} \omega(f, [x_{k-1}, x_k])\, \Delta x_k < \varepsilon.$$

> [!abstract] 引理：紧集上连续函数的一致连续性（[[Heine-Cantor定理|Heine-Cantor 定理]]）
> 若 $f$ 在紧集 $K \subseteq \mathbb{R}$ 上连续，则 $f$ 在 $K$ 上一致连续。

---

## 定理

设 $I$ 为有界区间，$f: I \to \mathbb{R}$ 既是分段连续的又是有界的。则 $f$ 是 Riemann 可积的。

---

## 证明

### 前提准备：归结为闭区间

若 $I$ 是退化区间（$\varnothing$ 或单点 $\{a\}$），结论平凡成立。

设 $I$ 是端点为 $a < b$ 的有界区间。将 $f$ 延拓至 $[a, b]$：在 $I$ 不包含的端点处令 $f$ 取任意值（例如 $0$）。修改有限个点的函数值不影响 Riemann 可积性（上和与下和均不变）。因此不失一般性，设

$$I = [a, b], \quad |f(x)| \leq M, \quad \forall\, x \in [a, b].$$

设 $a = c_0 < c_1 < \cdots < c_N = b$ 是使 $f$ 在每个 $(c_{j-1}, c_j)$ 上连续的分划。$\square$

---

### 核心思路

将 $[a,b]$ 分为两类区域：

- **坏区域**：分划点 $c_0, c_1, \ldots, c_N$ 的 $\delta$-邻域，$f$ 可能不连续，但总长度可控；
- **好区域**：远离分划点的部分，$f$ 连续，用一致连续性控制振幅。

---

### 第一步：选取 $\delta$，划分好区域与坏区域

给定 $\varepsilon > 0$。选取 $\delta > 0$ 满足：

$$\delta < \frac{1}{3} \min_{1 \leq j \leq N} (c_j - c_{j-1}), \qquad 4MN\delta < \frac{\varepsilon}{2}. \quad \cdots (\ast)$$

> [!info] 为何需要两个条件
> 第一个条件保证各分划点的 $\delta$-邻域互不重叠，从而好区域 $[c_{j-1}+\delta,\, c_j - \delta]$ 非空。第二个条件控制坏区域对 $U - L$ 的贡献。

**坏区域**：$[a, a+\delta]$，$[c_j - \delta, c_j + \delta]$（$1 \leq j \leq N-1$），$[b - \delta, b]$。共 $N+1$ 段，总长度

$$\ell_{\text{bad}} = \delta + 2\delta(N-1) + \delta = 2N\delta.$$

**好区域**：$[c_{j-1} + \delta,\, c_j - \delta]$，$j = 1, \dots, N$。每段上 $f$ 连续。$\square$

### 第二步：控制坏区域的贡献

在每段坏区域 $J$ 上，$|f| \leq M$，故

$$\omega(f, J) = \sup_J f - \inf_J f \leq 2M.$$

坏区域对上下和之差的贡献为

$$\sum_{\text{bad}} \omega(f, J)\, |J| \leq 2M \cdot \ell_{\text{bad}} = 2M \cdot 2N\delta = 4MN\delta < \frac{\varepsilon}{2}. \quad \cdots (\star)$$

其中最后一步用了 $(\ast)$ 的第二个条件。$\square$

### 第三步：控制好区域的贡献

对每个 $j = 1, \dots, N$，$f$ 在紧集 $[c_{j-1} + \delta,\, c_j - \delta]$ 上连续。由 Heine-Cantor 定理，$f$ 在其上一致连续：存在 $\eta_j > 0$ 使得

$$|x - y| < \eta_j \implies |f(x) - f(y)| < \frac{\varepsilon}{2(b - a)}.$$

令 $\eta = \min(\eta_1, \dots, \eta_N) > 0$。对每个好区域 $[c_{j-1} + \delta,\, c_j - \delta]$，取网格间距 $< \eta$ 的分划。则在每个子区间 $J$ 上

$$\omega(f, J) < \frac{\varepsilon}{2(b - a)}.$$

好区域的总长度不超过 $b - a$，故好区域对上下和之差的贡献为

$$\sum_{\text{good}} \omega(f, J)\, |J| < \frac{\varepsilon}{2(b - a)} \cdot (b - a) = \frac{\varepsilon}{2}. \quad \cdots (1)$$

$\square$

### 第四步：合并

将坏区域的分划点与好区域的分划点合并为 $[a,b]$ 的一个总分划 $P$。由 $(\star)$ 和 $(1)$：

$$U(f, P) - L(f, P) = \sum_{\text{bad}} \omega(f, J)\, |J| + \sum_{\text{good}} \omega(f, J)\, |J| < \frac{\varepsilon}{2} + \frac{\varepsilon}{2} = \varepsilon.$$

由 Riemann 可积的判定准则，$f$ 在 $[a, b]$ 上 Riemann 可积。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明的核心是**好坏区域分割**：
>
> 1. **坏区域**（分划点的 $\delta$-邻域）：$f$ 可能不连续，但 $f$ 有界保证振幅 $\leq 2M$，而总长度 $2N\delta$ 可通过 $\delta \to 0$ 任意缩小，贡献 $\leq 4MN\delta$；
> 2. **好区域**（远离分划点的紧子区间）：$f$ 连续且定义在紧集上，Heine-Cantor 定理保证一致连续，细分后每段振幅任意小，贡献 $< \frac{\varepsilon}{2}$；
> 3. **合并**：两部分各贡献 $< \frac{\varepsilon}{2}$，总计 $< \varepsilon$。
>
> 直觉上：有限个不连续点只能造成"有限宽度"的坏影响，而有界性保证坏影响的"高度"有限。宽度 $\times$ 高度可以任意小。

> [!warning] 有界性不可省略
> 分段连续本身不蕴含有界。例如 $f: (0, 1] \to \mathbb{R}$，$f(x) = 1/x$ 在 $(0, 1]$ 上连续（从而分段连续），但无界，且不是 Riemann 可积的。有界性保证了坏区域的振幅受控。
