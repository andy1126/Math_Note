---
title: 正则奇点与 Frobenius 方法
date: 2026-06-20
tags:
  - 微分方程
  - ODE
  - 级数解法
  - Frobenius方法
  - 正则奇点
  - 指标方程
---

# 正则奇点与 Frobenius 方法

## 预备定义

仍考虑标准形二阶齐次线性方程
$$y'' + p(x)\, y' + q(x)\, y = 0. \quad \cdots (\mathrm{H})$$
不失一般性设奇点在 $x_0 = 0$。在常点处的幂级数法见 [[常点附近的幂级数解]]；本文处理"温和"的奇点。

> [!note] 正则奇点（regular singular point）
> 称 $x = 0$ 为 $(\mathrm{H})$ 的**正则奇点**，若它是奇点（$p$ 或 $q$ 在 $0$ 处不解析），但
> $$x\,p(x) \quad \text{与} \quad x^2 q(x) \quad \text{都在 } x = 0 \text{ 处解析}.$$
> 等价地，$p$ 在 $0$ 处至多一阶极点、$q$ 在 $0$ 处至多二阶极点。不满足此条件的奇点称**非正则（irregular）奇点**。

记解析展开
$$x\,p(x) = \sum_{k=0}^{\infty} P_k x^k = P(x), \qquad x^2 q(x) = \sum_{k=0}^{\infty} Q_k x^k = Q(x),$$
则
$$p(x) = \frac{P(x)}{x} = \frac{P_0}{x} + P_1 + \cdots, \qquad q(x) = \frac{Q(x)}{x^2} = \frac{Q_0}{x^2} + \frac{Q_1}{x} + \cdots.$$
两个**最低阶系数** $P_0 = \lim_{x\to 0} x p(x)$、$Q_0 = \lim_{x \to 0} x^2 q(x)$ 决定下面的指标方程。

> [!note] Frobenius 级数
> 形如
> $$y(x) = x^r \sum_{n=0}^{\infty} a_n x^n = \sum_{n=0}^{\infty} a_n x^{n+r}, \qquad a_0 \neq 0,$$
> 的级数（$r$ 为待定的实/复指数，允许非整数）称 **Frobenius 级数**。约定 $a_0 \neq 0$ 以使 $r$ 为真正的领头指数。

> [!abstract] 引理：第二解的降阶构造
> 若已知 $(\mathrm{H})$ 的一个非零解 $y_1$，则可设 $y_2 = y_1 \int \dfrac{e^{-\int p\,dx}}{y_1^2}\,dx$ 得到与之线性独立的第二解。这是 Frobenius 重根 / 整数差情形中出现 $\ln$ 项的根源。详见 [[降阶法]]。

> [!abstract] 引理：解的唯一性（Picard-Lindelöf）
> 在远离奇点处系数连续，初值问题有唯一解。详见 [[Picard-Lindelöf定理]]。

---

## 定理

> [!important] Frobenius 定理
> 设 $x = 0$ 为 $(\mathrm{H})$ 的正则奇点，$P = xp$、$Q = x^2 q$ 在 $|x| < R$ 内解析。定义**指标方程（indicial equation）**
> $$I(r) := r(r-1) + P_0\, r + Q_0 = 0, \quad \cdots (\mathrm{IND})$$
> 设其两根为 $r_1, r_2$（约定 $\operatorname{Re} r_1 \geq \operatorname{Re} r_2$）。则在 $0 < x < R$ 上存在基本解组，且依据 $r_1 - r_2$ 的类型分三种情形：
>
> **情形 1（$r_1 - r_2 \notin \mathbb{Z}$）**：两个独立 Frobenius 解
> $$y_1 = x^{r_1}\sum_{n\geq 0} a_n x^n, \qquad y_2 = x^{r_2}\sum_{n\geq 0} b_n x^n \quad (a_0 = b_0 = 1).$$
>
> **情形 2（$r_1 = r_2 =: r$，重根）**：一个 Frobenius 解与一个**带对数项**的解
> $$y_1 = x^{r}\sum_{n\geq 0} a_n x^n, \qquad y_2 = y_1 \ln x + x^{r}\sum_{n\geq 1} c_n x^n.$$
>
> **情形 3（$r_1 - r_2 = N \in \mathbb{Z}_{>0}$，正整数差）**：较大根仍给 Frobenius 解；较小根的解可能含对数项
> $$y_1 = x^{r_1}\sum_{n\geq 0} a_n x^n, \qquad y_2 = \kappa\, y_1 \ln x + x^{r_2}\sum_{n\geq 0} c_n x^n \quad (c_0 = 1),$$
> 其中常数 $\kappa$ 可能为 $0$（此时无对数项，两个纯 Frobenius 解）。

---

## 证明

证明的主线：把 Frobenius 级数代入 $(\mathrm{H})$，对齐**最低次幂**得指标方程，对齐一般次幂得递推；再按 $I(r_1 + n)$ 是否退化为零分情形。

### 第一部分：指标方程与一般递推

