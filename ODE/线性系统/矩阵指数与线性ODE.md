---
title: 矩阵指数函数与线性微分方程
date: 2026-04-14
tags:
  - 线性代数
  - 微分方程
  - 矩阵指数
  - 常微分方程
  - Jordan标准形
---

# 矩阵指数函数与线性微分方程

## 预备定义

> [!note] 矩阵范数（operator norm）
> 设 $A \in \mathbb{R}^{n \times n}$（或 $\mathbb{C}^{n \times n}$）。$A$ 的**算子范数**（operator norm）定义为
> $$\|A\| = \sup_{\mathbf{x} \neq 0} \frac{\|A\mathbf{x}\|}{\|\mathbf{x}\|}$$
> 其中 $\|\cdot\|$ 为 $\mathbb{R}^n$ 上的某一范数。算子范数满足**次可乘性**（submultiplicativity）：
> $$\|AB\| \leq \|A\|\,\|B\|$$

> [!note] 矩阵级数的收敛
> 设 $\{A_k\}_{k=0}^{\infty}$ 为矩阵序列，$A_k \in \mathbb{R}^{n \times n}$。称级数 $\sum_{k=0}^{\infty} A_k$ **绝对收敛**，若
> $$\sum_{k=0}^{\infty} \|A_k\| < \infty$$
> 绝对收敛蕴含收敛（因为 $\mathbb{R}^{n \times n}$ 关于任一矩阵范数是完备的）。

> [!note] 矩阵指数函数（matrix exponential）
> 设 $A \in \mathbb{R}^{n \times n}$。$A$ 的**矩阵指数函数**定义为
> $$e^{A} = \exp(A) = \sum_{k=0}^{\infty} \frac{A^k}{k!} = I + A + \frac{A^2}{2!} + \frac{A^3}{3!} + \cdots$$
> 其中 $A^0 = I$（单位矩阵）。

> [!note] 一阶线性常微分方程组
> 设 $A \in \mathbb{R}^{n \times n}$ 为常数矩阵，$\mathbf{x}(t) \in \mathbb{R}^n$。**齐次线性常微分方程组**的初值问题（initial value problem, IVP）为
> $$\begin{cases} \mathbf{x}'(t) = A\,\mathbf{x}(t) \\ \mathbf{x}(0) = \mathbf{x}_0 \end{cases}$$
> 其中 $\mathbf{x}_0 \in \mathbb{R}^n$ 为给定的初始值。

---

## 定理

**(i)** 对任意 $A \in \mathbb{R}^{n \times n}$，矩阵级数 $\sum_{k=0}^{\infty} \dfrac{A^k}{k!}$ 绝对收敛，故 $e^A$ 是良定义的。

**(ii)** 矩阵指数函数满足以下性质：
- $e^{0} = I$
- 若 $AB = BA$，则 $e^{A+B} = e^A e^B$
- $e^{(s+t)A} = e^{sA}\,e^{tA}$，对一切 $s, t \in \mathbb{R}$ 成立
- $(e^A)^{-1} = e^{-A}$

**(iii)**（**微分性质**）设 $A \in \mathbb{R}^{n \times n}$ 为常数矩阵。则
$$\frac{d}{dt} e^{tA} = A\,e^{tA} = e^{tA}\,A$$

**(iv)**（**齐次方程的解**）初值问题 $\mathbf{x}' = A\mathbf{x}$，$\mathbf{x}(0) = \mathbf{x}_0$ 的**唯一解**为
$$\mathbf{x}(t) = e^{tA}\,\mathbf{x}_0$$

**(v)**（**非齐次方程：常数变易法**）初值问题
$$\mathbf{x}'(t) = A\,\mathbf{x}(t) + \mathbf{f}(t), \qquad \mathbf{x}(0) = \mathbf{x}_0$$
的唯一解为
$$\mathbf{x}(t) = e^{tA}\,\mathbf{x}_0 + \int_0^t e^{(t-s)A}\,\mathbf{f}(s)\,ds$$

