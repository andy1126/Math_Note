---
title: 最大模原理与 Schwarz 引理
date: 2026-05-30
tags:
  - 复分析
  - 全纯函数
  - 最大模原理
  - Schwarz引理
  - 平均值性质
---

# 最大模原理与 Schwarz 引理

## 预备定义

> [!note] 全纯函数
> 设 $\Omega \subset \mathbb{C}$ 开。称 $f: \Omega \to \mathbb{C}$ 在 $z_0 \in \Omega$ **全纯**（holomorphic），若极限
> $$f'(z_0) = \lim_{h \to 0} \frac{f(z_0 + h) - f(z_0)}{h}$$
> 存在。$f \in H(\Omega)$ 表示在 $\Omega$ 上处处全纯。

> [!note] 单位圆盘
> $$\mathbb{D} := \{ z \in \mathbb{C} : |z| < 1 \}, \quad \partial\mathbb{D} := \{ |z| = 1 \}.$$

> [!abstract] 引理：Cauchy 积分公式
> 设 $f \in H(\Omega)$，$\overline{D(z_0, r)} \subset \Omega$。则
> $$f(z_0) = \frac{1}{2\pi i} \oint_{|z - z_0| = r} \frac{f(z)}{z - z_0}\,dz = \frac{1}{2\pi} \int_0^{2\pi} f(z_0 + r e^{i\theta})\,d\theta.$$
> 第二等式即**平均值性质**（mean value property）。详见 [[柯西积分公式]]。

> [!abstract] 引理：开映射定理（Open Mapping Theorem）
> 若 $f \in H(\Omega)$ 非常数（在每连通分支上），则 $f$ 是开映射：$f(U)$ 对 $\Omega$ 中开集 $U$ 仍为开集。

---

## 定理 A（最大模原理 / Maximum Modulus Principle）

设 $\Omega \subset \mathbb{C}$ 为**连通**开集，$f \in H(\Omega)$。

**(i)（强形式）** 若 $|f|$ 在 $\Omega$ 内某点 $z_0$ 取到局部极大，则 $f$ 在 $\Omega$ 上为常数。

**(ii)（边界形式）** 若 $\Omega$ 有界，$f \in H(\Omega) \cap C(\overline{\Omega})$，则
$$\max_{z \in \overline{\Omega}} |f(z)| = \max_{z \in \partial\Omega} |f(z)|.$$

---

## 证明 A

### 方法一：由平均值性质

设 $|f|$ 在 $z_0$ 取局部极大值 $M = |f(z_0)|$。取 $r > 0$ 充分小使 $\overline{D(z_0, r)} \subset \Omega$ 且 $|f(z)| \leq M$ 于该闭盘。

由平均值性质：
$$M = |f(z_0)| = \left| \frac{1}{2\pi} \int_0^{2\pi} f(z_0 + r e^{i\theta})\,d\theta \right| \leq \frac{1}{2\pi} \int_0^{2\pi} |f(z_0 + r e^{i\theta})|\,d\theta \leq M.$$

**等号链强制**：积分中 $|f(z_0 + r e^{i\theta})| = M$ 几乎处处；由 $f$ 连续故处处。再由三角不等式取等 $\Leftrightarrow$ 被积函数辐角相同 $\Leftrightarrow$ $f$ 在圆 $|z - z_0| = r$ 上为常数 $= f(z_0)$。

对一切 $0 < r' \leq r$ 同样推理：$f \equiv f(z_0)$ 于 $D(z_0, r)$。

### 第二步：连通性传播

令 $S = \{ z \in \Omega : f(z) = f(z_0) \}$。

- **$S$ 非空**：$z_0 \in S$。
- **$S$ 闭**：$f$ 连续。
- **$S$ 开**：由上一步，若 $z \in S$，则 $f \equiv f(z_0)$ 于 $z$ 的某邻域。

$\Omega$ 连通 $\Rightarrow S = \Omega$，即 $f \equiv f(z_0)$。$\square$

### 方法二：由开映射定理（更简洁）

假设 $f$ 非常数。由开映射定理，$f(\Omega)$ 为开集。$f(z_0)$ 是 $f(\Omega)$ 内点，故存在 $\varepsilon > 0$ 使 $D(f(z_0), \varepsilon) \subset f(\Omega)$。

