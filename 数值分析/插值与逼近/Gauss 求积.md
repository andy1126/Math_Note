---
title: Gauss 求积：正交多项式与高斯节点
date: 2026-06-14
tags:
  - 数值分析
  - 插值与逼近
  - Gauss求积
  - 正交多项式
  - Legendre
  - 代数精度
---

# Gauss 求积：正交多项式与高斯节点

> 目标：通过最优选择求积节点，使 $n$ 点公式达到 $2n - 1$ 阶代数精度——这是节点+权重自由度允许的理论上限。Gauss 求积揭示了正交多项式的根作为最优节点的深刻原理，是高精度数值积分的基石。

---

## 预备定义

> [!note] 定义 1（带权求积公式）
> 设 $[a, b]$ 为求积区间（可为无穷区间），$w(x) > 0$ 为可积权函数。**带权求积公式**形如
> $$\int_a^b w(x) f(x) dx \approx \sum_{k=1}^n A_k f(x_k)$$
> 其中 $\{x_k\}_{k=1}^n \subset [a, b]$ 为**节点**（nodes），$\{A_k\}_{k=1}^n$ 为**权重**（weights / coefficients）。$n$ 称为公式的**阶数**或**点数**。

> [!note] 定义 2（代数精度）
> 求积公式的**代数精度**为整数 $m$，若：
> - 对所有 $f \in \mathbb{P}_m$（次数 $\leq m$ 多项式空间），公式精确成立
> - 存在某个 $f \in \mathbb{P}_{m+1}$ 使公式不精确
>
> 代数精度衡量公式对低次多项式的"完美"程度。例如，中点公式 $1$ 阶，Simpson 公式 $3$ 阶。

> [!note] 定义 3（自由度计数与最高代数精度）
> $n$ 点公式有 $n$ 个节点 + $n$ 个权重 = $2n$ 个待定参数。要求公式对 $\{1, x, x^2, \ldots, x^{2n-1}\}$ 全部精确，恰是 $2n$ 个方程：
> $$\sum_{k=1}^n A_k x_k^j = \int_a^b w(x) x^j dx, \quad j = 0, 1, \ldots, 2n-1$$
> 故**理论上限**为 $2n - 1$ 阶代数精度。Gauss 求积达到此上限。

> [!note] 定义 4（正交多项式族）
> 在 $L^2_w([a, b])$ 上以内积
> $$\langle f, g \rangle_w = \int_a^b w(x) f(x) g(x) dx$$
> 对单项式列 $1, x, x^2, \ldots$ 作 Gram-Schmidt 正交化，得**正交多项式族** $\{p_k(x)\}_{k \geq 0}$，满足：
> - $\deg p_k = k$
> - $\langle p_j, p_k \rangle_w = h_k \delta_{jk}$（$h_k > 0$）
> - 三项递推：$p_{k+1}(x) = (\alpha_k x + \beta_k) p_k(x) - \gamma_k p_{k-1}(x)$

> [!note] 定义 5（经典正交多项式族 表）
> 不同区间与权对应不同经典族：
>
> | 区间 | 权 $w(x)$ | 正交多项式 | 求积命名 |
> |------|----------|-----------|---------|
> | $[-1, 1]$ | $1$ | [[Legendre多项式的正交性\|Legendre]] $P_n$ | Gauss-Legendre |
> | $[-1, 1]$ | $1/\sqrt{1-x^2}$ | [[Chebyshev 多项式与最佳一致逼近\|Chebyshev]] $T_n$ | Gauss-Chebyshev |
> | $[0, \infty)$ | $e^{-x}$ | Laguerre $L_n$ | Gauss-Laguerre |
> | $(-\infty, \infty)$ | $e^{-x^2}$ | Hermite $H_n$ | Gauss-Hermite |
>
> 这些正交族全部为相应 [[Sturm-Liouville特征函数正交性|Sturm-Liouville 问题]] 的特征函数，正交性由 SL 理论统一保证。

---

## 引理

> [!abstract] 引理 1（正交多项式根的实性、单性、区间内性）
> 正交多项式 $p_n$ 的 $n$ 个根**全部为实数、互异（单根）**，且全部位于开区间 $(a, b)$ 内。

**证明**：设 $p_n$ 在 $(a, b)$ 内**变号**于 $\xi_1 < \xi_2 < \cdots < \xi_m$（$m \leq n$，因 $\deg p_n = n$）。需证 $m = n$。

构造辅助多项式
$$q(x) = (x - \xi_1)(x - \xi_2) \cdots (x - \xi_m), \quad \deg q = m$$

