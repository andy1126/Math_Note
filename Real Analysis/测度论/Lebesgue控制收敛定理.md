---
title: Lebesgue 控制收敛定理 (DCT)
date: 2026-05-28
tags:
  - 实分析
  - 测度论
  - Lebesgue积分
  - 控制收敛定理
  - Dominated Convergence
---

# Lebesgue 控制收敛定理 (DCT)

## 预备定义

> [!note] 可积函数
> 设 $f: X \to \overline{\mathbb{R}}$ 可测。称 $f$ **可积**（integrable），若 $\int_X |f|\,d\mu < +\infty$，记作 $f \in L^1(\mu)$。此时定义
> $$\int_X f\,d\mu := \int_X f^+\,d\mu - \int_X f^-\,d\mu,$$
> 其中 $f^+ = \max(f, 0)$，$f^- = \max(-f, 0)$。

> [!note] 几乎处处
> 称性质 $P$ **几乎处处**（almost everywhere, a.e.）成立，若存在 $N \in \mathcal{M}$ 使 $\mu(N) = 0$ 且 $P$ 在 $X \setminus N$ 上处处成立。

> [!abstract] 引理：可积函数的基本性质
> 1. $|\int f\,d\mu| \leq \int |f|\,d\mu$；
> 2. $f, g \in L^1 \Rightarrow f + g \in L^1$ 且积分线性；
> 3. $f \in L^1 \Rightarrow f$ 几乎处处有限（即 $\mu\{|f| = +\infty\} = 0$）。

> [!abstract] 引理：Fatou 引理
> 设 $\{f_n\}$ 非负可测。则
> $$\int_X \liminf_n f_n\,d\mu \leq \liminf_n \int_X f_n\,d\mu.$$
> 详见 [[Fatou引理]]。

---

## 定理（Lebesgue 控制收敛定理）

设 $(X, \mathcal{M}, \mu)$ 为测度空间，$\{f_n\}_{n=1}^\infty$ 为 $X$ 上可测函数列。若存在 $g \in L^1(\mu)$ 使

**(D1)** $|f_n(x)| \leq g(x)$ a.e. $x \in X$，对一切 $n$；

**(D2)** $f_n(x) \to f(x)$ a.e. $x \in X$，

则 $f \in L^1(\mu)$，且

$$\lim_{n \to \infty} \int_X f_n\,d\mu = \int_X f\,d\mu,\qquad \lim_{n \to \infty} \int_X |f_n - f|\,d\mu = 0.$$

---

## 证明

### 第 0 步：化简到处处成立

设 $N_n$ 为 (D1) 失败的零测集，$N_0$ 为 (D2) 失败的零测集。令 $N = N_0 \cup \bigcup_n N_n$，则 $\mu(N) = 0$。

在 $X \setminus N$ 上 (D1)(D2) 处处成立。修改 $f_n, f$ 在 $N$ 上为 $0$ 不改变可测性、积分与极限（零测集上的修改不影响积分）。**以下假设 (D1)(D2) 处处成立**。$\square$

### 第一步：$f$ 可测且 $f \in L^1$

由 [[可测函数的逐点极限仍可测]]，$f = \lim_n f_n$ 可测。

由 (D1) 取极限，$|f| \leq g$。由积分单调性 $\int |f| \leq \int g < +\infty$，故 $f \in L^1$。$\square$

### 第二步：对 $g + f_n \geq 0$ 应用 Fatou

由 (D1)，$g + f_n \geq 0$ 处处成立。由 (D2)，$g + f_n \to g + f$ 处处。Fatou 引理：
$$\int_X (g + f)\,d\mu = \int_X \liminf_n (g + f_n)\,d\mu \leq \liminf_n \int_X (g + f_n)\,d\mu.$$

由积分线性（$g \in L^1$，$f \in L^1$，$f_n \in L^1$——后者由 $|f_n| \leq g$）：
$$\int g + \int f \leq \int g + \liminf_n \int f_n.$$

由 $\int g$ 有限，可两边减去：
$$\int_X f\,d\mu \leq \liminf_n \int_X f_n\,d\mu. \quad \cdots (\leq)$$

### 第三步：对 $g - f_n \geq 0$ 应用 Fatou

由 (D1)，$g - f_n \geq 0$ 处处。由 (D2)，$g - f_n \to g - f$ 处处。Fatou 引理：
$$\int (g - f) \leq \liminf_n \int (g - f_n).$$

