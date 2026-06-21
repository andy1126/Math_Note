---
title: Airy 方程的幂级数解
date: 2026-06-20
tags:
  - 题解
  - 微分方程
  - ODE
  - 级数解法
  - Airy方程
  - 幂级数解
  - 特殊函数
---

# Airy 方程的幂级数解

## 题目

> 在常点 $x = 0$ 附近求 **Airy 方程**
> $$y'' - xy = 0$$
> 的幂级数解，并给出两个线性独立解的级数表达式（写出前几项）。

---

## 预备定义与定理

> [!note] Airy 方程
> $$y'' - xy = 0$$
> 是二阶变系数线性齐次方程。写成标准形 $y'' + p(x) y' + q(x) y = 0$，其中 $p(x) \equiv 0$，$q(x) = -x$。二者均在 $\mathbb{R}$ 上解析（实为多项式），故**每一点都是常点**。

> [!note] 标准形与常点
> 对 $y'' + p y' + q y = 0$，称 $x_0$ 为**常点**（ordinary point），若 $p, q$ 在 $x_0$ 附近解析（可展为收敛幂级数）。此时方程的任意解也在 $x_0$ 处解析，收敛半径 $\geq$ 到最近奇点的距离。详见 [[常点附近的幂级数解]]。

> [!abstract] 引理：Fuchs 存在定理（常点情形）
> 在常点处存在两个线性独立的解析解，其幂级数系数由 $a_0 = y(0), a_1 = y'(0)$ 经递推关系唯一确定，且收敛半径 $\geq$ 方程系数到最近奇点的距离。详见 [[常点附近的幂级数解]]。

> [!abstract] 引理：Cauchy 乘积与级数恒等定理
> 两个幂级数的乘积由 Cauchy 乘积公式给出；若一个幂级数在收敛圆内恒为零，则其所有系数为零。这两个事实是代入级数、对齐系数"的代数学依据。

> [!abstract] 定义：Airy 函数
> Airy 方程的两个标准线性独立解记为 $\operatorname{Ai}(x)$ 与 $\operatorname{Bi}(x)$，统称 **Airy 函数**。$\operatorname{Ai}(x)$ 满足 $x \to +\infty$ 时 $\operatorname{Ai}(x) \to 0$；$\operatorname{Bi}(x)$ 是与之独立、在 $x \to +\infty$ 时发散的解。本文求出的级数即 $\operatorname{Ai}$ 与 $\operatorname{Bi}$ 的 Taylor 展式（至常数的线性组合）。

---

## 解答

### 第一步：设幂级数形式

设解为 $x = 0$ 处的幂级数（常点，$x_0 = 0$）：
$$y(x) = \sum_{n=0}^{\infty} a_n x^n = a_0 + a_1 x + a_2 x^2 + a_3 x^3 + \cdots,$$
其中 $a_0 = y(0)$，$a_1 = y'(0)$ 为两个自由参数。

逐项求导：
$$y'(x) = \sum_{n=1}^{\infty} n a_n x^{n-1} = \sum_{n=0}^{\infty} (n+1) a_{n+1} x^n,$$
$$y''(x) = \sum_{n=2}^{\infty} n(n-1) a_n x^{n-2} = \sum_{n=0}^{\infty} (n+2)(n+1) a_{n+2} x^n.$$

### 第二步：代入 Airy 方程

将 $y''$ 与 $-x y$ 代入 $y'' - xy = 0$：
$$y'' - x y = \sum_{n=0}^{\infty} (n+2)(n+1) a_{n+2} x^n \;-\; x \sum_{n=0}^{\infty} a_n x^n = 0.$$

将第二项的指标移位：$x \sum a_n x^n = \sum_{n=0}^{\infty} a_n x^{n+1} = \sum_{m=1}^{\infty} a_{m-1} x^m$。令 $m = n$：
$$\sum_{n=0}^{\infty} (n+2)(n+1) a_{n+2} x^n \;-\; \sum_{n=1}^{\infty} a_{n-1} x^n = 0.$$

