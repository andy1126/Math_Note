---
title: 多元 Taylor 公式
date: 2026-06-18
tags:
  - 多元微积分
  - Taylor展开
  - Hessian矩阵
  - 多重指标
  - 链式法则
  - 余项估计
---

# 多元 Taylor 公式

## 预备定义

> [!note] Hessian 矩阵
> 设 $f: U \subseteq \mathbb{R}^n \to \mathbb{R}$ 为 $C^2$ 类函数。$f$ 在点 $\mathbf{x}_0 \in U$ 处的 **Hessian 矩阵**（Hessian matrix）定义为
> $$H_f(\mathbf{x}_0) = \left( \frac{\partial^2 f}{\partial x_i \partial x_j}(\mathbf{x}_0) \right)_{1 \leq i,j \leq n}.$$
> 由 Schwarz 定理（$C^2$ 条件保证混合偏导数可交换），$H_f(\mathbf{x}_0)$ 是 $n \times n$ 实对称矩阵。其二次型为
> $$\mathbf{h}^T H_f(\mathbf{x}_0)\, \mathbf{h} = \sum_{i,j=1}^n \frac{\partial^2 f}{\partial x_i \partial x_j}(\mathbf{x}_0)\, h_i h_j.$$

> [!note] 多重指标记号（multi-index notation）
> 设 $\alpha = (\alpha_1, \dots, \alpha_n) \in \mathbb{N}_0^n$（$\mathbb{N}_0 = \{0,1,2,\dots\}$）。定义：
> - $|\alpha| = \alpha_1 + \cdots + \alpha_n$（**阶数**）；
> - $\alpha! = \alpha_1! \, \alpha_2! \cdots \alpha_n!$；
> - 对 $\mathbf{h} = (h_1, \dots, h_n) \in \mathbb{R}^n$，记 $\mathbf{h}^\alpha = h_1^{\alpha_1} h_2^{\alpha_2} \cdots h_n^{\alpha_n}$；
> - **偏导数** $\displaystyle \partial^\alpha f = \frac{\partial^{|\alpha|} f}{\partial x_1^{\alpha_1} \cdots \partial x_n^{\alpha_n}}$.
>
> 这一记号的目的：一元 Taylor 公式中 $\dfrac{f^{(k)}(x_0)}{k!} h^k$ 的多元推广天然写作 $\displaystyle \frac{\partial^\alpha f(\mathbf{x}_0)}{\alpha!} \mathbf{h}^\alpha$——每一项对应一个"导数的阶在各个变量上的分布"。

> [!abstract] 引理：多重指标多项式展开公式
> 设 $\mathbf{x} = (x_1, \dots, x_n)$，$\mathbf{y} = (y_1, \dots, y_n)$。则对任意整数 $m \geq 0$，
> $$(\mathbf{x} \cdot \mathbf{y})^m = (x_1 y_1 + \cdots + x_n y_n)^m = \sum_{|\alpha| = m} \frac{m!}{\alpha!}\, \mathbf{x}^\alpha \mathbf{y}^\alpha.$$
> **证明**：由多项式定理直接展开即得。此恒等式是将 "微分算子多项式" $(\sum h_i \frac{\partial}{\partial x_i})^m$ 展开为各阶偏导数的桥梁。$\square$

前置概念见 [[偏导数与方向导数]]（偏导数、梯度、Schwarz 定理）、[[全微分与可微性]]（一阶可微）、[[多元链式法则]]（复合函数 $g(t) = f(\mathbf{x}_0 + t\mathbf{h})$ 的各阶导数）。

---

## 定理

### 二阶 Taylor 展开

设 $f: U \subseteq \mathbb{R}^n \to \mathbb{R}$ 为 $C^2$ 类函数，$U$ 为开集，$\mathbf{x}_0 \in U$。则对充分小的 $\mathbf{h} \in \mathbb{R}^n$，

$$f(\mathbf{x}_0 + \mathbf{h}) = f(\mathbf{x}_0) + \nabla f(\mathbf{x}_0) \cdot \mathbf{h} + \frac{1}{2} \mathbf{h}^T H_f(\mathbf{x}_0)\, \mathbf{h} + o(\|\mathbf{h}\|^2), \quad \cdots (1)$$

其中 $\dfrac{o(\|\mathbf{h}\|^2)}{\|\mathbf{h}\|^2} \to 0$（当 $\|\mathbf{h}\| \to 0$）。

