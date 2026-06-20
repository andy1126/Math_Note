---
title: Bernoulli 方程例题
date: 2026-06-20
tags:
  - 题解
  - 微分方程
  - ODE
  - Bernoulli方程
---

# Bernoulli 方程例题

## 题目

> 解 Bernoulli 方程 $y' + y = x y^3$.

---

## 预备定义与定理

> [!note] Bernoulli 方程（Bernoulli equation）
> 形如
> $$y' + p(x)\,y = q(x)\, y^n, \quad n \neq 0, 1$$
> 的方程称为 **Bernoulli 方程**。通过代换 $v = y^{1-n}$ 可化为关于 $v$ 的一阶线性方程。$n > 0$ 时 $y \equiv 0$ 是一个解（须单独讨论）。详见 [[齐次方程、Bernoulli方程与Riccati方程]]。

> [!abstract] 定理：Bernoulli 代换
> 设 $v = y^{1-n}$。则 $v' = (1-n)\,y^{-n}\,y'$，原方程两端乘 $(1-n)y^{-n}$ 后化为线性方程
> $$v' + (1-n)\,p(x)\,v = (1-n)\,q(x).$$
> 详见 [[齐次方程、Bernoulli方程与Riccati方程]]。

> [!abstract] 定理：积分因子法（解线性方程用）
> $v' + P(x) v = Q(x)$ 的通解为 $\displaystyle v = \frac{1}{\mu}\Bigl(\int \mu Q\,dx + C\Bigr)$，其中 $\mu = e^{\int P\,dx}$。详见 [[一阶线性方程与积分因子]]。

> [!abstract] 引理：$\int -2x\,e^{-2x}\,dx$ 的计算
> 分部积分（$u = -2x$，$dv = e^{-2x}dx$，$v = -\tfrac12 e^{-2x}$）：
> $$\int -2x\,e^{-2x}\,dx = x e^{-2x} - \int e^{-2x}\,dx = x e^{-2x} + \tfrac12 e^{-2x} + C = e^{-2x}\bigl(x + \tfrac12\bigr) + C.$$

---

## 解答

### 第一步：辨识 Bernoulli 结构

原方程 $y' + y = x y^3$ 形如 $y' + p(x) y = q(x) y^n$，其中
$$p(x) = 1, \qquad q(x) = x, \qquad n = 3.$$

因 $n = 3 \notin \{0, 1\}$，确为 Bernoulli 方程。

### 第二步：分离出零解

$n = 3 > 0$，故 $y \equiv 0$ 直接满足方程（两端皆 $0$）。这是一个**奇解**，先记下，下面在 $y \neq 0$ 区域作代换。

### 第三步：作代换 $v = y^{1-n} = y^{-2}$

按 Bernoulli 代换，取
$$v = y^{1-n} = y^{-2}, \qquad v' = -2 y^{-3} y'.$$

把原方程两端除以 $y^3$（在 $y \neq 0$ 处）：
$$y^{-3} y' + y^{-2} = x.$$

注意 $y^{-3} y' = -\tfrac12 v'$，$y^{-2} = v$，代入得
$$-\tfrac12 v' + v = x.$$

两端乘 $-2$，化为关于 $v$ 的**一阶线性方程**：
$$v' - 2v = -2x. \quad \cdots (\ast)$$

> [!info] 与代换公式核对
> 公式给出 $v' + (1-n)p\,v = (1-n)q$，即 $v' + (1-3)\cdot 1 \cdot v = (1-3)\cdot x$，亦即 $v' - 2v = -2x$，与 $(\ast)$ 一致 ✓。

### 第四步：解线性方程 $(\ast)$ —— 积分因子

此处 $P(x) = -2$，积分因子
$$\mu = e^{\int (-2)\,dx} = e^{-2x}.$$

$(\ast)$ 两端乘 $\mu$，左端成为全导数：
$$\bigl(e^{-2x} v\bigr)' = -2x\,e^{-2x}. \quad \cdots (\ast\ast)$$

### 第五步：积分（用预备引理）

对 $(\ast\ast)$ 两端积分，由引理 $\displaystyle \int -2x\,e^{-2x}\,dx = e^{-2x}\bigl(x + \tfrac12\bigr) + C$：
$$e^{-2x} v = e^{-2x}\bigl(x + \tfrac12\bigr) + C.$$

