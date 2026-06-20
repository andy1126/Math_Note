---
title: Radon-Nikodym 定理
date: 2026-05-28
tags:
  - 实分析
  - 测度论
  - Radon-Nikodym
  - 绝对连续
  - 测度
  - Hilbert空间
---

# Radon-Nikodym 定理

## 预备定义

> [!note] 符号测度
> 称 $\mathcal{M}$ 上的可数可加函数 $\lambda: \mathcal{M} \to [-\infty, +\infty]$ 为**符号测度**（signed measure），若 $\lambda(\varnothing) = 0$ 且 $\lambda$ 取值仅可取 $+\infty$ 或 $-\infty$ 之一（不能两者都取）。

> [!note] 绝对连续
> 设 $\mu, \nu$ 为 $(X, \mathcal{M})$ 上的测度。称 $\nu$ 对 $\mu$ **绝对连续**（absolutely continuous），记 $\nu \ll \mu$，若
> $$\mu(A) = 0 \Longrightarrow \nu(A) = 0, \quad \forall\, A \in \mathcal{M}.$$

> [!note] 奇异
> 称 $\mu, \nu$ **互相奇异**（mutually singular），记 $\mu \perp \nu$，若存在 $A \in \mathcal{M}$ 使 $\mu(A) = 0$ 与 $\nu(A^c) = 0$。

> [!note] σ-有限
> 同 [[Fubini-Tonelli定理]] 中定义。本节默认所有测度均为 σ-有限。

> [!abstract] 引理：Hilbert 空间表示定理 (Riesz)
> 设 $H$ 为 Hilbert 空间，$L: H \to \mathbb{R}$ 为有界线性泛函。则存在唯一 $g \in H$ 使
> $$L(f) = \langle f, g \rangle, \quad \forall\, f \in H.$$
> 详见 [[Hilbert空间正交基的基数不变性]]（相关 Hilbert 空间笔记）。

> [!abstract] 引理：MCT / DCT
> 见 [[单调收敛定理]]、[[Lebesgue控制收敛定理]]。

---

## 定理（Radon-Nikodym, von Neumann 证法）

设 $(X, \mathcal{M})$ 为可测空间，$\mu, \nu$ 为其上的 **σ-有限**测度，且 $\nu \ll \mu$。则存在可测函数 $f: X \to [0, +\infty)$ 使

$$\nu(A) = \int_A f\,d\mu, \quad \forall\, A \in \mathcal{M}.$$

$f$ 在 $\mu$-a.e. 意义下唯一，记作 $f = \dfrac{d\nu}{d\mu}$，称 **Radon-Nikodym 导数**。

**Lebesgue 分解推论**：去掉 $\nu \ll \mu$ 假设，任何 σ-有限符号测度 $\nu$ 可唯一分解为 $\nu = \nu_{\mathrm{ac}} + \nu_{\mathrm{s}}$，其中 $\nu_{\mathrm{ac}} \ll \mu$，$\nu_{\mathrm{s}} \perp \mu$。

---

## 证明

### 前提验证：化归到有限测度情形

由 σ-有限性，$X = \bigsqcup_n X_n$，$\mu(X_n) < \infty$ 且 $\nu(X_n) < \infty$（取交并细化）。若在每个 $X_n$ 上构造 $f_n \geq 0$ 使 $\nu(A) = \int_A f_n\,d\mu$（$A \subseteq X_n$），则 $f = \sum_n f_n \mathbf{1}_{X_n}$ 即所求。**以下假设 $\mu(X), \nu(X) < \infty$。**

### 第一步：在 $L^2(\mu + \nu)$ 上构造线性泛函

令 $\sigma = \mu + \nu$（有限测度）。考虑 Hilbert 空间 $H = L^2(\sigma)$，内积 $\langle f, g \rangle_\sigma = \int fg\,d\sigma$。

定义
$$L(f) := \int_X f\,d\nu, \quad f \in H.$$

> [!important] $L$ 的有界性（用到 $\nu \leq \sigma$）
> 由 Cauchy-Schwarz：
> $$|L(f)| \leq \int |f|\,d\nu \leq \int |f|\,d\sigma \leq \|f\|_{L^2(\sigma)} \cdot \sigma(X)^{1/2}.$$
> 故 $L$ 是 $H$ 上的有界线性泛函，$\|L\| \leq \sigma(X)^{1/2}$。