$p_n \cdot q$ 在 $(a, b)$ 内**不变号**：因 $p_n$ 与 $q$ 在每个 $\xi_i$ 处同时变号，乘积变号互相抵消，故 $p_n q$ 在 $(a, b)$ 内保持同号（不妨设 $\geq 0$）。又 $w > 0$，故
$$\int_a^b w(x) p_n(x) q(x) dx > 0 \tag{1}$$

另一方面，若 $m < n$，则 $q \in \mathbb{P}_{n-1}$，由正交性 $p_n \perp \mathbb{P}_{n-1}$，
$$\int_a^b w p_n q dx = 0 \tag{2}$$
$(1)$ 与 $(2)$ 矛盾。故 $m = n$，即 $p_n$ 在 $(a, b)$ 内有 $n$ 个变号点，全部为单根、实根、内点。$\square$

> [!abstract] 引理 2（Gauss 权重正性）
> 取 Gauss 节点 $\{x_k\}_{k=1}^n$ 为 $p_n$ 的根，权重定义为
> $$A_k = \int_a^b w(x) \ell_k(x) dx, \quad \ell_k(x) = \prod_{j \neq k} \frac{x - x_j}{x_k - x_j}$$
> 则所有 $A_k > 0$。

**证明**：注意 $\ell_k \in \mathbb{P}_{n-1}$，故 $\ell_k^2 \in \mathbb{P}_{2n-2} \subset \mathbb{P}_{2n-1}$。

后面将证 Gauss 求积对 $\mathbb{P}_{2n-1}$ 精确，故
$$\int_a^b w(x) \ell_k^2(x) dx = \sum_{j=1}^n A_j \ell_k^2(x_j) \tag{3}$$

由 Lagrange 基函数性质 $\ell_k(x_j) = \delta_{jk}$，故 $\ell_k^2(x_j) = \delta_{jk}$。$(3)$ 化为
$$\int_a^b w \ell_k^2 dx = A_k \tag{4}$$

LHS $> 0$（因 $w > 0$ 且 $\ell_k^2 \geq 0$ 不恒零），故 $A_k > 0$。$\square$

---

## 主定理

> [!important] 定理 1（Gauss 求积存在唯一性 + $2n-1$ 阶代数精度）
> 取节点 $\{x_k\}_{k=1}^n$ 为正交多项式 $p_n$（关于权 $w$）的 $n$ 个根，权重
> $$A_k = \int_a^b w(x) \ell_k(x) dx, \quad \ell_k(x) = \prod_{j \neq k} \frac{x - x_j}{x_k - x_j}$$
> 则求积公式
> $$\boxed{\int_a^b w(x) f(x) dx \approx \sum_{k=1}^n A_k f(x_k)}$$
> 对所有 $f \in \mathbb{P}_{2n-1}$ **精确**，即代数精度恰为 $2n - 1$。
>
> 此外，$n$ 点公式中**唯一**达到此精度的就是上述 Gauss 求积公式（节点必须为 $p_n$ 的根）。

> [!important] 定理 2（Gauss 求积余项）
> 设 $f \in C^{2n}[a, b]$，$\gamma_n$ 为 $p_n$ 的首项系数。存在 $\xi \in (a, b)$ 使
> $$R_n(f) = \int_a^b w f dx - \sum_{k=1}^n A_k f(x_k) = \frac{f^{(2n)}(\xi)}{(2n)! \, \gamma_n^2} \int_a^b w(x) p_n^2(x) dx$$
>
> 余项含 $f^{(2n)}$，故对解析函数 $R_n$ 随 $n$ **指数衰减**——这是 Gauss 求积高效的根本原因。

---

## 证明

**$2n - 1$ 阶精度证明**：设 $f \in \mathbb{P}_{2n-1}$。用 $p_n$（$\deg p_n = n$）作多项式长除：
$$f(x) = p_n(x) q(x) + r(x), \quad \deg q \leq n - 1, \quad \deg r \leq n - 1 \tag{5}$$

**积分侧**：
$$\int_a^b w f dx = \int_a^b w p_n q dx + \int_a^b w r dx$$

由正交性 $p_n \perp \mathbb{P}_{n-1}$，且 $q \in \mathbb{P}_{n-1}$，故第一项为 $0$：
$$\int_a^b w f dx = \int_a^b w r dx \tag{6}$$

**求积侧**：在 Gauss 节点 $x_k$ 处 $p_n(x_k) = 0$，故由 $(5)$
$$f(x_k) = p_n(x_k) q(x_k) + r(x_k) = r(x_k)$$
$$\sum_{k=1}^n A_k f(x_k) = \sum_{k=1}^n A_k r(x_k) \tag{7}$$

权重 $A_k$ 由 Lagrange 插值积分定义，故 $n$ 点求积对 $\mathbb{P}_{n-1}$（即至多 $n-1$ 次多项式可被 Lagrange 插值精确重构）精确成立。$r \in \mathbb{P}_{n-1}$，故
$$\sum_{k=1}^n A_k r(x_k) = \int_a^b w r dx \tag{8}$$

