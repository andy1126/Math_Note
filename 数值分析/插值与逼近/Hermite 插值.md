---
title: Hermite 插值的存在性与唯一性
date: 2026-06-14
tags:
  - 数值分析
  - 插值与逼近
  - Hermite插值
  - 误差估计
  - 重节点差商
---

# Hermite 插值的存在性与唯一性

## 预备定义

> [!note] 定义 1（Hermite 插值问题）
> 给定 $n+1$ 个互异节点 $x_0 < x_1 < \cdots < x_n$，以及在每个节点处的函数值 $f(x_i)$ 与导数值 $f'(x_i)$（$i = 0, 1, \ldots, n$），共 $2n+2$ 个插值条件。Hermite 插值问题是寻找一个次数 $\leq 2n+1$ 的多项式 $H_{2n+1}(x)$，使得
> $$H_{2n+1}(x_i) = f(x_i), \quad H_{2n+1}'(x_i) = f'(x_i), \quad i = 0, 1, \ldots, n.$$
> 这是 [[Lagrange插值误差估计|Lagrange 插值]] 在导数信息上的自然推广。

> [!note] 定义 2（一般 Hermite 插值的推广）
> 在节点 $x_i$ 处给定 $0$ 阶到 $m_i$ 阶导数 $f^{(j)}(x_i)$（$j = 0, 1, \ldots, m_i$），共 $N = \sum_{i=0}^n (m_i + 1)$ 个插值条件，求 $H \in \mathbb{P}_{N-1}$ 满足：
> $$H^{(j)}(x_i) = f^{(j)}(x_i), \quad j = 0, \ldots, m_i, \quad i = 0, \ldots, n.$$
> 当所有 $m_i = 0$ 时即退化为 Lagrange 插值；当所有 $m_i = 1$ 时为标准 Hermite 插值。

> [!note] 定义 3（Hermite 基函数 $\alpha_i, \beta_i$）
> 对标准 Hermite 插值（$m_i = 1$）的情形，存在两组基函数 $\alpha_i(x), \beta_i(x) \in \mathbb{P}_{2n+1}$（$i = 0, \ldots, n$）满足：
> - $\alpha_i(x_j) = \delta_{ij}, \quad \alpha_i'(x_j) = 0$
> - $\beta_i(x_j) = 0, \quad \beta_i'(x_j) = \delta_{ij}$
>
> 其中 $\delta_{ij}$ 为 Kronecker 符号。