> [!info] 二阶展开的直观
> 一元 Taylor 公式 $f(x_0 + h) = f(x_0) + f'(x_0)h + \frac{1}{2}f''(x_0)h^2 + o(h^2)$ 在多元的忠实推广：数 $f'(x_0)$ 换为梯度向量 $\nabla f(\mathbf{x}_0)$，数 $f''(x_0)$ 换为 Hessian 矩阵 $H_f(\mathbf{x}_0)$，而 $\frac{1}{2}f''(x_0)h^2$ 换为二次型 $\frac{1}{2}\mathbf{h}^T H_f(\mathbf{x}_0)\mathbf{h}$。

### 一般 $k$ 阶 Taylor 公式

设 $f: U \subseteq \mathbb{R}^n \to \mathbb{R}$ 为 $C^{k+1}$ 类函数（或 $C^k$ 类，视余项形式而定），$\mathbf{x}_0 \in U$。

**多重指标形式**：

$$f(\mathbf{x}_0 + \mathbf{h}) = \sum_{|\alpha| \leq k} \frac{\partial^\alpha f(\mathbf{x}_0)}{\alpha!}\, \mathbf{h}^\alpha + R_k(\mathbf{h}). \quad \cdots (2)$$

其中 $\sum_{|\alpha| \leq k}$ 表示对所有满足 $\alpha_1 + \cdots + \alpha_n \leq k$ 的多重指标 $\alpha$ 求和。

**三种余项形式**：

**(i) Peano 余项**（要求 $f \in C^k$）：
$$R_k(\mathbf{h}) = o(\|\mathbf{h}\|^k), \quad \|\mathbf{h}\| \to 0.$$

**(ii) Lagrange 余项**（要求 $f \in C^{k+1}$）：
$$R_k(\mathbf{h}) = \sum_{|\alpha| = k+1} \frac{\partial^\alpha f(\mathbf{x}_0 + \theta \mathbf{h})}{\alpha!}\, \mathbf{h}^\alpha,$$
其中 $\theta = \theta(\mathbf{h}) \in (0,1)$ 依赖于 $\mathbf{h}$.

**(iii) 积分余项**（要求 $f \in C^{k+1}$）：
$$R_k(\mathbf{h}) = (k+1) \sum_{|\alpha| = k+1} \frac{\mathbf{h}^\alpha}{\alpha!} \int_0^1 (1-t)^k\, \partial^\alpha f(\mathbf{x}_0 + t\mathbf{h})\, dt.$$

> [!info] "一阶 Taylor 公式"即全微分
> 当 $k = 1$ 时，$(2)$ 化为
> $$f(\mathbf{x}_0 + \mathbf{h}) = f(\mathbf{x}_0) + \nabla f(\mathbf{x}_0) \cdot \mathbf{h} + o(\|\mathbf{h}\|).$$
> 这恰是 [[全微分与可微性]] 中可微性的定义。因此，多元 Taylor 公式可以理解为**高阶可微性的定量刻画**——$f \in C^k$ 意味着它在 $\mathbf{x}_0$ 附近可被一个 $k$ 次多项式以 $o(\|\mathbf{h}\|^k)$ 精度逼近。

---

## 证明

我们给出核心证明框架：将多元问题降维为一元问题。先证二阶展开 $(1)$（最常用），再给出一般 $k$ 阶的推导要点。

### 二阶展开的证明

#### 第一步：化为一元函数

固定 $\mathbf{x}_0$ 与方向 $\mathbf{h}$（$\mathbf{h} \neq \mathbf{0}$，充分小使线段 $\mathbf{x}_0 + t\mathbf{h} \;(0 \leq t \leq 1)$ 含于 $U$）。定义

$$g(t) = f(\mathbf{x}_0 + t\mathbf{h}), \quad t \in [0,1].$$

由于 $f \in C^2(U)$，$g$ 在 $[0,1]$ 上 $C^2$（复合 $C^2$ 函数与仿射映射）。

#### 第二步：计算 $g$ 的各阶导数

由 [[多元链式法则]]：