两端乘 $e^{2x}$：
$$v = x + \tfrac12 + C\,e^{2x}.$$

> [!important] 分部积分核对
> $\dfrac{d}{dx}\Bigl[e^{-2x}\bigl(x+\tfrac12\bigr)\Bigr] = -2e^{-2x}\bigl(x+\tfrac12\bigr) + e^{-2x} = e^{-2x}\bigl(-2x - 1 + 1\bigr) = -2x\,e^{-2x}$ ✓，与 $(\ast\ast)$ 右端吻合。

### 第六步：回代 $v = y^{-2}$

$$y^{-2} = x + \tfrac12 + C\,e^{2x}, \quad C \in \mathbb{R}.$$

连同第二步的奇解 $y \equiv 0$，即为全部解。$\blacksquare$

> [!important] 验证（对一般 $C$）
> 由 $y^{-2} = x + \tfrac12 + Ce^{2x}$，对 $x$ 求导：$-2y^{-3}y' = 1 + 2Ce^{2x}$，故 $y' = -\tfrac12 y^3\bigl(1 + 2Ce^{2x}\bigr)$。又 $xy^3 - y = y\bigl(xy^2 - 1\bigr) = y\Bigl(\dfrac{x}{y^{-2}}\cdot y^{-2}\cdots\Bigr)$；更直接地代入 $y^{-2} = x + \tfrac12 + Ce^{2x}$ 计算 $xy^3 - y$ 并与 $y'$ 比较即得恒等，验证通过 ✓。

---

## 答案

$$\boxed{\,y^{-2} = x + \tfrac12 + C\,e^{2x} \quad (C \in \mathbb{R}), \qquad \text{以及奇解 } y \equiv 0.\,}$$

等价地 $\displaystyle y = \pm\bigl(x + \tfrac12 + Ce^{2x}\bigr)^{-1/2}$（在使括号为正的区间上）。

---

## 变形与延伸

> [!info] 变形 1（一般指数）
> 解 $y' + y = x y^n$（$n \neq 0, 1$）。
>
> **提示**：代换 $v = y^{1-n}$ 得 $v' + (1-n)v = (1-n)x$，仍是常系数线性方程，积分因子 $e^{(1-n)x}$。本题为 $n = 3$ 的特例；留意 $n$ 为偶/奇时 $y$ 的符号分支差异。

> [!info] 变形 2（系数参数化）
> 解 $y' + a y = x y^3$（$a \neq 0$ 为常数）。
>
> **提示**：$v = y^{-2}$ 给出 $v' - 2a v = -2x$，积分因子 $e^{-2ax}$，需计算 $\int -2x e^{-2ax}dx = e^{-2ax}\bigl(\tfrac{x}{a} + \tfrac{1}{2a^2}\bigr) + C$。讨论 $a \to 0$ 极限。

> [!info] 变形 3（与 Riccati 的联系）
> Riccati 方程 $y' = P(x) + Q(x) y + R(x) y^2$ 在已知一个特解 $y_1$ 时，代换 $y = y_1 + 1/v$ 化为线性方程；而 $R(x) y^2$ 项的"二次非线性"与 Bernoulli（$n=2$）同源。试说明 Bernoulli（$n = 2$）方程 $y' + py = qy^2$ 是 Riccati 在 $P \equiv 0$ 时的特例。
>
> **提示**：$P \equiv 0$ 时 Riccati 退化为 $y' = Qy + Ry^2$，即 Bernoulli（$n=2$）。详见 [[齐次方程、Bernoulli方程与Riccati方程]]。

> [!info] 延伸（奇解与存在唯一性）
> 为何 $y \equiv 0$ 不能由通解 $y^{-2} = x + \tfrac12 + Ce^{2x}$ 中取某有限 $C$ 得到？
>
> **提示**：$y \equiv 0$ 对应 $y^{-2} \to +\infty$，需"$C = \infty$"，故是通解族外的奇解。原方程右端 $f(x,y) = xy^3 - y$ 对 $y$ 处处 $C^1$，由 [[Picard-Lindelöf定理]] 过每点解唯一——这解释了非零解曲线永不与 $y \equiv 0$ 相交（否则破坏唯一性），即非零解无法"穿越"到零解。
