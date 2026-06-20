---
title: Banach 不动点定理（压缩映射原理）
date: 2026-05-23
tags:
  - 泛函分析
  - 度量空间
  - 不动点理论
  - 压缩映射
  - 完备性
---

# Banach 不动点定理（压缩映射原理）

> [!info] 相关笔记
> 本笔记为**泛函分析语境**下的版本。度量空间基础语境下的版本参见 [[Banach不动点定理|Banach 不动点定理（度量空间版）]]。

## 预备定义

> [!note] 度量空间
> 称二元组 $(X, d)$ 为**度量空间**（metric space），若 $X$ 为非空集合，$d: X \times X \to \mathbb{R}_{\geq 0}$ 满足：
> 1. $d(x, y) = 0 \iff x = y$；
> 2. $d(x, y) = d(y, x)$（对称性）；
> 3. $d(x, z) \leq d(x, y) + d(y, z)$（三角不等式）。

> [!note] 完备度量空间
> 称度量空间 $(X, d)$ 为**完备的**（complete），若 $X$ 中的每个 Cauchy 序列都在 $X$ 中收敛。

> [!note] 压缩映射
> 设 $(X, d)$ 为度量空间，$T: X \to X$ 为映射。若存在常数 $k \in [0, 1)$，使得
> $$d(T(x), T(y)) \leq k \cdot d(x, y), \quad \forall\, x, y \in X,$$
> 则称 $T$ 为 $X$ 上的**压缩映射**（contraction），$k$ 称为**压缩常数**（contraction constant）。

> [!note] 不动点
> 称 $x^* \in X$ 为映射 $T: X \to X$ 的**不动点**（fixed point），若 $T(x^*) = x^*$。

> [!abstract] 引理：压缩映射是 Lipschitz 连续的
> 设 $T: X \to X$ 是压缩常数为 $k$ 的压缩映射。则 $T$ 在 $X$ 上连续。

**证明**：对任意 $\varepsilon > 0$，取 $\delta = \varepsilon$（不妨设 $k > 0$；若 $k = 0$ 则 $T$ 为常值映射，平凡连续）。当 $d(x, y) < \delta$ 时，
$$d(T(x), T(y)) \leq k \cdot d(x, y) < k\delta < \delta = \varepsilon. \quad \square$$

---

## 定理

设 $(X, d)$ 为**非空完备**度量空间，$T: X \to X$ 为压缩常数 $k \in [0, 1)$ 的压缩映射。则：

**(i)**（存在唯一性）$T$ 在 $X$ 中存在唯一的不动点 $x^* \in X$。

**(ii)**（构造性收敛）对任意初始点 $x_0 \in X$，由迭代式
$$x_{n+1} = T(x_n), \quad n = 0, 1, 2, \ldots$$
定义的序列 $\{x_n\}$ 收敛于 $x^*$。

**(iii)**（误差估计）有先验估计
$$d(x_n, x^*) \leq \frac{k^n}{1 - k} \cdot d(x_1, x_0). \quad \cdots (\ast)$$

---

## 证明

### 第一步：构造迭代序列并证其为 Cauchy 序列

任取 $x_0 \in X$（由 $X$ 非空保证可取），定义 $x_{n+1} = T(x_n)$。

#### (a) 相邻项距离的几何衰减

由压缩性质，对任意 $n \geq 1$，
$$d(x_{n+1}, x_n) = d(T(x_n), T(x_{n-1})) \leq k \cdot d(x_n, x_{n-1}).$$

迭代该不等式 $n$ 次，得
$$d(x_{n+1}, x_n) \leq k^n \cdot d(x_1, x_0). \quad \cdots (\star)$$

#### (b) 任意两项距离的估计

设 $m > n \geq 0$。由三角不等式及 $(\star)$，
$$
\begin{aligned}
d(x_m, x_n) &\leq \sum_{i=n}^{m-1} d(x_{i+1}, x_i) \\
&\leq \sum_{i=n}^{m-1} k^i \cdot d(x_1, x_0) \\
&= k^n \cdot \frac{1 - k^{m-n}}{1 - k} \cdot d(x_1, x_0) \\
&\leq \frac{k^n}{1 - k} \cdot d(x_1, x_0). \quad \cdots (\dagger)
\end{aligned}
$$

