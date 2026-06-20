---
title: Lax-Milgram 定理
date: 2026-05-28
tags:
  - 泛函分析
  - Hilbert空间
  - Lax-Milgram
  - 弱解
  - 双线性型
  - PDE
---

# Lax-Milgram 定理

## 预备定义

> [!note] Hilbert 空间
> 设 $(H, \langle \cdot, \cdot \rangle)$ 为内积空间。若 $H$ 在导出范数 $\|x\| = \sqrt{\langle x, x \rangle}$ 下完备，则称 **Hilbert 空间**。

> [!note] 双线性型
> 称 $a: H \times H \to \mathbb{R}$ 为**双线性型**，若 $a$ 关于每个变量分别是线性的。

> [!note] 有界与强制
> 称双线性型 $a$ 是：
> - **有界**（bounded）：存在 $M > 0$ 使 $|a(u, v)| \leq M\, \|u\|\, \|v\|$；
> - **强制**（coercive）：存在 $\alpha > 0$ 使 $a(u, u) \geq \alpha\, \|u\|^2$。

> [!abstract] 引理：Riesz 表示定理
> 设 $H$ 为 Hilbert 空间，$L \in H^\ast$（有界线性泛函）。则存在唯一 $w \in H$ 使
> $$L(v) = \langle w, v \rangle, \quad \forall\, v \in H.$$
> 且 $\|w\|_H = \|L\|_{H^\ast}$。

> [!abstract] 引理：Banach 不动点定理
> 闭子集上的 $L$-压缩映射（$L < 1$）有唯一不动点。详见 [[Banach 不动点定理|Banach 不动点定理（压缩映射原理）]]。

---

## 定理（Lax-Milgram）

设 $H$ 为 Hilbert 空间，$a: H \times H \to \mathbb{R}$ 为**有界**且**强制**的双线性型（常数 $M, \alpha$），$L: H \to \mathbb{R}$ 为有界线性泛函。则存在**唯一** $u \in H$ 使

$$a(u, v) = L(v), \quad \forall\, v \in H, \quad \cdots (\mathrm{LM})$$

且
$$\|u\|_H \leq \frac{1}{\alpha}\, \|L\|_{H^\ast}.$$

---

## 证明

### 前提验证：对称情形的"Riesz 直证"

> [!info] 简单情形
> 若 $a$ 对称（$a(u, v) = a(v, u)$）且强制，则 $a$ 本身是 $H$ 的新内积，导出等价范数。直接用 Riesz 定理（关于内积 $a$）即得 $u$。但本证明不假设对称。

### 第一步：用 Riesz 把 $a(u, \cdot)$ 化为线性算子

固定 $u \in H$，映射 $v \mapsto a(u, v)$ 是 $H$ 上的有界线性泛函（由 $a$ 双线性 + 有界）。由 Riesz，存在唯一 $A u \in H$ 使
$$a(u, v) = \langle A u, v \rangle, \quad \forall\, v \in H.$$

**$A$ 的性质**：

- **线性**：由 $a$ 关于第一变量线性 + Riesz 表示元素唯一性。
- **有界**：$\|A u\|^2 = \langle Au, Au \rangle = a(u, Au) \leq M\,\|u\|\,\|Au\|$，故 $\|Au\| \leq M\|u\|$。
- **下方控制（来自强制性）**：
  $$\alpha\,\|u\|^2 \leq a(u, u) = \langle Au, u \rangle \leq \|Au\|\,\|u\|,$$
  即 $\|Au\| \geq \alpha\,\|u\|$。

### 第二步：用 Riesz 把 $L$ 表示

由 Riesz 应用于 $L \in H^\ast$：存在 $f \in H$ 使 $L(v) = \langle f, v \rangle$，$\|f\| = \|L\|_{H^\ast}$。

### 第三步：(LM) 等价于算子方程 $A u = f$

(LM) ⇔ $\langle Au, v \rangle = \langle f, v \rangle$ 对一切 $v \in H$ ⇔ $Au = f$。

**目标**：证明 $A: H \to H$ 是**双射**（满射 + 单射）；单射给出唯一性，满射给出存在性。

### 第四步：单射 + 值域闭

**单射**：$Au = 0 \Rightarrow \|Au\| = 0 \geq \alpha\|u\|$，故 $u = 0$。$\square$

**值域闭**：设 $Au_n \to y$。由 $\|A(u_n - u_m)\| \geq \alpha\|u_n - u_m\|$：
$$\|u_n - u_m\| \leq \frac{1}{\alpha}\|Au_n - Au_m\| \to 0.$$

故 $\{u_n\}$ 是 Cauchy 序列。由 $H$ 完备，$u_n \to u$。由 $A$ 连续（有界），$Au_n \to Au$，故 $y = Au \in \operatorname{Ran}(A)$。$\square$

### 第五步：满射（值域稠密 + 闭）

由第四步，值域 $\operatorname{Ran}(A)$ 是 $H$ 的闭子空间。剩余证 $\operatorname{Ran}(A)^\perp = \{0\}$。