存在 $w \in D(f(z_0), \varepsilon)$ 使 $|w| > |f(z_0)|$（沿 $f(z_0)$ 的同方向延长）。则存在 $z_\ast \in \Omega$ 使 $f(z_\ast) = w$，$|f(z_\ast)| > |f(z_0)|$。与"$z_0$ 是 $|f|$ 局部极大点"矛盾。$\square$

### (ii) 由 (i) 推出

$\overline{\Omega}$ 紧 $\Rightarrow |f|$ 在 $\overline{\Omega}$ 取最大值于某点 $z_\ast$。若 $z_\ast \in \Omega$，由 (i) $f$ 为常数，结论平凡。否则 $z_\ast \in \partial\Omega$。$\blacksquare$

---

## 定理 B（Schwarz 引理）

设 $f: \mathbb{D} \to \mathbb{D}$ 全纯且 $f(0) = 0$。则

**(i)** $|f(z)| \leq |z|$ 对一切 $z \in \mathbb{D}$；

**(ii)** $|f'(0)| \leq 1$；

**(iii)（等式情形）** 若存在 $z_0 \in \mathbb{D} \setminus \{0\}$ 使 $|f(z_0)| = |z_0|$，或 $|f'(0)| = 1$，则存在 $|\lambda| = 1$ 使 $f(z) = \lambda z$（即 $f$ 为绕原点的旋转）。

---

## 证明 B

### 第一步：构造辅助函数

定义
$$g(z) := \begin{cases} f(z) / z, & z \in \mathbb{D} \setminus \{0\} \\ f'(0), & z = 0. \end{cases}$$

由 $f(0) = 0$ 与 $f$ 全纯，$f$ 在 $0$ 附近 Taylor 展开 $f(z) = f'(0) z + a_2 z^2 + \cdots$，故 $f(z)/z = f'(0) + a_2 z + \cdots$ 在 $0$ 处也解析。即 $g \in H(\mathbb{D})$（**可去奇点**的标准应用）。

### 第二步：在小圆盘 $\overline{D(0, r)}$ 上估计

固定 $0 < r < 1$。对 $|z| = r$，$|f(z)| < 1$（$f$ 取值于 $\mathbb{D}$），故
$$|g(z)| = \frac{|f(z)|}{|z|} < \frac{1}{r}.$$

由**最大模原理**（定理 A.ii）应用于 $g$ 在 $\overline{D(0, r)}$ 上：
$$|g(z)| \leq \max_{|w| = r} |g(w)| \leq \frac{1}{r}, \quad \forall\, |z| \leq r.$$

### 第三步：令 $r \to 1^-$

对每个固定的 $z \in \mathbb{D}$，取 $r$ 使 $|z| < r < 1$，得 $|g(z)| \leq 1/r$。令 $r \to 1^-$：
$$|g(z)| \leq 1, \quad \forall\, z \in \mathbb{D}.$$

即 $|f(z)/z| \leq 1$（$z \neq 0$）与 $|g(0)| = |f'(0)| \leq 1$。结论 (i), (ii) 得证。$\square$

### 第四步：等式情形

若 $|g(z_0)| = 1$ 于某 $z_0 \in \mathbb{D}$：$|g|$ 在 $\mathbb{D}$ 内点取到极大值 $1$（由步骤三的上界）。由最大模原理强形式 (i)，$g$ 为常数 $\lambda$，$|\lambda| = 1$。即 $f(z) = \lambda z$。

- $|f(z_0)| = |z_0|$ 对应 $|g(z_0)| = 1$；
- $|f'(0)| = 1$ 对应 $|g(0)| = 1$。

两情形结论相同。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> **最大模原理**：全纯函数的"积分平均 = 中心值"压制了 $|f|$ 取局部极大的可能。三种证法相互呼应：
> 1. **平均值法**：圆周积分取等 $\Rightarrow$ $|f|$ 在圆上为常数 $\Rightarrow$ $f$ 在圆上为常数 $\Rightarrow$ 连通性传播；
> 2. **开映射法**：非常数全纯函数像开 $\Rightarrow$ 像中没有"边界点"性质 $\Rightarrow$ $|f|$ 不能内取极大；
> 3. **调和函数视角**：$\log |f|$ 在零点之外调和，调和函数极值原理直接给出（见 [[调和函数的极值原理]]）。
>
> **Schwarz 引理**：核心技巧是**除以 $z$ 得到可去奇点**，再用最大模原理。这是"Schwarz-Pick 不等式"、"Hyperbolic 度量收缩性"的源头。