> [!info] 几何级数求和的必要性
> 此处必须用 $\sum k^i$ 的求和而非简单放缩，否则得到的上界 $(m-n) k^n d(x_1, x_0)$ 中 $m - n$ 可能任意大，无法控制。$1 - k > 0$ 是 $k < 1$ 的关键作用。

#### (c) Cauchy 性

由 $k < 1$，$k^n \to 0$。故对任意 $\varepsilon > 0$，存在 $N$ 使得当 $n \geq N$ 时
$$\frac{k^n}{1 - k} \cdot d(x_1, x_0) < \varepsilon.$$

此时对一切 $m > n \geq N$，由 $(\dagger)$ 有 $d(x_m, x_n) < \varepsilon$。故 $\{x_n\}$ 是 Cauchy 序列。$\square$

### 第二步：极限存在并为不动点

> [!important] 完备性的核心运用
> 仅在此处使用 $X$ 的完备性：Cauchy 序列**未必**自然有极限，必须依赖度量空间的完备性。

由 $X$ 完备，$\{x_n\}$ 收敛于某点 $x^* \in X$。

由引理，$T$ 连续，故
$$T(x^*) = T\left(\lim_{n \to \infty} x_n\right) = \lim_{n \to \infty} T(x_n) = \lim_{n \to \infty} x_{n+1} = x^*.$$

故 $x^*$ 为 $T$ 的不动点。$\square$

### 第三步：唯一性

**反证法**：假设 $x^*, y^*$ 均为 $T$ 的不动点，即 $T(x^*) = x^*$ 且 $T(y^*) = y^*$。

则
$$d(x^*, y^*) = d(T(x^*), T(y^*)) \leq k \cdot d(x^*, y^*).$$

即 $(1 - k) \cdot d(x^*, y^*) \leq 0$。由 $k < 1$，$1 - k > 0$，故 $d(x^*, y^*) \leq 0$，从而 $d(x^*, y^*) = 0$，即 $x^* = y^*$。$\square$

### 第四步：误差估计 $(\ast)$

在 $(\dagger)$ 中令 $m \to \infty$：由 $x_m \to x^*$ 及度量的连续性，
$$d(x_n, x^*) = \lim_{m \to \infty} d(x_m, x_n) \leq \frac{k^n}{1 - k} \cdot d(x_1, x_0). \quad \square$$

### 总结

综合四步：
1. 迭代序列 $\{x_n\}$ 为 Cauchy 序列。 ✓
2. 由完备性，$\{x_n\}$ 收敛于 $x^* \in X$，且 $x^*$ 为不动点。 ✓
3. 不动点唯一。 ✓
4. 误差估计 $(\ast)$ 成立。 ✓

故 $T$ 在 $X$ 中具有唯一不动点 $x^*$，迭代序列收敛于 $x^*$，且满足先验误差估计。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 整个证明可以概括为**"压缩 + 完备 = 不动点"**：
> 1. **压缩性** $\Longrightarrow$ 相邻项距离按几何级数衰减 $\Longrightarrow$ 迭代序列是 Cauchy 序列；
> 2. **完备性** $\Longrightarrow$ Cauchy 序列收敛；
> 3. **连续性**（压缩 $\Rightarrow$ Lipschitz $\Rightarrow$ 连续） $\Longrightarrow$ 极限点是不动点；
> 4. **压缩性再次使用** $\Longrightarrow$ 不动点唯一。
>
> 该证明是**构造性**的：不仅证明存在性，还给出迭代算法以及收敛速率（线性收敛，率为 $k$）。

> [!warning] 各条件的必要性
> - **完备性不可去**：在 $X = (0, 1)$（带通常距离，不完备）上，$T(x) = x/2$ 是压缩映射，但其"不动点" $0 \notin X$。
> - **$k < 1$ 不可放宽至 $k = 1$**：$T(x) = x + 1$ 在 $\mathbb{R}$ 上满足 $|T(x) - T(y)| = |x - y|$（$k = 1$），但无不动点。
> - **$T$ 必须将 $X$ 映入自身**：若 $T: X \to Y \supsetneq X$，迭代可能跳出 $X$，定理失效。

---

## 应用

### 应用一：Picard–Lindelöf 定理（常微分方程局部存在唯一性）