---

## 第(i)部分的证明：收敛性

**目标**：证明 $\sum_{k=0}^{\infty} \dfrac{\|A^k\|}{k!} < \infty$。

由次可乘性，$\|A^k\| \leq \|A\|^k$。因此

$$\sum_{k=0}^{\infty} \frac{\|A^k\|}{k!} \leq \sum_{k=0}^{\infty} \frac{\|A\|^k}{k!} = e^{\|A\|} < \infty$$

右端是标量指数函数级数，已知收敛。故矩阵级数绝对收敛。$\square$

> [!info] 为何收敛性如此直接
> 关键在于次可乘性将矩阵级数的收敛问题**归约**为标量级数的收敛问题。阶乘 $k!$ 增长远快于 $\|A\|^k$，这保证了对**任意**矩阵 $A$（无论范数多大）级数都收敛。

---

## 第(ii)部分的证明：基本性质

### 性质 1：$e^0 = I$

$$e^0 = \sum_{k=0}^{\infty} \frac{0^k}{k!} = I + 0 + 0 + \cdots = I \quad \square$$

### 性质 2：若 $AB = BA$，则 $e^{A+B} = e^A e^B$

**已知**：$A$ 与 $B$ 可交换。

由绝对收敛，可以重排级数乘积（Cauchy 乘积）：

$$e^A e^B = \left(\sum_{j=0}^{\infty} \frac{A^j}{j!}\right)\left(\sum_{k=0}^{\infty} \frac{B^k}{k!}\right) = \sum_{m=0}^{\infty} \sum_{j+k=m} \frac{A^j B^k}{j!\,k!}$$

因为 $AB = BA$，所以二项式定理对矩阵成立：

$$\sum_{j+k=m} \frac{A^j B^k}{j!\,k!} = \frac{1}{m!}\sum_{j=0}^{m} \binom{m}{j} A^j B^{m-j} = \frac{(A+B)^m}{m!}$$

故

$$e^A e^B = \sum_{m=0}^{\infty} \frac{(A+B)^m}{m!} = e^{A+B} \quad \square$$

> [!warning] 交换性条件不可省略
> 若 $AB \neq BA$，一般**不成立** $e^{A+B} = e^A e^B$。例如取
> $$A = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}, \quad B = \begin{pmatrix} 0 & 0 \\ 1 & 0 \end{pmatrix}$$
> 可验证 $e^{A+B} \neq e^A e^B$。正确的一般公式由 **Baker-Campbell-Hausdorff 公式**给出。

### 性质 3：$e^{(s+t)A} = e^{sA}\,e^{tA}$

$sA$ 和 $tA$ 显然可交换（$sA \cdot tA = st A^2 = tA \cdot sA$），故由性质 2，

$$e^{(s+t)A} = e^{sA + tA} = e^{sA}\,e^{tA} \quad \square$$

### 性质 4：$(e^A)^{-1} = e^{-A}$

由性质 3（取 $s = 1$，$t = -1$），

$$e^A e^{-A} = e^{A + (-A)} = e^0 = I$$

同理 $e^{-A} e^A = I$。故 $e^{-A}$ 为 $e^A$ 的逆矩阵。$\square$

> [!important] 矩阵指数恒可逆
> 性质 4 表明 $e^A$ 对**任意** $A$ 都是可逆矩阵，即 $e^A \in \mathrm{GL}(n)$。事实上，$\det(e^A) = e^{\mathrm{tr}(A)} > 0$（**Jacobi 公式**）。

---

## 第(iii)部分的证明：微分性质

**目标**：证明 $\dfrac{d}{dt} e^{tA} = A\,e^{tA}$。

逐项对 $t$ 求导（级数一致收敛保证了逐项求导的合法性）：