合并 $(6), (7), (8)$：
$$\int_a^b w f dx = \int_a^b w r dx = \sum_{k=1}^n A_k r(x_k) = \sum_{k=1}^n A_k f(x_k)$$

即 Gauss 求积对 $\mathbb{P}_{2n-1}$ 精确。$\square$

**最优性（不可达 $2n$ 阶）**：取
$$f(x) = \prod_{k=1}^n (x - x_k)^2 \in \mathbb{P}_{2n}$$
显然 $f(x) \geq 0$ 且不恒零，故 $\int_a^b w f dx > 0$。但 $f(x_k) = 0$ for all $k$，故 $\sum A_k f(x_k) = 0$。两侧不等，故 $n$ 点公式不可能达到 $2n$ 阶代数精度。$2n - 1$ 阶为上限。$\square$

**唯一性**：若另一组节点 $\{\tilde x_k\}$ 给出 $2n - 1$ 阶精度公式，定义 $\tilde p(x) = \prod (x - \tilde x_k) \in \mathbb{P}_n$。对任意 $q \in \mathbb{P}_{n-1}$，$\tilde p \cdot q \in \mathbb{P}_{2n-1}$，由精度
$$\int_a^b w \tilde p q dx = \sum_k \tilde A_k \tilde p(\tilde x_k) q(\tilde x_k) = 0$$
（因 $\tilde p(\tilde x_k) = 0$）。故 $\tilde p \perp \mathbb{P}_{n-1}$，由正交多项式唯一性（首项系数固定下），$\tilde p$ 与 $p_n$ 仅差常数倍，即 $\{\tilde x_k\}$ 必为 $p_n$ 的根。$\square$

---

## 总结

> [!info] 核心要点
> - **节点选择**：Gauss 节点 = 正交多项式 $p_n$（关于积分权 $w$）的根
> - **代数精度**：$2n - 1$ 阶（达到 $2n$ 自由度允许的理论上限）
> - **权重**：$A_k = \int w \ell_k dx > 0$（正性保证数值稳定）
> - **余项**：$\propto f^{(2n)}(\xi)$，对光滑函数指数衰减
> - **几何意义**：将多项式空间 $\mathbb{P}_{2n-1}$ 分解为 $\mathbb{P}_{n-1} \oplus p_n \cdot \mathbb{P}_{n-1}$，正交性消去后者
> - **与等距节点对比**：[[Newton-Cotes 数值积分|Newton-Cotes]] $n$ 点至多 $n$ 阶；Gauss $n$ 点达 $2n-1$ 阶——精度近翻倍

---

## 应用

### 应用 1：Gauss-Legendre 2 点公式

- 区间 $[-1, 1]$，权 $w \equiv 1$
- $P_2(x) = \frac{1}{2}(3x^2 - 1)$，根 $x_{1,2} = \pm 1/\sqrt{3}$
- 由对称性 $A_1 = A_2$，由 $\int_{-1}^1 1 dx = 2$ 得 $A_1 = A_2 = 1$

$$\int_{-1}^1 f(x) dx \approx f(-1/\sqrt{3}) + f(1/\sqrt{3})$$

**精度验证**：
- $f(x) = x^3$（应精确，3 = $2n - 1$）：左边 $= 0$；右边 $= -3^{-3/2} + 3^{-3/2} = 0$ ✓
- $f(x) = x^4$（不精确）：左边 $= 2/5 = 0.4$；右边 $= 2 \cdot (1/3)^2 = 2/9 \approx 0.222$ ✗

仅 $2$ 个函数求值即达 $3$ 阶精度，远超梯形（1 阶）与 Simpson（3 阶但需 3 点）。

### 应用 2：Gauss-Legendre 3 点公式

- $P_3(x) = \frac{1}{2}(5x^3 - 3x)$，根 $x = 0, \pm\sqrt{3/5}$
- 权重 $A_1 = A_3 = 5/9$，$A_2 = 8/9$

$$\int_{-1}^1 f(x) dx \approx \frac{5}{9} f\left(-\sqrt{\tfrac{3}{5}}\right) + \frac{8}{9} f(0) + \frac{5}{9} f\left(\sqrt{\tfrac{3}{5}}\right)$$

代数精度 $5$ 阶。

**算例**：$\int_{-1}^1 e^x dx = e - e^{-1} \approx 2.35040$。
$$\approx \frac{5}{9} e^{-0.7746} + \frac{8}{9} \cdot 1 + \frac{5}{9} e^{0.7746} \approx 2.35034$$
误差 $\sim 6 \times 10^{-5}$，对比 Simpson 三点 $\approx 2.36205$（误差 $\sim 10^{-2}$），Gauss 优势明显。