### 第三步：对齐 $x^n$ 系数，导出递推

将两个级数写成一个关于 $x^n$ 的统一级数：

- $n = 0$ 项：仅来自第一级数：$(2)(1) a_2 = 2a_2$；
- $n = 1$ 项：$(3)(2) a_3 - a_0 = 6a_3 - a_0$；
- $n \geq 2$ 项：$(n+2)(n+1) a_{n+2} - a_{n-1}$。

由幂级数恒等定理（所有系数为零）：
$$n = 0:\quad 2 a_2 = 0 \;\Longrightarrow\; a_2 = 0. \quad \cdots (1)$$
$$n \geq 1:\quad (n+2)(n+1)\, a_{n+2} = a_{n-1}. \quad \cdots (2)$$

> [!important] 递推的关键特征
> 递推 $(2)$ 把 $a_{n+2}$ 与**三步之前**的系数 $a_{n-1}$ 联系起来（索引差为 $3$）。这意味着指标按**模 $3$ 分为三个独立序列**：$\{a_{3k}\}$、$\{a_{3k+1}\}$、$\{a_{3k+2}\}$。又由 $(1)$ 知 $a_2 = 0$，故**所有 $a_{3k+2} = 0$**。

### 第四步：求解 $\{a_{3k}\}$ 序列（对应 $a_0$）

令 $n = 3k + 1$（即 $n-1 = 3k$）：
$$(3k+3)(3k+2)\, a_{3k+3} = a_{3k}.$$

改写成从 $a_{3k}$ 到 $a_{3(k+1)}$ 的递推：
$$a_{3(k+1)} = \frac{a_{3k}}{(3k+3)(3k+2)}, \qquad k \geq 0.$$

**计算前几项**：
$$a_0 \ (\text{自由}), \quad a_3 = \frac{a_0}{3 \cdot 2} = \frac{a_0}{6}, \quad a_6 = \frac{a_3}{6 \cdot 5} = \frac{a_0}{180}, \quad a_9 = \frac{a_6}{9 \cdot 8} = \frac{a_0}{12960}.$$

**通项**：
$$a_{3k} = \frac{a_0}{(3k)(3k-1)(3k-3)(3k-4)\cdots(3)(2)} = \frac{a_0}{3^{2k}\, k!\, \big(k-\frac{1}{3}\big)\big(k-\frac{4}{3}\big)\cdots\big(\frac{2}{3}\big)},$$
或写作
$$a_{3k} = a_0 \cdot \frac{1}{(3k)(3k-1)(3k-3)(3k-4)\cdots 3 \cdot 2}.$$

取 $a_0 = 1, a_1 = 0$，得第一组解：
$$y_1(x) = 1 + \frac{x^3}{6} + \frac{x^6}{180} + \frac{x^9}{12960} + \cdots$$

### 第五步：求解 $\{a_{3k+1}\}$ 序列（对应 $a_1$）

令 $n = 3k + 2$（即 $n-1 = 3k+1$）：
$$(3k+4)(3k+3)\, a_{3k+4} = a_{3k+1}.$$

即
$$a_{3(k+1)+1} = \frac{a_{3k+1}}{(3k+4)(3k+3)}, \qquad k \geq 0.$$

**计算前几项**：
$$a_1 \ (\text{自由}), \quad a_4 = \frac{a_1}{4 \cdot 3} = \frac{a_1}{12}, \quad a_7 = \frac{a_4}{7 \cdot 6} = \frac{a_1}{504}, \quad a_{10} = \frac{a_7}{10 \cdot 9} = \frac{a_1}{45360}.$$

取 $a_0 = 0, a_1 = 1$，得第二组解：
$$y_2(x) = x + \frac{x^4}{12} + \frac{x^7}{504} + \frac{x^{10}}{45360} + \cdots$$

### 第六步：收敛半径

