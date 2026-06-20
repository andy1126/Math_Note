---
title: Sobolev嵌入定理
date: 2026-04-11
tags:
  - 数学物理方法
  - 偏微分方程
  - Sobolev空间
  - 嵌入定理
  - 泛函分析
  - 弱解理论
---

# Sobolev嵌入定理

## 预备定义

> [!note] 弱导数
> 设 $\Omega \subset \mathbb{R}^n$ 为开集，$u \in L^1_{loc}(\Omega)$。若存在 $v \in L^1_{loc}(\Omega)$ 使得对所有测试函数 $\varphi \in C_c^\infty(\Omega)$：
> $$\int_\Omega u \frac{\partial \varphi}{\partial x_i} dx = -\int_\Omega v \varphi dx$$
> 则称 $v$ 为 $u$ 关于 $x_i$ 的**弱导数**，记作 $\dfrac{\partial u}{\partial x_i} = v$。
>
> 直观上，弱导数是通过分部积分公式定义的"广义导数"，允许不可微函数拥有导数。

> [!note] Sobolev空间 $W^{k,p}(\Omega)$
> 设 $k \in \mathbb{N}$，$1 \leq p \leq \infty$。定义**Sobolev空间**：
> $$W^{k,p}(\Omega) = \{u \in L^p(\Omega) : D^\alpha u \in L^p(\Omega), \forall |\alpha| \leq k\}$$
> 其中 $D^\alpha u$ 表示 $u$ 的 $\alpha$ 阶弱导数。
>
> 装备范数：
> $$\|u\|_{W^{k,p}} = \left(\sum_{|\alpha| \leq k} \|D^\alpha u\|_{L^p}^p\right)^{1/p}$$
> （当 $p = \infty$ 时取上确界）。
>
> $W^{k,p}(\Omega)$ 是Banach空间。特别地，$W^{k,2}(\Omega)$ 记作 $H^k(\Omega)$，是Hilbert空间。

> [!note] 空间 $W_0^{k,p}(\Omega)$
> $C_c^\infty(\Omega)$（紧支集光滑函数空间）在 $W^{k,p}(\Omega)$ 中的闭包记为 $W_0^{k,p}(\Omega)$。
>
> 直观含义：$W_0^{k,p}(\Omega)$ 中的函数在边界 $\partial\Omega$ 上"以广义意义"为零。

> [!note] Hölder空间 $C^{k,\alpha}(\bar{\Omega})$
> 设 $0 < \alpha \leq 1$。函数 $u$ 的**Hölder半范数**：
> $$[u]_\alpha = \sup_{x \neq y} \frac{|u(x) - u(y)|}{|x - y|^\alpha}$$
>
> **Hölder空间**：
> $$C^{k,\alpha}(\bar{\Omega}) = \{u \in C^k(\bar{\Omega}) : [D^\beta u]_\alpha < \infty, \forall |\beta| = k\}$$
> 装备范数 $\|u\|_{C^{k,\alpha}} = \|u\|_{C^k} + \max_{|\beta|=k} [D^\beta u]_\alpha$。

> [!abstract] 引理：Sobolev空间的逼近性质
> 若 $\Omega$ 有界且边界满足适当正则性，则 $C^\infty(\bar{\Omega})$ 在 $W^{k,p}(\Omega)$ 中稠密。
>
> **证明概要**：通过磨光（mollification）和局部拉直边界构造逼近序列。

---

## 定理

设 $\Omega \subset \mathbb{R}^n$ 为有界开区域，边界 $\partial\Omega \in C^1$，$k \in \mathbb{N}$，$1 \leq p < \infty$。

### 第一部分：连续嵌入

**(i) Morrey嵌入**（$kp > n$）：
若 $kp > n$，则
$$W^{k,p}(\Omega) \hookrightarrow C^{k - [\frac{n}{p}] - 1, \gamma}(\bar{\Omega})$$
其中 $\gamma = [\frac{n}{p}] + 1 - \frac{n}{p}$（当 $\frac{n}{p} \notin \mathbb{N}$）或任意 $0 < \gamma < 1$（当 $\frac{n}{p} \in \mathbb{N}$）。

特别地，当 $k = 1, p > n$：
$$W^{1,p}(\Omega) \hookrightarrow C^{0,1-\frac{n}{p}}(\bar{\Omega})$$

**(ii) Gagliardo-Nirenberg-Sobolev嵌入**（$kp < n$）：
若 $kp < n$，定义Sobolev共轭指数：
$$p^* = \frac{np}{n - kp}$$
则
$$W^{k,p}(\Omega) \hookrightarrow L^q(\Omega), \quad \forall 1 \leq q \leq p^*$$
特别地：
$$W^{1,p}(\Omega) \hookrightarrow L^{p^*}(\Omega), \quad p^* = \frac{np}{n-p}$$

