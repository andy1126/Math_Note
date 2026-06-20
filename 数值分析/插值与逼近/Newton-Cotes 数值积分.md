---
title: Newton-Cotes 数值积分
date: 2026-06-14
tags:
  - 数值分析
  - 插值与逼近
  - 数值积分
  - 求积公式
---

# Newton-Cotes 数值积分

Newton-Cotes 公式是最经典的**等距节点求积公式**：用插值多项式 $L_n$ 近似被积函数 $f$，再积分 $L_n$。它包含梯形法、Simpson 法、Boole 法等耳熟能详的工具，但也有"高阶不稳定"的著名陷阱（Runge 现象）。本笔记建立其理论框架与实战要点，并与 [[Gauss 求积]] 形成对比。

## 预备定义

> [!note] 定义 1（求积公式）
> 形如
> $$Q_n(f) = \sum_{i=0}^n A_i f(x_i) \approx \int_a^b f(x)\, dx$$
> 的近似式，其中 $\{x_i\}$ 称为**节点**，$\{A_i\}$ 称为**权重**（quadrature weights）。

> [!note] 定义 2（Newton-Cotes 公式）
> 取等距节点 $x_i = a + ih$，$h = (b-a)/n$，$i = 0, 1, \ldots, n$。权重由 [[Lagrange插值误差估计|Lagrange 基]] 积分给出：
> $$A_i = \int_a^b \ell_i(x)\, dx, \quad \ell_i(x) = \prod_{j \neq i} \frac{x - x_j}{x_i - x_j}$$
> 此为**闭型**（closed form）Newton-Cotes（端点入选）。开型则把端点排除。

> [!note] 定义 3（代数精度）
> 若求积公式对所有次数 $\leq m$ 的多项式精确，但对某 $m+1$ 次多项式不精确，则称其代数精度为 $m$。Newton-Cotes（$n$ 个间隔）至少有 $n$ 次精度；偶数 $n$ 升至 $n+1$ 次。

> [!note] 定义 4（复合公式）
> 将 $[a, b]$ 等分 $N$ 段，每段长 $h = (b-a)/N$，对每段用同一低阶 Newton-Cotes，并求和：
> $$Q_N(f) = \sum_{k=0}^{N-1} Q^{(\text{段})}([x_k, x_{k+1}])$$
> 这是抑制 Runge 现象的标准做法。

## 引理：误差核

> [!abstract] 引理（Newton-Cotes 误差核）
> 设 $f \in C^{n+1}[a, b]$。则
> $$\int_a^b f(x)\, dx - \sum_{i=0}^n A_i f(x_i) = \frac{1}{(n+1)!} \int_a^b f^{(n+1)}(\xi(x))\, \omega(x)\, dx$$
> 其中 $\omega(x) = \prod_{i=0}^n (x - x_i)$。源自 [[Lagrange插值误差估计]] 的余项 $f - L_n = \dfrac{f^{(n+1)}(\xi)}{(n+1)!}\omega(x)$ 直接积分而得。

**关键观察**：
- 当 $n$ 偶时，$\omega$ 关于区间中点反对称，$\int_a^b \omega\, dx = 0$；通过更精细的 Peano 核分析，**多一阶**精度。
- 当 $n$ 奇时，$\int_a^b \omega \neq 0$，精度只到 $n+1$。

这就是为什么 Simpson（$n=2$，4 阶精度）远优于 3/8（$n=3$，同样 4 阶精度但需更多函数值）的原因。

## 主定理

> [!important] 定理：复合 Simpson 误差
> 设 $f \in C^4[a, b]$，$N$ 偶数，$h = (b-a)/N$。则存在 $\xi \in (a, b)$ 使
> $$\int_a^b f(x)\, dx - S_N(f) = -\frac{(b-a)\, h^4}{180} f^{(4)}(\xi)$$
> 即复合 Simpson **4 阶收敛**（$h \to 0$ 时误差 $\sim h^4$）。

其中
$$S_N(f) = \frac{h}{3}\Bigl[f_0 + 4\!\!\sum_{i\,\text{奇}} f_i + 2\!\!\sum_{i\,\text{偶}, i\neq 0,N}\!\! f_i + f_N\Bigr]$$

## 证明

**单段 Simpson 误差**（已知，证明用 Peano 核或 Taylor 展开）：在 $[x_k, x_{k+2}]$（长度 $2h$），
$$\int_{x_k}^{x_{k+2}} f - \frac{h}{3}[f_k + 4 f_{k+1} + f_{k+2}] = -\frac{h^5}{90} f^{(4)}(\xi_k), \quad \xi_k \in (x_k, x_{k+2})$$