即
$$\int g - \int f \leq \int g - \limsup_n \int f_n,$$

> [!info] 为何 $\liminf(-a_n) = -\limsup a_n$
> 由定义：$\liminf_n (-a_n) = \sup_N \inf_{n \geq N}(-a_n) = \sup_N(-\sup_{n \geq N} a_n) = -\inf_N \sup_{n \geq N} a_n = -\limsup_n a_n$。

故
$$\limsup_n \int_X f_n\,d\mu \leq \int_X f\,d\mu. \quad \cdots (\geq)$$

### 第四步：合并

由 $(\leq)$ 与 $(\geq)$：
$$\limsup_n \int f_n \leq \int f \leq \liminf_n \int f_n.$$

但恒有 $\liminf \leq \limsup$，故两端相等：
$$\lim_n \int_X f_n\,d\mu = \int_X f\,d\mu. \quad \square$$

### 第五步：$L^1$ 收敛 $\int |f_n - f| \to 0$

由 (D1) 与 $|f| \leq g$：
$$|f_n - f| \leq |f_n| + |f| \leq 2g.$$

令 $h_n = 2g - |f_n - f| \geq 0$。由 (D2)，$|f_n - f| \to 0$ 处处，故 $h_n \to 2g$ 处处。

Fatou：
$$\int 2g = \int \liminf_n h_n \leq \liminf_n \int h_n = \int 2g - \limsup_n \int |f_n - f|.$$

由 $\int 2g < \infty$ 可减：
$$\limsup_n \int_X |f_n - f|\,d\mu \leq 0.$$

由非负性，$\lim_n \int |f_n - f| = 0$。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> DCT 的核心是**用控制函数 $g$ "压制"序列**，再**双向应用 Fatou**：
> 1. $g + f_n \geq 0$ → Fatou → 下界 $(\leq)$；
> 2. $g - f_n \geq 0$ → Fatou → 上界 $(\geq)$。
>
> 控制函数 $g$ 是**消除质量逃逸**的关键。Fatou 引理两个标准反例（[[Fatou引理]] 中的 $\mathbf{1}_{[n, n+1]}$ 和 $n\mathbf{1}_{[0, 1/n]}$）都因无 $L^1$ 控制——前者质量逃向无穷，后者质量集中到一点——而出现严格不等。一旦存在 $g \in L^1$ 控制 $|f_n|$，这两种情形均被排除。
>
> 第五步的 $L^1$ 收敛是同一技巧的副产品：用 $2g$ 控制 $|f_n - f|$，再做一次 Fatou。

> [!warning] 控制函数不可省略
> 反例（Fatou 的 $\mathbf{1}_{[n,n+1]}$）：$f_n \to 0$ 处处，但 $\int f_n = 1$。控制 $|f_n| \leq \mathbf{1}_{[1, \infty)} = g$，而 $g \notin L^1(\mathbb{R})$（$\int g = \infty$）——DCT 失效。
>
> 反例：$f_n = n\mathbf{1}_{[0, 1/n]}$ 同样无 $L^1$ 控制。

> [!info] 推论：积分号下求导
> 设 $f(x, t)$ 关于 $x$ 可测、关于 $t$ 可微，$|\partial_t f(x, t)| \leq g(x)$ 且 $g \in L^1$。则
> $$\frac{d}{dt} \int_X f(x, t)\,d\mu(x) = \int_X \frac{\partial f}{\partial t}(x, t)\,d\mu(x).$$
> 取 $t_n \to t$，$\dfrac{f(x, t_n) - f(x, t)}{t_n - t} \to \partial_t f(x, t)$ 处处；由中值定理 $|\cdot| \leq g(x)$。应用 DCT 即得。这是 PDE、概率论、统计力学中无处不在的工具。

> [!info] 推论：Lebesgue–Vitali 收敛
> DCT 的 $L^1$ 收敛部分（$\int |f_n - f| \to 0$）说明：**a.e. 逐点收敛 + $L^1$ 控制 ⇒ $L^1$ 收敛**。但反之不真——$L^1$ 收敛不蕴含 a.e. 收敛（只能取出子列）。a.e. 收敛与 $L^1$ 收敛的精细关系由 Vitali 收敛定理刻画（用一致可积取代 $L^1$ 控制）。