考虑初值问题
$$\begin{cases} y'(t) = f(t, y(t)), \\ y(t_0) = y_0, \end{cases}$$
其中 $f: [t_0 - a, t_0 + a] \times \overline{B}(y_0, b) \to \mathbb{R}^n$ 连续，且关于 $y$ 满足 Lipschitz 条件
$$\|f(t, y_1) - f(t, y_2)\| \leq L \|y_1 - y_2\|.$$

#### 思路

将 ODE 转化为积分方程：
$$y(t) = y_0 + \int_{t_0}^{t} f(s, y(s)) \, ds.$$

定义算子 $T$ 作用于连续函数空间：
$$(T\varphi)(t) = y_0 + \int_{t_0}^{t} f(s, \varphi(s)) \, ds.$$

#### 应用 Banach 不动点定理

- **空间**：取 $X = \{\varphi \in C([t_0 - h, t_0 + h]; \mathbb{R}^n) : \|\varphi - y_0\|_\infty \leq b\}$，配上上确界范数诱导的度量。
- **完备性**：$C([t_0 - h, t_0 + h]; \mathbb{R}^n)$ 在上确界范数下完备，$X$ 是其闭子集，故 $X$ 完备。
- **压缩性**：当 $h$ 充分小（具体地 $h < 1/L$）时，
$$
\|T\varphi - T\psi\|_\infty \leq h \cdot L \cdot \|\varphi - \psi\|_\infty,
$$
即 $T$ 为压缩常数 $k = hL < 1$ 的压缩映射。

由 Banach 不动点定理，存在唯一 $y \in X$ 满足 $Ty = y$，即原 ODE 在 $[t_0 - h, t_0 + h]$ 上存在唯一解。

> [!important] 不动点定理为何"恰好"适用
> ODE 解的存在唯一性问题，本质上就是寻找积分算子 $T$ 的不动点。压缩条件来自 $f$ 的 Lipschitz 性，完备性来自 $C$ 空间的标准结果。两者的结合精确对应了 Banach 不动点定理的假设。

---

### 应用二：Newton 迭代法的局部收敛性

设 $g: \mathbb{R} \to \mathbb{R}$ 二次连续可微，$x^*$ 为方程 $g(x) = 0$ 的单根（即 $g'(x^*) \neq 0$）。Newton 迭代式为
$$x_{n+1} = N(x_n), \quad N(x) := x - \frac{g(x)}{g'(x)}.$$

#### 压缩性的验证

计算
$$N'(x) = \frac{g(x) g''(x)}{[g'(x)]^2}.$$

在 $x^*$ 处，$g(x^*) = 0$，故 $N'(x^*) = 0$。由连续性，存在 $x^*$ 的邻域 $U$ 及 $k < 1$，使得 $|N'(x)| \leq k$ 对一切 $x \in U$ 成立。

由中值定理，$N$ 在闭邻域 $\overline{U}$ 上压缩。

#### 应用 Banach 不动点定理

取 $X = \overline{U}$（取适当紧邻域使 $N(X) \subseteq X$），则 $(X, |\cdot|)$ 完备，$N: X \to X$ 压缩。由 Banach 不动点定理，$N$ 在 $X$ 中有唯一不动点，即 $x^*$，且初值充分接近 $x^*$ 时 Newton 迭代收敛于 $x^*$。

> [!info] Newton 法的"超线性"收敛
> 标准 Banach 不动点定理只保证线性收敛（率为 $k$）。但因为 $N'(x^*) = 0$，Newton 法实际具有**二次收敛**速率：$|x_{n+1} - x^*| \leq C |x_n - x^*|^2$。这一额外的速率需独立分析，不能直接从不动点定理读出。

---

### 应用三：线性方程组的迭代解法（Jacobi / Gauss-Seidel 迭代收敛性）

设线性方程组 $A\mathbf{x} = \mathbf{b}$，将 $A$ 分解为 $A = M - N$（$M$ 可逆且易求逆），则
$$\mathbf{x} = M^{-1} N \mathbf{x} + M^{-1} \mathbf{b}.$$

定义 $T(\mathbf{x}) = M^{-1} N \mathbf{x} + M^{-1} \mathbf{b}$。

#### 压缩性的判据

