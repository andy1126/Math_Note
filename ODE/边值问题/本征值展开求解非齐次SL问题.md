---
title: 本征值展开求解非齐次 SL 问题
date: 2026-06-20
tags:
  - 微分方程
  - ODE
  - 边值问题
  - Sturm-Liouville
  - 本征值
  - 本征函数展开
  - Green函数
---

# 本征值展开求解非齐次 SL 问题

## 预备定义

> [!note] 正则 Sturm-Liouville 问题
> 考虑 $[a, b]$ 上的 SL 算子
> $$\mathcal{L} y := \frac{1}{w(x)}\Big[-(p(x)\, y')' + q(x)\, y\Big],$$
> 配以分离型齐次边界条件。其中 $p \in C^1[a, b],\ p > 0$；$q, w \in C[a, b],\ w > 0$。权函数 $w$ 使 $\mathcal{L}$ 在 $L^2_w(a, b)$ 中自伴（$\langle u, v \rangle_w := \int_a^b u v\, w\,dx$）。

> [!note] 本征值与本征函数
> $\mathcal{L} \phi_n = \lambda_n \phi_n$，其中 $\{\phi_n\}_{n=1}^\infty$ 为完备正交系：
> $$\int_a^b \phi_m(x)\, \phi_n(x)\, w(x)\, dx = \delta_{mn} \|\phi_n\|_w^2.$$
> 且 $0 \leq \lambda_1 < \lambda_2 < \cdots \to \infty$。详见 [[Sturm-Liouville定理]]。

> [!abstract] 定理：本征函数展开定理（广义 Fourier 级数）
> 对任意充分光滑的 $f$（满足边界条件），有在 $L^2_w$ 意义下的展开
> $$f(x) = \sum_{n=1}^{\infty} c_n \phi_n(x), \qquad c_n = \frac{\langle f, \phi_n \rangle_w}{\|\phi_n\|_w^2} = \frac{\int_a^b f(x) \phi_n(x) w(x)\, dx}{\int_a^b \phi_n(x)^2 w(x)\, dx}.$$
> 详见 [[Sturm-Liouville定理]] 及 [[Sturm-Liouville特征函数正交性]]。

> [!abstract] 引理：Green 函数的谱表示（Mercer 定理的 SL 版）
> 若 $\lambda = 0$ 不是本征值（即齐次问题只有零解），则 Green 函数有本征函数展开
> $$G(x, \xi) = \sum_{n=1}^{\infty} \frac{\phi_n(x)\, \phi_n(\xi)}{\lambda_n \|\phi_n\|_w^2}.$$
> 该级数在 $x \neq \xi$ 处逐点收敛，且 $L^2_w$ 意义下收敛到 $G$。

---

## 定理

考虑非齐次 SL 问题
$$\begin{cases} \mathcal{L} y = \frac{1}{w}\big[-(p y')' + q y\big] = f(x), & x \in (a, b), \\ \alpha_1 y(a) + \alpha_2 y'(a) = 0, \\ \beta_1 y(b) + \beta_2 y'(b) = 0. \end{cases} \quad \cdots (\mathrm{NH})$$

设 $0$ 不是 $\mathcal{L}$ 的本征值（即 $\lambda_n \neq 0$ 对所有 $n$）。则：

**(i)（本征函数展开解法）** 将解 $y$ 和右端 $f$ 均按正交归一化本征函数 $\{\phi_n\}$ 展开：
$$y = \sum_{n=1}^{\infty} a_n \phi_n, \qquad f = \sum_{n=1}^{\infty} c_n \phi_n,$$
则解由
$$a_n = \frac{c_n}{\lambda_n}$$
唯一确定。

**(ii)（显式公式）** (NH) 的解为
$$y(x) = \sum_{n=1}^{\infty} \frac{\langle f, \phi_n \rangle_w}{\lambda_n \|\phi_n\|_w^2}\, \phi_n(x).$$

**(iii)（与 Green 函数的等价性）** 上述级数展开与 Green 函数积分表示等价：
$$\sum_{n=1}^{\infty} \frac{\phi_n(x)}{\lambda_n \|\phi_n\|_w^2} \int_a^b f(\xi) \phi_n(\xi) w(\xi) d\xi = \int_a^b G(x, \xi) f(\xi) w(\xi) d\xi.$$

---

## 证明

### 第一步：将方程两边按本征函数展开

设 $y = \sum a_n \phi_n$，$f = \sum c_n \phi_n$。将展开式代入 $\mathcal{L} y = f$。由 $\mathcal{L}$ 的线性性与 $\mathcal{L} \phi_n = \lambda_n \phi_n$：
$$\mathcal{L} y = \mathcal{L}\!\left(\sum_{n=1}^{\infty} a_n \phi_n\right) = \sum_{n=1}^{\infty} a_n \lambda_n \phi_n = \sum_{n=1}^{\infty} c_n \phi_n.$$

> [!important] 逐项作用的合法性
> 对充分光滑的 $y$（$y \in C^2$ 且满足边界条件），其本征函数展开可逐项微分两次——这由 SL 本征函数系在更强范数下的完备性（例如 $H^2$ Sobolev 范数）保证。此处以形式推导为主，具体正则性讨论略。

### 第二步：由正交性解出系数

对两端取与 $\phi_m$ 的 $w$-内积：
$$\left\langle \sum_{n=1}^{\infty} a_n \lambda_n \phi_n,\ \phi_m \right\rangle_w = \left\langle \sum_{n=1}^{\infty} c_n \phi_n,\ \phi_m \right\rangle_w.$$

由正交归一性（设已归一化 $\|\phi_n\|_w = 1$，否则带上分母），当 $m = n$ 时内积为 $1$，否则为 $0$：
$$a_m \lambda_m = c_m \;\Longrightarrow\; a_m = \frac{c_m}{\lambda_m}. \quad \square$$

这证明了 **(i)** 和 **(ii)**。

> [!important] $\lambda_n \neq 0$ 的必要性
> 若某个 $\lambda_k = 0$，则 $a_k$ 无法由 $c_k / \lambda_k$ 确定。此时非齐次问题可解的充要条件是 $c_k = 0$（Fredholm 二择一：$\langle f, \phi_k \rangle_w = 0$），且 $a_k$ 为自由参数（即解不唯一，可加齐次解的任意倍数）。

### 第三步：与 Green 函数积分表示的等价性

将 $c_n = \int_a^b f(\xi) \phi_n(\xi) w(\xi) d\xi$ 代入 **(ii)**：
$$y(x) = \sum_{n=1}^{\infty} \frac{\phi_n(x)}{\lambda_n \|\phi_n\|_w^2} \int_a^b f(\xi) \phi_n(\xi) w(\xi) d\xi.$$

交换积分与求和（由 $\sum \frac{\phi_n(x)\phi_n(\xi)}{\lambda_n}$ 的 $L^2$ 收敛性及 $f$ 的光滑性合法）：
$$y(x) = \int_a^b \left( \sum_{n=1}^{\infty} \frac{\phi_n(x) \phi_n(\xi)}{\lambda_n \|\phi_n\|_w^2} \right) f(\xi) w(\xi) d\xi.$$

括号中级数恰为 Green 函数的谱展开 $G(x, \xi)$，故 $y(x) = \int_a^b G(x, \xi) f(\xi) w(\xi) d\xi$。这证明了 **(iii)**。$\blacksquare$

> [!info] 两种方法的互补性
> - **Green 函数法**：$G$ 一旦求出，对任意 $f$ 只需一次积分——但 $G$ 本身是分段定义的（在 $\xi$ 处拼接），不易推广到高维；
> - **本征函数展开法**：思路统一（展开 + 除本征值），直接推广到高维 PDE——但每个 $f$ 需要重新算展开系数，且级数收敛速度取决于 $f$ 的光滑性。
>
> 二者等价，选择取决于"是一次性算 $G$ 还是每次算系数"。

---

## 例：$-y'' = f$ 的本征函数展开

在 $[0, 1]$ 上，$\mathcal{L} = -d^2/dx^2$，Dirichlet 边条件 $y(0) = y(1) = 0$。本征函数（归一化）：
$$\phi_n(x) = \sqrt{2} \sin(n\pi x), \quad \lambda_n = n^2 \pi^2, \quad \|\phi_n\|_w = 1 \ (w = 1).$$

非齐次问题 $-y'' = f$ 的展开解：
$$y(x) = \sum_{n=1}^{\infty} \frac{2}{n^2 \pi^2} \left( \int_0^1 f(\xi) \sin(n\pi \xi) d\xi \right) \sin(n\pi x).$$

同时 Green 函数的谱展开恰为：
$$G(x, \xi) = \frac{2}{\pi^2} \sum_{n=1}^{\infty} \frac{\sin(n\pi x) \sin(n\pi \xi)}{n^2},$$
与 [[Green函数例题]] 的分段线性核完全一致。

---

## 证明思路总结

> [!tip] 关键思想
> 本征函数展开法的本质是**把微分算子对角化**：
> 1. 在 $\{\phi_n\}$ 这组基底下，$\mathcal{L}$ 是对角矩阵 $\operatorname{diag}(\lambda_1, \lambda_2, \ldots)$；
> 2. 于是 $\mathcal{L} y = f$ 变成无穷多个解耦的代数方程 $\lambda_n a_n = c_n$；
> 3. "解方程"变成了"做除法"：$a_n = c_n / \lambda_n$。
>
> 这与线性代数中"在特征基下求解 $A\mathbf{x} = \mathbf{b}$，答案 $\mathbf{x} = \sum (b_i / \lambda_i) \mathbf{v}_i$"**完全相同**——本征函数展开只是把有限维谱定理搬到微分算子。

> [!warning] 边界条件的核心作用
> 本征函数 $\phi_n$ 各自满足齐次边界条件，故 $\sum a_n \phi_n$ 自动满足边条件。这是该方法**不需要单独处理边条件**的原因——边条件已被"编码"进基底。
>
> 反之若 $f$ 不满足展开定理的光滑性条件（如 $f \notin L^2$ 或 $f$ 与边条件不兼容），级数解的收敛性可能退化（仅在弱意义下成为解）。

> [!info] 本征值 $\lambda = 0$ 的情形
> 若某个本征值为零（如 Neumann 边条件 $\phi'(0) = \phi'(1) = 0$ 下 $\lambda_0 = 0,\ \phi_0 = 1$），则当 $c_0 \neq 0$ 时问题无解；$c_0 = 0$ 时解含任意常数。这与有限维 $A\mathbf{x} = \mathbf{b}$ 中 $A$ 奇异的二择一完全对偶。处理方式：将 $\lambda = 0$ 的本征函数排除在展开外，解定义在正交补空间上。
