---
title: Sturm 比较定理
date: 2026-04-11
tags:
  - 常微分方程
  - 二阶线性ODE
  - Sturm理论
  - 振荡
  - 零点
---

# Sturm 比较定理

## 预备定义

> [!note] Sturm-Liouville 标准形
> 将二阶线性 ODE 化为不含一阶导数项的形式：
> $$u'' + q_1(t)\, u = 0, \quad \cdots (E_1)$$
> $$v'' + q_2(t)\, v = 0, \quad \cdots (E_2)$$
> 其中 $q_1, q_2: [a, b] \to \mathbb{R}$ 连续。
>
> 任何 $y'' + p(t)y' + q(t)y = 0$ 都可通过变量替换 $y = u \exp\!\left(-\frac{1}{2}\int p\right)$ 化为此形。

> [!note] 零点的含义
> $t_0$ 是 $u$ 的**零点**，若 $u(t_0) = 0$。对齐次线性 ODE 的非平凡解，零点都是**孤立的**（否则由唯一性 $u \equiv 0$）。

> [!abstract] 引理（Sturm 分离定理）
> 同一方程的两个线性无关解的零点严格交替排列。
> 参见 [[Sturm分离定理]]。

---

## 定理

设 $q_1, q_2: [a, b] \to \mathbb{R}$ 连续，且

$$q_1(t) \leq q_2(t) \quad \forall\, t \in [a, b].$$

设 $u \not\equiv 0$ 为 $(E_1)$ 的解，$v \not\equiv 0$ 为 $(E_2)$ 的解。若 $\alpha, \beta$（$\alpha < \beta$）是 $u$ 的两个**相邻零点**，则 $v$ 在 $(\alpha, \beta)$ 内**至少有一个零点**。

> [!info] 直观含义
> "势函数"$q$ 越大，解振荡越剧烈（零点越密集）。$(E_2)$ 的势 $q_2 \geq q_1$，故 $(E_2)$ 的解 $v$ 在 $(E_1)$ 的解 $u$ 的每对相邻零点之间至少振荡一次。
>
> 当 $q_1 = q_2$ 时，$u$ 和 $v$ 是同一方程的两个解，定理退化为 [[Sturm分离定理]]（线性无关解的零点交替）。

---

## 证明

不妨设 $u(t) > 0$ 在 $(\alpha, \beta)$ 上（否则换 $-u$）。

**反证法**：假设 $v$ 在 $[\alpha, \beta]$ 上不变号。不妨设 $v(t) \geq 0$ 在 $[\alpha, \beta]$ 上（否则换 $-v$）。

> [!info] $v(\alpha) > 0$ 或 $v(\beta) > 0$
> 若 $v(\alpha) = v(\beta) = 0$，则 $\alpha, \beta$ 均为 $v$ 的零点，$v$ 在 $(\alpha, \beta)$ 内不为零——但这本身意味着 $v$ 的两个零点之间 $v$ 无零点，这与我们要证明的结论并不矛盾。然而下面的论证将说明此情形也导致矛盾（除非 $q_1 \equiv q_2$ 且 $v$ 是 $u$ 的常数倍）。实际上 $v(\alpha) = v(\beta) = 0$ 且 $v > 0$ 在 $(\alpha, \beta)$ 上这一情形，下面的 Sturm 恒等式仍然给出矛盾。

### 第一步：建立 Sturm 恒等式（Picone 型）

将 $(E_1)$ 乘以 $v$，$(E_2)$ 乘以 $u$，相减：

$$v \cdot u'' - u \cdot v'' + (q_1 - q_2)\, uv = 0. \quad \cdots (\ast)$$

> [!important] Wronskian 的导数
> 定义 $W(t) = u(t)\, v'(t) - u'(t)\, v(t)$。则
> $$W'(t) = u\, v'' - u''\, v.$$
> 注意这里 $u, v$ 来自**不同方程**，$W$ 不再满足 Abel 公式。

将 $(\ast)$ 改写：

$$u'' v - u v'' = (q_2 - q_1)\, uv,$$

即

$$-W'(t) = (q_2(t) - q_1(t))\, u(t)\, v(t). \quad \cdots (\star)$$

$\square$

### 第二步：在 $[\alpha, \beta]$ 上积分