### 应用 3：Gauss-Chebyshev 求积（带奇异核）

- 区间 $[-1, 1]$，权 $w(x) = 1/\sqrt{1 - x^2}$
- 节点为 [[Chebyshev 多项式与最佳一致逼近|Chebyshev 多项式 $T_n$]] 的根
$$x_k = \cos\left(\frac{(2k - 1)\pi}{2n}\right), \quad k = 1, \ldots, n$$
- 权重**全部相等**：$A_k = \pi / n$

$$\int_{-1}^1 \frac{f(x)}{\sqrt{1 - x^2}} dx \approx \frac{\pi}{n} \sum_{k=1}^n f(x_k)$$

**用途**：积分核含 $1/\sqrt{1-x^2}$ 奇异权时（如圆盘上的奇异积分、谱方法），Gauss-Chebyshev 自然吸收奇异性，节点+权重显式简单。与 FFT 结合可在 $O(n \log n)$ 计算大量节点上的多项式值。

### 应用 4：一般区间的变量代换

要计算 $\int_a^b f(x) dx$，作线性代换 $x = \frac{b-a}{2} t + \frac{a+b}{2}$，$t \in [-1, 1]$：
$$\int_a^b f(x) dx = \frac{b - a}{2} \int_{-1}^1 f\left(\frac{b-a}{2} t + \frac{a+b}{2}\right) dt$$

应用 $n$ 点 Gauss-Legendre：
$$\approx \frac{b - a}{2} \sum_{k=1}^n A_k f\left(\frac{b-a}{2} t_k + \frac{a+b}{2}\right)$$

复合 Gauss（区间细分 + 各子区间用低阶 Gauss）兼顾精度与稳定性。

### 应用 5：与 Newton-Cotes 对比及 Golub-Welsch 算法

| 比较项 | [[Newton-Cotes 数值积分\|Newton-Cotes]] | Gauss-Legendre |
|-------|------------------------------------|----------------|
| 节点 | 等距 | $P_n$ 的根 |
| $n$ 点精度 | $\leq n$（偶数 $n$ 加 1） | $2n - 1$ |
| 权重正性 | $n \geq 9$ 出现负权（Runge 风险） | 全部正 |
| 易用性 | 节点显式 | 需查表/算法 |

**Golub-Welsch 算法**：将正交多项式三项递推转为对称三对角矩阵
$$J = \begin{pmatrix} a_0 & b_1 & & \\ b_1 & a_1 & b_2 & \\ & b_2 & a_2 & \ddots \\ & & \ddots & \ddots \end{pmatrix}$$
$J$ 的特征值 $=$ Gauss 节点；首特征向量分量平方 $\times \int w dx =$ 权重。$O(n^2)$ 高效计算。

**Gauss-Kronrod 嵌入式**：在 $n$ 点 Gauss 上添加 $n+1$ 个新节点，构成 $2n + 1$ 点 Kronrod 公式（$3n + 1$ 阶精度）。两阶估计差给出**误差估计**，是自适应求积（QUADPACK 库）的核心。

---

## 证明思路总结

> [!tip] 思路核心
> - **自由度计数**：$n$ 节点 $+$ $n$ 权 $= 2n$ 参数 $\Rightarrow$ 最高 $2n - 1$ 阶精度（上限论证）
> - **节点取正交多项式根**：使长除 $f = p_n q + r$ 时 $\int w p_n q = 0$（正交消项）
> - **关键代数恒等式**：$f \in \mathbb{P}_{2n-1}$，长除后 $r \in \mathbb{P}_{n-1}$，求积对 $\mathbb{P}_{n-1}$ 自动精确（Lagrange 系数）
> - **权重正性**：用 $\ell_k^2 \in \mathbb{P}_{2n-2}$ 与 $2n-1$ 阶精度，得 $A_k = \int w \ell_k^2 > 0$
> - **根的实性区间内性**：源自 [[Sturm-Liouville特征函数正交性|Sturm-Liouville]] 特征函数振荡定理与 [[Legendre多项式的正交性|Legendre 正交性]]
> - **唯一性**：节点决定 $p_n$，正交多项式族在首项归一下唯一
> - **余项 $f^{(2n)}$**：插值误差理论 + 正交性 $\Rightarrow$ 高阶光滑性带来超指数收敛
> - **算法实现**：Golub-Welsch（三对角特征值）；自适应：Gauss-Kronrod 嵌入估计
> - **特殊权变体**：Gauss-Legendre（$w=1$）、Gauss-Chebyshev（$1/\sqrt{1-x^2}$）、Gauss-Hermite（$e^{-x^2}$）、Gauss-Laguerre（$e^{-x}$）—— 统一框架，权选择由问题物理决定

$\blacksquare$
