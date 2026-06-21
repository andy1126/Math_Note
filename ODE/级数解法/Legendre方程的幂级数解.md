---
title: Legendre 方程的幂级数解
date: 2026-06-20
tags:
  - 题解
  - 微分方程
  - ODE
  - 级数解法
  - Legendre方程
  - Legendre多项式
  - 本征值
---

# Legendre 方程的幂级数解

## 题目

> 在常点 $x = 0$ 附近求 **Legendre 方程**
> $$(1 - x^2) y'' - 2x y' + \lambda y = 0, \quad \lambda \in \mathbb{R}$$
> 的幂级数解（至 $x^4$ 项），讨论 $\lambda = n(n+1)$（$n \in \mathbb{N}$）时级数截断为 **Legendre 多项式**的条件。

---

## 预备定义与定理

> [!note] Legendre 方程
> 标准形 $y'' + p(x) y' + q(x) y = 0$，其中
> $$p(x) = -\frac{2x}{1 - x^2}, \qquad q(x) = \frac{\lambda}{1 - x^2}.$$
> $p, q$ 均在 $x = 0$ 处解析，故 $x = 0$ 是常点。奇点在 $x = \pm 1$（分母零点），故幂级数解的收敛半径**至少为 $1$**。

> [!abstract] 定理：常点的幂级数解（Fuchs 定理）
> 在常点 $x_0$ 处存在两个线性独立的解析解，收敛半径 $\geq$ $x_0$ 到最近奇点的距离。对 Legendre 方程，该距离为 $1$。详见 [[常点附近的幂级数解]]。

> [!abstract] 引理：Cauchy 乘积
> 两个幂级数的乘积 $\big(\sum a_n x^n\big) \big(\sum b_n x^n\big) = \sum \big(\sum_{j=0}^n a_j b_{n-j}\big) x^n$。

> [!note] Legendre 多项式 $P_n(x)$
> 当 $\lambda = n(n+1)$（$n \in \mathbb{N}$）时，Legendre 方程有次数为 $n$ 的多项式解——标准化后即为 **Legendre 多项式** $P_n(x)$。$P_n(1) = 1$，$P_n$ 在 $[-1, 1]$ 上正交（$L^2$ 内积权函数 $w \equiv 1$），是 $[-1, 1]$ 上 Sturm-Liouville 本征值问题的本征函数。详见 [[Sturm-Liouville定理]]。

---

## 解答

### 第一步：设幂级数 $y = \sum a_n x^n$

设 $y = \sum_{n=0}^\infty a_n x^n$，则
$$y' = \sum_{n=1}^\infty n a_n x^{n-1}, \qquad y'' = \sum_{n=2}^\infty n(n-1) a_n x^{n-2}.$$

### 第二步：代入 Legendre 方程

代入 $(1 - x^2) y'' - 2x y' + \lambda y = 0$：
$$y'' - x^2 y'' - 2x y' + \lambda y = 0.$$

各项的级数表示：
- $y''$：$\sum_{n=0}^\infty (n+2)(n+1) a_{n+2} x^n$
- $-x^2 y''$：$-\sum_{n=2}^\infty n(n-1) a_n x^n$
- $-2x y'$：$-2\sum_{n=1}^\infty n a_n x^n$
- $\lambda y$：$\lambda \sum_{n=0}^\infty a_n x^n$

### 第三步：对齐 $x^n$ 系数

对 $n \geq 0$，合并四项的 $x^n$ 系数：
$$(n+2)(n+1) a_{n+2} - n(n-1) a_n - 2n a_n + \lambda a_n = 0.$$

化简系数中 $a_n$ 的因子：$-n(n-1) - 2n + \lambda = -n^2 + n - 2n + \lambda = \lambda - n(n+1)$。故
$$(n+2)(n+1) a_{n+2} + \big[\lambda - n(n+1)\big] a_n = 0, \quad n \geq 2 \text{ 时 } x^2 y'' \text{ 项才出现}.$$

> [!info] $n = 0, 1$ 分别处理
> $n = 0$：$2 \cdot 1 \cdot a_2 + \lambda a_0 = 0 \;\Longrightarrow\; a_2 = -\frac{\lambda}{2} a_0$。
> $n = 1$：$3 \cdot 2 \cdot a_3 + (\lambda - 2) a_1 = 0 \;\Longrightarrow\; a_3 = -\frac{\lambda - 2}{6} a_1$。
>
> $n \geq 2$：$(n+2)(n+1) a_{n+2} + [\lambda - n(n+1)] a_n = 0$。此公式对 $n = 0, 1$ 也成立（验算确认）。

### 第四步：递推关系

对 $n \geq 0$，
$$a_{n+2} = \frac{n(n+1) - \lambda}{(n+2)(n+1)}\, a_n. \quad \cdots (\ast)$$

递推只连接相差 $2$ 的指标，故**偶次系数与奇次系数各自独立递推**。
- 偶次：$a_0 \to a_2 \to a_4 \to a_6 \to \cdots$
- 奇次：$a_1 \to a_3 \to a_5 \to a_7 \to \cdots$