$$\frac{d}{dt} e^{tA} = \frac{d}{dt} \sum_{k=0}^{\infty} \frac{(tA)^k}{k!} = \frac{d}{dt} \sum_{k=0}^{\infty} \frac{t^k A^k}{k!} = \sum_{k=1}^{\infty} \frac{k\,t^{k-1} A^k}{k!} = \sum_{k=1}^{\infty} \frac{t^{k-1} A^k}{(k-1)!}$$

令 $m = k - 1$：

$$= \sum_{m=0}^{\infty} \frac{t^m A^{m+1}}{m!} = A \sum_{m=0}^{\infty} \frac{(tA)^m}{m!} = A\,e^{tA}$$

由于 $A$ 与 $e^{tA}$ 可交换（$e^{tA}$ 是 $A$ 的幂级数），同理可得 $= e^{tA}\,A$。$\square$

> [!info] 逐项求导的合法性
> 设 $S_N(t) = \sum_{k=0}^{N} \frac{t^k A^k}{k!}$。其导数级数满足
> $$\sum_{k=1}^{\infty} \left\|\frac{k\,t^{k-1} A^k}{k!}\right\| \leq \sum_{k=1}^{\infty} \frac{|t|^{k-1} \|A\|^k}{(k-1)!} = \|A\|\,e^{|t|\,\|A\|} < \infty$$
> 对任意有界区间上一致收敛，故逐项求导合法。

---

## 第(iv)部分的证明：齐次方程的解

**目标**：证明 $\mathbf{x}(t) = e^{tA}\,\mathbf{x}_0$ 是 $\mathbf{x}' = A\mathbf{x}$，$\mathbf{x}(0) = \mathbf{x}_0$ 的唯一解。

### 存在性

令 $\mathbf{x}(t) = e^{tA}\,\mathbf{x}_0$。验证：

**初始条件**：$\mathbf{x}(0) = e^{0 \cdot A}\,\mathbf{x}_0 = I \cdot \mathbf{x}_0 = \mathbf{x}_0$。 ✓

**满足方程**：由第(iii)部分的微分性质，

$$\mathbf{x}'(t) = \frac{d}{dt}\left(e^{tA}\,\mathbf{x}_0\right) = A\,e^{tA}\,\mathbf{x}_0 = A\,\mathbf{x}(t) \quad \checkmark$$

### 唯一性

设 $\mathbf{y}(t)$ 为任意满足 $\mathbf{y}' = A\mathbf{y}$，$\mathbf{y}(0) = \mathbf{x}_0$ 的解。定义辅助函数

$$\mathbf{z}(t) = e^{-tA}\,\mathbf{y}(t)$$

对 $\mathbf{z}(t)$ 求导（乘积法则）：

$$\mathbf{z}'(t) = \frac{d}{dt}\left(e^{-tA}\right)\,\mathbf{y}(t) + e^{-tA}\,\mathbf{y}'(t) = -A\,e^{-tA}\,\mathbf{y}(t) + e^{-tA}\,A\,\mathbf{y}(t)$$

$$= e^{-tA}\left(-A + A\right)\mathbf{y}(t) = \mathbf{0}$$

> [!info] 为何 $-Ae^{-tA}$ 可以提取为 $e^{-tA}(-A)$
> 因为 $A$ 与 $e^{-tA}$ 可交换（$e^{-tA}$ 是 $A$ 的幂级数），所以
> $$A\,e^{-tA} = e^{-tA}\,A$$

故 $\mathbf{z}(t)$ 为常数，即 $\mathbf{z}(t) = \mathbf{z}(0) = e^{0}\,\mathbf{y}(0) = \mathbf{x}_0$。

因此

$$e^{-tA}\,\mathbf{y}(t) = \mathbf{x}_0 \implies \mathbf{y}(t) = e^{tA}\,\mathbf{x}_0$$

这与 $\mathbf{x}(t)$ 一致，故解唯一。$\square$

> [!tip] 与标量情形的类比
> 标量 ODE $x' = ax$，$x(0) = x_0$ 的唯一解为 $x(t) = e^{at}\,x_0$。矩阵指数将这一公式**完美推广**到高维情形。唯一性证明中的 $\mathbf{z}(t) = e^{-tA}\mathbf{y}(t)$ 技巧，类比于标量情形中乘以 $e^{-at}$ 的积分因子法。

