---
title: Clairaut 方程与奇解
date: 2026-06-20
tags:
  - 微分方程
  - ODE
  - 初等解法
  - Clairaut方程
  - 奇解
  - 包络
---

# Clairaut 方程与奇解

## 预备定义

> [!note] Clairaut 方程
> 形如
> $$y = x\, y' + f(y'), \quad \cdots (\mathrm{C})$$
> 的一阶 ODE 称为 **Clairaut 方程**，其中 $f \in C^2$。它是 Lagrange 方程 $y = x g(y') + f(y')$ 在 $g(p) = p$ 时的特殊情况，即"从切线方程出发构造的 ODE"。

> [!note] 奇解（singular solution）
> 称 ODE 的一个解为**奇解**，若在其图像上的每一点，初值问题的唯一性均失效——即过该点至少还有另一个不同的解。奇解的几何本质是**解族的包络**（envelope）。Clairaut 方程是产生奇解的最简单机制。

> [!note] 包络（envelope）
> 设 $\Phi(x, y, C) = 0$ 为一族曲线（通解）。该族的**包络**为一条曲线，它在每一点与族中某条曲线相切，且本身不由族中任一条曲线整体给出。包络由
> $$\begin{cases} \Phi(x, y, C) = 0, \\ \frac{\partial \Phi}{\partial C}(x, y, C) = 0 \end{cases}$$
> 消去 $C$ 得到（此即 $C$-判别式，$C$-discriminant）。

> [!abstract] 引理：Picard-Lindelöf 唯一性定理
> 若 $F(x, y)$ 关于 $y$ 局部 Lipschitz，则初值问题局部唯一。奇解只能出现在 Lipschitz 条件失效的曲线上。详见 [[Picard-Lindelöf定理]]。

---

## 定理

设 $f \in C^2$ 且 $f'' \not\equiv 0$。考虑 Clairaut 方程
$$y = x\, y' + f(y'). \quad \cdots (\mathrm{C})$$

**(i)（通解族——直线族）** 对任意 $C \in \mathbb{R}$，
$$y = C x + f(C) \quad \cdots (\ast)$$
是 (C) 的解。这些解是一族**直线**（斜率为 $C$，截距为 $f(C)$）。

**(ii)（奇解——包络）** 从通解族 $(\ast)$ 和 $C$-判别式
$$\begin{cases} y = C x + f(C), \\ 0 = x + f'(C) \end{cases}$$
消去 $C$ 得到的曲线是 (C) 的**奇解**，它是通解直线族的**包络**。该奇解在参数形式下为
$$\begin{cases} x = -f'(p), \\ y = -p f'(p) + f(p), \end{cases} \quad p = y'.$$

**(iii)（解的结构）** (C) 的完整解集 = 直线族 $y = C x + f(C)$ + 奇解（包络曲线）。初值落在奇解上的点处唯一性失效：过该点既有奇解，又有以该点为切点的某条直线解。

---

## 证明

### 第(i)部分：直线族是解

将 $y = Cx + f(C)$ 代入 (C)。左端 $y = Cx + f(C)$；右端 $x y' + f(y') = x \cdot C + f(C) = Cx + f(C)$。两端恒等。$\square$

### 第(ii)部分：奇解作为包络

#### 推导

引入参数 $p := y'$。将 (C) 对 $x$ 求导：
$$y' = (x y')' + f'(y') \cdot y'' \;\Longrightarrow\; p = p + x p' + f'(p) p' \;\Longrightarrow\; p'\,(x + f'(p)) = 0.$$

> [!important] 因子分解给出两条路
> 乘积 $p'\,(x + f'(p)) = 0$ 意味着在每一点处，要么 $p' = 0$，要么 $x + f'(p) = 0$。

**(a) $p' = 0$**：即 $y' = p = C$ 为常数，代入原方程 $y = x C + f(C)$——这正是通解直线族。