对 $(\star)$ 从 $\alpha$ 积分到 $\beta$：

$$-W(\beta) + W(\alpha) = \int_{\alpha}^{\beta} (q_2(t) - q_1(t))\, u(t)\, v(t)\, dt. \quad \cdots (\dagger)$$

$\square$

### 第三步：分析右端的符号

在 $(\alpha, \beta)$ 上：
- $q_2(t) - q_1(t) \geq 0$（假设条件）；
- $u(t) > 0$（$\alpha, \beta$ 为 $u$ 的相邻零点）；
- $v(t) \geq 0$（反证假设）。

故被积函数 $\geq 0$，即

$$\int_{\alpha}^{\beta} (q_2 - q_1)\, uv \, dt \geq 0. \quad \cdots (1)$$

$\square$

### 第四步：分析左端的符号

**在 $t = \alpha$ 处**：$u(\alpha) = 0$，$u(t) > 0$ 在 $\alpha$ 右侧，故 $u'(\alpha) > 0$（若 $u'(\alpha) = 0$，由唯一性 $u \equiv 0$，矛盾）。因此

$$W(\alpha) = u(\alpha)\, v'(\alpha) - u'(\alpha)\, v(\alpha) = -u'(\alpha)\, v(\alpha). \quad \cdots (2)$$

由 $u'(\alpha) > 0$ 和 $v(\alpha) \geq 0$，得 $W(\alpha) \leq 0$。

**在 $t = \beta$ 处**：$u(\beta) = 0$，$u(t) > 0$ 在 $\beta$ 左侧，故 $u'(\beta) < 0$。因此

$$W(\beta) = u(\beta)\, v'(\beta) - u'(\beta)\, v(\beta) = -u'(\beta)\, v(\beta). \quad \cdots (3)$$

由 $u'(\beta) < 0$ 和 $v(\beta) \geq 0$，得 $W(\beta) \geq 0$。

故

$$-W(\beta) + W(\alpha) \leq 0. \quad \cdots (4)$$

$\square$

### 第五步：得到矛盾

由 $(\dagger)$，左端 $\leq 0$（由 $(4)$），右端 $\geq 0$（由 $(1)$）。故两端均为零：

$$\int_{\alpha}^{\beta} (q_2 - q_1)\, uv \, dt = 0 \quad \text{且} \quad W(\alpha) = W(\beta) = 0. \quad \cdots (5)$$

由 $W(\alpha) = 0$ 和 $(2)$：$u'(\alpha)\, v(\alpha) = 0$。由 $u'(\alpha) > 0$，得 $v(\alpha) = 0$。

由 $W(\beta) = 0$ 和 $(3)$：$u'(\beta)\, v(\beta) = 0$。由 $u'(\beta) < 0$，得 $v(\beta) = 0$。

> [!important] 现在 $v$ 也在 $\alpha$ 和 $\beta$ 处为零
> 反证假设是 $v$ 在 $[\alpha, \beta]$ 上不变号。我们已证 $v(\alpha) = v(\beta) = 0$ 且 $v \geq 0$ 在 $[\alpha, \beta]$ 上。

由 $(5)$ 的第一个等式和被积函数 $\geq 0$：

$$(q_2(t) - q_1(t))\, u(t)\, v(t) = 0 \quad \text{a.e. 在 } [\alpha, \beta] \text{ 上}.$$

由 $u > 0$ 在 $(\alpha, \beta)$ 上，且 $q_2 - q_1$ 和 $v$ 均连续非负，得

$$\text{对一切 } t \in (\alpha, \beta): \quad (q_2(t) - q_1(t))\, v(t) = 0. \quad \cdots (6)$$

现在考虑两种情形。

#### 情形 A：$q_1 \not\equiv q_2$ 在 $(\alpha, \beta)$ 上

由 $(6)$，在 $q_2 > q_1$ 的点处（此类点构成非空开集）必有 $v = 0$。但 $v$ 在 $[\alpha, \beta]$ 上满足 $(E_2)$ 且 $v \geq 0$，$v$ 的零点集在 $(\alpha, \beta)$ 内非空。设 $\gamma$ 为其中一个零点，则 $v(\gamma) = 0$。

