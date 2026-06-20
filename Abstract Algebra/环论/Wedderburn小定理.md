---
title: Wedderburn 小定理
date: 2026-04-11
tags:
  - 抽象代数
  - 环论
  - 除环
  - 有限域
  - 分圆多项式
  - 类方程
---

# Wedderburn 小定理

## 预备定义

> [!note] 除环（division ring / skew field）
> 含单位元 $1 \neq 0$ 的环 $D$，若每个非零元素都有乘法逆元，称为**除环**。
> 若乘法还满足交换律，则 $D$ 为**域**（field）。
>
> 经典的非交换除环：Hamilton 四元数 $\mathbb{H} = \{a + bi + cj + dk\}$（无限除环）。

> [!note] 中心
> 环 $D$ 的**中心**为 $Z(D) = \{z \in D : zx = xz \;\forall x \in D\}$。
> 对有限除环 $D$，$Z(D)$ 是有限域，故 $Z(D) \cong \mathbb{F}_q$（$q = p^n$，某个素数 $p$）。

> [!note] 中心化子
> 对 $x \in D$，其**中心化子**为 $C_D(x) = \{y \in D : yx = xy\}$。
> $C_D(x)$ 是包含 $Z(D)$ 的 $D$ 的子除环。

> [!note] 分圆多项式
> 第 $d$ 个**分圆多项式**（cyclotomic polynomial）定义为
> $$\Phi_d(x) = \prod_{\substack{\zeta^d = 1 \\ \zeta \text{ 为本原}}} (x - \zeta) \in \mathbb{Z}[x],$$
> 其中乘积遍历所有本原 $d$ 次单位根。$\deg \Phi_d = \varphi(d)$（Euler 函数）。
>
> 基本性质：$x^d - 1 = \prod_{e \mid d} \Phi_e(x)$，故对 $e \mid d$、$e < d$，$\Phi_d(x) \mid \dfrac{x^d - 1}{x^e - 1}$。

> [!abstract] 引理：$|\Phi_d(q)| > q - 1$ 对整数 $q \geq 2$，$d \geq 2$
> $$\Phi_d(q) = \prod_{\zeta} (q - \zeta),$$
> 其中 $\zeta$ 遍历本原 $d$ 次单位根。对 $d \geq 2$，每个 $\zeta \neq 1$，故
> $$|q - \zeta|^2 = q^2 - 2q\cos\theta + 1 > q^2 - 2q + 1 = (q-1)^2,$$
> 其中 $\theta = \arg\zeta \neq 0$（因 $\cos\theta < 1$）。故 $|q - \zeta| > q - 1$ 对每个因子成立，从而
> $$|\Phi_d(q)| = \prod_\zeta |q - \zeta| > (q - 1)^{\varphi(d)} \geq q - 1.$$

$\square$

---

## 定理

**每个有限除环都是域。**

即：若 $D$ 为有限除环，则 $D$ 的乘法是交换的。

> [!info] 定理的惊人之处
> 有限性与交换性看似毫无关系——无限除环（如四元数 $\mathbb{H}$）完全可以非交换。但 Wedderburn 定理表明，在有限世界中，除环的结构受到极强的算术约束，强到**迫使交换性成立**。
>
> 等价表述：有限域的完整分类为 $\mathbb{F}_{p^n}$（每个阶有且仅有一个，至同构），不遗漏任何非交换的可能。

---

## 证明

设 $D$ 为有限除环，$F = Z(D) \cong \mathbb{F}_q$（$q = p^n$）。$D$ 是 $F$ 上的有限维向量空间，设 $\dim_F D = d$，则 $|D| = q^d$。

**目标**：证明 $d = 1$，即 $D = F$（交换）。

**反证法**：假设 $d \geq 2$。

### 第一步：乘法群的类方程

$D^\times = D \setminus \{0\}$ 是阶为 $q^d - 1$ 的（一般非交换）群。$D^\times$ 通过共轭作用在自身上：$g \cdot x = gxg^{-1}$。

对 $x \in D^\times$，共轭类大小 $= [D^\times : C_{D^\times}(x)]$。

- 若 $x \in F^\times = Z(D^\times)$：共轭类大小为 $1$，共 $q - 1$ 个。
- 若 $x \notin F^\times$：$C_D(x)$ 是严格介于 $F$ 和 $D$ 之间的子除环，$\dim_F C_D(x) = d_x$，其中 $d_x \mid d$，$1 < d_x < d$。此时 $|C_{D^\times}(x)| = q^{d_x} - 1$，共轭类大小为 $\dfrac{q^d - 1}{q^{d_x} - 1}$。