---

## 第(v)部分的证明：常数变易法

**目标**：证明非齐次方程 $\mathbf{x}' = A\mathbf{x} + \mathbf{f}(t)$，$\mathbf{x}(0) = \mathbf{x}_0$ 的解为

$$\mathbf{x}(t) = e^{tA}\,\mathbf{x}_0 + \int_0^t e^{(t-s)A}\,\mathbf{f}(s)\,ds \quad \cdots (\star)$$

### 推导思路

设 $\mathbf{x}(t)$ 为解，令

$$\mathbf{v}(t) = e^{-tA}\,\mathbf{x}(t)$$

对 $\mathbf{v}(t)$ 求导：

$$\mathbf{v}'(t) = -A\,e^{-tA}\,\mathbf{x}(t) + e^{-tA}\,\mathbf{x}'(t) = -A\,e^{-tA}\,\mathbf{x}(t) + e^{-tA}\left(A\mathbf{x}(t) + \mathbf{f}(t)\right)$$

$$= e^{-tA}\,\mathbf{f}(t)$$

两端从 $0$ 积分到 $t$：

$$\mathbf{v}(t) - \mathbf{v}(0) = \int_0^t e^{-sA}\,\mathbf{f}(s)\,ds$$

$$e^{-tA}\,\mathbf{x}(t) - \mathbf{x}_0 = \int_0^t e^{-sA}\,\mathbf{f}(s)\,ds$$

两端左乘 $e^{tA}$：

$$\mathbf{x}(t) = e^{tA}\,\mathbf{x}_0 + \int_0^t e^{tA}\,e^{-sA}\,\mathbf{f}(s)\,ds = e^{tA}\,\mathbf{x}_0 + \int_0^t e^{(t-s)A}\,\mathbf{f}(s)\,ds$$

这就是 $(\star)$ 式。

### 验证

反过来验证 $(\star)$ 确实满足方程和初始条件。

**初始条件**：$\mathbf{x}(0) = e^0 \mathbf{x}_0 + \int_0^0 (\cdots)\,ds = \mathbf{x}_0$。 ✓

**满足方程**：对 $(\star)$ 求导。记 $\mathbf{x}(t) = e^{tA}\,\mathbf{x}_0 + \mathbf{w}(t)$，其中

$$\mathbf{w}(t) = \int_0^t e^{(t-s)A}\,\mathbf{f}(s)\,ds = e^{tA}\int_0^t e^{-sA}\,\mathbf{f}(s)\,ds$$

由 Leibniz 积分法则：

$$\mathbf{w}'(t) = A\,e^{tA}\int_0^t e^{-sA}\,\mathbf{f}(s)\,ds + e^{tA}\,e^{-tA}\,\mathbf{f}(t) = A\,\mathbf{w}(t) + \mathbf{f}(t)$$

故

$$\mathbf{x}'(t) = A\,e^{tA}\,\mathbf{x}_0 + A\,\mathbf{w}(t) + \mathbf{f}(t) = A\left(e^{tA}\,\mathbf{x}_0 + \mathbf{w}(t)\right) + \mathbf{f}(t) = A\,\mathbf{x}(t) + \mathbf{f}(t) \quad \checkmark$$

唯一性由与第(iv)部分相同的论证可得。$\square$

---

## 附录：矩阵指数的计算方法

矩阵指数 $e^{tA}$ 在理论上由无穷级数定义，但在实际计算中，通常采用以下方法。

### 方法一：对角化

**适用条件**：$A$ 可对角化，即 $A = P D P^{-1}$，其中 $D = \mathrm{diag}(\lambda_1, \ldots, \lambda_n)$。

此时

$$e^{tA} = P\,e^{tD}\,P^{-1} = P\,\mathrm{diag}(e^{\lambda_1 t}, \ldots, e^{\lambda_n t})\,P^{-1}$$