两个自由度 $(a_0, a_1)$ 恰好对应两个线性独立解。

### 第五步：计算前几项

以 $a_0, a_1$ 为自由参数：
$$\begin{aligned}
a_2 &= -\frac{\lambda}{2} a_0, \qquad &
a_3 &= -\frac{\lambda - 2}{6} a_1, \\
a_4 &= \frac{6 - \lambda}{12} a_2 = \frac{\lambda(\lambda - 6)}{24} a_0, \qquad &
a_5 &= \frac{12 - \lambda}{20} a_3 = \frac{(\lambda - 2)(\lambda - 12)}{120} a_1.
\end{aligned}$$

故
$$\begin{aligned}
y_{\text{even}} &= a_0 \left(1 - \frac{\lambda}{2} x^2 + \frac{\lambda(\lambda - 6)}{24} x^4 - \cdots \right), \\
y_{\text{odd}} &= a_1 \left(x - \frac{\lambda - 2}{6} x^3 + \frac{(\lambda - 2)(\lambda - 12)}{120} x^5 - \cdots \right).
\end{aligned}$$

### 第六步：本征值截断 ⇒ Legendre 多项式

考察递推 $(\ast)$ 的分子：$n(n+1) - \lambda$。当 $\lambda = n(n+1)$ 时，分子在 $n = \lambda$ 对应的指标处**变为零**，递推在此"卡住"。

更精确地：若 $\lambda = N(N+1)$（$N \in \mathbb{N}$），则当 $n = N$ 时分子为零，故 $a_{N+2} = 0$，进而 $a_{N+4} = a_{N+6} = \cdots = 0$——**级数截断为 $N$ 次多项式**。

- $N$ 为偶数：偶次序列截断，奇次序列仍为无穷级数（在 $|x| = 1$ 处发散）；
- $N$ 为奇数：奇次序列截断。

取 $a_1 = 0$（$N$ 偶）或 $a_0 = 0$（$N$ 奇），并标准化 $P_N(1) = 1$，即得 Legendre 多项式：

$$P_0 = 1,\ P_1 = x,\ P_2 = \frac{1}{2}(3x^2 - 1),\ P_3 = \frac{1}{2}(5x^3 - 3x),\ P_4 = \frac{1}{8}(35x^4 - 30x^2 + 3).$$

### 第七步：收敛半径

当 $\lambda \neq N(N+1)$ 时，递推 $a_{n+2}/a_n \to 1$（$n \to \infty$），由比值判别法，收敛半径 $R = 1$。这恰为 $x_0 = 0$ 到最近奇点 $x = \pm 1$ 的距离——与 Fuchs 定理的上界精确吻合。$\blacksquare$

---

## 答案

Legendre 方程在 $x = 0$ 处的两个线性独立级数解：
$$\boxed{ y_1 = 1 - \frac{\lambda}{2} x^2 + \frac{\lambda(\lambda - 6)}{24} x^4 - \cdots } \quad (\text{偶函数})$$
$$\boxed{ y_2 = x - \frac{\lambda - 2}{6} x^3 + \frac{(\lambda - 2)(\lambda - 12)}{120} x^5 - \cdots } \quad (\text{奇函数})$$

当 $\lambda = n(n+1)$（$n \in \mathbb{N}$）时，偶（$n$ 偶）或奇（$n$ 奇）级数截断为 $n$ 次 Legendre 多项式 $P_n(x)$。

---

## 变形与延伸

> [!info] 变形 1（Rodrigues 公式与正交性）
> Legendre 多项式有简洁的显式表示 $P_n(x) = \frac{1}{2^n n!} \frac{d^n}{dx^n} (x^2 - 1)^n$（Rodrigues 公式）。由此可证正交性 $\int_{-1}^1 P_m(x) P_n(x) dx = \frac{2}{2n+1} \delta_{mn}$。
>
> **提示**：反复分部积分，边界项在 $x = \pm 1$ 处因 $(x^2 - 1)^n$ 的零点而消失。正交性是 [[Sturm-Liouville定理]] 的经典实例。

> [!info] 变形 2（在 $x = 1$ 附近的 Frobenius 展开）
> 讨论 Legendre 方程在奇点 $x = 1$ 处的 Frobenius 级数（指标方程 $r = 0$ 为二重根）。
>
> **提示**：$x = 1$ 是正则奇点（$p, q$ 有简单极点）。作 $t = x - 1$ 平移，第一个解为 $P_n(1 + t)$ 的级数，第二个解含 $\ln t$——即第二类 Legendre 函数 $Q_n$。

> [!info] 延伸（球谐函数与 Laplace 方程的分离变量）
> 连带 Legendre 方程 $(1 - x^2) y'' - 2xy' + \big(\lambda - \frac{m^2}{1 - x^2}\big) y = 0$ 来自球坐标下 Laplace 算子的 $\theta$-向分离。其解为连带 Legendre 函数 $P_\ell^m(\cos\theta)$，与球谐函数 $Y_\ell^m(\theta, \phi)$ 的关系是 `数学物理方法/` 的核心内容。