$$
\begin{aligned}
g'(t) &= \sum_{i=1}^n \frac{\partial f}{\partial x_i}(\mathbf{x}_0 + t\mathbf{h})\, h_i = \nabla f(\mathbf{x}_0 + t\mathbf{h}) \cdot \mathbf{h}, \\[4pt]
g''(t) &= \frac{d}{dt} \left( \sum_{i=1}^n \frac{\partial f}{\partial x_i}(\mathbf{x}_0 + t\mathbf{h})\, h_i \right)
= \sum_{i,j=1}^n \frac{\partial^2 f}{\partial x_i \partial x_j}(\mathbf{x}_0 + t\mathbf{h})\, h_i h_j \\
&= \mathbf{h}^T H_f(\mathbf{x}_0 + t\mathbf{h})\, \mathbf{h}.
\end{aligned}
$$

#### 第三步：应用一元 Taylor 公式（积分余项）

对 $g$ 在 $t=0$ 处应用一元 Taylor 公式至一阶，带积分余项（通过分部积分可得）：

$$g(1) = g(0) + g'(0) + \int_0^1 (1-t)\, g''(t)\, dt. \quad \cdots (\ast)$$

代入 $g(1) = f(\mathbf{x}_0 + \mathbf{h})$、$g(0) = f(\mathbf{x}_0)$、$g'(0) = \nabla f(\mathbf{x}_0) \cdot \mathbf{h}$，以及 $g''(t)$ 的表达式：

$$f(\mathbf{x}_0 + \mathbf{h}) = f(\mathbf{x}_0) + \nabla f(\mathbf{x}_0) \cdot \mathbf{h} + \int_0^1 (1-t)\, \mathbf{h}^T H_f(\mathbf{x}_0 + t\mathbf{h})\, \mathbf{h}\, dt.$$

#### 第四步：拆出二阶主项并估计余项

将 $H_f(\mathbf{x}_0 + t\mathbf{h})$ 分解为 $H_f(\mathbf{x}_0) + E(t\mathbf{h})$，其中

$$E(t\mathbf{h}) = H_f(\mathbf{x}_0 + t\mathbf{h}) - H_f(\mathbf{x}_0).$$

代入积分项：

$$
\begin{aligned}
\int_0^1 (1-t)\, \mathbf{h}^T H_f(\mathbf{x}_0 + t\mathbf{h})\, \mathbf{h}\, dt
&= \mathbf{h}^T H_f(\mathbf{x}_0)\, \mathbf{h} \underbrace{\int_0^1 (1-t)\, dt}_{=\, 1/2} \\
&\quad + \int_0^1 (1-t)\, \mathbf{h}^T E(t\mathbf{h})\, \mathbf{h}\, dt \\[4pt]
&= \frac{1}{2} \mathbf{h}^T H_f(\mathbf{x}_0)\, \mathbf{h} + R(\mathbf{h}),
\end{aligned}
$$

其中余项 $R(\mathbf{h}) = \displaystyle \int_0^1 (1-t)\, \mathbf{h}^T E(t\mathbf{h})\, \mathbf{h}\, dt$.

#### 第五步：证明 $R(\mathbf{h}) = o(\|\mathbf{h}\|^2)$

由于 $f \in C^2$，$H_f$ 在 $\mathbf{x}_0$ 处连续，故 $E(t\mathbf{h}) \to \mathbf{0}$ 当 $\mathbf{h} \to \mathbf{0}$，且该收敛关于 $t \in [0,1]$ 一致（因 $\|t\mathbf{h}\| \leq \|\mathbf{h}\|$）。记

$$\eta(\mathbf{h}) = \sup_{t \in [0,1]} \|E(t\mathbf{h})\|,$$

则 $\eta(\mathbf{h}) \to 0$ 当 $\mathbf{h} \to \mathbf{0}$。于是

$$
\begin{aligned}
|R(\mathbf{h})|
&\leq \int_0^1 (1-t)\, \left| \mathbf{h}^T E(t\mathbf{h})\, \mathbf{h} \right| dt \\
&\leq \int_0^1 (1-t)\, \|E(t\mathbf{h})\| \, \|\mathbf{h}\|^2 \, dt \\
&\leq \eta(\mathbf{h})\, \|\mathbf{h}\|^2 \int_0^1 (1-t)\, dt
= \frac{1}{2} \eta(\mathbf{h})\, \|\mathbf{h}\|^2.
\end{aligned}
$$

因此 $\displaystyle \frac{|R(\mathbf{h})|}{\|\mathbf{h}\|^2} \leq \frac{1}{2} \eta(\mathbf{h}) \to 0$，即 $R(\mathbf{h}) = o(\|\mathbf{h}\|^2)$。$\square$

至此二阶展开 $(1)$ 得证。