**(iii) 临界情形**（$kp = n$）：
若 $kp = n$，则
$$W^{k,p}(\Omega) \hookrightarrow L^q(\Omega), \quad \forall 1 \leq q < \infty$$

### 第二部分：紧嵌入（Rellich-Kondrachov定理）

**(iv) 紧嵌入**：
在(i)-(iii)的嵌入中，若 $q$ 严格小于临界指数（即 $q < p^*$ 当 $kp < n$；$q < \infty$ 当 $kp = n$；任意 $q$ 当 $kp > n$），则嵌入是**紧的**：
$$W^{k,p}(\Omega) \subset\subset L^q(\Omega)$$
（紧嵌入意味着有界集在像空间中是列紧的）

---

## 第(i)部分的证明：Morrey嵌入（$p > n$ 情形）

### 目标
证明当 $p > n$ 时，$W^{1,p}$ 函数实际上是Hölder连续的。

### 证明过程

#### 第一步：简化假设

由Sobolev空间的逼近性质，只需对 $u \in C^1(\bar{\Omega})$ 证明估计，再取极限。

设 $u \in C^1(\bar{B})$，其中 $B = B_r(x_0) \subset\subset \Omega$ 是任意球。

#### 第二步：均值表示

对任意 $x, y \in B$，由Newton-Leibniz公式：
$$u(x) - u(y) = \int_0^1 \frac{d}{dt} u(tx + (1-t)y) dt = \int_0^1 \nabla u(tx + (1-t)y) \cdot (x-y) dt$$

#### 第三步：建立逐点估计

对 $B$ 积分平均：
$$\begin{aligned}
|u(x) - \bar{u}_B| &= \left|\frac{1}{|B|}\int_B [u(x) - u(y)] dy\right| \\
&\leq \frac{1}{|B|}\int_B \int_0^1 |\nabla u(tx + (1-t)y)| |x-y| dt dy
\end{aligned}$$

其中 $\bar{u}_B = \dfrac{1}{|B|}\int_B u(y) dy$ 是均值。

#### 第四步：变量替换与估计

令 $z = tx + (1-t)y$，则 $y = \dfrac{z - tx}{1-t}$，$dy = \dfrac{dz}{(1-t)^n}$。

当 $y \in B$ 且固定 $t$，$z$ 在球 $B_{(1-t)r}(tx + (1-t)x_0)$ 内。

利用 $|x - y| \leq 2r$ 和 Hölder 不等式：
$$\begin{aligned}
|u(x) - \bar{u}_B| &\leq \frac{C}{r^n} \int_0^1 \int_{B_{(1-t)r}(\cdots)} |\nabla u(z)| \frac{2r}{(1-t)^n} dz dt \\
&\leq \frac{C}{r^{n-1}} \int_0^1 \frac{1}{(1-t)^n} \|\nabla u\|_{L^p} |B_{(1-t)r}|^{1-1/p} dt
\end{aligned}$$

计算：$|B_{(1-t)r}|^{1-1/p} = C r^{n(1-1/p)} (1-t)^{n(1-1/p)}$

$$|u(x) - \bar{u}_B| \leq C r^{1-n/p} \|\nabla u\|_{L^p} \int_0^1 (1-t)^{-n/p} dt$$

#### 第五步：积分收敛性

积分 $\displaystyle\int_0^1 (1-t)^{-n/p} dt$ 收敛当且仅当 $-n/p > -1$，即 $p > n$。

此时：
$$|u(x) - \bar{u}_B| \leq C r^{1-n/p} \|\nabla u\|_{L^p}$$

#### 第六步：Hölder连续性

对任意 $x, y \in \Omega$，取 $r = |x-y|$，$B$ 包含 $x, y$。

$$|u(x) - u(y)| \leq |u(x) - \bar{u}_B| + |u(y) - \bar{u}_B| \leq C |x-y|^{1-n/p} \|\nabla u\|_{L^p}$$

因此 $[u]_{1-n/p} \leq C \|\nabla u\|_{L^p}$，即 $u \in C^{0,1-n/p}$。

结合 $\|u\|_{L^\infty} \leq C \|u\|_{W^{1,p}}$（由上述估计），得：
$$\|u\|_{C^{0,1-n/p}} \leq C \|u\|_{W^{1,p}} \quad \square$$

---

## 第(ii)部分的证明：Gagliardo-Nirenberg-Sobolev嵌入（$p < n$ 情形）

