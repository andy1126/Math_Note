---
title: 齐次方程、Bernoulli 方程与 Riccati 方程
date: 2026-06-20
tags:
  - 微分方程
  - ODE
  - 初等解法
  - 变量代换
  - Bernoulli方程
  - Riccati方程
  - 齐次方程
---

# 齐次方程、Bernoulli 方程与 Riccati 方程

## 预备定义

> [!note] 齐次方程（homogeneous equation）
> 形如
> $$\frac{dy}{dx} = f\!\left(\frac{y}{x}\right) \quad \cdots (\mathrm{Hom})$$
> 的一阶 ODE 称为**齐次方程**（亦有"零次齐次"之名），其中 $f: \mathbb{R} \to \mathbb{R}$ 连续。其等价微分形式
> $$M(x, y)\,dx + N(x, y)\,dy = 0$$
> 中的 $M, N$ 为同次齐次函数（即 $M(tx, ty) = t^k M(x, y)$ 且 $N(tx, ty) = t^k N(x, y)$，约分后即化为 $y' = f(y/x)$ 的形式）。

> [!note] Bernoulli 方程
> 形如
> $$\frac{dy}{dx} + P(x)\, y = Q(x)\, y^n, \quad n \in \mathbb{R} \quad \cdots (\mathrm{B})$$
> 的一阶 ODE 称为 **Bernoulli 方程**，其中 $P, Q$ 在开区间 $I$ 上连续。
> - $n = 0$：退化为一阶线性方程；
> - $n = 1$：退化为齐次线性方程 $y' + (P - Q) y = 0$；
> - $n \neq 0, 1$：非线性，但可通过变量代换**线性化**。

> [!note] Riccati 方程
> 形如
> $$\frac{dy}{dx} = P(x) + Q(x)\, y + R(x)\, y^2, \quad R \not\equiv 0 \quad \cdots (\mathrm{R})$$
> 的一阶 ODE 称为 **Riccati 方程**，其中 $P, Q, R$ 在 $I$ 上连续。这是仅有的**二次非线性**一阶方程，无法通过初等代换直接积出；但若**已知一个特解**，则可降阶为 Bernoulli / 线性方程。

> [!abstract] 引理：Picard-Lindelöf 存在唯一性
> 若方程右端 $F(x, y)$ 连续且关于 $y$ 局部 Lipschitz，则初值问题局部存在唯一解。详见 [[Picard-Lindelöf定理]]。本文所有代换在 Lipschitz 保持之下均合法。

> [!abstract] 引理：一阶线性方程的通解公式
> $y' + P y = Q$ 的通解为
> $$y = e^{-\int P\,dx}\left(\int e^{\int P\,dx} Q\,dx + C\right).$$
> 详见 [[一阶线性方程与积分因子]]。

---

## 定理

### 定理 1：齐次方程的解法

设 $f$ 连续。考虑
$$\frac{dy}{dx} = f\!\left(\frac{y}{x}\right), \quad x > 0\ (\text{或 } x < 0). \quad \cdots (\mathrm{Hom})$$

作代换 $v = \dfrac{y}{x}$（即 $y = xv$），则 (Hom) 化为可分离变量方程
$$\frac{dv}{dx} = \frac{f(v) - v}{x}. \quad \cdots (\mathrm{Hom}^*)$$

进而：
- 若 $f(v) - v \neq 0$，分离变量 $\displaystyle \int \frac{dv}{f(v) - v} = \int \frac{dx}{x} + C = \ln|x| + C$；
- 若存在 $v_0$ 使 $f(v_0) = v_0$，则 $y = v_0 x$ 是 (Hom) 的**直线解**。

### 定理 2：Bernoulli 方程的线性化

设 $P, Q$ 在 $I$ 上连续，$n \neq 0, 1$。考虑
$$y' + P(x)\, y = Q(x)\, y^n. \quad \cdots (\mathrm{B})$$

作代换 $v = y^{1-n}$，则 (B) 等价于**一阶线性方程**
$$v' + (1 - n) P(x)\, v = (1 - n) Q(x). \quad \cdots (\mathrm{B}^*)$$

> [!warning] 常数解 $y \equiv 0$
> 若 $n > 0$，$y \equiv 0$ 是 (B) 的解（称为零解或平凡解），但代换 $v = y^{1-n}$ 在此处奇异（$1 - n < 0$ 时分母为零）。$y \equiv 0$ 必须**单独列出**，不被线性化公式涵盖。

### 定理 3：Riccati 方程的降阶（已知一特解）

设 $P, Q, R$ 在 $I$ 上连续，$R \not\equiv 0$。考虑
$$y' = P(x) + Q(x)\, y + R(x)\, y^2. \quad \cdots (\mathrm{R})$$

若已知一个特解 $y_1(x)$，则作代换
$$y = y_1 + \frac{1}{u} \quad (\text{或等价地 } u = \frac{1}{y - y_1}),$$

(R) 化为关于 $u$ 的**一阶线性方程**
$$u' + \big(Q(x) + 2R(x) y_1(x)\big)\, u = -R(x). \quad \cdots (\mathrm{R}^*)$$