> [!note] 定义 4（Hermite 基函数的显式表达式）
> 设 $\ell_i(x) = \prod_{j \neq i} \frac{x - x_j}{x_i - x_j}$ 为 [[Lagrange插值误差估计|Lagrange 插值]] 基函数，则：
> $$\alpha_i(x) = \bigl[1 - 2(x - x_i) \ell_i'(x_i)\bigr] \ell_i^2(x)$$
> $$\beta_i(x) = (x - x_i) \ell_i^2(x)$$
> 因此 Hermite 插值多项式可写为
> $$H_{2n+1}(x) = \sum_{i=0}^n \bigl[f(x_i) \alpha_i(x) + f'(x_i) \beta_i(x)\bigr].$$

> [!note] 定义 5（重节点 Newton 形式与重节点差商）
> 把每个节点 $x_i$ 看作重复 $m_i + 1$ 次的节点，扩展节点序列为 $\tilde{x}_0, \tilde{x}_1, \ldots, \tilde{x}_{N-1}$。借助 [[Newton 差商插值]] 的 Newton 形式，定义重节点差商：
> $$f[\underbrace{x_i, x_i, \ldots, x_i}_{k+1 \text{ 次}}] = \frac{f^{(k)}(x_i)}{k!}.$$
> 此定义可由互异节点情形的差商通过节点合并取极限严格证明。

> [!note] 定义 6（节点多项式）
> 记
> $$\omega(x) = \prod_{i=0}^n (x - x_i),$$
> 称为 Hermite 插值的节点多项式。在 Hermite 插值的余项分析中将出现 $\omega^2(x)$，与 Lagrange 余项中的 $\omega(x)$ 相比幂次翻倍。

## 引理

> [!abstract] 引理 1（重节点差商的存在性）
> 设 $f \in C^k[a,b]$。若节点 $x_{i_0}, x_{i_1}, \ldots, x_{i_k}$ 中部分节点重合，则差商存在且
> $$f[x_{i_0}, x_{i_1}, \ldots, x_{i_k}] = \frac{f^{(k)}(\xi)}{k!},$$
> 其中 $\xi$ 介于这些节点的最小值与最大值之间。当所有节点重合到 $x_0$ 时，差商即为 $f^{(k)}(x_0)/k!$。

> [!abstract] 引理 2（Hermite 基函数的良定性）
> 基函数 $\alpha_i(x), \beta_i(x)$ 满足 $\deg \alpha_i \leq 2n+1$、$\deg \beta_i \leq 2n+1$，并且唯一确定。
>
> **简要证明**：$\ell_i^2(x)$ 在 $x_j$（$j \neq i$）处为 2 重零，已满足 $\beta_i$ 在这些点的两个条件；剩余在 $x_i$ 处的两个条件用一次因子 $(x - x_i)$ 与线性修正 $1 - 2(x-x_i)\ell_i'(x_i)$ 唯一调谐。次数计数：$\deg \ell_i^2 = 2n$，乘以一次因子至多 $2n+1$。

## 主定理

> [!important] 定理 1（Hermite 插值的存在性与唯一性）
> 给定 $n+1$ 个互异节点 $x_0, x_1, \ldots, x_n$ 与函数值 $f(x_i)$、导数值 $f'(x_i)$，则存在唯一的次数 $\leq 2n+1$ 多项式 $H_{2n+1}(x)$ 满足全部 $2n+2$ 个插值条件。

> [!important] 定理 2（Hermite 插值余项公式）
> 设 $f \in C^{2n+2}[a,b]$，$x_0, \ldots, x_n \in [a,b]$。对任意 $x \in [a,b]$，存在 $\xi = \xi(x) \in (a, b)$ 使
> $$f(x) - H_{2n+1}(x) = \frac{f^{(2n+2)}(\xi)}{(2n+2)!} \, \omega^2(x),$$
> 其中 $\omega(x) = \prod_{i=0}^n (x - x_i)$。注意是节点多项式的**平方**，与 Lagrange 余项相比幂次翻倍。

## 证明

### 存在唯一性证明（线性代数路径）

将 $H \in \mathbb{P}_{2n+1}$ 视作 $2n+2$ 维线性空间中的元素。插值条件给出从 $\mathbb{P}_{2n+1}$ 到 $\mathbb{R}^{2n+2}$ 的线性映射
$$\Phi(p) = \bigl(p(x_0), p'(x_0), p(x_1), p'(x_1), \ldots, p(x_n), p'(x_n)\bigr).$$

**唯一性蕴含存在性**：由维数相等，$\Phi$ 是单射当且仅当为满射。故只需证明 $\ker \Phi = \{0\}$。

设 $H_1, H_2 \in \mathbb{P}_{2n+1}$ 都满足全部插值条件。令 $p = H_1 - H_2 \in \mathbb{P}_{2n+1}$，则
$$p(x_i) = 0, \quad p'(x_i) = 0, \quad i = 0, 1, \ldots, n.$$
即每个 $x_i$ 都是 $p$ 的至少 2 重根。共 $2(n+1) = 2n+2$ 个根（计重数）。但 $\deg p \leq 2n+1 < 2n+2$，故 $p \equiv 0$，即 $H_1 = H_2$。

由此唯一性成立，且由线性映射的维数定理可推出存在性。$\square$

### 余项证明（辅助函数 + Rolle 定理）

固定 $x \in [a,b]$，$x \notin \{x_0, x_1, \ldots, x_n\}$（否则等式两端皆为零，结论平凡成立）。构造辅助函数：
$$\varphi(t) = f(t) - H_{2n+1}(t) - K \omega^2(t),$$
其中常数 $K$ 选取使 $\varphi(x) = 0$，即
$$K = \frac{f(x) - H_{2n+1}(x)}{\omega^2(x)}.$$

**统计 $\varphi$ 的零点**：

1. 在节点 $x_i$（$i = 0, \ldots, n$）处：
   - $\varphi(x_i) = f(x_i) - H_{2n+1}(x_i) - K \omega^2(x_i) = 0 - 0 = 0$（因 $\omega(x_i) = 0$）
   - $\varphi'(t) = f'(t) - H_{2n+1}'(t) - 2K \omega(t) \omega'(t)$，故
   $$\varphi'(x_i) = f'(x_i) - H_{2n+1}'(x_i) - 2K \omega(x_i) \omega'(x_i) = 0 - 0 = 0.$$
   即每个 $x_i$ 是 $\varphi$ 的至少 2 重零点。

2. 在 $t = x$ 处：$\varphi(x) = 0$（由 $K$ 的取法）。

故 $\varphi$ 在 $[a,b]$ 上至少有 $2(n+1) + 1 = 2n+3$ 个零点（计重数：$n+1$ 个节点各贡献 2 重，加上 $x$ 处的单零点）。

**Rolle 定理迭代**：由 Rolle 定理（参考 [[Lagrange插值误差估计|Lagrange 插值]] 的余项推导套路），$\varphi'$ 至少有 $2n+2$ 个零点，$\varphi''$ 至少有 $2n+1$ 个零点，……，依此类推 $2n+2$ 次后，$\varphi^{(2n+2)}$ 至少有 1 个零点。

设 $\xi \in (a, b)$ 满足 $\varphi^{(2n+2)}(\xi) = 0$。又由：
- $H_{2n+1} \in \mathbb{P}_{2n+1}$，故 $H_{2n+1}^{(2n+2)} \equiv 0$；
- $\omega^2(t) \in \mathbb{P}_{2n+2}$ 且首项系数为 $1$，故 $(\omega^2)^{(2n+2)}(t) = (2n+2)!$。

代入 $\varphi^{(2n+2)}(\xi) = 0$ 得：
$$0 = f^{(2n+2)}(\xi) - 0 - K \cdot (2n+2)!.$$
解出
$$K = \frac{f^{(2n+2)}(\xi)}{(2n+2)!}.$$

代回 $K$ 的定义式：
$$f(x) - H_{2n+1}(x) = K \omega^2(x) = \frac{f^{(2n+2)}(\xi)}{(2n+2)!} \omega^2(x). \quad \square$$

## 总结

> [!info] 总结
> Hermite 插值通过同时匹配节点处的函数值与（高阶）导数值，将插值问题的精度推到 $2n+2$ 阶。其本质有三种等价表述：
> 1. **基函数表述**：用 $\alpha_i, \beta_i$ 显式构造，结构清晰；
> 2. **重节点 Newton 形式**：将 [[Newton 差商插值]] 的差商定义自然延拓到节点重合的情形；
> 3. **线性代数表述**：插值映射 $\Phi: \mathbb{P}_{2n+1} \to \mathbb{R}^{2n+2}$ 是双射。
>
> 三种表述在算法实现、误差分析、几何应用上各有侧重。

## 应用

### 应用 1：3 阶 Hermite 插值（$n = 1$）

取 $f(x) = x e^x$，节点 $x_0 = 0, x_1 = 1$：
- $f(0) = 0, \quad f'(0) = 1$（因 $f'(x) = (1+x)e^x$）
- $f(1) = e \approx 2.71828, \quad f'(1) = 2e \approx 5.43656$

为简化数值演示，改用 $f(x) = e^x - 1$，使数值更直观。但保留原骨架以 $f(x) = x e^x$ 演示，则有 $f(1) = e \approx 2.7183$，$f'(1) = 2e$。

显式计算基函数：
- $\ell_0(x) = 1 - x$，$\ell_0'(x_0) = -1$
- $\ell_1(x) = x$，$\ell_1'(x_1) = 1$
- $\alpha_0(x) = [1 - 2(x - 0)(-1)](1 - x)^2 = (1 + 2x)(1 - x)^2$
- $\alpha_1(x) = [1 - 2(x - 1)(1)] x^2 = (3 - 2x) x^2$
- $\beta_0(x) = x (1 - x)^2$
- $\beta_1(x) = (x - 1) x^2$

故
$$H_3(x) = 0 \cdot \alpha_0(x) + e \cdot \alpha_1(x) + 1 \cdot \beta_0(x) + 2e \cdot \beta_1(x).$$

在 $x = 0.5$ 处：
- $\alpha_1(0.5) = 2 \cdot 0.25 = 0.5$
- $\beta_0(0.5) = 0.5 \cdot 0.25 = 0.125$
- $\beta_1(0.5) = -0.5 \cdot 0.25 = -0.125$
- $H_3(0.5) = e \cdot 0.5 + 0.125 + 2e \cdot (-0.125) = 0.5e + 0.125 - 0.25e = 0.25e + 0.125 \approx 0.8046$

真值 $f(0.5) = 0.5 \cdot e^{0.5} \approx 0.8244$，绝对误差约 $0.02$，远优于同节点 Lagrange 线性插值。

### 应用 2：误差衰减率对比

考察 $f(x) = \cos x$ 在 $[0, \pi]$ 上的插值：

- **Lagrange 插值**（$n+1$ 节点）：误差量级
$$|f(x) - L_n(x)| \leq \frac{\|f^{(n+1)}\|_\infty}{(n+1)!} \cdot |\omega(x)| \sim \frac{1}{(n+1)!} h^{n+1}.$$

- **Hermite 插值**（同样 $n+1$ 节点，但带导数）：误差量级
$$|f(x) - H_{2n+1}(x)| \leq \frac{\|f^{(2n+2)}\|_\infty}{(2n+2)!} \cdot \omega^2(x) \sim \frac{1}{(2n+2)!} h^{2n+2}.$$

在 $n = 2$（3 节点）情形：Lagrange 为 $O(h^3)$，Hermite 为 $O(h^6)$。当 $h = 0.1$：
- Lagrange 误差约 $10^{-3}$；
- Hermite 误差约 $10^{-7}$。

**代价**：Hermite 需要导数信息；当导数不可得（如纯采样数据），需通过差分估计，可能引入新误差源。

### 应用 3：CAGD 中的 Bézier-Hermite 曲线

计算机辅助几何设计（CAGD）中：给定端点位置 $\mathbf{P}_0, \mathbf{P}_1$ 与端点切向量 $\mathbf{T}_0, \mathbf{T}_1$，唯一存在三次 Hermite 曲线
$$\mathbf{C}(t) = h_{00}(t) \mathbf{P}_0 + h_{10}(t) \mathbf{T}_0 + h_{01}(t) \mathbf{P}_1 + h_{11}(t) \mathbf{T}_1, \quad t \in [0, 1],$$
其中 $h_{00}, h_{01}, h_{10}, h_{11}$ 为标准三次 Hermite 基。借助 [[Newton 差商插值]] 的重节点差商表示（节点序列 $0, 0, 1, 1$），可一行写出此曲线。该形式是动画轨迹规划、机器人路径插补、字体设计的基础。

## 证明思路总结

> [!tip] 关键
> - Hermite 插值是 [[Lagrange插值误差估计|Lagrange 插值]] 的"导数增强"版本：每个节点贡献 $m_i + 1$ 个条件而非 1 个；
> - 余项中节点多项式 $\omega(x)$ 升级为 $\omega^2(x)$，幂次翻倍 $\Rightarrow$ 收敛阶提升至 $2n+2$；
> - 重节点差商让 Newton 形式自然推广到 Hermite，无需引入新基（参考 [[Newton 差商插值]]）；
> - 证明套路统一：构造辅助函数 $\varphi(t) = f(t) - H(t) - K \omega^2(t)$，Rolle 定理迭代次数 = 多项式次数 + 1；
> - 高阶 Hermite 数值条件差，实践常用**分段三次 Hermite**（如 PCHIP，piecewise cubic Hermite interpolating polynomial）保单调性；
> - 三次 Hermite 是计算机图形学、轨迹规划、CAD 几何造型的基础工具（端点位置 + 切向）。

$\blacksquare$
