---
title: Sturm-Liouville 特征函数正交性
date: 2026-04-11
tags:
  - 数学物理方法
  - Sturm-Liouville问题
  - 特征值问题
  - 正交性
  - 分离变量法
---

# Sturm-Liouville 特征函数正交性

## 预备定义

> [!note] Sturm-Liouville 型方程
> 称二阶常微分方程为 **Sturm-Liouville 型方程**（S-L 型），若可写成如下形式：
> $$\frac{d}{dx}\left[p(x)\frac{dy}{dx}\right] + [\lambda w(x) - q(x)]y = 0$$
> 其中：
> - $p(x), p'(x), q(x), w(x)$ 是区间 $[a, b]$ 上的实值连续函数；
> - $p(x) > 0$，$w(x) > 0$（$w(x)$ 称为**权函数**）；
> - $\lambda$ 为参数。

> [!note] 正则 Sturm-Liouville 问题
> 给定 S-L 型方程及边界条件：
> $$\begin{cases}
> \displaystyle\frac{d}{dx}\left[p(x)\frac{dy}{dx}\right] + [\lambda w(x) - q(x)]y = 0, & a < x < b \\[10pt]
> \alpha_1 y(a) + \alpha_2 y'(a) = 0, & (\alpha_1^2 + \alpha_2^2 > 0) \\[5pt]
> \beta_1 y(b) + \beta_2 y'(b) = 0, & (\beta_1^2 + \beta_2^2 > 0)
> \end{cases}$$
> 其中 $p(x) > 0$ 且 $w(x) > 0$ 在 $[a, b]$ 上成立。求使该问题有非零解的 $\lambda$ 值及相应解，称为**正则 Sturm-Liouville 问题**（正则 S-L 问题）。

> [!note] 特征值与特征函数
> 使 S-L 问题有非零解的参数值 $\lambda$ 称为**特征值**（eigenvalue），相应的非零解 $y(x)$ 称为对应于该特征值的**特征函数**（eigenfunction）。

> [!note] 加权内积
> 在 $L^2_w([a,b])$ 上定义加权内积
> $$\langle u, v \rangle_w = \int_a^b u(x)\, v(x)\, w(x)\, dx.$$

