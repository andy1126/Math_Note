---
title: Gronwall 不等式（积分形式与微分形式）
date: 2026-05-28
tags:
  - 微分方程
  - ODE
  - Gronwall不等式
  - 不等式
  - 稳定性
---

# Gronwall 不等式（积分形式与微分形式）

## 预备定义

> [!note] 连续函数与积分
> 本节中 $u, \alpha, \beta: [a, b] \to \mathbb{R}$ 均为连续函数。所有积分均为 Riemann 积分（或等价 Lebesgue 积分）。

> [!abstract] 引理：积分号下求导
> 设 $\Phi(t) = \int_a^t \beta(s) u(s)\,ds$，其中 $\beta, u$ 连续。则 $\Phi \in C^1[a, b]$，
> $$\Phi'(t) = \beta(t) u(t).$$
> 这是 Lebesgue 微分定理或 Newton-Leibniz 公式的直接推论。

> [!abstract] 引理：一阶线性 ODE 的积分因子法
> 考虑 $y'(t) = \beta(t)\, y(t) + f(t)$。乘以积分因子 $e^{-\int_a^t \beta(s)\,ds}$ 化为
> $$\frac{d}{dt}\!\left[e^{-\int_a^t \beta} \cdot y(t)\right] = e^{-\int_a^t \beta} \cdot f(t).$$
> 从 $a$ 积分到 $t$ 即解出 $y(t)$。

---

## 定理

### 积分形式（标准 Gronwall）

设 $u, \beta: [a, b] \to \mathbb{R}$ 连续，$\beta \geq 0$，$\alpha \in \mathbb{R}$。若

$$u(t) \leq \alpha + \int_a^t \beta(s)\, u(s)\,ds, \quad \forall\, t \in [a, b], \quad \cdots (\mathrm{IG})$$

则

$$u(t) \leq \alpha \cdot \exp\!\left(\int_a^t \beta(s)\,ds\right), \quad \forall\, t \in [a, b].$$

### 微分形式

设 $v \in C^1[a, b]$ 满足 $v'(t) \leq \beta(t)\, v(t)$（$\beta$ 连续）。则

$$v(t) \leq v(a) \cdot \exp\!\left(\int_a^t \beta(s)\,ds\right), \quad \forall\, t \in [a, b].$$

**推广（$\alpha$ 为可变函数）**：若 $\alpha: [a, b] \to \mathbb{R}$ 连续且 $u(t) \leq \alpha(t) + \int_a^t \beta(s) u(s)\,ds$，则

$$u(t) \leq \alpha(t) + \int_a^t \alpha(s)\beta(s)\exp\!\left(\int_s^t \beta(r)\,dr\right) ds.$$

---

## 第(i)部分的证明：积分形式

### 第一步：构造辅助函数

令
$$\Phi(t) := \int_a^t \beta(s)\, u(s)\,ds.$$

由 $\beta, u$ 连续，$\Phi \in C^1[a, b]$ 且 $\Phi(a) = 0$，$\Phi'(t) = \beta(t)\, u(t)$。

### 第二步：将假设 $(\mathrm{IG})$ 翻译为微分不等式

由 $(\mathrm{IG})$，$u(t) \leq \alpha + \Phi(t)$。乘以 $\beta(t) \geq 0$（**此处用到 $\beta \geq 0$**）：
$$\beta(t)\, u(t) \leq \beta(t) (\alpha + \Phi(t)),$$

即
$$\Phi'(t) \leq \beta(t)\, \Phi(t) + \alpha\, \beta(t). \quad \cdots (\ast)$$

### 第三步：积分因子法

