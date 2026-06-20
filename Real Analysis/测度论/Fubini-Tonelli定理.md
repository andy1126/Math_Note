---
title: Fubini-Tonelli 定理
date: 2026-05-28
tags:
  - 实分析
  - 测度论
  - 乘积测度
  - Fubini
  - Tonelli
  - 累次积分
---

# Fubini-Tonelli 定理

## 预备定义

> [!note] σ-有限测度
> 称测度空间 $(X, \mathcal{M}, \mu)$ 为 **σ-有限**，若 $X = \bigcup_{n=1}^\infty X_n$ 其中 $X_n \in \mathcal{M}$ 且 $\mu(X_n) < +\infty$。Lebesgue 测度即 σ-有限（$\mathbb{R}^n = \bigcup_k [-k, k]^n$）。

> [!note] 乘积 σ-代数
> 设 $(X, \mathcal{M})$，$(Y, \mathcal{N})$ 为可测空间。**矩形** $A \times B$（$A \in \mathcal{M}$，$B \in \mathcal{N}$）生成的 $X \times Y$ 上的 σ-代数记作 $\mathcal{M} \otimes \mathcal{N}$。

> [!note] 乘积测度
> 设 $\mu, \nu$ 均为 σ-有限。存在唯一的 $X \times Y$ 上的测度 $\mu \otimes \nu$，使得
> $$(\mu \otimes \nu)(A \times B) = \mu(A) \cdot \nu(B), \quad A \in \mathcal{M},\ B \in \mathcal{N}$$
> （约定 $0 \cdot \infty = 0$）。存在唯一性由 Carathéodory 扩张定理保证。

> [!note] 切片函数
> 对 $f: X \times Y \to \overline{\mathbb{R}}$，固定 $x \in X$，定义 $f_x: Y \to \overline{\mathbb{R}}$ 为 $f_x(y) = f(x, y)$；对称地定义 $f^y$。

> [!abstract] 引理：可测性的切片
> 设 $f$ 为 $\mathcal{M} \otimes \mathcal{N}$-可测。则
> 1. 对一切 $x$，$f_x$ 是 $\mathcal{N}$-可测；
> 2. 对一切 $y$，$f^y$ 是 $\mathcal{M}$-可测。
>
> **证明骨架**：先验证对矩形 $A \times B$ 的指示函数 $\mathbf{1}_{A \times B}(x, y) = \mathbf{1}_A(x)\mathbf{1}_B(y)$ 成立；用单调类定理（或 π-λ 定理）推广到全体 $\mathcal{M} \otimes \mathcal{N}$ 可测集；再用简单函数逼近推广到非负可测函数。$\square$

> [!abstract] 引理：Lebesgue 控制收敛定理 (DCT)
> 见 [[Lebesgue控制收敛定理]]。

---

## 定理

设 $(X, \mathcal{M}, \mu)$，$(Y, \mathcal{N}, \nu)$ 均为 σ-有限测度空间。

### Tonelli 定理（非负情形）

若 $f: X \times Y \to [0, +\infty]$ 为 $\mathcal{M} \otimes \mathcal{N}$-可测，则

**(T1)** $x \mapsto \int_Y f(x, y)\,d\nu(y)$ 是 $\mathcal{M}$-可测；对称地，$y \mapsto \int_X f(x, y)\,d\mu(x)$ 是 $\mathcal{N}$-可测；

**(T2)** 三种积分相等：
$$\int_{X \times Y} f\, d(\mu \otimes \nu) = \int_X\!\left(\int_Y f(x, y)\,d\nu(y)\right) d\mu(x) = \int_Y\!\left(\int_X f(x, y)\,d\mu(x)\right) d\nu(y).$$

### Fubini 定理（可积情形）

若 $f \in L^1(\mu \otimes \nu)$，则

**(F1)** $f_x \in L^1(\nu)$ 对 $\mu$-a.e. $x$；$f^y \in L^1(\mu)$ 对 $\nu$-a.e. $y$；

**(F2)** $x \mapsto \int_Y f(x, y)\,d\nu(y)$ 属于 $L^1(\mu)$；对称地；