**(b) $x + f'(p) = 0$**：从中解得 $x = -f'(p)$。代入原方程：
$$y = (-f'(p)) \cdot p + f(p) = -p f'(p) + f(p).$$

$p$ 作为参数跑遍，$(x(p), y(p))$ 描出一条曲线——这就是奇解。它是直线族 $y = Cx + f(C)$ 的**包络**。

#### 包络验证

直线族 $\Phi(x, y, C) := y - Cx - f(C) = 0$。$C$-判别式：
$$\frac{\partial \Phi}{\partial C} = -x - f'(C) = 0 \;\Longrightarrow\; x = -f'(C).$$

代入 $\Phi = 0$ 得 $y = C(-f'(C)) + f(C)$。这正是参数形式 $($ 以 $C = p)$。由包络理论，该曲线在每一点与族中某直线相切（切点处的 $C$ 即该直线的参数）。故它是奇解。$\square$

### 第(iii)部分：唯一性失效的几何解释

在奇解上任取一点 $(x_0, y_0)$。该点同时在奇解和以 $C = p_0$（该点处的 $y'$ 值）为参数的直线解上，且二者在该点相切（一阶导数相同）。由 Cauchy 问题局部解的唯一性，该点处至少有两个不同的解——故唯一性失效。

> [!important] 奇解处 Lipschitz 条件恰好失效
> 将 (C) 写成 $y' = F(x, y)$ 的形式需要从 $y = xy' + f(y')$ 中解出 $y'$。在包络上的点处，$\frac{\partial}{\partial p}(xp + f(p)) = x + f'(p) = 0$，隐函数定理失效——$y'$ 不能被表为 $(x, y)$ 的单值函数。这恰好是 Lipschitz 条件（甚至连续性）失效的位置——与 [[Picard-Lindelöf定理]] 的警告完全吻合。$\blacksquare$

---

## 例：$y = xy' - \frac{1}{4}(y')^2$

$f(p) = -\frac{1}{4} p^2$，$f'(p) = -\frac{1}{2} p$，$f''(p) = -\frac{1}{2} \neq 0$。

- **通解**：$y = Cx - \frac{C^2}{4}$（直线族）。
- **奇解**：$x = -f'(p) = p/2$，$y = -p(p/2) - p^2/4 = p^2/4$。消去 $p = 2x$ 得 $y = x^2$。

直线族 $y = Cx - C^2/4$ 的每一条都是抛物线 $y = x^2$ 的切线（在 $x = C/2$ 处相切）。抛物线是整族直线的包络——从下方包围。初值在抛物线上时，过该点既有抛物线解又有切线解，唯一性失效。

---

## 证明思路总结

> [!tip] 关键思想
> Clairaut 方程的求解利用了**对 $x$ 求导后自动分解为乘积**的结构：
> $$p'\,(x + f'(p)) = 0.$$
> - $p' = 0$ → 通解直线族（$y'$ 为常数）；
> - $x + f'(p) = 0$ → 奇解（包络）。
>
> 几何本质：Clairaut 方程是**"从切线方程反推曲线"**的方程。直线族的每条线是某点处切线的自然延拓；奇解是所有这些切线的"切点轨迹"——即包络。

> [!warning] 与分离变量丢失解的对比
> [[可分离变量方程]] 中丢失常数解是因为"除以 $g(y)$"；Clairaut 中奇解出现在隐函数定理失效处。两种"丢失解"的机制不同，但最终都指向 [[Picard-Lindelöf定理]] 的 Lipschitz 条件的必要性。

> [!info] Clairaut $\subset$ Lagrange
> Lagrange 方程 $y = x g(y') + f(y')$ 包含 Clairaut（$g(p) = p$）作为特例。Lagrange 方程的通法同样是对 $x$ 求导，得到关于 $p$ 与 $x$ 的一阶方程——通常可用一阶线性方程或积分因子处理，但一般情况下不保证有奇解。