在某向量范数 $\|\cdot\|$ 下，
$$\|T(\mathbf{x}) - T(\mathbf{y})\| = \|M^{-1} N (\mathbf{x} - \mathbf{y})\| \leq \|M^{-1} N\| \cdot \|\mathbf{x} - \mathbf{y}\|.$$

故 $T$ 在 $(\mathbb{R}^n, \|\cdot\|)$ 上压缩 $\iff \|M^{-1} N\| < 1$。

#### 结论

由 Banach 不动点定理，当 $\|M^{-1} N\| < 1$ 时，迭代格式 $\mathbf{x}_{n+1} = T(\mathbf{x}_n)$ 对任意初始向量收敛于方程组的唯一解。

| 迭代方法 | $M$ 的选取 |
|---------|-----------|
| Jacobi 迭代 | $M = D$（$A$ 的对角部分） |
| Gauss-Seidel 迭代 | $M = D + L$（下三角部分） |

---

### 应用四：积分方程的可解性（Volterra 型）

考虑第二类 Volterra 积分方程
$$\varphi(t) = f(t) + \lambda \int_{a}^{t} K(t, s) \varphi(s) \, ds, \quad t \in [a, b],$$
其中 $f \in C[a, b]$，$K \in C([a, b]^2)$。

定义 $T: C[a, b] \to C[a, b]$ 为
$$(T\varphi)(t) = f(t) + \lambda \int_{a}^{t} K(t, s) \varphi(s) \, ds.$$

#### 关键技巧：等价范数

直接估计得 $|\lambda| \cdot \|K\|_\infty \cdot (b - a)$，仅当此值 $< 1$ 时压缩，限制了 $\lambda$ 的范围。

**改进**：引入加权范数
$$\|\varphi\|_\beta := \sup_{t \in [a, b]} e^{-\beta(t - a)} |\varphi(t)|, \quad \beta > 0.$$

此范数与上确界范数等价，故 $(C[a, b], \|\cdot\|_\beta)$ 完备。经计算，
$$\|T\varphi - T\psi\|_\beta \leq \frac{|\lambda| \cdot \|K\|_\infty}{\beta} \|\varphi - \psi\|_\beta.$$

取 $\beta$ 充分大（如 $\beta > |\lambda| \cdot \|K\|_\infty$），$T$ 在 $\|\cdot\|_\beta$ 下压缩。

#### 结论

由 Banach 不动点定理，**对任意 $\lambda \in \mathbb{R}$**，Volterra 方程都有唯一解 $\varphi \in C[a, b]$。

> [!tip] 等价范数技巧的威力
> 通过更换为等价的加权范数（Bielecki 范数），可以"人为地"放大压缩常数的灵活性，从而扩大定理的适用范围。这是泛函分析中一个非常重要的技术。

---

## 总结表：各应用对应的关键映射

| 应用领域 | 度量空间 $X$ | 压缩映射 $T$ | 不动点的含义 |
|---------|------------|-------------|-------------|
| ODE 局部解 | $C([t_0 - h, t_0 + h])$ 中闭球 | $(T\varphi)(t) = y_0 + \int_{t_0}^t f(s, \varphi(s))ds$ | ODE 的解 |
| Newton 法 | $\overline{U} \subset \mathbb{R}$ | $N(x) = x - g(x)/g'(x)$ | 方程 $g(x) = 0$ 的根 |
| 线性方程组 | $\mathbb{R}^n$ | $T(\mathbf{x}) = M^{-1}N\mathbf{x} + M^{-1}\mathbf{b}$ | $A\mathbf{x} = \mathbf{b}$ 的解 |
| Volterra 方程 | $(C[a,b], \|\cdot\|_\beta)$ | $(T\varphi)(t) = f(t) + \lambda \int_a^t K(t,s)\varphi(s)ds$ | 积分方程的解 |

> [!tip] 统一的方法论
> Banach 不动点定理的应用都遵循同一模式：
> 1. **建模**：将待求对象（解、根、不动点）表达为某算子的不动点；
> 2. **空间**：选取合适的完备度量空间，使待求对象落在其中；
> 3. **压缩**：通过选取参数（步长、范数权重等）使算子成为压缩映射；
> 4. **结论**：得到存在唯一性 + 迭代算法 + 误差估计。