**(F3)** 三种积分相等：
$$\int_{X \times Y} f = \int_X\!\int_Y f\,d\nu\,d\mu = \int_Y\!\int_X f\,d\mu\,d\nu.$$

---

## 第(i)部分的证明：Tonelli

### 第一步：对矩形指示函数

设 $E = A \times B$（$A \in \mathcal{M}$，$B \in \mathcal{N}$）。则
$$\mathbf{1}_E(x, y) = \mathbf{1}_A(x)\, \mathbf{1}_B(y).$$

切片 $(\mathbf{1}_E)_x = \mathbf{1}_A(x)\, \mathbf{1}_B$，故
$$\int_Y (\mathbf{1}_E)_x\,d\nu = \mathbf{1}_A(x)\, \nu(B).$$

这是 $\mathcal{M}$-可测的（$\mathbf{1}_A$ 可测，$\nu(B)$ 是常数）。再积分：
$$\int_X \int_Y \mathbf{1}_E\,d\nu\,d\mu = \nu(B) \int_X \mathbf{1}_A\,d\mu = \mu(A)\nu(B) = (\mu \otimes \nu)(E). \quad \square$$

### 第二步：扩展到 $\mathcal{M} \otimes \mathcal{N}$-可测集 $E$

记 $\mathcal{E} = \{E \in \mathcal{M} \otimes \mathcal{N} :$ Tonelli 对 $\mathbf{1}_E$ 成立 $\}$。第一步表明矩形 $\subseteq \mathcal{E}$。

**断言**：$\mathcal{E}$ 是单调类（对单调极限封闭）。

- $E_n \uparrow E$：$\mathbf{1}_{E_n} \uparrow \mathbf{1}_E$。对每个 $x$ 应用 MCT 于内积分得 $\int (\mathbf{1}_{E_n})_x\,d\nu \uparrow \int (\mathbf{1}_E)_x\,d\nu$，可测性继承。再对外积分应用 MCT。乘积测度由 σ-加性也单调递增。三者相等沿极限保持。
- $E_n \downarrow E$（用 σ-有限性）：先约束到有限测度子空间再如上处理。

由单调类定理，矩形生成的 σ-代数 $\subseteq \mathcal{E}$，即 $\mathcal{M} \otimes \mathcal{N} \subseteq \mathcal{E}$。$\square$

> [!important] σ-有限性的关键作用
> 单调类论证要求**乘积测度有限**才能处理减法 / 下降序列。σ-有限性将 $X \times Y$ 切成可数个有限测度块，逐块论证再合并。**若失去 σ-有限性，Fubini-Tonelli 通常失败**——见反例。

### 第三步：扩展到非负简单函数

设 $\varphi = \sum_{k=1}^n c_k \mathbf{1}_{E_k}$（$c_k \geq 0$，$E_k \in \mathcal{M} \otimes \mathcal{N}$）。由第二步与积分线性，Tonelli 对 $\varphi$ 成立。$\square$

### 第四步：非负可测 $f$ 的简单函数逼近

由简单函数逼近定理（[[可测函数的逐点极限仍可测]]），存在 $0 \leq \varphi_n \uparrow f$ 为简单函数。

- 切片 $(\varphi_n)_x \uparrow f_x$。MCT：$\int_Y (\varphi_n)_x\,d\nu \uparrow \int_Y f_x\,d\nu$，左端 $\mathcal{M}$-可测、单调递增故极限 $\mathcal{M}$-可测——(T1) 得证。
- 对外积分再 MCT：$\int_X \int_Y \varphi_n\,d\nu\,d\mu \uparrow \int_X \int_Y f\,d\nu\,d\mu$。
- 乘积积分 $\int \varphi_n\,d(\mu\otimes\nu) \uparrow \int f\,d(\mu\otimes\nu)$（MCT）。
- 第三步保证 $\varphi_n$ 的三种积分相等。

取极限：(T2) 得证。$\square$

---

## 第(ii)部分的证明：Fubini

设 $f \in L^1(\mu \otimes \nu)$。

### 第一步：分解 $f = f^+ - f^-$

