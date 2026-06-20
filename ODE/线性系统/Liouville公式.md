---
title: Liouville 公式（Abel-Liouville formula）
date: 2026-04-11
tags:
  - 常微分方程
  - 线性系统
  - Wronskian
  - 行列式
  - 迹
---

# Liouville 公式

## 预备定义

> [!note] 线性 ODE 系统
> 设 $A: I \to \mathbb{R}^{n \times n}$ 为区间 $I$ 上的连续矩阵值函数。**齐次线性系统**为
> $$X'(t) = A(t)\, X(t),$$
> 其中 $X(t) \in \mathbb{R}^{n \times n}$。当 $X(t)$ 为列向量 $x(t) \in \mathbb{R}^n$ 时，即 $x' = A(t)\,x$。

> [!note] 基本矩阵（fundamental matrix）
> 设 $\Phi(t) \in \mathbb{R}^{n \times n}$ 满足 $\Phi' = A(t)\, \Phi$ 且 $\det \Phi(t_0) \neq 0$ 对某个 $t_0 \in I$ 成立。则 $\Phi$ 的 $n$ 个列向量构成解空间的一组基，称 $\Phi$ 为**基本矩阵**。

> [!note] Wronskian
> 对基本矩阵 $\Phi(t)$，其**Wronskian** 定义为
> $$W(t) = \det \Phi(t).$$
> 更一般地，对 $n$ 个解 $x_1, \ldots, x_n$，$W(t) = \det\big[x_1(t) \mid \cdots \mid x_n(t)\big]$。

> [!note] 矩阵的迹
> 方阵 $A = (a_{ij})_{n \times n}$ 的**迹**（trace）为
> $$\operatorname{tr}(A) = \sum_{i=1}^{n} a_{ii}.$$

> [!abstract] 引理：行列式对矩阵的微分（Jacobi 公式的特殊情形）
> 设 $\Phi(t)$ 为可微矩阵值函数，列向量记为 $\varphi_1(t), \ldots, \varphi_n(t)$。则
> $$\frac{d}{dt} \det \Phi(t) = \sum_{k=1}^{n} \det\big[\varphi_1(t) \mid \cdots \mid \varphi_k'(t) \mid \cdots \mid \varphi_n(t)\big].$$
> 即**逐列求导再求和**：每次对第 $k$ 列求导，其余列不动，将所有 $n$ 个行列式相加。

**证明**：行列式是列向量的多重线性函数。对 $n$-线性函数 $D(\varphi_1, \ldots, \varphi_n) = \det[\varphi_1 \mid \cdots \mid \varphi_n]$ 应用乘积法则（Leibniz rule 的多重线性推广）即得。$\square$

---

## 定理

设 $A: I \to \mathbb{R}^{n \times n}$ 连续，$\Phi(t)$ 为 $X' = A(t)\, X$ 的基本矩阵，$W(t) = \det \Phi(t)$。则对一切 $t, t_0 \in I$，

$$\boxed{\, W(t) = W(t_0) \exp\!\left(\int_{t_0}^{t} \operatorname{tr}(A(s))\, ds\right). \,}$$

等价地，$W$ 满足一阶线性 ODE：

$$W'(t) = \operatorname{tr}(A(t))\, W(t).$$

> [!info] 直接推论
> $W(t)$ 要么恒为零，要么处处非零。因此，$n$ 个解线性无关的判据不依赖于 $t$ 的选取：在某一点线性无关等价于在整个区间上线性无关。

---

## 证明

记 $\Phi(t)$ 的列向量为 $\varphi_1(t), \ldots, \varphi_n(t)$。

### 第一步：对 $W(t)$ 求导

由引理（逐列求导），

$$W'(t) = \sum_{k=1}^{n} \det\big[\varphi_1(t) \mid \cdots \mid \varphi_k'(t) \mid \cdots \mid \varphi_n(t)\big]. \quad \cdots (\ast)$$

$\square$

### 第二步：用 ODE 替换 $\varphi_k'$

每个 $\varphi_k$ 是 $x' = A(t)\, x$ 的解，故

$$\varphi_k'(t) = A(t)\, \varphi_k(t) = \sum_{i=1}^{n} a_{ik}(t)\, \varphi_i(t),$$