**累加**：复合 Simpson 由 $N/2$ 段拼接，
$$E = \int_a^b f - S_N(f) = -\sum_{k=1}^{N/2} \frac{h^5}{90} f^{(4)}(\xi_k) = -\frac{h^5}{90} \cdot \frac{N}{2} \cdot \frac{2}{N}\sum_{k=1}^{N/2} f^{(4)}(\xi_k)$$

由 $f^{(4)}$ 连续性 + 算术平均介值定理，存在 $\xi \in (a, b)$ 使
$$\frac{2}{N}\sum_{k=1}^{N/2} f^{(4)}(\xi_k) = f^{(4)}(\xi)$$

代入：
$$E = -\frac{h^5}{90} \cdot \frac{N}{2} \cdot f^{(4)}(\xi) = -\frac{N h^5}{180} f^{(4)}(\xi)$$

利用 $N h = (b-a)$，$N h^5 = (b-a) h^4$：
$$E = -\frac{(b-a)\, h^4}{180} f^{(4)}(\xi) \quad \square$$

## 总结

> [!info] Newton-Cotes 公式速查表
>
> | 公式 | $n$ | 系数（乘 $(b-a)$ 因子） | 误差主项 | 精度 |
> |---|---|---|---|---|
> | 梯形 | 1 | $\frac{1}{2}[1, 1]$ | $-\frac{(b-a)^3}{12} f''(\xi)$ | 1 |
> | Simpson 1/3 | 2 | $\frac{1}{6}[1, 4, 1]$ | $-\frac{(b-a)^5}{2880} f^{(4)}(\xi)$ | 3 |
> | Simpson 3/8 | 3 | $\frac{1}{8}[1, 3, 3, 1]$ | $-\frac{(b-a)^5}{6480} f^{(4)}(\xi)$ | 3 |
> | Boole | 4 | $\frac{1}{90}[7, 32, 12, 32, 7]$ | $-\frac{(b-a)^7}{1935360} f^{(6)}(\xi)$ | 5 |
>
> **规律**：偶数 $n$ 多一阶精度（节点对称性使 $\omega$ 一阶矩消失）。
>
> **复合公式误差**：
> - 复合梯形：$-\dfrac{(b-a) h^2}{12} f''(\xi)$，2 阶
> - 复合 Simpson：$-\dfrac{(b-a) h^4}{180} f^{(4)}(\xi)$，4 阶

> [!warning] Runge 现象警告
> 当 $n \geq 8$ 时，闭型 Newton-Cotes 权重出现**负系数**，且权重总和的绝对值随 $n$ 发散。后果：
> - 数值不稳（被减相消放大舍入）
> - 对光滑但有限解析半径的 $f$（如 $1/(1+x^2)$ 在 $[-5, 5]$）公式发散
>
> **实践守则**：永远不要在大区间上用单一高阶 Newton-Cotes。要么**复合**低阶，要么**自适应**，要么转 [[Gauss 求积]]。

## 应用

### 应用 1：复合 Simpson 数值实例

计算 $\displaystyle I = \int_0^1 e^{x^2}\, dx$（无初等解析解，参考值 $I \approx 1.46265\,17459$）。

取 $N = 4$，$h = 0.25$，节点函数值：
- $f(0) = 1$
- $f(0.25) = e^{0.0625} \approx 1.0645$
- $f(0.5) = e^{0.25} \approx 1.2840$
- $f(0.75) = e^{0.5625} \approx 1.7551$
- $f(1) = e \approx 2.7183$

复合 Simpson：
$$S_4 = \frac{0.25}{3}\bigl[1 + 4(1.0645 + 1.7551) + 2(1.2840) + 2.7183\bigr]$$
$$= \frac{0.25}{3}[1 + 4 \cdot 2.8196 + 2.5680 + 2.7183] = \frac{0.25}{3} \cdot 17.5647 \approx 1.46373$$

误差 $\approx 1.46373 - 1.46265 \approx 1.08 \times 10^{-3}$。

理论估计：$f^{(4)}(x) = e^{x^2}(16 x^4 + 48 x^2 + 12)$，在 $[0,1]$ 上 $\max |f^{(4)}| = f^{(4)}(1) = e \cdot 76 \approx 206.6$。
$$|E| \leq \frac{1 \cdot 0.25^4}{180} \cdot 206.6 \approx \frac{0.00391}{180} \cdot 206.6 \approx 4.49 \times 10^{-3}$$