> [!abstract] 引理：$e^{PBP^{-1}} = P\,e^B\,P^{-1}$
> 由 $(PBP^{-1})^k = PB^k P^{-1}$（归纳可证），代入级数得
> $$e^{PBP^{-1}} = \sum_{k=0}^{\infty} \frac{(PBP^{-1})^k}{k!} = P\left(\sum_{k=0}^{\infty} \frac{B^k}{k!}\right)P^{-1} = P\,e^B\,P^{-1} \quad \square$$

> [!info] 计算实例
> 设 $A = \begin{pmatrix} 1 & 0 \\ 0 & 2 \end{pmatrix}$（已经是对角矩阵）。则
> $$e^{tA} = \begin{pmatrix} e^t & 0 \\ 0 & e^{2t} \end{pmatrix}$$
> 方程 $\mathbf{x}' = A\mathbf{x}$，$\mathbf{x}(0) = (1, 3)^T$ 的解为 $\mathbf{x}(t) = (e^t, 3e^{2t})^T$。

### 方法二：Jordan 标准形

**适用条件**：$A$ 不可对角化。设 $A = P J P^{-1}$，其中 $J$ 为 Jordan 标准形。

$$e^{tA} = P\,e^{tJ}\,P^{-1}$$

对每个 Jordan 块 $J_m(\lambda) = \lambda I + N$（其中 $N$ 为幂零矩阵，$N^m = 0$），

$$e^{tJ_m(\lambda)} = e^{\lambda t}\,e^{tN} = e^{\lambda t} \begin{pmatrix} 1 & t & \frac{t^2}{2!} & \cdots & \frac{t^{m-1}}{(m-1)!} \\ 0 & 1 & t & \cdots & \frac{t^{m-2}}{(m-2)!} \\ \vdots & & \ddots & \ddots & \vdots \\ 0 & 0 & \cdots & 1 & t \\ 0 & 0 & \cdots & 0 & 1 \end{pmatrix}$$

> [!info] 计算实例：$2 \times 2$ Jordan 块
> 设 $A = \begin{pmatrix} 3 & 1 \\ 0 & 3 \end{pmatrix} = 3I + N$，其中 $N = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}$，$N^2 = 0$。
>
> 因为 $3I$ 与 $N$ 可交换，故
> $$e^{tA} = e^{3tI}\,e^{tN} = e^{3t}\begin{pmatrix} 1 & t \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} e^{3t} & te^{3t} \\ 0 & e^{3t} \end{pmatrix}$$

### 方法三：Cayley-Hamilton 定理

**适用条件**：低维矩阵（$n = 2, 3$），特征多项式已知。

由 Cayley-Hamilton 定理，$A$ 满足自身的特征方程 $p(A) = 0$，因此 $A$ 的高次幂可以用 $I, A, \ldots, A^{n-1}$ 线性表示。

对 $2 \times 2$ 矩阵，$e^{tA}$ 可以写成

$$e^{tA} = \alpha(t)\,I + \beta(t)\,A$$

其中 $\alpha(t)$, $\beta(t)$ 由特征值确定：

- 若 $\lambda_1 \neq \lambda_2$：$\alpha(t) = \dfrac{\lambda_2 e^{\lambda_1 t} - \lambda_1 e^{\lambda_2 t}}{\lambda_2 - \lambda_1}$，$\beta(t) = \dfrac{e^{\lambda_1 t} - e^{\lambda_2 t}}{\lambda_1 - \lambda_2}$
- 若 $\lambda_1 = \lambda_2 = \lambda$：$\alpha(t) = (1 - \lambda t)\,e^{\lambda t}$，$\beta(t) = t\,e^{\lambda t}$

---

## 综合实例

