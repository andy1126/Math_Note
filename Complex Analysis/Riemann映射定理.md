---
title: Riemann映射定理
date: 2026-04-11
tags:
  - 数学物理方法
  - 复分析
  - 共形映射
  - 单连通区域
  - Riemann映射
  - 正规族
---

# Riemann映射定理

## 预备定义

> [!note] 共形映射
> 设 $\Omega_1, \Omega_2 \subset \mathbb{C}$ 为区域。称解析函数 $f: \Omega_1 \to \Omega_2$ 为**共形映射**（conformal mapping），若 $f$ 是双射且 $f'(z) \neq 0$ 对所有 $z \in \Omega_1$ 成立。
>
> **等价条件**：$f$ 是解析双射 $\Leftrightarrow$ $f$ 是单叶解析函数（univalent function）。
>
> **几何意义**：共形映射保持角度和局部形状，仅进行旋转和伸缩。

> [!note] 单连通区域
> 区域 $\Omega \subset \mathbb{C}$ 称为**单连通**（simply connected），若它的补集 $\mathbb{C} \setminus \Omega$ 是连通的。
>
> **等价刻画**：
> - $\Omega$ 内任意简单闭合曲线可在 $\Omega$ 内连续收缩为一点
> - 对任意 $z_0 \notin \Omega$，$\log(z - z_0)$ 可在 $\Omega$ 上定义单值解析分支
> - 对 $\Omega$ 内任意解析函数 $f$，存在原函数 $F$ 使得 $F' = f$

> [!note] 正规族
> 设 $\mathcal{F}$ 是区域 $\Omega$ 上的一族解析函数。称 $\mathcal{F}$ 是**正规族**（normal family），若 $\mathcal{F}$ 中任意序列都包含子列在 $\Omega$ 的紧子集上一致收敛。
>
> **Montel定理**：若 $\mathcal{F}$ 在 $\Omega$ 的紧子集上一致有界，则 $\mathcal{F}$ 是正规族。

> [!note] 单叶函数类 $\mathcal{S}$
> 记 $\mathcal{S}$ 为所有满足以下条件的单叶解析函数 $f: \mathbb{D} \to \mathbb{C}$ 的集合：
> - $f(0) = 0$
> - $f'(0) = 1$
>
> **Koebe 1/4定理**：若 $f \in \mathcal{S}$，则 $B(0, 1/4) \subset f(\mathbb{D})$。

---

## 定理

### Riemann映射定理

设 $\Omega \subset \mathbb{C}$ 是真单连通区域（即 $\Omega \neq \mathbb{C}$），$z_0 \in \Omega$。则存在唯一的共形映射 $f: \Omega \to \mathbb{D}$（单位圆盘），满足：

$$f(z_0) = 0, \quad f'(z_0) > 0$$

**推论**：任意两个真单连通区域都是共形等价的。

---

## 证明

### 目标
构造从单连通区域 $\Omega$ 到单位圆盘 $\mathbb{D}$ 的共形映射。

### 证明策略

1. **归约**：利用单连通性将 $\Omega$ 映射到有界区域
2. **极值问题**：构造适当的函数族，寻找"最大"的映射
3. **紧性**：利用Montel定理抽取收敛子列
4. **单叶性验证**：证明极值函数是单射
5. **满射性**：证明极值函数的像是整个单位圆盘

### 证明过程

#### 第一步：归约到有界区域

**引理**：若 $\Omega$ 是真单连通区域，则存在共形映射 $g: \Omega \to \Omega'$，其中 $\Omega'$ 是有界区域。

**证明**：取 $a \notin \Omega$。由于 $\Omega$ 单连通，$\log(z - a)$ 可在 $\Omega$ 上定义单值解析分支 $h(z)$。

$e^{h(z)} = z - a$ 是单射，故 $h$ 也是单射。

$h(\Omega)$ 不包含任何竖直线段（否则 $e^h$ 会多值），特别地存在 $w_0$ 和 $\varepsilon > 0$ 使得 $|h(z) - w_0| \geq \varepsilon$ 对所有 $z \in \Omega$ 成立。

则 $g(z) = \dfrac{1}{h(z) - w_0}$ 将 $\Omega$ 映射到有界区域。$\square$

#### 第二步：构造极值函数族

假设 $\Omega$ 是有界单连通区域，$z_0 \in \Omega$。定义：

$$\mathcal{F} = \{f: \Omega \to \mathbb{D} \mid f \text{ 解析，单叶，} f(z_0) = 0\}$$

**非空性**：由于 $\Omega$ 有界，存在 $R > 0$ 使得 $\Omega \subset B(0, R)$。