实际误差 $1.08 \times 10^{-3}$ 落在估计内，验证理论。

### 应用 2：精度阶数对比

取 $\displaystyle I = \int_0^\pi \sin x\, dx = 2$，$N = 4$，$h = \pi/4$。

**复合梯形**：
$$T_4 = h\bigl[\tfrac{1}{2}f(0) + f(\pi/4) + f(\pi/2) + f(3\pi/4) + \tfrac{1}{2}f(\pi)\bigr]$$
$$= \frac{\pi}{4}\bigl[0 + \tfrac{\sqrt{2}}{2} + 1 + \tfrac{\sqrt{2}}{2} + 0\bigr] = \frac{\pi}{4}(1 + \sqrt{2}) \approx 0.7854 \cdot 2.4142 \approx 1.8961$$
误差 $\approx 0.1039$。

**复合 Simpson**：
$$S_4 = \frac{h}{3}\bigl[0 + 4(\tfrac{\sqrt{2}}{2} + \tfrac{\sqrt{2}}{2}) + 2 \cdot 1 + 0\bigr] = \frac{\pi/4}{3}[4\sqrt{2} + 2] \approx 0.2618 \cdot 7.6569 \approx 2.0046$$
误差 $\approx 0.0046$。

**对比**：Simpson 误差比梯形小约 23 倍。当 $N$ 加倍：梯形误差 $\to 1/4$，Simpson 误差 $\to 1/16$。这正是阶数差异（$h^2$ vs $h^4$）的实际表现。

### 应用 3：Runge 现象灾难案例

经典反例：$\displaystyle I = \int_{-5}^{5} \frac{1}{1 + x^2}\, dx = 2\arctan 5 \approx 2.7468$。

**用单一 $n = 10$ 闭型 Newton-Cotes**（11 个等距节点）：

权重 $A_i$（已查表，乘 $(b-a)/598752 = 10/598752$ 后）：
$$[16067, 106300, -48525, 272400, -260550, 427368, -260550, 272400, -48525, 106300, 16067]$$

注意权重存在**负值且绝对值很大**（$-260550$ 等）！

代入 $f(x_i) = 1/(1 + x_i^2)$，$x_i = -5 + i$，会得到与 $2.7468$ 严重偏离的结果（具体值依赖累计舍入，但几个量级的误差是常态）。这与被积函数光滑无关——Runge 现象本质是高次插值多项式在等距节点上的振荡。

**正确做法**：
- 复合 Simpson $N = 100$：误差 $< 10^{-6}$
- 自适应 Simpson：少得多的函数求值即可达到同等精度
- [[Gauss 求积]] $n = 10$：误差 $\sim 10^{-12}$

## 算法关键点

> [!tip] Newton-Cotes 实战要诀
> - **核心思想**：等距节点的插值多项式积分 = 求积公式。误差直接继承 [[Lagrange插值误差估计|插值误差]]。
> - **偶数阶优势**：偶数 $n$ 多一阶精度（对称性使 $\omega$ 的一阶矩消失）。所以梯形不如 Simpson，3/8 不如 1/3。
> - **高阶禁用**：$n \geq 8$ 起权重变号，结果发散——**绝不用单一高阶**。
> - **复合是王道**：固定低阶（Simpson 最常用），分段求和；阶数 $h^4$ 对大多数光滑函数已够用。
> - **自适应（adaptive Simpson）**：估每段误差 $|S_{2N} - S_N|/15$（外推），超阈值则二分该段。耗费集中在难处。
> - **奇异点**：端点奇异（如 $\int_0^1 \ln x\, dx$）建议**开型** Newton-Cotes 或变量替换。
> - **对比** [[Gauss 求积]]：等距节点 $n+1$ 个，精度 $\leq n+1$（偶数 $n$）；Gauss 节点同样数量精度达 $2n+1$，节点是 Legendre 多项式零点（非等距）。Gauss 在光滑函数上精度碾压 Newton-Cotes。

> [!warning] 常见陷阱
> - **复合 Simpson 要求 $N$ 偶**，否则需要在末段补 3/8 法则。
> - 自适应估计 $|S_{2N} - S_N|/15$ 假设 $f^{(4)}$ 在该段内"近似常数"——剧烈振荡的 $f$ 上估计偏乐观。
> - 复合公式中**端点权重减半**容易写错；建议先写非复合（$h \cdot \text{average}$）再扩展。

$\blacksquare$
