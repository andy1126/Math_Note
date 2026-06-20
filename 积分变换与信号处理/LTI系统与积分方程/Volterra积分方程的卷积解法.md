---
title: 用卷积定理求解 Volterra 积分方程
date: 2026-04-18
tags:
  - 积分变换
  - Laplace变换
  - 卷积
  - 积分方程
  - Volterra方程
---

# 用卷积定理求解 Volterra 积分方程

## 预备定义

> [!note] 第二类 Volterra 积分方程
> 形如
> $$f(t) = g(t) + \lambda \int_0^t K(t - \tau)\, f(\tau)\, d\tau$$
> 的方程称为**第二类 Volterra 积分方程**（Volterra integral equation of the second kind），其中 $g(t)$ 为已知函数，$K$ 为**卷积核**（convolution kernel），$\lambda$ 为参数，$f(t)$ 为待求解的未知函数。
>
> 注意积分项 $\int_0^t K(t-\tau)\,f(\tau)\,d\tau = (K * f)(t)$ 恰为 $K$ 与 $f$ 的卷积。

> [!abstract] Laplace 变换的卷积定理
> 设 $f, g$ 为指数阶的局部可积函数，则
> $$\mathcal{L}\{f * g\}(s) = F(s) \cdot G(s),$$
> 其中 $F(s) = \mathcal{L}\{f\}(s)$，$G(s) = \mathcal{L}\{g\}(s)$。
>
> 详见 [[Laplace 变换的卷积定理|Laplace 变换的卷积定理]]。

> [!info] 本节用到的 Laplace 变换对
>
> | $f(t)$ | $F(s) = \mathcal{L}\{f\}(s)$ |
> |--------|-------------------------------|
> | $t$ | $\dfrac{1}{s^2}$ |
> | $\sin t$ | $\dfrac{1}{s^2 + 1}$ |
> | $\dfrac{t^n}{n!}$ | $\dfrac{1}{s^{n+1}}$ |

---

## 命题

求解如下第二类 Volterra 积分方程：

$$f(t) = t + \int_0^t f(\tau)\, \sin(t - \tau)\, d\tau, \quad t \geq 0. \quad \cdots (\ast)$$

则其唯一连续解为

$$f(t) = t + \frac{t^3}{6}.$$

---

## 证明

证明分为两部分：先用 Laplace 变换与卷积定理**推导**解，再**验证**所得函数确实满足原方程。

### 第一部分：推导解

#### 第一步：识别卷积结构

将 $(\ast)$ 改写为

$$f(t) = t + (\sin * f)(t),$$

其中 $(\sin * f)(t) = \int_0^t \sin(t - \tau)\, f(\tau)\, d\tau$ 为 $\sin t$ 与 $f(t)$ 的卷积。$\square$

#### 第二步：对两端取 Laplace 变换

设 $F(s) = \mathcal{L}\{f\}(s)$。对 $(\ast)$ 两端取 Laplace 变换：

$$F(s) = \mathcal{L}\{t\}(s) + \mathcal{L}\{\sin * f\}(s).$$

由已知变换对，$\mathcal{L}\{t\} = \dfrac{1}{s^2}$。

由**卷积定理**，

$$\mathcal{L}\{\sin * f\}(s) = \mathcal{L}\{\sin t\}(s) \cdot F(s) = \frac{1}{s^2 + 1} \cdot F(s).$$

因此得到

$$F(s) = \frac{1}{s^2} + \frac{F(s)}{s^2 + 1}. \quad \cdots (\star)$$

> [!important] 卷积定理的核心作用
> 卷积定理将积分方程 $(\ast)$ 中的**卷积积分**转化为频域中的**乘法**，从而将函数方程降维为关于 $F(s)$ 的**代数方程** $(\star)$。这正是 Laplace 变换方法求解积分方程的关键。

$\square$

#### 第三步：求解代数方程

由 $(\star)$，将含 $F(s)$ 的项移至左端：

$$F(s) - \frac{F(s)}{s^2 + 1} = \frac{1}{s^2}.$$

提取公因子：

$$F(s) \left(1 - \frac{1}{s^2 + 1}\right) = \frac{1}{s^2}.$$

化简括号内的表达式：

$$1 - \frac{1}{s^2 + 1} = \frac{s^2 + 1 - 1}{s^2 + 1} = \frac{s^2}{s^2 + 1}.$$

因此

$$F(s) \cdot \frac{s^2}{s^2 + 1} = \frac{1}{s^2},$$

解得

$$F(s) = \frac{s^2 + 1}{s^2} \cdot \frac{1}{s^2} = \frac{s^2 + 1}{s^4} = \frac{1}{s^2} + \frac{1}{s^4}. \quad \cdots (1)$$

$\square$

#### 第四步：取 Laplace 逆变换

由 $(1)$ 和已知变换对：

$$\mathcal{L}^{-1}\!\left\{\frac{1}{s^2}\right\} = t, \qquad \mathcal{L}^{-1}\!\left\{\frac{1}{s^4}\right\} = \frac{t^3}{3!} = \frac{t^3}{6}.$$

因此

$$f(t) = t + \frac{t^3}{6}. \quad \square$$

---

### 第二部分：验证解

**目标**：验证 $f(t) = t + \dfrac{t^3}{6}$ 满足原方程 $(\ast)$。