则 $f(z) = \dfrac{z - z_0}{2R}$ 将 $\Omega$ 映射到 $\mathbb{D}$ 且满足条件，故 $\mathcal{F} \neq \emptyset$。

#### 第三步：极值问题

考虑极值问题：
$$M = \sup_{f \in \mathcal{F}} |f'(z_0)|$$

**关键观察**：$|f'(z_0)|$ 衡量了 $f$ 在 $z_0$ 处的"伸缩率"。"最大"的映射将"尽可能大地"打开区域。

**有界性**：由Cauchy估计，对任意 $f \in \mathcal{F}$：
$$|f'(z_0)| \leq \frac{1}{\text{dist}(z_0, \partial\Omega)} < \infty$$

故 $M < \infty$。

#### 第四步：极值函数的存在性

取序列 $\{f_n\} \subset \mathcal{F}$ 使得 $|f_n'(z_0)| \to M$。

**应用Montel定理**：由于 $f_n: \Omega \to \mathbb{D}$ 一致有界，$\{f_n\}$ 是正规族。

因此存在子列（仍记为 $\{f_n\}$）在 $\Omega$ 的紧子集上一致收敛于某解析函数 $f$。

由Weierstrass收敛定理：
$$f_n' \to f' \text{ 在紧集上一致收敛}$$

故 $|f'(z_0)| = M$。

#### 第五步：$f$ 是单射

**反证法**：假设存在 $z_1 \neq z_2$ 使得 $f(z_1) = f(z_2) = w$。

由于 $f_n$ 都是单射，$f_n(z_1) \neq f_n(z_2)$ 对所有 $n$ 成立。

考虑 $g_n(z) = f_n(z) - f_n(z_1)$。$g_n$ 在 $z_2$ 附近不为零，但 $g_n(z_2) \to f(z_2) - f(z_1) = 0$。

由Hurwitz定理，若 $f$ 不是常数，则 $f_n$ 的零点会收敛到 $f$ 的零点。但这与 $f_n$ 单射矛盾。

（更严谨的论证：设 $h_n(z) = f_n(z) - f_n(z_2)$，则 $h_n(z_1) \to 0$，$h_n(z_2) = 0$。由Rouché定理的论证可导出矛盾。）

因此 $f$ 是单射，即 $f \in \mathcal{F}$。$\square$

#### 第六步：$f$ 是满射（$f(\Omega) = \mathbb{D}$）

**反证法**：假设 $f(\Omega) \subsetneq \mathbb{D}$，即存在 $w_0 \in \mathbb{D} \setminus f(\Omega)$。

**构造自同构**：令
$$\varphi_w(z) = \frac{z - w}{1 - \bar{w}z}$$

这是单位圆盘的自同构，将 $w$ 映到 $0$。

**构造分支**：考虑 $\psi(z) = \sqrt{\varphi_{w_0}(f(z))}$。

由于 $w_0 \notin f(\Omega)$，$\varphi_{w_0}(f(z)) \neq 0$ 在 $\Omega$ 上，且由于 $\Omega$ 单连通，可定义单值解析分支 $\psi(z) = \sqrt{\varphi_{w_0}(f(z))}$。

**再作自同构**：令 $g(z) = \varphi_{\psi(z_0)}(\psi(z))$。

则 $g: \Omega \to \mathbb{D}$，$g(z_0) = 0$，且 $g$ 是单射（复合单射函数）。

故 $g \in \mathcal{F}$。

**计算导数**：由链式法则：
$$g'(z_0) = \varphi_{\psi(z_0)}'(\psi(z_0)) \cdot \psi'(z_0)$$

$$\psi'(z_0) = \frac{1}{2\sqrt{\varphi_{w_0}(f(z_0))}} \cdot \varphi_{w_0}'(f(z_0)) \cdot f'(z_0) = \frac{1}{2\sqrt{-w_0}} \cdot (1 - |w_0|^2) \cdot f'(z_0)$$

（这里 $\varphi_{w_0}(0) = -w_0$，$\varphi_{w_0}'(0) = 1 - |w_0|^2$）

经计算：
$$|g'(z_0)| = \frac{1 + |w_0|}{2\sqrt{|w_0|}} \cdot |f'(z_0)| > |f'(z_0)| = M$$

（因为 $\dfrac{1 + t}{2\sqrt{t}} > 1$ 对 $0 < t < 1$）

这与 $M$ 的极大性矛盾！

因此 $f(\Omega) = \mathbb{D}$。$\square$

#### 第七步：唯一性

设 $f_1, f_2: \Omega \to \mathbb{D}$ 都满足条件。考虑 $h = f_2 \circ f_1^{-1}: \mathbb{D} \to \mathbb{D}$。