### 第二步：Riesz 表示

由 Riesz 表示定理，存在 $g \in H = L^2(\sigma)$ 使
$$\int_X f\,d\nu = \int_X f g\,d\sigma, \quad \forall\, f \in L^2(\sigma). \quad \cdots (\ast)$$

### 第三步：$0 \leq g < 1$ σ-a.e.

#### 3.1 $g \geq 0$ σ-a.e.

取 $A = \{g < 0\}$，$f = \mathbf{1}_A$。则 $f \in L^2(\sigma)$，
$$\nu(A) = \int_A g\,d\sigma \leq 0.$$

由 $\nu \geq 0$，$\nu(A) = 0 = \int_A g\,d\sigma$。但 $g < 0$ 在 $A$ 上，故 $\sigma(A) = 0$。$\square$

#### 3.2 $g < 1$ σ-a.e.

取 $A = \{g \geq 1\}$，$f = \mathbf{1}_A$：
$$\nu(A) = \int_A g\,d\sigma \geq \sigma(A) = \mu(A) + \nu(A).$$

故 $\mu(A) \leq 0$，即 $\mu(A) = 0$。由 $\nu \ll \mu$，$\nu(A) = 0$，故 $\sigma(A) = 0$。$\square$

> [!important] $\nu \ll \mu$ 在此处出场
> 整个证明 $\nu \ll \mu$ 仅在此处使用一次：用于把 $\mu(A) = 0$ 升级为 $\sigma(A) = 0$。若无此假设，$\{g \geq 1\}$ 可能 $\mu$-零测但 $\nu$-非零，构造仅给出 Lebesgue 分解而非 R-N 表示。

修改 $g$ 在零测集上：可设 $0 \leq g(x) < 1$ 处处。

### 第四步：化 $(\ast)$ 为 R-N 形式

$(\ast)$ 改写：$\sigma = \mu + \nu$，故
$$\int f\,d\nu = \int fg\,d\mu + \int fg\,d\nu,$$

即
$$\int f(1 - g)\,d\nu = \int fg\,d\mu, \quad \forall\, f \in L^2(\sigma). \quad \cdots (\sharp)$$

> [!info] 直觉：将 $g$ 改写为 $f := \dfrac{g}{1-g}$
> 想取测试函数 $f = h/(1-g)$（$h \geq 0$ 可测），令 $(\sharp)$ 左端变成 $\int h\,d\nu$。但需先确认 $f \in L^2(\sigma)$。这要做近似——用 $f_n = h \mathbf{1}_{\{g \leq 1 - 1/n\}} / (1 - g)$，再 MCT 取极限。

#### 4.1 对 $f \in L^2(\sigma)$ 的近似

固定 $A \in \mathcal{M}$，定义
$$f_n(x) = \frac{\mathbf{1}_A(x)}{1 - g(x)} \cdot \mathbf{1}_{\{g(x) \leq 1 - 1/n\}}.$$

$f_n$ 有界（$|f_n| \leq n$），故 $f_n \in L^2(\sigma)$。代入 $(\sharp)$：
$$\int_A (1 - g) \cdot \frac{\mathbf{1}_{\{g \leq 1-1/n\}}}{1 - g}\,d\nu = \int_A g \cdot \frac{\mathbf{1}_{\{g \leq 1-1/n\}}}{1 - g}\,d\mu,$$

即
$$\int_A \mathbf{1}_{\{g \leq 1 - 1/n\}}\,d\nu = \int_A \frac{g}{1 - g} \cdot \mathbf{1}_{\{g \leq 1-1/n\}}\,d\mu. \quad \cdots (\flat)$$

#### 4.2 $n \to \infty$：MCT 双边

- 左端 $\mathbf{1}_{\{g \leq 1 - 1/n\}} \uparrow \mathbf{1}_{\{g < 1\}} = 1$ σ-a.e.（第 3.2 步）。由 MCT 左端 $\uparrow \nu(A)$。
- 右端 $\dfrac{g}{1-g}\mathbf{1}_{\{g \leq 1-1/n\}} \uparrow \dfrac{g}{1-g}$ σ-a.e.。由 MCT 右端 $\uparrow \int_A \dfrac{g}{1-g}\,d\mu$。