更一般地，Riccati 方程可通过代换 $y = -\dfrac{1}{R}\dfrac{w'}{w}$ 化为一个**二阶线性齐次方程**
$$R w'' - (R' + QR) w' + PR^2 w = 0.$$

---

## 定理 1 的证明：齐次方程

### 第一步：代换 $v = y/x$

设 $y = \varphi(x)$ 为 (Hom) 在 $x > 0$ 上的解。令 $v(x) := \dfrac{\varphi(x)}{x}$，则 $\varphi(x) = x v(x)$。求导：
$$\varphi'(x) = v(x) + x v'(x).$$

### 第二步：代入原方程

将 $\varphi'(x) = f(\varphi(x)/x) = f(v(x))$ 代入上式：
$$v + x v' = f(v) \;\Longrightarrow\; x v' = f(v) - v.$$

因 $x > 0$（或 $x < 0$ 时类似），两端除以 $x$ 得
$$v' = \frac{f(v) - v}{x}. \quad \square$$

这是标准的可分离变量方程（见 [[可分离变量方程]]），积分后回代 $v = y/x$ 即得通解。

### 第三步：直线解

若 $f(v_0) = v_0$，则 $v(x) \equiv v_0$ 满足 $v' = 0 = (f(v_0) - v_0)/x$，故 $y = v_0 x$ 是解。$\square$

> [!info] 为何称为"齐次"
> 方程 $M\,dx + N\,dy = 0$ 中 $M, N$ 为同次齐次函数的条件，等价于方向场的斜率只依赖于 $y/x$ 的比值——这是"尺度不变性"（缩放 $x, y$ 等倍，斜率不变）。代换 $v = y/x$ 消去此不变性，化为可分离变量。

---

## 定理 2 的证明：Bernoulli 方程的线性化

### 第一步：构造代换

设 $y > 0$（$y < 0$ 类似，注意 $y^n$ 和 $y^{1-n}$ 的定义）。令
$$v = y^{1-n}.$$

求导（链式法则）：
$$v' = (1 - n)\, y^{-n}\, y'.$$

### 第二步：用 $v$ 和 $v'$ 表达原方程

由 $y^{-n} = \dfrac{v'}{(1 - n) y'}$，但更方便的做法是将 (B) 两边同乘 $(1 - n) y^{-n}$：
$$(1 - n) y^{-n} y' + (1 - n) P(x)\, y^{1-n} = (1 - n) Q(x).$$

左端第一项恰为 $v'$，第二项为 $(1 - n) P(x)\, v$。故得
$$v' + (1 - n) P(x)\, v = (1 - n) Q(x). \quad \square$$

这就是标准的一阶线性方程，积分因子 $\mu = e^{(1-n)\int P\,dx}$ 可直接套用 [[一阶线性方程与积分因子]] 的通解公式求解。最后回代 $y = v^{\,1/(1-n)}$ 得原方程的解。

### 第三步：$n > 0$ 时的零解

若 $n > 0$，直接代入 $y \equiv 0$：左端 $0' + P \cdot 0 = 0$，右端 $Q \cdot 0^n = 0$（$n > 0$）。故 $y \equiv 0$ 为解。代换 $v = y^{1-n}$ 在此奇异，需单独登记。$\blacksquare$

---

## 定理 3 的证明：Riccati 方程的降阶

### 第一步：特解平移 + 倒数代换

设 $y_1$ 为 (R) 的一个特解。令
$$y = y_1 + \frac{1}{u}, \quad (u \neq 0).$$

求导：$y' = y_1' - \dfrac{u'}{u^2}$。代入 (R)：
$$y_1' - \frac{u'}{u^2} = P + Q \left(y_1 + \frac{1}{u}\right) + R \left(y_1 + \frac{1}{u}\right)^2.$$

### 第二步：消去非线性项

展开右端：
$$P + Q y_1 + \frac{Q}{u} + R y_1^2 + \frac{2R y_1}{u} + \frac{R}{u^2}.$$

注意到 $y_1$ 是特解，故 $y_1' = P + Q y_1 + R y_1^2$。将这些项从两端消去，剩下：
$$-\frac{u'}{u^2} = \frac{Q}{u} + \frac{2R y_1}{u} + \frac{R}{u^2}.$$

两端同乘 $-u^2$：
$$u' = -\big(Q + 2R y_1\big) u - R.$$

即
$$u' + \big(Q + 2R y_1\big) u = -R. \quad \square$$

这是一阶线性方程，求解 $u$ 后回代 $y = y_1 + 1/u$ 即得 (R) 的通解。

> [!important] 特解的重要性的几何解释
> Riccati 方程是射影 Riccati 流在仿射坐标下的局部形式。已知一个特解相当于知道相平面上一条积分曲线；Riccati 方程的解集在 Möbius 变换 $y \mapsto \dfrac{ay + b}{cy + d}$ 下封闭。代换 $y = y_1 + 1/u$ 正是把 $y_1$ 处的"无穷远"变为 $u$ 的零点，从而消灭二次项。

### 第三步：化为二阶线性方程

作代换 $y = -\dfrac{1}{R}\dfrac{w'}{w}$。则 $y' = -\dfrac{1}{R}\dfrac{w''}{w} + \dfrac{1}{R}\dfrac{(w')^2}{w^2} + \dfrac{R'}{R^2}\dfrac{w'}{w}$。代入 (R) 并整理，二次项 $y^2$ 中的 $(w')^2 / w^2$ 恰好与 $y'$ 中的同项抵消，得到关于 $w$ 的二阶线性方程：
$$R w'' - (R' + QR) w' + PR^2 w = 0.$$

这建立了 **Riccati 方程 ⇔ 二阶线性齐次方程** 的基本对应，是 [[Sturm-Liouville定理]] 与量子力学中 Schrödinger 方程的 Riccati 形式的理论基础。$\blacksquare$

---

## 一般解法（算法流程）

### 齐次方程求解步骤

1. **识别**：将 $y'$ 表为 $f(y/x)$ 或识别 $M, N$ 为同次齐次函数；
2. **代换**：令 $v = y/x$（即 $y = xv$，$y' = v + xv'$）；
3. **分离变量**：化方程为 $x v' = f(v) - v$，分离 $\dfrac{dv}{f(v) - v} = \dfrac{dx}{x}$；
4. **积分 + 回代**：积分得隐式 $G(v) = \ln|x| + C$，将 $v = y/x$ 代回；
5. **检查直线解**：若 $f(v_0) = v_0$，补上 $y = v_0 x$。

### Bernoulli 方程求解步骤

1. **识别**：确认方程为 $y' + P y = Q y^n$ 形式，确定 $n$；
2. **检查退化**：$n = 0$ 直接用一阶线性公式；$n = 1$ 为齐次线性；
3. **检查零解**：若 $n > 0$，登记 $y \equiv 0$ 为解；
4. **代换**：令 $v = y^{1-n}$，得线性方程 $v' + (1-n)P v = (1-n)Q$；
5. **解线性方程**：用积分因子法求 $v$；
6. **回代**：$y = v^{\,1/(1-n)}$。

### Riccati 方程求解步骤

1. **获取特解**：若未给出，需通过对称性 / 观察 / 待定系数法猜出一个特解 $y_1$；
2. **代换**：令 $y = y_1 + 1/u$；
3. **解线性方程**：$u' + (Q + 2R y_1) u = -R$；
4. **回代**：$y = y_1 + 1/u$，得到通解。

---

## 证明思路总结

> [!tip] 关键思想
> 三种方法的共同本质是**巧妙的因变量代换将非线性方程线性化**：
> 1. **齐次方程**：利用尺度不变性，$v = y/x$ 消去分子分母的同次性，化为可分离变量；
> 2. **Bernoulli 方程**：$v = y^{1-n}$ 利用了非线性项 $y^n$ 与线性项 $y$ 的幂次关系——求导后 $v'$ 含 $y^{-n}y'$，恰好与方程各项对齐，消去非线性；
> 3. **Riccati 方程**：$y = y_1 + 1/u$ 将二次项在平移后"吸收"到线性项中——其深层理由来自 Möbius 变换的群作用：Riccati 流在 $\mathrm{SL}(2, \mathbb{R})$ 作用下封闭，而 $y \mapsto 1/y$ 是其生成元之一。
>
> 三者递进：齐次 $\to$ 可分离；Bernoulli $\to$ 线性；Riccati $\to$ 二次非线性（需一特解）。

> [!info] 方法合法性与存在唯一性的联系
> - 所有代换都在解曲线满足 "$v$ 定义良好" 的区域上合法；
> - 若代换后的方程满足 [[Picard-Lindelöf定理]] 的条件（连续性 + Lipschitz），则其解唯一，再经逆代换得到原方程的唯一解；
> - Riccati 方程右端 $C^1$（甚至解析）故自动满足局部 Lipschitz，解存在唯一；但仅用初等积分法**无法从零解出通解**（必须"偷"一个特解）。

> [!warning] 代换的奇异点处理
> Bernoulli（$n > 0$）的零解 $y \equiv 0$ 以及齐次方程可能的直线解 $y = v_0 x$，都对应代换后方程中"分母为零"的点。这些**退化解**必须在代换前单独登记，否则被整个流程丢失。处理方式见 [[可分离变量方程]] 中关于"分离变量丢失的解"的讨论。

> [!info] Riccati 方程与二阶线性方程的联系
> Riccati 方程 $y' = P + Qy + Ry^2$ 经 $y = -\frac{1}{R}\frac{w'}{w}$ 变为二阶线性方程。这一联系是 [[Sturm-Liouville定理]] 中 Prüfer 变换 $y = \tan\theta$（本质上也是 Riccati 型）和量子力学 WKB 近似的数学源头。详见 [[正则奇点与Frobenius方法]]（从奇点分类角度审视同一变换）。