### 目标
证明 $W^{1,p}(\Omega) \hookrightarrow L^{p^*}(\Omega)$，其中 $p^* = \dfrac{np}{n-p}$。

### 证明过程（简化版：$p = 1, n = 2$）

#### 第一步：Gagliardo表示

对 $u \in C_c^1(\mathbb{R}^n)$，对第 $i$ 个坐标方向：
$$u(x) = \int_{-\infty}^{x_i} \frac{\partial u}{\partial x_i}(x_1, \ldots, t, \ldots, x_n) dt$$

因此：
$$|u(x)| \leq \int_{-\infty}^{\infty} |\nabla u(x_1, \ldots, t, \ldots, x_n)| dt$$

#### 第二步：乘积估计（$n = 2$ 情形）

$$|u(x)|^2 \leq \left(\int_{-\infty}^{\infty} |\partial_1 u| dx_1\right) \left(\int_{-\infty}^{\infty} |\partial_2 u| dx_2\right)$$

#### 第三步：积分

$$\int_{\mathbb{R}^2} |u|^2 dx \leq \int \left(\int |\partial_1 u| dx_1\right) \left(\int |\partial_2 u| dx_2\right) dx$$

交换积分次序：
$$= \left(\iint |\partial_1 u| dx_1 dx_2\right) \left(\iint |\partial_2 u| dx_1 dx_2\right) = \|\nabla u\|_{L^1}^2$$

因此 $\|u\|_{L^2} \leq \|\nabla u\|_{L^1}$，即 $p = 1$ 时 $p^* = 2 = \dfrac{2 \cdot 1}{2-1}$。$\square$

### 一般情形的证明思路

对一般 $p < n$，使用归纳法和Hölder不等式。

**关键步骤**：证明 $p = 1$ 时的嵌入：
$$\|u\|_{L^{n/(n-1)}} \leq C \|\nabla u\|_{L^1}$$

然后对一般 $p$，令 $v = |u|^\gamma$，选择适当的 $\gamma$ 使得 $|v|$ 的导数可被控制。

通过尺度分析（scaling argument）确定 $p^* = \dfrac{np}{n-p}$ 是唯一可能的临界指数。$\square$

---

## 第(iii)部分的说明：临界情形

当 $kp = n$ 时，$W^{k,p}$ 可以嵌入到任意 $L^q$（$q < \infty$），但不能嵌入到 $L^\infty$。

**反例**：设 $\Omega = B_1(0) \subset \mathbb{R}^2$，$u(x) = \ln|\ln|x||$。

- $u \in W^{1,2}(\Omega)$（因为 $kp = 2 = n$）
- 但 $u \notin L^\infty(\Omega)$（在 $x = 0$ 附近无界）

这说明临界情形的嵌入是"几乎连续"但不是真正的连续。$\square$

---
## 第(iv)部分的证明：Rellich-Kondrachov紧嵌入

### 目标
证明当 $q < p^*$ 时，嵌入 $W^{1,p}(\Omega) \hookrightarrow L^q(\Omega)$ 是紧的。

### 证明概要

#### 第一步：有界集在 $L^q$ 中的列紧性判别

利用**Fréchet-Kolmogorov定理**：$L^q(\Omega)$ 中的子集 $S$ 列紧当且仅当：
1. $S$ 有界
2. $S$ 在 $q$ 范数下等度连续：$\displaystyle\lim_{h \to 0} \sup_{f \in S} \|f(\cdot + h) - f\|_{L^q} = 0$

#### 第二步：利用Gagliardo-Nirenberg插值

对 $q < p^*$，存在 $\theta \in (0,1)$ 使得：
$$\frac{1}{q} = \frac{\theta}{1} + \frac{1-\theta}{p^*}$$

（即 $L^q$ 范数可由 $L^1$ 和 $L^{p^*}$ 范数插值得到）

#### 第三步：估计平移

对 $u \in W^{1,p}$，$\|u\|_{W^{1,p}} \leq M$：

$$\|u(\cdot + h) - u\|_{L^q} \leq \|u(\cdot + h) - u\|_{L^1}^\theta \|u(\cdot + h) - u\|_{L^{p^*}}^{1-\theta}$$

由Sobolev嵌入：$\|u(\cdot + h) - u\|_{L^{p^*}} \leq C M$

由 $W^{1,p} \hookrightarrow L^1$ 的等度连续性（或直接估计）：$\|u(\cdot + h) - u\|_{L^1} \to 0$ 当 $h \to 0$

因此 $W^{1,p}$ 中的有界集在 $L^q$（$q < p^*$）中等度连续，从而列紧。$\square$

---

## 重要推论

### 推论一：Poincaré不等式