其中 $a_{ik}(t)$ 是 $A(t)$ 的第 $(i,k)$ 元素（$A$ 的第 $i$ 行第 $k$ 列）。

> [!info] 矩阵乘法的列视角
> $A\varphi_k$ 是 $A$ 的各列以 $\varphi_k$ 的分量为系数的线性组合。但从列向量展开的角度，$A\varphi_k = \sum_{i} a_{ik} \varphi_i$ 表示将 $\varphi_k'$ 写成了**所有列向量** $\varphi_1, \ldots, \varphi_n$ 的线性组合。

将此代入 $(\ast)$ 中第 $k$ 项：

$$\det\big[\varphi_1 \mid \cdots \mid \varphi_k' \mid \cdots \mid \varphi_n\big] = \det\!\left[\varphi_1 \,\Big|\, \cdots \,\Big|\, \sum_{i=1}^{n} a_{ik}\, \varphi_i \,\Big|\, \cdots \,\Big|\, \varphi_n\right].$$

$\square$

### 第三步：利用行列式的多重线性与交替性

由行列式对第 $k$ 列的线性性，上式等于

$$\sum_{i=1}^{n} a_{ik}(t) \det\big[\varphi_1 \mid \cdots \mid \underbrace{\varphi_i}_{\text{第 } k \text{ 列}} \mid \cdots \mid \varphi_n\big].$$

当 $i \neq k$ 时，矩阵中有两列相同（$\varphi_i$ 同时出现在第 $i$ 列和第 $k$ 列），由行列式的**交替性**，该项为零。

仅 $i = k$ 时有非零贡献：

$$a_{kk}(t) \det\big[\varphi_1 \mid \cdots \mid \varphi_k \mid \cdots \mid \varphi_n\big] = a_{kk}(t)\, W(t).$$

$\square$

### 第四步：对 $k$ 求和

将第三步的结果代回 $(\ast)$：

$$W'(t) = \sum_{k=1}^{n} a_{kk}(t)\, W(t) = \operatorname{tr}(A(t))\, W(t). \quad \cdots (\star)$$

$\square$

### 第五步：求解一阶线性 ODE

$(\star)$ 是关于 $W$ 的一阶线性 ODE，直接积分：

$$\frac{W'(t)}{W(t)} = \operatorname{tr}(A(t)),$$

$$\ln |W(t)| - \ln |W(t_0)| = \int_{t_0}^{t} \operatorname{tr}(A(s))\, ds,$$

$$W(t) = W(t_0) \exp\!\left(\int_{t_0}^{t} \operatorname{tr}(A(s))\, ds\right).$$

> [!important] 指数函数永不为零
> 由于 $\exp(\cdot) > 0$，$W(t)$ 与 $W(t_0)$ 同号。特别地，$W(t_0) \neq 0 \iff W(t) \neq 0 \;\forall\, t \in I$。

$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本证明的核心是**行列式的多重线性与交替性**的精妙配合：
> 1. **逐列求导**：将 $W'$ 展开为 $n$ 个行列式之和，每个只对一列求导；
> 2. **ODE 代入**：用 $\varphi_k' = A\varphi_k = \sum_i a_{ik}\varphi_i$ 替换；
> 3. **交替性消去**：$i \neq k$ 时两列相同，行列式为零。仅 $i = k$ 存活，贡献 $a_{kk} W$；
> 4. **对角元求和**：$n$ 项求和恰得 $\operatorname{tr}(A)\cdot W$。
>
> 整个论证将 $n \times n$ 矩阵 ODE 的复杂信息浓缩为一个**标量一阶 ODE** $W' = \operatorname{tr}(A)\, W$，体现了**迹是行列式的无穷小版本**这一深层联系。

> [!warning] 常见误区与推广
> - **Liouville 公式不要求 $A$ 为常数**。对变系数系统同样成立，这是它的威力所在。
> - **几何解读**：$n$ 个解张成的平行体的"体积"$|W(t)|$ 按速率 $\operatorname{tr}(A)$ 指数增长或衰减。当 $\operatorname{tr}(A) = 0$（如 Hamilton 系统）时，体积守恒——这就是 **Liouville 定理**在经典力学中的体现。
> - **非齐次系统**：对 $x' = A(t)x + b(t)$，Wronskian 公式不变（非齐次项不影响齐次解的线性无关性）。