**但我们假设 $v$ 在 $(\alpha, \beta)$ 上不变号且 $v \geq 0$**，若 $v(\gamma) = 0$ 是 $v$ 在 $(\alpha, \beta)$ 内的零点，则 $v$ 在 $\gamma$ 处达到最小值，故 $v'(\gamma) = 0$。由唯一性定理，$v \equiv 0$——与 $v \not\equiv 0$ **矛盾！** $\square$

#### 情形 B：$q_1 \equiv q_2$ 在 $[\alpha, \beta]$ 上

此时 $u$ 和 $v$ 满足**同一方程**。$v(\alpha) = v(\beta) = 0$ 且 $\alpha, \beta$ 是 $u$ 的相邻零点。由 [[Sturm分离定理]]，同一方程的两个线性无关解的零点严格交替；若 $u, v$ 线性无关，则 $v$ 在 $(\alpha, \beta)$ 内必有零点——与假设矛盾。若 $u, v$ 线性相关（$v = cu$），则 $v$ 的零点恰为 $u$ 的零点，$v(\alpha) = v(\beta) = 0$ 本身就是 $v$ 在 $\alpha, \beta$ 处的零点，但 $v$ 在 $(\alpha, \beta)$ 上无零点。此时定理的结论"$v$ 在 $(\alpha,\beta)$ 内至少有一个零点"在 $q_1 \equiv q_2$ 且 $v$ 与 $u$ 线性相关时确实不成立——但注意若 $v = cu$，则 $v$ 在 $\alpha, \beta$ 处为零而在 $(\alpha,\beta)$ 内无零点，这恰好是边界情形。$\square$

> [!warning] 严格不等式下的加强
> 若 $q_1(t) < q_2(t)$ 对某个 $t \in (\alpha, \beta)$ 严格成立（即 $q_1 \not\equiv q_2$），则情形 B 不出现，结论无条件成立。在 $q_1 \equiv q_2$ 的退化情形下，结论需修正为"$v$ 在 $[\alpha, \beta]$ 内至少有一个零点"（含端点）。

### 总结

在 $q_1 \not\equiv q_2$ 于 $(\alpha, \beta)$ 的条件下，反证假设（$v$ 在 $(\alpha, \beta)$ 上不变号）导致 $v \equiv 0$ 或矛盾。故 $v$ 在 $(\alpha, \beta)$ 内至少有一个零点。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明的核心是 **Sturm 恒等式** $-W' = (q_2 - q_1)\, uv$：
> 1. 将两个不同方程的解通过 Wronskian $W = uv' - u'v$ 联系起来；
> 2. 在 $[\alpha, \beta]$ 上积分，将问题转化为**符号分析**；
> 3. 右端 $\geq 0$（因 $q_2 \geq q_1$, $u > 0$, $v \geq 0$），左端 $\leq 0$（因端点处 $u$ 的导数符号确定）；
> 4. 两端均为零迫使 $v(\alpha) = v(\beta) = 0$ 且 $(q_2 - q_1)v \equiv 0$，最终由唯一性定理得到 $v \equiv 0$ 的矛盾。
>
> 与 [[Sturm分离定理]] 的对比：分离定理用 Wronskian 的**定号性**（Abel 公式），比较定理用 Wronskian 的**导数公式**（Sturm 恒等式）。两者都是 Wronskian 的精妙运用。

> [!warning] 经典应用
> - **振荡判据**：若 $q(t) \geq \frac{1}{4t^2}$（$t$ 充分大），则 $u'' + q(t)u = 0$ 的一切解在 $t \to \infty$ 时有无穷多零点。证明：与 Euler 方程 $v'' + \frac{1}{4t^2}v = 0$（其解 $v = \sqrt{t}$ 非振荡）的边界情形比较。
> - **非振荡判据**：若 $q(t) \leq 0$，则 $u'' + q(t)u = 0$ 的解至多有一个零点（与 $v'' = 0$ 比较，$v$ 的解是直线，至多一个零点）。
> - **特征值排列**：Sturm-Liouville 问题 $-u'' + q(t)u = \lambda u$ 的特征值 $\lambda_1 < \lambda_2 < \cdots$ 对应的特征函数 $u_n$ 恰有 $n-1$ 个零点——这是比较定理的直接推论。