> [!info] 完整示例：求解二维线性系统
> 考虑方程组
> $$\mathbf{x}' = \begin{pmatrix} 0 & 1 \\ -2 & -3 \end{pmatrix}\mathbf{x}, \qquad \mathbf{x}(0) = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$$
>
> **第一步**：求特征值。$\det(A - \lambda I) = \lambda^2 + 3\lambda + 2 = (\lambda + 1)(\lambda + 2) = 0$，故 $\lambda_1 = -1$，$\lambda_2 = -2$。
>
> **第二步**：求特征向量。
> - $\lambda_1 = -1$：$(A + I)\mathbf{v} = 0 \Rightarrow \mathbf{v}_1 = (1, -1)^T$
> - $\lambda_2 = -2$：$(A + 2I)\mathbf{v} = 0 \Rightarrow \mathbf{v}_2 = (1, -2)^T$
>
> **第三步**：对角化。$A = PDP^{-1}$，其中
> $$P = \begin{pmatrix} 1 & 1 \\ -1 & -2 \end{pmatrix}, \quad D = \begin{pmatrix} -1 & 0 \\ 0 & -2 \end{pmatrix}, \quad P^{-1} = \begin{pmatrix} 2 & 1 \\ -1 & -1 \end{pmatrix}$$
>
> **第四步**：计算 $e^{tA}$。
> $$e^{tA} = P \begin{pmatrix} e^{-t} & 0 \\ 0 & e^{-2t} \end{pmatrix} P^{-1} = \begin{pmatrix} 2e^{-t} - e^{-2t} & e^{-t} - e^{-2t} \\ -2e^{-t} + 2e^{-2t} & -e^{-t} + 2e^{-2t} \end{pmatrix}$$
>
> **第五步**：写出解。
> $$\mathbf{x}(t) = e^{tA}\begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 2e^{-t} - e^{-2t} \\ -2e^{-t} + 2e^{-2t} \end{pmatrix}$$
>
> **验证**：$\mathbf{x}(0) = (2 - 1,\, -2 + 2)^T = (1, 0)^T$。 ✓
> 且当 $t \to \infty$ 时，$\mathbf{x}(t) \to \mathbf{0}$（因为两个特征值都为负数，系统渐近稳定）。

---

## 证明思路总结

> [!tip] 关键思想
> 1. **矩阵指数是标量指数的自然推广**：用幂级数 $\sum \frac{A^k}{k!}$ 定义，其收敛性由次可乘性和标量级数 $e^{\|A\|}$ 保证。
> 2. **微分性质是核心**：$\frac{d}{dt}e^{tA} = Ae^{tA}$ 是连接矩阵指数与微分方程的桥梁——它使得 $e^{tA}\mathbf{x}_0$ 自动满足 $\mathbf{x}' = A\mathbf{x}$。
> 3. **唯一性的证明技巧**：构造 $\mathbf{z}(t) = e^{-tA}\mathbf{y}(t)$ 并证明 $\mathbf{z}' = 0$，这是**积分因子法**在矩阵情形的推广。
> 4. **常数变易法**直接推广标量的 $x(t) = e^{at}x_0 + \int_0^t e^{a(t-s)}f(s)\,ds$，关键是令 $\mathbf{v}(t) = e^{-tA}\mathbf{x}(t)$ 消去齐次部分。
> 5. **计算方法**的核心思想是**化简 $A$ 的结构**：对角化、Jordan 分解、或 Cayley-Hamilton 降幂，将矩阵指数归约为标量指数的简单组合。

> [!warning] 常见误区
> - $e^{A+B} = e^A e^B$ 仅在 $AB = BA$ 时成立。对不可交换矩阵，需使用 BCH 公式或 Trotter 乘积公式 $e^{A+B} = \lim_{n\to\infty} (e^{A/n}e^{B/n})^n$。
> - $e^{tA}$ 与 $A$ 可交换，但 $e^{tA}$ 与一般矩阵 $B$ 不可交换。
> - 数值计算中，直接用幂级数截断计算 $e^A$ 是**不稳定的**。实践中通常使用 scaling and squaring 方法或 Padé 近似。