设 $w \in \operatorname{Ran}(A)^\perp$。则
$$\langle Au, w \rangle = 0, \quad \forall\, u \in H.$$

取 $u = w$：$\langle Aw, w \rangle = 0$。由强制性
$$\alpha\,\|w\|^2 \leq a(w, w) = \langle Aw, w \rangle = 0.$$

故 $w = 0$。即 $\operatorname{Ran}(A)^\perp = \{0\}$。

由 Hilbert 空间分解 $H = \operatorname{Ran}(A) \oplus \operatorname{Ran}(A)^\perp = \operatorname{Ran}(A)$，故 $A$ 满射。$\square$

### 第六步：解的范数估计

由 $A u = f$ 与第一步：
$$\alpha\,\|u\| \leq \|Au\| = \|f\| = \|L\|_{H^\ast},$$
即
$$\|u\| \leq \frac{\|L\|_{H^\ast}}{\alpha}. \quad \blacksquare$$

---

## 备选证明（Banach 不动点版）

更直观的替代：把方程 $Au = f$ 改写为
$$u = u - \rho(Au - f) =: T_\rho(u),$$

其中 $\rho > 0$ 是参数。

**$T_\rho$ 压缩**：
$$\|T_\rho u_1 - T_\rho u_2\|^2 = \|u_1 - u_2\|^2 - 2\rho \langle A(u_1 - u_2), u_1 - u_2 \rangle + \rho^2 \|A(u_1 - u_2)\|^2.$$

代入 $\langle A v, v \rangle \geq \alpha \|v\|^2$ 与 $\|Av\| \leq M\|v\|$：
$$\|T_\rho u_1 - T_\rho u_2\|^2 \leq (1 - 2\rho\alpha + \rho^2 M^2) \|u_1 - u_2\|^2.$$

最优化（取 $\rho = \alpha/M^2$）得压缩系数
$$\sqrt{1 - \alpha^2/M^2} < 1.$$

由 [[Banach 不动点定理|压缩映射原理]] 唯一不动点存在——即 (LM) 的解。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> Lax-Milgram 是 **Riesz + 强制性** 的精妙组合：
> 1. **Riesz 化简**：把双线性 $a(u, v)$ 表示为 $\langle Au, v \rangle$，把 (LM) 化为算子方程 $Au = f$；
> 2. **强制性给出双侧控制**：$\alpha\|u\| \leq \|Au\| \leq M\|u\|$——下界保证单射 + 值域闭，再用 $\operatorname{Ran}^\perp = \{0\}$ 推满射。
>
> 与对称情形（$a$ 是新内积，直接 Riesz）相比，**不对称情形需要"算子化"** 才能处理。Banach 不动点版（备选）更几何：$T_\rho$ 是梯度下降，强制性即"有梯度可以下降"。
>
> 物理含义：**有界 = 能量受控**，**强制 = 能量正定（无零模）**。两者保证微弱解唯一存在。

> [!warning] 强制性是关键
> **反例**：取 $H = \ell^2$，$a(u, v) = \langle Au, v \rangle$，$A: e_n \mapsto e_n / n$。$a$ 有界但不强制（$a(e_n, e_n) = 1/n \to 0$，$\alpha = 0$）。取 $L(v) = \sum v_k$（属于 $\ell^2$ 仅当对应 $f_k = 1$ 不在 $\ell^2$，但形式上 $L$ 在稠密子空间定义）；方程 $u_n / n = 1$ 给 $u_n = n$，$\|u\| = \infty$。**无解或解不在 $H$ 中**。

> [!info] 应用：PDE 弱解
> **标准应用**：考虑 Poisson 方程 $-\Delta u = f$，$u|_{\partial\Omega} = 0$。
>
> 设 $H = H^1_0(\Omega)$（含零迹的 $H^1$ Sobolev 空间），$a(u, v) = \int_\Omega \nabla u \cdot \nabla v\,dx$，$L(v) = \int_\Omega f v\,dx$。
>
> - **有界性**：$|a(u, v)| \leq \|\nabla u\|_{L^2} \|\nabla v\|_{L^2}$（Cauchy-Schwarz）；
> - **强制性**：由 Poincaré 不等式 $\|\nabla u\|_{L^2}^2 \geq C \|u\|_{H^1_0}^2$；
> - **$L$ 有界性**：$|L(v)| \leq \|f\|_{L^2} \|v\|_{L^2} \leq C\|f\|_{L^2} \|v\|_{H^1_0}$（仍由 Poincaré）。
>
> Lax-Milgram 即给出**弱解唯一存在**。这是椭圆型 PDE 求解的标准框架。详见 [[Sobolev嵌入定理]]。
>
> **后续**：弱解的正则性、与经典解的关系、Galerkin 数值近似（有限元方法的理论根据）。

> [!info] 推广
> - **Stampacchia 不等式**：把 (LM) 推广到凸闭子集上的变分不等式，对应有约束极小化；
> - **Babuška-Lax-Milgram 定理**：放宽对称性，允许 $a$ 在两个不同空间 $U \times V$ 上的"inf-sup"条件——是混合有限元、Stokes 问题的关键工具。