### 一般 $k$ 阶展开的推导要点

#### 高阶导数的递推

对 $g(t) = f(\mathbf{x}_0 + t\mathbf{h})$，由链式法则反复求导（或由多重指标多项式展开公式），得到

$$g^{(m)}(t) = \sum_{|\alpha| = m} \frac{m!}{\alpha!}\, \partial^\alpha f(\mathbf{x}_0 + t\mathbf{h})\, \mathbf{h}^\alpha. \quad \cdots (\dagger)$$

> [!info] $(\dagger)$ 的归纳验证
> 当 $m=1$：$g'(t) = \sum_{i=1}^n \frac{\partial f}{\partial x_i} h_i = \sum_{|\alpha|=1} \frac{1!}{\alpha!} \partial^\alpha f \, \mathbf{h}^\alpha$（单分量的多重指标 $\alpha = \mathbf{e}_i$）。
>
> 设对 $m$ 成立。对 $g^{(m)}(t)$ 再求一次导数，由乘积规则及 $\partial_{x_j} \partial^\alpha f = \partial^{\alpha+\mathbf{e}_j} f$，可重组为 $m+1$ 阶形式。组合系数恰为 $\frac{m!}{\alpha!} \to \frac{(m+1)!}{\alpha'!}$（因为 $\binom{m+1}{\alpha'} = \cdots$），归纳成立。$\square$

#### 应用一元 Taylor 定理

对 $g(1)$ 应用一元 Taylor 定理（三种余项任选其一）并代入 $(\dagger)$，即得 $(2)$ 的三种余项形式。例如，积分余项形式的推导为：

由一元 Taylor 公式（积分余项）：

$$g(1) = \sum_{m=0}^{k} \frac{g^{(m)}(0)}{m!} + \frac{1}{k!} \int_0^1 (1-t)^k g^{(k+1)}(t)\, dt.$$

将 $(\dagger)$ 代入求和项：

$$\sum_{m=0}^{k} \frac{g^{(m)}(0)}{m!} = \sum_{m=0}^{k} \sum_{|\alpha|=m} \frac{\partial^\alpha f(\mathbf{x}_0)}{\alpha!}\, \mathbf{h}^\alpha = \sum_{|\alpha| \leq k} \frac{\partial^\alpha f(\mathbf{x}_0)}{\alpha!}\, \mathbf{h}^\alpha.$$

将 $(\dagger)$（取 $m = k+1$）代入积分项：

$$
\begin{aligned}
\frac{1}{k!} \int_0^1 (1-t)^k g^{(k+1)}(t)\, dt
&= \frac{1}{k!} \int_0^1 (1-t)^k \sum_{|\alpha| = k+1} \frac{(k+1)!}{\alpha!}\, \partial^\alpha f(\mathbf{x}_0 + t\mathbf{h})\, \mathbf{h}^\alpha \, dt \\[4pt]
&= (k+1) \sum_{|\alpha| = k+1} \frac{\mathbf{h}^\alpha}{\alpha!} \int_0^1 (1-t)^k\, \partial^\alpha f(\mathbf{x}_0 + t\mathbf{h})\, dt,
\end{aligned}
$$

此即积分余项。Lagrange 余项用一元中值定理形式的 Taylor 公式即得；Peano 余项要求较轻（$f \in C^k$），由连续性与一致估计可得 $o(\|\mathbf{h}\|^k)$。$\blacksquare$

---

## 应用实例

> [!example] 例 1：求 $f(x,y) = e^x \cos y$ 在原点处的二阶 Taylor 展开
>
> **计算各阶偏导数**：
>
> $$f(0,0) = e^0 \cos 0 = 1.$$
>
> $$f_x = e^x \cos y, \quad f_x(0,0) = 1; \qquad f_y = -e^x \sin y, \quad f_y(0,0) = 0.$$
>
> $$f_{xx} = e^x \cos y, \quad f_{xx}(0,0) = 1;$$
> $$f_{xy} = -e^x \sin y, \quad f_{xy}(0,0) = 0;$$
> $$f_{yy} = -e^x \cos y, \quad f_{yy}(0,0) = -1.$$
>
> 于是 $\nabla f(0,0) = (1, 0)$，$H_f(0,0) = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$。
>
> **代入公式** $(1)$：
>
> $$\begin{aligned}
> f(x,y) &= 1 + \begin{pmatrix}1 & 0\end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} + \frac{1}{2} \begin{pmatrix} x & y \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} + o(x^2 + y^2) \\[4pt]
> &= 1 + x + \frac{1}{2}\bigl(x^2 - y^2\bigr) + o(x^2 + y^2).
> \end{aligned}$$
>
> **检验**：在原点附近，$f(x,0) \approx 1 + x + \frac{x^2}{2}$（一元 $e^x$ 的二阶展开），$f(0,y) \approx 1 - \frac{y^2}{2}$（一元 $\cos y$ 的二阶展开），与展开式吻合。