则 $h(0) = 0$，$h'(0) = \dfrac{f_2'(z_0)}{f_1'(z_0)} > 0$。

由Schwarz引理：$|h(z)| \leq |z|$，且 $|h'(0)| \leq 1$。

同样 $h^{-1}$ 也满足Schwarz引理条件，故 $|h'(0)| \geq 1$。

因此 $|h'(0)| = 1$，由Schwarz引理的等号情形，$h(z) = e^{i\theta}z$。

但 $h'(0) > 0$，故 $e^{i\theta} = 1$，$h(z) = z$。

因此 $f_1 = f_2$。$\square$

---

## 重要推论

### 推论一：边界的对应

> [!abstract] 边界对应定理
> 若 $\Omega$ 的边界 $\partial\Omega$ 是Jordan曲线，则Riemann映射 $f$ 可连续延拓到 $\bar{\Omega}$，给出 $\bar{\Omega}$ 到 $\overline{\mathbb{D}}$ 的同胚。

### 推论二：共形等价类

> [!abstract] 分类定理
> 复平面上的单连通区域只有两种共形等价类：
> - $\mathbb{C}$ 本身（Liouville定理：有界整函数必常数，故不存在到 $\mathbb{D}$ 的共形映射）
> - 真单连通区域（都与 $\mathbb{D}$ 共形等价）

### 推论三：Green函数与Riemann映射

> [!abstract] Green函数表示
> 设 $f: \Omega \to \mathbb{D}$ 是Riemann映射，$f(z_0) = 0$。则 $\Omega$ 的Green函数：
> $$G(z, z_0) = -\frac{1}{2\pi} \log|f(z)|$$

---

## 典型例子

### 例一：上半平面到单位圆盘

**映射**：$f(z) = \dfrac{z - i}{z + i}$

- 将上半平面 $\mathbb{H} = \{z: \text{Im } z > 0\}$ 映到 $\mathbb{D}$
- $f(i) = 0$
- $f'(i) = \dfrac{2i}{(i+i)^2} = \dfrac{2i}{-4} = -\dfrac{i}{2}$

正规化：$g(z) = \dfrac{f(z)}{|f'(i)|} = 2i \cdot \dfrac{z - i}{z + i}$

则 $g'(i) = 1 > 0$。

### 例二：无限带状区域到上半平面

**映射**：$f(z) = e^z$

- 将带状区域 $\{z: 0 < \text{Im } z < \pi\}$ 映到上半平面 $\mathbb{H}$

### 例三：多边形到上半平面（Schwarz-Christoffel映射）

若 $\Omega$ 是多边形，Riemann映射由Schwarz-Christoffel公式显式给出：
$$f(z) = A \int^z \prod_{k=1}^n (\zeta - a_k)^{\alpha_k - 1} d\zeta + B$$

其中 $a_k$ 是实轴上的点，对应多边形的顶点，$\alpha_k\pi$ 是顶点的内角。

---

## 相关笔记

- [[柯西积分公式]] - 解析函数的基本性质
- [[调和函数的极值原理]] - 边界行为与唯一性
- [[泊松积分公式]] - 单位圆盘上的边值问题
- [[留数定理]] - 共形映射与围道积分

---

## 证明思路总结

> [!tip] 关键思想
> Riemann映射定理的证明体现了**极值原理**与**紧性论证**的强大结合：
>
> 1. **极值问题的设置**：
>    - 不是直接构造映射，而是寻找"最优"的映射
>    - $|f'(z_0)|$ 最大意味着映射在 $z_0$ 处"最展开"
>    - 这种"贪心"策略最终得到整个单位圆盘
>
> 2. **存在性的核心步骤**：
>    - Montel定理提供紧性（正规族）
>    - Weierstrass定理保证极限函数的解析性
>    - Hurwitz定理保持单叶性
>
> 3. **满射性的证明技巧**：
>    - 反证法：假设不满，则可通过平方根构造"更大"的映射
>    - 这是对极值性的直接违反
>    - 平方根的存在性依赖于 $\Omega$ 的单连通性
>
> 4. **单连通的本质作用**：
>    - 对数、平方根等分支的存在性
>    - 只有单连通区域才能与 $\mathbb{D}$ 共形等价
>    - 多连通区域（如圆环）有不同的共形等价类

> [!warning] 构造性证明的缺失
> Riemann映射定理是**存在性**定理，证明不给出映射的具体构造。对具体区域，需要其他方法（如Schwarz-Christoffel公式、迭代算法等）来近似或显式构造映射。

> [!info] 物理应用
> Riemann映射在流体力学（理想流体绕流）、静电学（导体形状与电容）、弹性力学中有重要应用。共形映射将复杂边界的边值问题转化为单位圆盘上的标准问题。