> [!abstract] 引理：Lagrange 恒等式
> 对 S-L 型微分算子 $\mathcal{L}[y] = -\dfrac{d}{dx}\left[p(x)\dfrac{dy}{dx}\right] + q(x)y$，及任意两个具有二阶连续导数的函数 $u, v$，有：
> $$\int_a^b \left[u \mathcal{L}[v] - v \mathcal{L}[u]\right] dx = -\big[p(x)(v u' - u v')\big]_a^b$$
>
> **证明**：详见 [[Sturm-Liouville定理#预备定义]]中的推导，或直接由分部积分验证。

---

## 定理

设 $\lambda_m$ 和 $\lambda_n$ 是正则 Sturm-Liouville 问题的两个不同特征值（$\lambda_m \neq \lambda_n$），$\phi_m(x)$ 和 $\phi_n(x)$ 是对应的特征函数。则：

**(i) 正交性**：$\phi_m$ 与 $\phi_n$ 关于权函数 $w(x)$ 正交，即
$$\langle \phi_m, \phi_n \rangle_w = \int_a^b \phi_m(x) \phi_n(x) w(x)\, dx = 0$$

**(ii) 实特征值**：所有特征值都是实数。

**(iii) 特征函数的单重性**：对应于同一特征值的线性无关特征函数至多只有一个（即每个特征值的几何重数为 1）。

---

## 第(i)部分的证明：正交性

### 目标
证明对应于不同特征值的特征函数关于权函数 $w(x)$ 正交。

### 证明过程

#### 第一步：写出特征方程

**已知**：
- $\phi_m$ 对应特征值 $\lambda_m$：$\mathcal{L}[\phi_m] = \lambda_m w \phi_m$
- $\phi_n$ 对应特征值 $\lambda_n$：$\mathcal{L}[\phi_n] = \lambda_n w \phi_n$

#### 第二步：应用 Lagrange 恒等式

由 Lagrange 恒等式：
$$\int_a^b \left[\phi_m \mathcal{L}[\phi_n] - \phi_n \mathcal{L}[\phi_m]\right] dx = -\big[p(x)(\phi_m \phi_n' - \phi_n \phi_m')\big]_a^b$$

**关键观察**：由边界条件，右端边界项为零。验证如下：

在 $x = a$ 处，$\phi_m$ 和 $\phi_n$ 均满足 $\alpha_1 y(a) + \alpha_2 y'(a) = 0$。

- **若 $\alpha_2 \neq 0$**：则 $y'(a) = -\dfrac{\alpha_1}{\alpha_2}y(a)$，故
  $$\phi_m(a)\phi_n'(a) - \phi_n(a)\phi_m'(a) = \phi_m(a)\left(-\frac{\alpha_1}{\alpha_2}\phi_n(a)\right) - \phi_n(a)\left(-\frac{\alpha_1}{\alpha_2}\phi_m(a)\right) = 0$$

- **若 $\alpha_2 = 0$**：则 $\phi_m(a) = \phi_n(a) = 0$，边界项自然为零。

右端点 $x = b$ 同理。因此边界项 $-\big[p(x)(\phi_m \phi_n' - \phi_n \phi_m')\big]_a^b = 0$。$\square$

#### 第三步：代入并完成证明

代入特征方程：
$$\int_a^b \left[\phi_m (\lambda_n w \phi_n) - \phi_n (\lambda_m w \phi_m)\right] dx = 0$$

$$(\lambda_n - \lambda_m) \int_a^b \phi_m(x) \phi_n(x) w(x)\, dx = 0$$

由于 $\lambda_m \neq \lambda_n$，必有：
$$\int_a^b \phi_m(x) \phi_n(x) w(x)\, dx = 0 \quad \square$$

---

## 第(ii)部分的证明：特征值为实数

### 目标
证明正则 S-L 问题的所有特征值都是实数。

### 证明

**反证法**：假设存在复特征值 $\lambda = \alpha + i\beta$（$\beta \neq 0$），对应特征函数 $\phi(x)$（可能为复值）。

#### 第一步：构造共轭问题

取 S-L 方程的复共轭。由于 $p(x), q(x), w(x)$ 都是实值函数，$\bar{\lambda} = \alpha - i\beta$ 也是特征值，对应特征函数 $\bar{\phi}(x)$。

#### 第二步：应用正交性

若 $\beta \neq 0$，则 $\lambda \neq \bar{\lambda}$，是两个不同的特征值。

由第(i)部分证明的正交性：
$$\int_a^b \phi(x) \overline{\phi(x)} w(x)\, dx = \int_a^b |\phi(x)|^2 w(x)\, dx = 0$$

#### 第三步：导出矛盾

由于 $w(x) > 0$ 且 $|\phi(x)|^2 \geq 0$ 连续，上述积分为零意味着 $\phi(x) \equiv 0$，与特征函数的定义（非零解）**矛盾！**

因此所有特征值都是实数。$\square$

---

## 第(iii)部分的证明：特征值的几何重数为 1

### 目标
证明对应于同一特征值的线性无关特征函数至多只有一个。

### 证明（使用 Picard-Lindelöf 定理）

设 $\lambda$ 是某特征值，$\phi_1(x)$ 和 $\phi_2(x)$ 是对应于 $\lambda$ 的两个特征函数。两者均满足相同的二阶 ODE 和左端边界条件：
$$\alpha_1 y(a) + \alpha_2 y'(a) = 0$$

**关键观察**：该边界条件将初值 $(y(a), y'(a))$ 限制在一维子空间上。

- 若 $\alpha_2 \neq 0$：则 $y'(a) = -\dfrac{\alpha_1}{\alpha_2} y(a)$，比值固定
- 若 $\alpha_2 = 0$：则 $y(a) = 0$，方向固定

因此存在常数 $c$ 使得 $\phi_2(a) = c \phi_1(a)$ 且 $\phi_2'(a) = c \phi_1'(a)$。

由 [[Picard-Lindelöf定理]]（初值问题解的唯一性），$\phi_2(x) = c \cdot \phi_1(x)$ 对所有 $x \in [a,b]$ 成立。

故 $\phi_1$ 和 $\phi_2$ **线性相关**，即特征值的几何重数为 1。$\square$

---

## 重要推论

### 推论一：振荡定理

> [!abstract] 振荡定理（Oscillation Theorem）
> 第 $n$ 个特征函数 $y_n$（对应第 $n$ 个特征值 $\lambda_n$）在开区间 $(a, b)$ 内恰有 $n - 1$ 个零点。
>
> **证明**：详见 [[Sturm-Liouville定理#第(iv)部分的证明：振荡定理]]，核心工具是 Prüfer 变换。

**例子验证**：
- Fourier 正弦级数：$y_n(x) = \sin(nx)$ 在 $(0, \pi)$ 内有 $n-1$ 个零点 $x = \dfrac{k\pi}{n}$（$k = 1, 2, \ldots, n-1$）
- Legendre 多项式：$P_n(x)$ 在 $(-1, 1)$ 内有 $n$ 个零点

### 推论二：特征值离散性与渐近行为

> [!abstract] 特征值序列
> 正则 S-L 问题的特征值构成严格递增无界序列：
> $$\lambda_1 < \lambda_2 < \lambda_3 < \cdots, \quad \lambda_n \to +\infty \text{ 当 } n \to \infty$$
>
> **Weyl 渐近律**：$\lambda_n \sim \dfrac{\pi^2 n^2}{\left(\int_a^b \sqrt{w(x)/p(x)}\, dx\right)^2}$（当 $n \to \infty$）
>
> **证明**：详见 [[Sturm-Liouville定理#第(iii)部分的证明：特征值简单且离散]]，核心工具是 Prüfer 变换和角度函数的单调性。

### 推论三：特征函数的完备性

> [!abstract] 完备性定理
> 正则 S-L 问题的特征函数系 $\{y_n(x)\}_{n=1}^\infty$ 在带权 $L^2_w$ 空间中是**完备的**，即对任意 $f \in L^2([a,b], w)$，可展开为
> $$f(x) = \sum_{n=1}^\infty c_n y_n(x), \quad c_n = \frac{\langle f, y_n \rangle_w}{\langle y_n, y_n \rangle_w}$$
> 级数在 $L^2_w$ 范数下收敛。
>
> **证明**：详见 [[Sturm-Liouville定理#第(v)部分的证明：完备性]]，通过 Green 函数构造紧致自伴积分算子，应用谱定理。

### 推论四：Rayleigh 商

> [!abstract] Rayleigh 商
> 设 $\lambda_1$ 是最小特征值，则
> $$\lambda_1 = \min_{y \neq 0} \frac{\int_a^b \left[p(x)(y')^2 + q(x)y^2\right] dx}{\int_a^b w(x)y^2\, dx}$$
> 其中极小取遍满足边界条件的所有非零函数。更一般地，第 $n$ 个特征值可由极小-极大原理（min-max principle）刻画。

---

## 典型例子

### 例子一：Fourier 级数

取 $p(x) = 1, q(x) = 0, w(x) = 1$，区间 $[0, \pi]$，边界条件 $y(0) = y(\pi) = 0$。

S-L 问题化为：
$$y'' + \lambda y = 0, \quad y(0) = y(\pi) = 0$$

特征值：$\lambda_n = n^2$（$n = 1, 2, 3, \ldots$）

特征函数：$y_n(x) = \sin(nx)$

正交性：$\displaystyle\int_0^\pi \sin(mx)\sin(nx)\, dx = 0$（$m \neq n$）

零点：$y_n$ 在 $(0, \pi)$ 内有 $n-1$ 个零点 $x_k = \dfrac{k\pi}{n}$（$k = 1, \ldots, n-1$），与振荡定理一致。

### 例子二：Legendre 方程

取 $p(x) = 1-x^2, q(x) = 0, w(x) = 1$，区间 $[-1, 1]$（奇异 S-L 问题，$p(\pm 1) = 0$）。

$$(1-x^2)y'' - 2xy' + \lambda y = 0$$

特征值：$\lambda_n = n(n+1)$（$n = 0, 1, 2, \ldots$）

特征函数：Legendre 多项式 $P_n(x)$

正交性：$\displaystyle\int_{-1}^1 P_m(x)P_n(x)\, dx = 0$（$m \neq n$）

### 例子三：Bessel 方程

取 $p(x) = x, q(x) = \nu^2/x, w(x) = x$，区间 $[0, a]$（奇异 S-L 问题，$p(0) = 0$）。

$$x^2 y'' + xy' + (\lambda x^2 - \nu^2)y = 0$$

特征值：$\lambda_n = (j_{\nu,n}/a)^2$，其中 $j_{\nu,n}$ 是 Bessel 函数 $J_\nu$ 的第 $n$ 个零点。

特征函数：$\phi_n(x) = J_\nu(j_{\nu,n}x/a)$

正交性：$\displaystyle\int_0^a J_\nu\left(\frac{j_{\nu,m}x}{a}\right)J_\nu\left(\frac{j_{\nu,n}x}{a}\right)x\, dx = 0$（$m \neq n$）

---

## 相关笔记

- [[Sturm-Liouville定理]] - 完整的谱理论，包含 Lagrange 恒等式证明、Prüfer 变换、振荡定理、完备性的谱定理证明
- [[Sturm比较定理]] - 零点比较理论基础
- [[Picard-Lindelöf定理]] - 初值问题解的存在唯一性
- [[Liouville公式]] - Wronskian 的性质

---

## 证明思路总结

> [!tip] 关键思想
> Sturm-Liouville 特征函数正交性的证明核心在于 **Lagrange 恒等式** 与 **边界条件** 的结合：
>
> 1. **正交性的来源**：
>    - 两个不同特征值对应的特征函数满足：$\mathcal{L}[\phi] = \lambda w \phi$
>    - Lagrange 恒等式的左端给出 $(\lambda_m - \lambda_n)\langle \phi_m, \phi_n \rangle_w$
>    - 分离型边界条件保证右端边界项为零，从而迫使内积为零
>
> 2. **实特征值的机制**：
>    - 复特征值必成共轭对出现
>    - 若存在非实特征值，则与其共轭构成不同特征值
>    - 正交性迫使特征函数为零，矛盾
>
> 3. **单重性的本质**（Picard-Lindelöf 观点）：
>    - 二阶线性 ODE 的解空间是二维的
>    - 一个边界条件（分离型）将初值限制在一维子空间
>    - 由初值问题唯一性，解在该子空间内唯一确定
>    - 因此每个特征值只对应一个线性无关特征函数
>
> 4. **更深层的结构**（详见 [[Sturm-Liouville定理]]）：
>    - Prüfer 变换揭示了特征值的离散性和振荡定理
>    - 算子理论视角：$\mathcal{L}$ 是自伴算子，谱定理保证特征函数完备性

> [!warning] 正则性条件的必要性
> 定理要求 $p(x) > 0$ 和 $w(x) > 0$ 在**闭区间** $[a,b]$ 上成立。若 $p(x)$ 在端点处为零（如 Legendre 方程的 $p(x) = 1-x^2$、Bessel 方程的 $p(x) = x$），则称为**奇异 S-L 问题**，需要额外的分析（Weyl 的极限点/极限圆分类）。

> [!info] 分离变量法的理论基础
> Sturm-Liouville 理论是分离变量法求解偏微分方程的数学基础：
> - 波动方程、热传导方程、Laplace 方程在柱坐标、球坐标下的分离变量都导出 S-L 问题
> - 正交性保证级数展开的系数可由内积唯一确定：$c_n = \dfrac{\langle f, y_n \rangle_w}{\langle y_n, y_n \rangle_w}$
> - 完备性保证展开可以在 $L^2$ 意义下逼近任意（足够光滑的）函数
> - 振荡定理解释了为什么高阶模式有更多节点（如振动的弦、膜）