#### 第一步：化为带 $P, Q$ 的形式

把 $(\mathrm{H})$ 两边乘 $x^2$：
$$x^2 y'' + x\,[x p(x)]\, y' + [x^2 q(x)]\, y = 0, \quad\text{即}\quad x^2 y'' + x P(x)\, y' + Q(x)\, y = 0. \quad \cdots (\mathrm{H}')$$
这是 **Euler 型 + 解析微扰** 的标准书写：$P, Q$ 解析使下面的代入合法。

#### 第二步：代入 Frobenius 级数

设 $y = \sum_{n\geq 0} a_n x^{n+r}$。则
$$y' = \sum_{n\geq 0}(n+r) a_n x^{n+r-1}, \qquad y'' = \sum_{n\geq 0}(n+r)(n+r-1) a_n x^{n+r-2}.$$
于是
$$x^2 y'' = \sum_{n\geq 0}(n+r)(n+r-1) a_n x^{n+r}, \qquad x\,y' = \sum_{n\geq 0}(n+r) a_n x^{n+r}.$$
配合 $P(x) = \sum_k P_k x^k$、$Q(x) = \sum_k Q_k x^k$，用 Cauchy 乘积，$(\mathrm{H}')$ 左端 $x^{n+r}$ 的系数为
$$\big[(n+r)(n+r-1) + P_0 (n+r) + Q_0\big] a_n + \sum_{j=0}^{n-1}\big[ (j+r) P_{n-j} + Q_{n-j}\big] a_j = 0.$$

记 $I(s) = s(s-1) + P_0 s + Q_0$，上式即
$$I(n+r)\, a_n = -\sum_{j=0}^{n-1}\big[(j+r) P_{n-j} + Q_{n-j}\big] a_j, \quad n \geq 0. \quad \cdots (\star)$$

#### 第三步：最低次幂 → 指标方程

取 $n = 0$（求和为空）：
$$I(r)\, a_0 = 0.$$
因约定 $a_0 \neq 0$，必有
$$\boxed{\,I(r) = r(r-1) + P_0 r + Q_0 = 0.\,} \quad \cdots (\mathrm{IND})$$
这就是**指标方程**。它是关于领头指数 $r$ 的二次方程，根 $r_1, r_2$ 即领头指数的两个候选。$\square$

> [!important] 指标方程 = 常点情形首项系数的"奇点版"
> 在 [[常点附近的幂级数解]] 中，递推左端首项是 $(m+2)(m+1)$，恒不为零。
> 在奇点处它被替换为 $I(n+r)$，而 $I(r) = 0$ 本身——首项系数**在 $n = 0$ 处退化为零**正是"奇点"的代数表现。能否继续递推，取决于 $I(r+n)$ 对后续 $n$ 是否再次为零。

#### 第四步：一般递推

对 $n \geq 1$，只要 $I(r + n) \neq 0$，可解出
$$a_n = \frac{-1}{I(r+n)} \sum_{j=0}^{n-1}\big[(j+r) P_{n-j} + Q_{n-j}\big] a_j. \quad \cdots (\star\star)$$
右端只含低指标 $a_0, \ldots, a_{n-1}$，故 $a_0 = 1$ 唯一确定整条级数——**前提是分母 $I(r+n)$ 永不为零**。收敛性由与常点情形相同的优级数论证保证，半径 $\geq R$。

### 第二部分：三种情形

设 $r_1, r_2$ 为 $(\mathrm{IND})$ 的根，$\operatorname{Re} r_1 \geq \operatorname{Re} r_2$。注意
$$I(s) = (s - r_1)(s - r_2),\quad\text{故}\quad I(r_2 + n) = (r_2 + n - r_1)(n) = n\,(n - (r_1 - r_2)).$$
分母 $I(r_2 + n)$ 在 $n = r_1 - r_2$ 时为零——这正是麻烦发生处。

#### 情形 1：$r_1 - r_2 \notin \mathbb{Z}$

对 $r = r_1$：$I(r_1 + n) = n(n + (r_1 - r_2)) \neq 0$（$n \geq 1$），递推 $(\star\star)$ 畅通，得 $y_1$。
对 $r = r_2$：$I(r_2 + n) = n(n - (r_1 - r_2))$，因 $r_1 - r_2 \notin \mathbb{Z}$ 故对一切 $n \geq 1$ 非零，递推畅通，得 $y_2$。

二者领头幂 $x^{r_1}, x^{r_2}$ 不同（差非整数），故 $y_1/y_2 \not\to$ 常数，**线性独立**。$\square$

#### 情形 2：$r_1 = r_2 = r$（重根）

只能得一个 Frobenius 解 $y_1 = x^r \sum a_n x^n$。第二解须用 **[[降阶法]]**：设 $y_2 = y_1 \cdot v$，代入 $(\mathrm{H})$ 得 $v$ 的一阶方程
$$v' = \frac{1}{y_1^2}\, e^{-\int p\,dx}.$$
由 $p \sim P_0/x$ 与 $y_1 \sim x^r$，被积函数 $\sim x^{-2r - P_0} = x^{-1}$（因重根时 $2r = 1 - P_0$，即 $P_0 = 1 - 2r$）。故 $v' \sim 1/x$，积分出 $\ln x$：
$$y_2 = y_1 \ln x + x^{r}\sum_{n\geq 1} c_n x^n. \quad \square$$

> [!info] 为何重根必出对数
> 重根 $\iff I(s) = (s-r)^2 \iff P_0 = 1 - 2r$。降阶法中 $e^{-\int p\,dx} = \exp(-\int (P_0/x + \cdots)) \sim x^{-P_0}$，而 $y_1^{-2} \sim x^{-2r}$，乘积 $\sim x^{-P_0 - 2r} = x^{-1}$，积分恰得 $\ln x$。这是对数项的**结构性**来源，与具体方程无关。

#### 情形 3：$r_1 - r_2 = N \in \mathbb{Z}_{>0}$

较大根 $r_1$：$I(r_1 + n) = n(n + N) \neq 0$，递推畅通，$y_1$ 为纯 Frobenius 解。

较小根 $r_2$：$I(r_2 + n) = n(n - N)$ 在 $n = N$ 处**为零**。此时 $(\star)$ 在 $n = N$ 变为
$$0 \cdot a_N = -\sum_{j=0}^{N-1}\big[(j + r_2) P_{N-j} + Q_{N-j}\big] a_j =: -\,S.$$

- 若 $S = 0$：方程 $0 = 0$ 自动成立，$a_N$ 可任取（通常取 $0$），递推可继续，得**第二个纯 Frobenius 解**（$\kappa = 0$）。
- 若 $S \neq 0$：出现矛盾 $0 = -S \neq 0$，纯 Frobenius 级数失败。须引入对数项，设
$$y_2 = \kappa\, y_1 \ln x + x^{r_2}\sum_{n\geq 0} c_n x^n,$$
代回后 $\ln x$ 项的系数确定 $\kappa \neq 0$，其余 $c_n$ 由修正递推确定。$\square$

> [!important] 把三情形统一看
> 关键量是 $I(r_2 + n) = n(n - (r_1 - r_2))$ 何时为零：
> - 非整数差：永不再为零 → 两个 Frobenius 解；
> - 重根（差 $0$）：$n = 0$ 即重根，第二解被迫降阶 → 必含 $\ln$；
> - 正整数差 $N$：$n = N$ 处分母为零 → 视相容性 $S$ 决定是否需 $\ln$。

### 总结

综合：正则奇点处恒可写出领头指数满足指标方程的 Frobenius 解；第二个独立解的形态由两根之差的算术性质决定。三种情形覆盖所有可能，故 $(\mathrm{H})$ 在 $0 < x < R$ 上总有基本解组。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> **正则奇点 = 首项系数"恰好"退化成指标方程，但不再退化得更糟。**
> 1. 乘 $x^2$ 化为 $x^2 y'' + xP y' + Q y = 0$，使 $P = xp$、$Q = x^2 q$ 解析——这是"正则"的全部含义；
> 2. 代入 $y = x^r\sum a_n x^n$，**最低次幂**给指标方程 $I(r) = 0$，**一般次幂**给递推 $I(r+n)a_n = (\text{低指标})$；
> 3. 第二解的命运全系于分母 $I(r_2 + n) = n(n - (r_1 - r_2))$ 是否再次为零：非整数差畅通无阻；重根与正整数差则可能逼出 $\ln$ 项，须用 [[降阶法]] 兜底。
>
> 一句话：**指标方程定领头指数，两根之差定第二解形态，对数项是降阶法在分母归零时的必然产物。**

> [!warning] 非正则奇点 Frobenius 失效
> 若 $xp$ 或 $x^2 q$ 仍不解析（如 $p = 1/x^2$），则上述代入产生的不是有限阶指标方程，Frobenius 级数一般**不收敛或不存在**，须改用渐近展开（如 WKB、不规则奇点的形式级数）。例：$x^3 y'' = y$ 在 $0$ 处为非正则奇点。

> [!info] 与 Sturm-Liouville 本征值问题的联系
> 许多经典本征方程（Bessel、Legendre、Laguerre、Hermite）都带有正则奇点，其在 $x = 0$（或 $\pm 1$）处的 Frobenius 行为决定了**哪一支解在奇点处有界**，从而挑选出物理上可接受的本征函数。这正是 [[Sturm-Liouville定理]] 中"在奇点处加正则性边界条件"的级数解释；具体见 [[Bessel方程的Frobenius解]]。

> [!info] 与常点情形的统一视角
> [[常点附近的幂级数解]] 是 Frobenius 的退化特例：常点处 $P_0 = Q_0 = 0$，指标方程 $r(r-1) = 0$ 给 $r = 0, 1$，两根差 $1 \in \mathbb{Z}_{>0}$ 但相容性 $S = 0$，于是得到两个从 $x^0, x^1$ 开始的纯幂级数解——正是常点的两个解析解。
