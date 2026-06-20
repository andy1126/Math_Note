---
title: Wronskian 与 Abel 公式
date: 2026-05-28
tags:
  - 微分方程
  - ODE
  - 线性系统
  - Wronskian
  - Abel公式
  - 线性独立性
---

# Wronskian 与 Abel 公式

## 预备定义

> [!note] $n$ 阶齐次线性 ODE
> 形如
> $$y^{(n)} + a_{n-1}(t)\, y^{(n-1)} + \cdots + a_1(t)\, y' + a_0(t)\, y = 0, \quad t \in I \quad \cdots (\mathrm{H})$$
> 的方程，其中 $a_k: I \to \mathbb{R}$ 连续，$I$ 为开区间。

> [!note] Wronskian（Wroński 行列式）
> 对 $I$ 上 $n - 1$ 次可微函数 $y_1, \ldots, y_n$，定义
> $$W(t) = W[y_1, \ldots, y_n](t) := \det\begin{pmatrix} y_1 & y_2 & \cdots & y_n \\ y_1' & y_2' & \cdots & y_n' \\ \vdots & \vdots & & \vdots \\ y_1^{(n-1)} & y_2^{(n-1)} & \cdots & y_n^{(n-1)} \end{pmatrix}.$$

> [!note] 线性独立
> 称 $y_1, \ldots, y_n$ 在 $I$ 上**线性独立**，若 $\sum_k c_k y_k(t) = 0$ 对所有 $t \in I$ 蕴含 $c_1 = \cdots = c_n = 0$。