需要计算卷积积分 $\displaystyle\int_0^t f(\tau)\,\sin(t - \tau)\,d\tau$ 并证明它等于 $f(t) - t = \dfrac{t^3}{6}$。

#### 第一步：展开卷积积分

$$\int_0^t f(\tau)\,\sin(t - \tau)\,d\tau = \int_0^t \left(\tau + \frac{\tau^3}{6}\right) \sin(t - \tau)\, d\tau.$$

将其拆为两个积分：

$$I_1 = \int_0^t \tau\, \sin(t - \tau)\, d\tau, \qquad I_2 = \int_0^t \frac{\tau^3}{6}\, \sin(t - \tau)\, d\tau.$$

$\square$

#### 第二步：计算 $I_1$

作换元 $u = t - \tau$，$du = -d\tau$。当 $\tau = 0$ 时 $u = t$；当 $\tau = t$ 时 $u = 0$。

$$I_1 = \int_t^0 (t - u)\,\sin u\,(-du) = \int_0^t (t - u)\,\sin u\, du.$$

展开：

$$I_1 = t \int_0^t \sin u\, du - \int_0^t u\,\sin u\, du.$$

分别计算：

$$\int_0^t \sin u\, du = [-\cos u]_0^t = 1 - \cos t.$$

$$\int_0^t u\,\sin u\, du = [-u\cos u]_0^t + \int_0^t \cos u\, du = -t\cos t + \sin t.$$

因此

$$I_1 = t(1 - \cos t) - (-t\cos t + \sin t) = t - t\cos t + t\cos t - \sin t = t - \sin t. \quad \square$$

#### 第三步：计算 $I_2$

同样用卷积定理在频域中验证。注意

$$I_2 = \frac{1}{6}(\tau^3 * \sin t).$$

由 Laplace 变换，$\mathcal{L}\{\tau^3\} = \dfrac{6}{s^4}$，$\mathcal{L}\{\sin t\} = \dfrac{1}{s^2+1}$。由卷积定理：

$$\mathcal{L}\{I_2\} = \frac{1}{6} \cdot \frac{6}{s^4} \cdot \frac{1}{s^2 + 1} = \frac{1}{s^4(s^2+1)}.$$

作部分分式分解：

$$\frac{1}{s^4(s^2+1)} = \frac{1}{s^4} - \frac{1}{s^2(s^2+1)} = \frac{1}{s^4} - \frac{1}{s^2} + \frac{1}{s^2+1}.$$

> [!info] 部分分式的推导
> 利用 $\dfrac{1}{s^2(s^2+1)} = \dfrac{1}{s^2} - \dfrac{1}{s^2+1}$（对 $\dfrac{1}{A \cdot B} = \dfrac{1}{B-A}\left(\dfrac{1}{A} - \dfrac{1}{B}\right)$ 令 $A = s^2$，$B = s^2+1$），代入得
> $$\frac{1}{s^4(s^2+1)} = \frac{1}{s^4} - \left(\frac{1}{s^2} - \frac{1}{s^2+1}\right) = \frac{1}{s^4} - \frac{1}{s^2} + \frac{1}{s^2+1}.$$

取逆变换：

$$I_2 = \frac{t^3}{6} - t + \sin t. \quad \square$$

#### 第四步：合并并验证

$$I_1 + I_2 = (t - \sin t) + \left(\frac{t^3}{6} - t + \sin t\right) = \frac{t^3}{6}.$$

因此

$$t + \int_0^t f(\tau)\,\sin(t-\tau)\,d\tau = t + \frac{t^3}{6} = f(t). \quad \checkmark$$

原方程 $(\ast)$ 得到验证。$\square$

---

### 总结

1. 识别卷积结构，将积分方程写为 $f = g + K * f$。 ✓
2. 取 Laplace 变换，由卷积定理将积分方程转化为代数方程。 ✓
3. 求解代数方程，得到 $F(s)$。 ✓
4. 取逆变换，得到 $f(t) = t + \dfrac{t^3}{6}$。 ✓
5. 代入原方程验证。 ✓

因此 $f(t) = t + \dfrac{t^3}{6}$ 是方程 $(\ast)$ 的唯一连续解。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本题展示了卷积定理在求解积分方程中的威力。核心思路可概括为三个字：**化乘除**。
>
> **积分方程（时域）**
> $$f(t) = t + \int_0^t f(\tau)\,\sin(t-\tau)\,d\tau$$
> $$\downarrow \quad \text{Laplace 变换 + 卷积定理}$$
> **代数方程（频域）**
> $$F(s) = \frac{1}{s^2} + \frac{F(s)}{s^2+1}$$
> $$\downarrow \quad \text{解代数方程}$$
> **显式解（频域）**
> $$F(s) = \frac{1}{s^2} + \frac{1}{s^4}$$
> $$\downarrow \quad \text{逆变换}$$
> **显式解（时域）**
> $$f(t) = t + \frac{t^3}{6}$$
>
> 卷积定理将**无法直接求解的函数方程**降维为**初等代数运算**，这正是 Laplace 变换方法的精髓。

> [!warning] 唯一性的保证
> 上述推导利用了 Laplace 变换的**单射性**（即逆变换的唯一性）：若两个连续函数有相同的 Laplace 变换，则它们相等。这保证了由 $F(s)$ 反演得到的 $f(t)$ 就是唯一解。严格地说，这依赖于 Lerch 定理：在连续函数类中，Laplace 变换是单射的。