由 $(2)$ 的递推，当 $n \to \infty$，
$$\frac{|a_{n+2}|}{|a_n|} \sim \frac{1}{(n+2)(n+1)} \to 0,$$

故 $\dfrac{|a_{n+1}|}{|a_n|} \to 0$，收敛半径 $R = \infty$。这与 Fuchs 定理一致：$p \equiv 0, q(x) = -x$ 在 $\mathbb{C}$ 上处处解析（无奇点），故解为**整函数**。

### 第七步：线性独立性与基本解组

$y_1(0) = 1,\ y_1'(0) = 0$；$y_2(0) = 0,\ y_2'(0) = 1$。故
$$W(0) = \det\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} = 1 \neq 0.$$

由 [[Wronskian与Abel公式]] 的线性独立性刻画，$y_1, y_2$ 线性独立，构成 Airy 方程的基本解组。$\blacksquare$

---

## 答案

Airy 方程 $y'' - xy = 0$ 的通解为
$$y = C_1 y_1 + C_2 y_2,$$
其中
$$\boxed{\,y_1(x) = 1 + \frac{x^3}{6} + \frac{x^6}{180} + \frac{x^9}{12960} + \cdots = \sum_{k=0}^{\infty} \frac{x^{3k}}{\prod_{j=1}^{k} (3j)(3j-1)}\,}$$
$$\boxed{\,y_2(x) = x + \frac{x^4}{12} + \frac{x^7}{504} + \frac{x^{10}}{45360} + \cdots = \sum_{k=0}^{\infty} \frac{x^{3k+1}}{\prod_{j=1}^{k} (3j+1)(3j)}\,}$$

（空积定义为 $1$，即 $k=0$ 时 $y_1$ 首项 $1$，$y_2$ 首项 $x$。）

---

## 变形与延伸

> [!info] 变形 1（含参数的 Airy 方程）
> 解 $y'' - \lambda x y = 0$（$\lambda \in \mathbb{R}$），讨论 $\lambda > 0$ 与 $\lambda < 0$ 时解的振荡行为。
>
> **提示**：$\lambda > 0$ 对应标准 Airy 函数；$\lambda < 0$ 时作变量替换 $x \mapsto -x$ 化为标准形。收敛半径仍为 $\infty$，但解的定性行为反转（从振荡 $\to$ 指数增长/衰减）。

> [!info] 变形 2（非零常点展开）
> 在 $x_0 = 1$ 处求 $y'' - xy = 0$ 的幂级数解（前几项）。
>
> **提示**：令 $t = x - 1$，则 $x = 1 + t$，方程化为 $y''(t) - (1 + t) y(t) = 0$。代入 $y = \sum a_n t^n$ 对齐系数。$1$ 项产生非齐次的递推结构（含 $a_n$ 与 $a_{n-1}$ 的耦合）。

> [!info] 延伸 1（Airy 函数的积分表示与渐近行为）
> $\operatorname{Ai}(x)$ 有积分表示 $\displaystyle \operatorname{Ai}(x) = \frac{1}{\pi} \int_0^{\infty} \cos\!\left(\frac{t^3}{3} + xt\right) dt$。讨论 $x \to +\infty$ 时 $\operatorname{Ai}(x)$ 的指数衰减行为与 $x \to -\infty$ 时的振荡行为。
>
> **提示**：Power series 在 $x \to \infty$ 时收敛极慢（虽半径 $\infty$，但截断误差大）；实际计算需用渐近展开或数值 ODE 求解。

> [!info] 延伸 2（Airy 方程在物理中的来源）
> Airy 方程出现于 WKB 近似在转向点（turning point）附近的一致化，以及量子力学中线性势 $V(x) = x$ 的 Schrödinger 方程。讨论 Airy 函数的零点分布（所有零点均在负实轴上）。
>
> **提示**：Airy 零点与 Sturm-Liouville 本征值问题密切相关——详见 [[Sturm-Liouville定理]] 和 [[Sturm比较定理]]。