> [!example] 例 2：用二阶 Taylor 展开作局部近似估值
>
> 利用例 1 的二阶展开，近似计算 $f(0.1, 0.05) = e^{0.1} \cos(0.05)$。
>
> **展开式估值**：$\mathbf{h} = (0.1, 0.05)$，$\|\mathbf{h}\|^2 = 0.01 + 0.0025 = 0.0125$。
>
> $$\begin{aligned}
> f(0.1, 0.05) &\approx 1 + 0.1 + \frac{1}{2}\bigl((0.1)^2 - (0.05)^2\bigr) \\
> &= 1 + 0.1 + \frac{1}{2}(0.01 - 0.0025) \\
> &= 1.1 + 0.00375 = 1.10375.
> \end{aligned}$$
>
> **精确值**：$e^{0.1} \approx 1.1051709$，$\cos(0.05) \approx 0.9987503$，乘积 $\approx 1.10379$。
>
> **误差**：$|1.10379 - 1.10375| \approx 4 \times 10^{-5}$。由余项为 $o(\|\mathbf{h}\|^2)$，理论误差应与 $\|\mathbf{h}\|^3$ 同阶（因三阶导数有界），估值约 $\frac{1}{6}\|\mathbf{h}\|^3 \cdot M_3$，与实际吻合。
>
> > [!info] 展开在极值判别中的应用
> > 在临界点 $\nabla f(\mathbf{x}_0) = \mathbf{0}$ 处，一阶项消失，函数的局部行为完全由二阶项 $\frac{1}{2}\mathbf{h}^T H_f(\mathbf{x}_0)\mathbf{h}$ 决定。这正是 [[多元函数极值的二阶充分条件]] 的核心依据：Hessian 正定 ⇒ 局部极小、负定 ⇒ 局部极大、不定 ⇒ 鞍点。

---

## 证明思路总结

> [!tip] 关键思想
> 多元 Taylor 公式的证明核心是**降维**：
>
> 1. **构造一元函数** $g(t) = f(\mathbf{x}_0 + t\mathbf{h})$，将所有方向的增量"压缩"进参数 $t$。
> 2. **用链式法则求导**：$g^{(m)}(t)$ 是各阶偏导数与 $\mathbf{h}$ 分量的多重线性组合——多重指标记号天然地组织了这些组合。
> 3. **套用一元 Taylor 定理**：将 $g$ 的展开直接翻译为 $f$ 的展开，余项形式（Peano / Lagrange / 积分）由对应的一元定理继承。
> 4. **余项的一致估计**：利用 $C^k$ 连续性，$o(\|\mathbf{h}\|^k)$ 的收敛关于方向一致，保证展开关于 $\|\mathbf{h}\|$ 的渐近性。
>
> 整个推导体现了多元微分学的核心方法：**通过限制在一条直线上，把多元问题转化为一元问题**。这一技巧在证明 [[反函数定理]]、[[隐函数定理]] 等深层定理中反复出现。

> [!warning] $C^k$ 条件的必要性
> 若 $f$ 仅为 $k$ 次可微（$k$ 阶偏导存在但不连续），Peano 余项的 $o(\|\mathbf{h}\|^k)$ 仍成立，但 Lagrange 或积分余项需要 $C^{k+1}$ 才能对中间点或全路径上的导数进行控制。这与一元情形完全相同。

---

## 相关笔记

- [[偏导数与方向导数]] — 偏导数、梯度、Schwarz 定理（Hessian 对称性）
- [[全微分与可微性]] — 一阶 Taylor 公式 = 可微性定义
- [[多元链式法则]] — $g(t) = f(\mathbf{x}_0 + t\mathbf{h})$ 的各阶导数计算
- [[多元函数极值的二阶充分条件]] — 二阶 Taylor 展开的直接应用
- [[反函数定理]] — Taylor 展开在局部线性化中的作用
- [[隐函数定理]] — 类似的逐阶展开思想