> [!abstract] 引理：行列式按列求导
> 设 $A(t) = (a_{ij}(t))$ 各列为 $\mathbf{c}_1(t), \ldots, \mathbf{c}_n(t)$。则
> $$\frac{d}{dt} \det A(t) = \sum_{j=1}^n \det(\mathbf{c}_1, \ldots, \mathbf{c}_j', \ldots, \mathbf{c}_n).$$
> 由 Leibniz 公式与 $\det$ 的多线性立刻得到。

> [!abstract] 引理：Picard-Lindelöf 唯一性
> 在 (H) 的系数连续假设下，初值问题 $y^{(k)}(t_0) = y_{0k}$（$k = 0, \ldots, n-1$）在 $I$ 上有唯一解。详见 [[Picard-Lindelöf定理]]。

---

## 定理

设 $y_1, \ldots, y_n$ 均为 (H) 在 $I$ 上的解。则：

**(i)（Abel 公式）** $W(t)$ 满足一阶线性 ODE
$$W'(t) = -a_{n-1}(t)\, W(t),$$

从而
$$W(t) = W(t_0)\, \exp\!\left(-\int_{t_0}^t a_{n-1}(s)\,ds\right), \quad t, t_0 \in I.$$

**(ii)（零-非零二分律）** $W(t)$ 要么在 $I$ 上恒为 $0$，要么处处非零。

**(iii)（线性独立性刻画）** $y_1, \ldots, y_n$ 在 $I$ 上线性独立 $\iff$ 存在 $t_0 \in I$ 使 $W(t_0) \neq 0$ $\iff$ $W(t) \neq 0$ 对所有 $t \in I$。

---

## 第(i)部分的证明：Abel 公式

### 第一步：按列求导

由引理（行列式按列求导）：
$$W'(t) = \sum_{j=1}^n \det\begin{pmatrix} y_1 & \cdots & y_j & \cdots & y_n \\ y_1' & \cdots & y_j' & \cdots & y_n' \\ \vdots & & \vdots & & \vdots \\ y_1^{(n-2)} & \cdots & y_j^{(n-2)} & \cdots & y_n^{(n-2)} \\ y_1^{(n-1)} & \cdots & \boxed{(y_j^{(n-1)})'} & \cdots & y_n^{(n-1)} \end{pmatrix}.$$

但 $(y_j^{(n-1)})' = y_j^{(n)}$，所以只有第 $n$ 行的导数项。

### 第二步：除最后一项外均消失

对 $j = 1, \ldots, n$，导数项把第 $n$ 行的 $y_j^{(n-1)}$ 替换成 $y_j^{(n)}$；其余 $n - 1$ 行未变。

> [!important] 几乎所有项都为 0 的原因
> 对 $1 \leq k \leq n - 2$，按列求导只动第 $k$ 行（$y_j^{(k-1)} \to y_j^{(k)}$），但该新行与下一行 $y_j^{(k)}$ 完全相同——行列式中两行相等故为 $0$。**真正非零的只有动到第 $n - 1$ 行（即原来含 $y_j^{(n-1)}$ 的那行）的项**。

更精确地：若按行（而非列）求导逐项展开 $W'$，导数作用到第 $k$ 行得到一个 $n \times n$ 行列式，其第 $k$ 行变为 $y_j^{(k)}$。但若 $k \leq n - 2$，新第 $k$ 行 = 原第 $k+1$ 行，行列式 = 0。仅 $k = n - 1$ 项幸存，给出
$$W'(t) = \det\begin{pmatrix} y_1 & \cdots & y_n \\ y_1' & \cdots & y_n' \\ \vdots & & \vdots \\ y_1^{(n-2)} & \cdots & y_n^{(n-2)} \\ y_1^{(n)} & \cdots & y_n^{(n)} \end{pmatrix}. \quad \cdots (\ast)$$

### 第三步：用 (H) 代换 $y_j^{(n)}$

每个 $y_j$ 满足 (H)：
$$y_j^{(n)} = -a_{n-1}(t)\, y_j^{(n-1)} - a_{n-2}(t)\, y_j^{(n-2)} - \cdots - a_0(t)\, y_j.$$

代入 $(\ast)$ 的第 $n$ 行。由行列式多线性，$W'(t)$ 拆为 $n$ 项：
$$W'(t) = -\sum_{k=0}^{n-1} a_k(t) \cdot \det\begin{pmatrix} y_1 & \cdots & y_n \\ y_1' & \cdots & y_n' \\ \vdots & & \vdots \\ y_1^{(n-2)} & \cdots & y_n^{(n-2)} \\ y_1^{(k)} & \cdots & y_n^{(k)} \end{pmatrix}.$$

### 第四步：除 $k = n - 1$ 外均为 0

对 $k = 0, 1, \ldots, n - 2$：第 $n$ 行 $y_j^{(k)}$ 与上面某一行（第 $k + 1$ 行）相同，行列式为 $0$。仅 $k = n - 1$ 项幸存：
$$W'(t) = -a_{n-1}(t) \cdot \det\begin{pmatrix} y_1 & \cdots & y_n \\ \vdots & & \vdots \\ y_1^{(n-2)} & \cdots & y_n^{(n-2)} \\ y_1^{(n-1)} & \cdots & y_n^{(n-1)} \end{pmatrix} = -a_{n-1}(t)\, W(t). \quad \square$$

### 第五步：解一阶线性 ODE

$W' = -a_{n-1}(t)\, W$ 的通解（积分因子法）：
$$W(t) = W(t_0)\, \exp\!\left(-\int_{t_0}^t a_{n-1}(s)\,ds\right). \quad \square$$

---

## 第(ii)部分的证明：零-非零二分律

由 (i) 的 Abel 公式，$\exp(\cdots) > 0$ 永远，故
$$W(t) = 0 \iff W(t_0) = 0$$

对任意 $t_0 \in I$。即 $W$ 要么恒 $0$，要么处处非 $0$。$\square$

---

## 第(iii)部分的证明：线性独立性刻画

### "$W(t_0) \neq 0 \Rightarrow$ 线性独立"

设 $\sum c_k y_k(t) \equiv 0$。逐次求导至 $n - 1$ 阶并在 $t_0$ 取值：
$$\sum_k c_k y_k^{(j)}(t_0) = 0, \quad j = 0, 1, \ldots, n - 1.$$

矩阵形式：
$$\begin{pmatrix} y_1(t_0) & \cdots & y_n(t_0) \\ \vdots & & \vdots \\ y_1^{(n-1)}(t_0) & \cdots & y_n^{(n-1)}(t_0) \end{pmatrix} \begin{pmatrix} c_1 \\ \vdots \\ c_n \end{pmatrix} = \mathbf{0}.$$

行列式 $W(t_0) \neq 0$ 故矩阵可逆，必 $c = 0$。即 $y_1, \ldots, y_n$ 线性独立。$\square$

### "线性独立 $\Rightarrow W(t_0) \neq 0$"（反证法）

假设 $W(t_0) = 0$，由 (ii) $W \equiv 0$。但需推出存在非平凡 $c$ 使 $\sum c_k y_k \equiv 0$。

由 $W(t_0) = 0$，存在非零 $\mathbf{c} = (c_1, \ldots, c_n)$ 使
$$\sum_k c_k y_k^{(j)}(t_0) = 0, \quad j = 0, \ldots, n - 1.$$

设 $z(t) = \sum_k c_k y_k(t)$。由 (H) 的线性性，$z$ 也满足 (H)，且初值
$$z(t_0) = z'(t_0) = \cdots = z^{(n-1)}(t_0) = 0.$$

由唯一性引理（Picard-Lindelöf），$z \equiv 0$ 在 $I$ 上。

> [!important] 唯一性的关键作用
> 第 (iii) 步反向证明需要：满足 (H) 且初值全零的解必恒零。这正是 ODE 唯一性（Picard-Lindelöf）的内容。**这一步用到了 $y_j$ 是 (H) 的解**——不假设这个，"Wronskian = 0 $\Rightarrow$ 线性相关"不成立（见反例）。

故 $\sum c_k y_k \equiv 0$，$\mathbf{c} \neq 0$，即 $y_1, \ldots, y_n$ 线性**相关**。**矛盾**。

故 $W(t_0) \neq 0$。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> Abel 公式的核心是**两次"零行列式坍缩"**：
> 1. 按列求导后，所有不动到第 $n - 1$ 行的项因为"两行相等"而消失，只剩 $(\ast)$；
> 2. 用 (H) 把 $y_j^{(n)}$ 用更低阶导数线性表示，再次按多线性展开，所有不是 $y_j^{(n-1)}$ 项也都"两行相等"地消失，只剩 $-a_{n-1} W$。
>
> 整个证明只靠**行列式多线性 + (H) 的线性表示**——一个纯代数事实。
>
> 几何含义：解空间是 $n$ 维向量空间；Wronskian 是 $n$ 个解在相空间 $(y, y', \ldots, y^{(n-1)})$ 中张成的体积；Abel 公式给出该体积演化的指数律。**$a_{n-1}$ 即相空间的"迹"（耗散率）**。

> [!warning] (iii) 中"$y_j$ 是 (H) 的解"不可省
> 反例：$y_1(t) = t^2$，$y_2(t) = t|t|$ 在 $\mathbb{R}$ 上：$y_1, y_2 \in C^1$，处处 $W = 0$（$y_2 = \pm y_1$），但 $y_1, y_2$ 线性独立（无 $c_1, c_2$ 同时使等式在 $t > 0$ 与 $t < 0$ 都成立）。
>
> 失败原因：$y_2 = t|t|$ 在 $t = 0$ 二阶不可微，不能是任何二阶线性 ODE 的解。Wronskian 法**仅对 (H) 的解才是线性独立的判定器**。

> [!info] 推论与应用
> **(1) 解空间维数**：(H) 的解空间是 $n$ 维向量空间。任取 $n$ 个线性独立解（如 $W(t_0) \neq 0$）即构成基底，称**基本解组**。
>
> **(2) 二阶情形的简洁形式**：$n = 2$，$(H): y'' + p(t) y' + q(t) y = 0$。
> $$W'(t) = -p(t) W(t) \Longrightarrow W(t) = W(t_0)\, e^{-\int_{t_0}^t p(s)\,ds}.$$
>
> **(3) 与 Liouville 公式的关系**：对线性系统 $\mathbf{x}' = A(t)\mathbf{x}$，基本矩阵 $\Phi(t)$ 的行列式满足
> $$\det \Phi(t) = \det \Phi(t_0)\, \exp\!\left(\int_{t_0}^t \operatorname{tr} A(s)\,ds\right),$$
> 这正是 [[Liouville公式]]。Wronskian + Abel 公式是其标量化形式：把 $n$ 阶 ODE 化为一阶系统后，$-a_{n-1}$ 即 $\operatorname{tr} A$。
>
> **(4) 常数变易法的基础**：用基本解组构造非齐次方程特解时，Wronskian 出现在分母（Cramer 法则解 $c_k'(t)$）。$W$ 非零保证可解性。