> [!info] 为何 $d_x \mid d$
> $C_D(x)$ 是包含 $F$ 的子除环。$D$ 是 $C_D(x)$ 上的有限维向量空间，设维数为 $e$，则 $q^d = |D| = |C_D(x)|^e = q^{d_x e}$，故 $d = d_x e$，即 $d_x \mid d$。

类方程：

$$q^d - 1 = (q - 1) + \sum_{x} \frac{q^d - 1}{q^{d_x} - 1}, \quad \cdots (\ast)$$

其中求和遍历所有非中心共轭类的代表元（每个对应某个 $d_x \mid d$，$1 < d_x < d$）。

$\square$

### 第二步：分圆多项式整除性

由 $x^d - 1 = \prod_{e \mid d} \Phi_e(x)$，得

$$\frac{x^d - 1}{x^{d_x} - 1} = \prod_{\substack{e \mid d \\ e \nmid d_x}} \Phi_e(x).$$

当 $d_x \mid d$ 且 $d_x < d$ 时，$d$ 本身满足 $d \mid d$ 但 $d \nmid d_x$（因 $d_x < d$），故 $\Phi_d(x)$ 出现在上述乘积中：

$$\Phi_d(x) \;\Big|\; \frac{x^d - 1}{x^{d_x} - 1} \quad \text{对每个 } d_x \mid d,\; d_x < d.$$

令 $x = q$：$\Phi_d(q)$ 整除类方程 $(\ast)$ 中每个求和项 $\dfrac{q^d - 1}{q^{d_x} - 1}$。

$\square$

### 第三步：$\Phi_d(q)$ 整除 $q - 1$

由 $(\ast)$：

$$q - 1 = (q^d - 1) - \sum_x \frac{q^d - 1}{q^{d_x} - 1}.$$

$\Phi_d(q)$ 整除 $q^d - 1$（因 $\Phi_d \mid x^d - 1$），也整除每个求和项（第二步）。故

$$\Phi_d(q) \mid (q - 1). \quad \cdots (\star)$$

$\square$

### 第四步：矛盾

由引理，$d \geq 2$ 且 $q \geq 2$ 时

$$|\Phi_d(q)| > q - 1.$$

但 $(\star)$ 要求 $\Phi_d(q)$ 整除 $q - 1$，即 $|\Phi_d(q)| \leq q - 1$。

**矛盾！**

故 $d = 1$，$D = F$ 是域。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明的三大支柱——群论、环论、数论——在类方程的一个等式中交汇：
>
> 1. **群论（类方程）**：$D^\times$ 的共轭类分解给出算术恒等式 $(\ast)$；
> 2. **环论（子除环结构）**：中心化子 $C_D(x)$ 的维数 $d_x$ 整除 $d$，控制了共轭类的大小；
> 3. **数论（分圆多项式）**：$\Phi_d(q) \mid (q^d - 1)/(q^{d_x}-1)$ 对每个 $d_x \mid d$、$d_x < d$ 成立 → $\Phi_d(q) \mid (q-1)$ → 与 $|\Phi_d(q)| > q - 1$ 矛盾。
>
> 本质上，分圆多项式的**大小估计**粉碎了非交换除环存在的算术可能性。$q - 1$ 太小，容不下 $\Phi_d(q)$。

> [!warning] 推广与联系
> - **有限域的唯一性**：结合 Wedderburn 定理和有限域理论，阶为 $p^n$ 的域存在且唯一（至同构），记为 $\mathbb{F}_{p^n}$。不存在其他有限除环。
> - **Artin-Zorn 定理**：每个有限**交替**除环（alternative division ring，满足 $(xx)y = x(xy)$ 和 $(yx)x = y(xx)$）也是域。证明方法类似。
> - **无限情形失败**：Hamilton 四元数 $\mathbb{H}$ 是无限非交换除环。有限性在证明中不可或缺（用于保证 $Z(D)$ 是有限域、类方程是有限和、$q$ 是整数）。
> - **与 [[Sylow定理]] 的方法论联系**：两者都利用**群作用 + 模 $p$ 的算术**提取结构信息。Sylow 用不动点定理（$|X| \equiv |X^P| \pmod{p}$），Wedderburn 用分圆整除性（$\Phi_d(q) \mid (q-1)$）。