$f^\pm = \max(\pm f, 0) \geq 0$ 可测。由 $|f| = f^+ + f^-$ 与 $\int |f| < \infty$：
$$\int f^+\,d(\mu \otimes \nu) < \infty,\quad \int f^-\,d(\mu \otimes \nu) < \infty.$$

由 Tonelli 应用于 $f^\pm$：
$$\int_X \!\int_Y f^\pm\,d\nu\,d\mu = \int_{X \times Y} f^\pm < \infty.$$

故 $\int_Y f^\pm(x, y)\,d\nu(y) < \infty$ 对 $\mu$-a.e. $x$（否则左端 $= \infty$，矛盾）。即 $(f_x)^\pm \in L^1(\nu)$ a.e.，故 $f_x \in L^1(\nu)$ a.e.——(F1) 得证。

### 第二步：积分线性

定义零测集 $N = \{x : f_x \notin L^1(\nu)\}$。对 $x \notin N$，
$$\int_Y f_x\,d\nu = \int_Y (f^+)_x\,d\nu - \int_Y (f^-)_x\,d\nu.$$

修改在 $N$ 上为 $0$（不改变 $\mu$-积分）。两端均 $\mathcal{M}$-可测、均在 $L^1(\mu)$ 中（由 Tonelli + 有限性），故差也是。（F2）得证。

### 第三步：三个积分相等

由 Tonelli 应用于 $f^+, f^-$：
$$\int_X\!\int_Y f\,d\nu\,d\mu = \int_X\!\int_Y f^+\,d\nu\,d\mu - \int_X\!\int_Y f^-\,d\nu\,d\mu = \int f^+ - \int f^- = \int f.$$

对称地，对 $Y$-累次积分也相等。(F3) 得证。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明骨架是经典的**测度论标准延伸链**：
> $$\text{矩形指示} \to \text{可测集指示} \to \text{简单函数} \to \text{非负可测} \to \text{可积}.$$
> 每一步都用前一步 + 单调类 / MCT / DCT 推进。
>
> Tonelli 是 Fubini 的"非负预备"——先在 $f^\pm \geq 0$ 上无条件交换累次积分，再用 $|f| \in L^1$ 把 $f^\pm$ 都拉入有限范围，最后由线性合并。
>
> **三步骤口诀**：(1) 验证 $\int |f| < \infty$（用 Tonelli！）；(2) 才能对 $f$ 用 Fubini 交换；(3) 切片 a.e. 良定。
>
> 实务中先用 Tonelli 算 $\int\int |f|$，若有限即正当地应用 Fubini。

> [!warning] σ-有限性不可省
> 反例：$X = Y = [0, 1]$，$\mu$ = Lebesgue 测度，$\nu$ = 计数测度（非 σ-有限）。$f = \mathbf{1}_{\{(x,x): x \in [0,1]\}}$。则
> - $\int_Y f(x, y)\,d\nu(y) = \nu(\{x\}) = 1$，故 $\int_X \int_Y f = 1$；
> - $\int_X f(x, y)\,d\mu(x) = \mu(\{y\}) = 0$，故 $\int_Y \int_X f = 0$。
>
> 两个累次积分都有限但不相等。

> [!warning] $|f| \in L^1$ 不可省（Fubini 情形）
> 反例：$X = Y = \mathbb{N}$ 配计数测度。$f(m, n) = \delta_{m,n} - \delta_{m, n+1}$。则
> - $\sum_n \sum_m f = \sum_n 0 = 0$；
> - $\sum_m \sum_n f = 1 + 0 + 0 + \cdots = 1$。
>
> 失败原因：$\sum |f(m, n)| = \infty$，不在 $L^1$。

> [!info] 应用：积分换序 / 卷积 / Plancherel
> Fubini-Tonelli 是测度论分析的工作母机：
> - **卷积**：$\|f \ast g\|_{L^1} \leq \|f\|_{L^1} \|g\|_{L^1}$ 即用 Fubini 交换；
> - **Plancherel 定理**：用 Fubini 处理 $\widehat{f \ast g} = \widehat{f} \cdot \widehat{g}$；
> - **概率论**：联合分布 = 边缘分布 × 条件分布的乘积积分；
> - **PDE**：Green 函数表示解时用 Fubini 交换 $x$, $y$ 积分。