故
$$\nu(A) = \int_A \frac{g}{1 - g}\,d\mu, \quad \forall\, A \in \mathcal{M}.$$

### 第五步：取 $f = \dfrac{g}{1 - g}$

由 $0 \leq g < 1$，$f = \dfrac{g}{1-g} \in [0, +\infty)$ 可测，且
$$\nu(A) = \int_A f\,d\mu, \quad \forall\, A \in \mathcal{M}. \quad \square$$

### 第六步：唯一性

设 $f_1, f_2$ 均满足 $\nu(A) = \int_A f_i\,d\mu$ 对一切 $A$。则对 $A = \{f_1 > f_2\}$：
$$0 = \nu(A) - \nu(A) = \int_A (f_1 - f_2)\,d\mu.$$

由 $f_1 - f_2 > 0$ 在 $A$ 上，必 $\mu(A) = 0$。对称 $\mu\{f_2 > f_1\} = 0$。故 $f_1 = f_2$ μ-a.e.。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想（von Neumann 法）
> 这是测度论中极优雅的"**借用 Hilbert 几何**"证法：
> 1. **打包**：把 $\mu, \nu$ 加成 $\sigma = \mu + \nu$，工作于 $L^2(\sigma)$；
> 2. **表示**：$f \mapsto \int f\,d\nu$ 是 $L^2(\sigma)$ 上的有界线性泛函；Riesz 给出 $g \in L^2(\sigma)$ 表示之；
> 3. **范围分析**：用测试函数 $f = \mathbf{1}_{\{g < 0\}}, \mathbf{1}_{\{g \geq 1\}}$ 锁定 $0 \leq g < 1$；
> 4. **代数变形**：$(\ast)$ 改写为 $\int f(1-g)\,d\nu = \int fg\,d\mu$，取代换 $f \to f/(1-g)$ 得 $\nu(A) = \int_A \dfrac{g}{1-g}\,d\mu$。
>
> **$\nu \ll \mu$ 的唯一使用点**：把 $\mu(\{g \geq 1\}) = 0$ 升级为 $\sigma(\{g \geq 1\}) = 0$，从而 $g < 1$ σ-a.e.。

> [!warning] σ-有限性不可省
> 反例：$X = \{0\}$，$\mathcal{M} = \{\varnothing, X\}$，$\mu$ 是 $\delta_0$（点测度），$\nu(\{0\}) = +\infty$。则 $\nu \ll \mu$（$\mu(\varnothing)=0 \Rightarrow \nu(\varnothing) = 0$），但找不到 $f: X \to [0, \infty)$ 使 $\nu = \int f\,d\mu$（任何有限 $f(0)$ 都不够）。失败原因：$\nu$ 非 σ-有限。

> [!info] Lebesgue 分解
> 去掉 $\nu \ll \mu$ 假设，按本证明：第 3.2 步无法保证 $\sigma(\{g \geq 1\}) = 0$，但 $\mu(\{g \geq 1\}) = 0$ 仍成立。令 $E = \{g \geq 1\}$（$\mu(E) = 0$）。在 $E^c$ 上得 $\nu_{\mathrm{ac}}(A) = \int_A \dfrac{g}{1-g}\mathbf{1}_{E^c}\,d\mu \ll \mu$；在 $E$ 上 $\nu_{\mathrm{s}}(A) = \nu(A \cap E)$ 满足 $\nu_{\mathrm{s}} \perp \mu$（因 $\mu(E) = 0$）。

> [!info] 应用
> - **概率论**：似然函数比 $\dfrac{dP_1}{dP_2}$；条件期望（$E[X|\mathcal{G}]$ 即 R-N 导数）；Girsanov 定理。
> - **泛函分析**：$L^p$-$L^q$ 对偶（$1 < p < \infty$）的表示定理；测度的极分解。
> - **PDE 与 Sobolev**：弱导数与函数表示——绝对连续度量的 R-N 导数与几乎处处可微的衔接。
> - **统计力学**：Boltzmann 分布的微观-宏观刻画。