> [!abstract] Poincaré不等式
> 设 $\Omega$ 有界，$1 \leq p < \infty$，则对 $u \in W_0^{1,p}(\Omega)$：
> $$\|u\|_{L^p} \leq C \|\nabla u\|_{L^p}$$
>
> 或对 $u \in W^{1,p}(\Omega)$，设 $\bar{u} = \dfrac{1}{|\Omega|}\int_\Omega u$：
> $$\|u - \bar{u}\|_{L^p} \leq C \|\nabla u\|_{L^p}$$

**证明概要**：反证法，利用紧嵌入和反设序列的收敛性导出矛盾。

### 推论二：椭圆方程的正则性

> [!abstract] 内部正则性
> 设 $u \in H^1(\Omega)$ 是 $-\Delta u = f$ 的弱解。若 $f \in L^p(\Omega)$，$p > n/2$，则 $u \in C^{0,\alpha}_{loc}(\Omega)$。

**证明**：由Sobolev嵌入和迭代论证（bootstrap argument）。

### 推论三：变分问题的解

> [!abstract] Dirichlet原理
> 能量泛函 $J(u) = \int_\Omega (\frac{1}{2}|\nabla u|^2 - fu) dx$ 在 $H_0^1(\Omega)$ 中有唯一极小元，且极小元满足 $-\Delta u = f$。

**存在性**：$H_0^1(\Omega)$ 是自反Banach空间，$J$ 强制且严格凸。

---

## 不同空间维数的嵌入表

| 空间 | $n = 1$ | $n = 2$ | $n = 3$ |
|-----|---------|---------|---------|
| $W^{1,1}$ | $\hookrightarrow L^\infty$ | $\hookrightarrow L^2$ | $\hookrightarrow L^{3/2}$ |
| $W^{1,2}$ | $\hookrightarrow C^{0,1/2}$ | $\hookrightarrow L^q$ ($\forall q$) | $\hookrightarrow L^6$ |
| $W^{1,3}$ | $\hookrightarrow C^{0,2/3}$ | $\hookrightarrow C^{0,1/3}$ | $\hookrightarrow L^\infty$ |
| $W^{2,2}$ | $\hookrightarrow C^{1,1/2}$ | $\hookrightarrow C^{0,\alpha}$ | $\hookrightarrow L^\infty$ |

> [!info] 规律总结
> - 随着空间维数 $n$ 增大，函数需要更多可积性才能保持连续性
> - $p > n$ 时 $W^{1,p}$ 函数连续，这是分析中常用的门槛

---

## 相关笔记

- [[热方程最大值原理]] - 经典解的正则性
- [[调和函数的极值原理]] - 调和函数的内部光滑性
- [[波动方程能量估计]] - 能量方法

---

## 证明思路总结

> [!tip] 关键思想
> Sobolev嵌入定理揭示了**可积性**与**光滑性**之间的深刻联系：
>
> 1. **Morrey嵌入（$p > n$）**的核心：
>    - 通过积分表示（Newton-Leibniz公式）将函数值与导数联系
>    - $p > n$ 保证了积分 $\int (1-t)^{-n/p} dt$ 的收敛
>    - 这给出了Hölder指数 $1 - n/p$ 的精确来源
>
> 2. **Gagliardo-Nirenberg嵌入（$p < n$）**的核心：
>    - 利用 $n$ 个方向积分的乘积估计
>    - 尺度分析（scaling argument）确定临界指数 $p^* = np/(n-p)$
>    - 临界指数是唯一的，体现了方程的**尺度不变性**
>
> 3. **紧嵌入的核心**：
>    - 有界区域 + 严格小于临界指数 = 额外紧性
>    - 这是椭圆方程解的存在性证明中抽取收敛子列的关键工具
>
> 4. **维度依赖性**：
>    - $n = 1$：$W^{1,1}$ 就嵌入到连续函数（绝对连续）
>    - $n \geq 2$：需要更强的可积性 $p > n$
>    - 这解释了为什么低维PDE理论比高维简单

> [!warning] 边界正则性的必要性
> 紧嵌入定理需要 $\partial\Omega$ 满足某种正则性（如 $C^1$）。对任意有界区域，Sobolev嵌入仍成立，但紧性可能失效。

> [!info] 推广
> - **分数阶Sobolev空间**：$W^{s,p}$，$s \in \mathbb{R}$，通过Fourier变换或插值定义
> - **迹定理**：$W^{1,p}(\Omega) \to L^q(\partial\Omega)$ 的限制映射
> - **演化方程**：抛物型Sobolev空间 $L^p(0,T; W^{k,p}(\Omega))$