> [!important] 几何解释
> 最大模原理：**全纯函数的"能量"由边界完全确定**。这是椭圆型 PDE（Laplace 方程）极值原理在复变量下的特殊形式。
>
> Schwarz 引理：从单位圆盘到单位圆盘且固定原点的全纯映射，**只能"压缩"不能"放大"**。等式情形说明唯一保持原点又保持距离的全纯自映射就是旋转。

> [!info] Schwarz-Pick 推广
> Schwarz 引理可去掉 $f(0) = 0$ 的限制：对任意 $f: \mathbb{D} \to \mathbb{D}$ 全纯，
> $$\left| \frac{f(z) - f(w)}{1 - \overline{f(w)} f(z)} \right| \leq \left| \frac{z - w}{1 - \bar w z} \right|,$$
> 即 $f$ 在**双曲度量** $ds = 2|dz|/(1 - |z|^2)$ 下是非膨胀映射（弱压缩）。**等号 $\Leftrightarrow f$ 是单位圆盘的全纯自同构（Möbius 变换 $\phi_a(z) = (z - a)/(1 - \bar a z)$ 之复合）**。

> [!info] $\operatorname{Aut}(\mathbb{D})$ 的刻画
> 由 Schwarz-Pick 等式情形，$\mathbb{D}$ 的全纯自同构群
> $$\operatorname{Aut}(\mathbb{D}) = \left\{ z \mapsto e^{i\theta} \cdot \frac{z - a}{1 - \bar a z} : \theta \in \mathbb{R},\ a \in \mathbb{D} \right\}.$$
> 这与双曲平面 $\mathbb{H}^2$ 的等距群 $\operatorname{PSL}(2, \mathbb{R})$ 同构。是 **Riemann 映射定理** + 单值化定理 + 双曲几何的桥梁。详见 [[Riemann映射定理]]。

> [!warning] 连通性必要
> 最大模原理强形式 (i) 需要 $\Omega$ **连通**。例如 $\Omega = D(0, 1) \cup D(3, 1)$，$f = 0$ 于左盘、$f = 1$ 于右盘（不是同一全纯函数，但可类似构造分块例）。**连通性确保"局部为常数"传播为"全局为常数"**。

> [!info] 应用
>
> **(1) Liouville 定理（新证）**：有界整函数 $f$ 满足 $|f(z)| \leq M$ 于 $\mathbb{C}$。但 Liouville 通常用 Cauchy 估计 $|f'(z)| \leq M/R \to 0$（$R \to \infty$）。最大模原理给出几何直观：整函数若有界，$|f|$ 在每个圆盘内取最大于边界。
>
> **(2) 代数基本定理（新证）**：非常数多项式 $p$ 若无零点，$1/p$ 整函数。当 $|z| \to \infty$，$|p(z)| \to \infty$，故 $|1/p|$ 在某有界闭区域取最大于内部 $\Rightarrow$ $1/p$ 常数 $\Rightarrow$ $p$ 常数，矛盾。
>
> **(3) Hadamard 三圆定理**：$M(r) = \max_{|z| = r} |f(z)|$ 是 $\log r$ 的对数凸函数。最大模原理 + 辅助函数 $z^\alpha f(z)$ 组合。

> [!info] 衔接其他笔记
> - **平均值性质** ← [[柯西积分公式]]；
> - **开映射定理**：本笔记中作为引理，依赖于"零点孤立 + 局部行为"。详细证明属于 [[复分析基本定理]] 系列；
> - **调和函数极值原理** → [[调和函数的极值原理]]：$\log|f|$、$\operatorname{Re} f$、$\operatorname{Im} f$ 都是调和的；
> - **Riemann 映射定理** → [[Riemann映射定理]]：单连通真子域均双全纯于 $\mathbb{D}$，证明中关键使用 Schwarz-Pick；
> - **辐角原理** → [[辐角原理与Rouché定理]]：另一类全纯函数"边界 vs 内部"对应（零点 - 极点数 = 辐角变化）。