> [!important] 积分因子的作用
> $(\ast)$ 形如 $\Phi' - \beta\Phi \leq \alpha\beta$。乘以积分因子 $\mu(t) = \exp\!\left(-\int_a^t \beta\right)$（恒正），左端化为全导数：
> $$\frac{d}{dt}[\mu(t)\, \Phi(t)] = \mu(t)(\Phi'(t) - \beta(t)\Phi(t)) \leq \mu(t) \cdot \alpha\, \beta(t).$$

### 第四步：从 $a$ 积分到 $t$

由 $\Phi(a) = 0$，$\mu(a) = 1$：
$$\mu(t)\, \Phi(t) \leq \alpha \int_a^t \mu(s)\, \beta(s)\,ds. \quad \cdots (\sharp)$$

> [!info] 处理右端积分
> 注意 $\dfrac{d}{ds}\mu(s) = -\beta(s)\mu(s)$，故 $\mu(s)\beta(s) = -\dfrac{d}{ds}\mu(s)$，从而
> $$\int_a^t \mu(s)\beta(s)\,ds = -[\mu(s)]_a^t = 1 - \mu(t).$$

代入 $(\sharp)$：
$$\mu(t)\, \Phi(t) \leq \alpha\, (1 - \mu(t)),$$

即
$$\Phi(t) \leq \alpha\, (\mu(t)^{-1} - 1) = \alpha\,\left(\exp\!\int_a^t \beta - 1\right). \quad \cdots (\flat)$$

### 第五步：回代回 $u$

由 $(\mathrm{IG})$：
$$u(t) \leq \alpha + \Phi(t) \leq \alpha + \alpha\!\left(\exp\!\int_a^t \beta - 1\right) = \alpha\, \exp\!\int_a^t \beta(s)\,ds. \quad \square$$

---

## 第(ii)部分的证明：微分形式

设 $v'(t) \leq \beta(t)\, v(t)$。

直接用积分因子。令 $w(t) = v(t)\,\mu(t)$，$\mu(t) = \exp\!\left(-\int_a^t \beta\right)$。

$$w'(t) = v'(t)\mu(t) + v(t)\mu'(t) = \mu(t)\left[v'(t) - \beta(t)v(t)\right] \leq 0.$$

故 $w$ 在 $[a, b]$ 上非增：$w(t) \leq w(a) = v(a)$。即
$$v(t)\,\mu(t) \leq v(a) \Longrightarrow v(t) \leq v(a)\, \exp\!\int_a^t \beta(s)\,ds. \quad \blacksquare$$

---

## 证明思路总结

> [!tip] 关键思想
> Gronwall 不等式的本质是**把积分不等式 (IG) 转译成微分不等式**，再用经典的积分因子法求解。
>
> 翻译的关键步骤：
> 1. 定义 $\Phi(t) = \int_a^t \beta u$，则 (IG) 改写为 $u \leq \alpha + \Phi$；
> 2. 乘 $\beta \geq 0$ 得 $\Phi' = \beta u \leq \beta(\alpha + \Phi)$，即 $\Phi' - \beta\Phi \leq \alpha\beta$；
> 3. 积分因子 $e^{-\int\beta}$ 将左端化为全导数，从 $a$ 积分即得显式上界。
>
> **核心比喻**：(IG) 是"u 被自己的过往值积分回打压制"；Gronwall 告诉我们这种"自反馈不等式"的指数上界仍由 $\beta$ 的累积决定。

> [!warning] $\beta \geq 0$ 不可省
> 第二步乘 $\beta(t)$ 时，若 $\beta(t) < 0$，则不等式方向反转，整个证明失效。$\beta$ 取负值时需要 $\beta \to |\beta|$ 等变体形式。

> [!info] 在 ODE 中的标准应用
> **应用 1（解的唯一性）**：设 $y_1, y_2$ 均满足 $y' = f(t, y)$，$f$ Lipschitz 常数为 $L$。则
> $$|y_1(t) - y_2(t)| \leq |y_1(a) - y_2(a)| + L\int_a^t |y_1(s) - y_2(s)|\,ds.$$
> 由 Gronwall（$\alpha = |y_1(a) - y_2(a)|$，$\beta = L$）：
> $$|y_1(t) - y_2(t)| \leq |y_1(a) - y_2(a)|\, e^{L(t-a)}.$$
> 若 $y_1(a) = y_2(a)$，则 $y_1 \equiv y_2$——这是 Picard-Lindelöf 定理唯一性的核心步骤，见 [[Picard-Lindelöf定理]]。
>
> **应用 2（解对初值连续依赖性）**：上式给出依赖于初值的 Lipschitz 估计，见 [[解对初值的连续依赖性]]。
>
> **应用 3（Runge-Kutta 误差传播）**：数值方法的全局收敛阶估计——局部截断误差经过 Gronwall 放大到全局——是后续 RK 收敛性证明的关键，见后续笔记 `Runge-Kutta方法的收敛性`。

> [!info] 推广 $\alpha(t)$ 形式
> 当 $\alpha$ 为时间变量函数时，同样用积分因子法。结果中含 $\int_a^t \alpha(s)\beta(s) e^{\int_s^t \beta}$ 项，反映了"过去时刻的输入 $\alpha(s)$ 经过 $[s, t]$ 期间的指数放大"。
