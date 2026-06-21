---
title: Poisson 方程的变分结构
date: 2026-06-21
tags:
  - 数学物理方法
  - 偏微分方程
  - 变分法
  - Sobolev空间
  - 弱解
---

# Poisson 方程的变分结构

## Dirichlet 原理

> [!note] Dirichlet 原理（古典形式）
> 设 $\Omega \subset \mathbb{R}^n$ 为有界区域。在所有满足边界条件 $u = g$（$\partial\Omega$）的函数中，Laplace 方程 $-\Delta u = 0$ 的解极小化 Dirichlet 能量：
> $$E[u] = \frac{1}{2} \int_\Omega |\nabla u|^2 dx$$
> 反之，Dirichlet 能量的极小元必是 Laplace 方程的解。

**证明**（变分法）：设 $u$ 为 Dirichlet 能量在容许函数类 $\mathcal{A} = \{u \in C^2(\Omega) \cap C(\overline{\Omega}) : u|_{\partial\Omega} = g\}$ 上的极小元。对任意 $v \in C_0^\infty(\Omega)$，令 $j(\varepsilon) = E[u + \varepsilon v]$。极小性给出 $j'(0) = 0$：

$$
0 = \frac{d}{d\varepsilon}\Big|_{\varepsilon=0} \frac{1}{2} \int_\Omega |\nabla(u+\varepsilon v)|^2 dx
  = \int_\Omega \nabla u \cdot \nabla v \, dx
  = -\int_\Omega (\Delta u) v \, dx
$$

由 $v$ 的任意性，$-\Delta u = 0$ 在 $\Omega$ 内成立。反之，若 $-\Delta u = 0$、$u|_{\partial\Omega} = g$，则对任意 $w \in \mathcal{A}$ 令 $v = w - u$（$v|_{\partial\Omega} = 0$）：

$$
E[w] = E[u] + E[v] + \int_\Omega \nabla u \cdot \nabla v \, dx
     = E[u] + \frac{1}{2} \int_\Omega |\nabla v|^2 dx \geq E[u]
$$

故 $u$ 确实是极小元。$\square$

> [!note] 推广到 Poisson 方程
> 对 $-\Delta u = f$、$u|_{\partial\Omega} = 0$，对应的能量泛函为：
> $$E[u] = \frac{1}{2} \int_\Omega |\nabla u|^2 dx - \int_\Omega f u \, dx$$
>
> 在 $H_0^1(\Omega)$ 上极小化此泛函等价于求解 Poisson 方程。

---

## 弱形式与 Sobolev 空间

古典的 Dirichlet 原理假设极小元存在且有二阶连续导数，但这需要事先验证。Sobolev 空间框架给出严格的数学基础。

> [!note] 弱形式（Weak Formulation）
> 对 $-\Delta u = f$ 在 $\Omega$、$u = 0$ 在 $\partial\Omega$，取试验函数 $v \in C_0^\infty(\Omega)$，分部积分得：
> $$\int_\Omega \nabla u \cdot \nabla v \, dx = \int_\Omega f v \, dx$$
>
> 此式**无需 $u$ 有二阶导数**，只需 $u, v$ 属于 Sobolev 空间 $H_0^1(\Omega)$。

**定义（弱解）**：对 $f \in L^2(\Omega)$，若 $u \in H_0^1(\Omega)$ 满足

$$
a(u, v) := \int_\Omega \nabla u \cdot \nabla v \, dx = \int_\Omega f v \, dx =: F(v), \quad \forall v \in H_0^1(\Omega)
$$

则称 $u$ 为 Dirichlet 问题的**弱解**。

> [!note] 双线性形式 $a(\cdot, \cdot)$ 的性质
> 1. **有界性**：$|a(u,v)| \leq \|u\|_{H^1} \|v\|_{H^1}$（Cauchy-Schwarz）
> 2. **强制性**（椭圆性）：若 $\Omega$ 有界，由 **Poincaré 不等式**：
>    $$\|u\|_{L^2(\Omega)} \leq C_\Omega \|\nabla u\|_{L^2(\Omega)}, \quad \forall u \in H_0^1(\Omega)$$
>    得 $a(u, u) = \|\nabla u\|_{L^2}^2 \geq \frac{1}{1+C_\Omega^2} \|u\|_{H^1}^2$

---

## Lax-Milgram 定理

> [!abstract] Lax-Milgram 定理
> 设 $H$ 为实 Hilbert 空间，$a: H \times H \to \mathbb{R}$ 为双线性形式，满足：
> 1. **有界性**：$|a(u,v)| \leq M \|u\| \|v\|$，$\forall u, v \in H$
> 2. **强制性**：$a(u,u) \geq \alpha \|u\|^2$，$\forall u \in H$（$\alpha > 0$）
>
> 则对任意有界线性泛函 $F \in H^*$，存在**唯一**的 $u \in H$ 使得
> $$a(u, v) = F(v), \quad \forall v \in H$$
> 且 $\|u\| \leq \frac{1}{\alpha} \|F\|_{H^*}$。

**证明思路**：对每个固定的 $u$，$v \mapsto a(u,v)$ 为有界线性泛函。由 Riesz 表示定理，
存在有界线性算子 $A: H \to H$ 使 $a(u,v) = \langle A u, v \rangle$。$A$ 有界且单射（强制性保证 $\ker A = \{0\}$）。证明 $A$ 满射的关键是证明 $\operatorname{ran} A$ 在 $H$ 中稠密且闭。强制性给出 $\operatorname{ran} A$ 是闭的；若 $\operatorname{ran} A \neq H$，则存在非零 $w \perp \operatorname{ran} A$，导出 $a(w,w) = \langle A w, w \rangle = 0$，与强制性矛盾。故 $A$ 为 $H \to H$ 的同构。令 $u = A^{-1} R_F$（$R_F$ 为 $F$ 的 Riesz 表示）即得解。$\square$

**直接推论**：对 Poisson 方程的弱形式 $a(u,v) = \int_\Omega \nabla u \cdot \nabla v$，$F(v) = \int_\Omega f v$，Lax-Milgram 定理保证对任意 $f \in L^2(\Omega)$ 存在唯一的弱解 $u \in H_0^1(\Omega)$。

---

## 等效极小原理

弱解 $u \in H_0^1(\Omega)$ 也是如下极小化问题的唯一解：

$$
u = \operatorname{argmin}_{v \in H_0^1(\Omega)} \left( \frac{1}{2} a(v,v) - F(v) \right)
$$

**证明**：设 $u$ 满足 $a(u,v)=F(v)$。对任意 $v \in H_0^1(\Omega)$，令 $w = v - u$，则

$$
\begin{aligned}
\left(\frac{1}{2} a(v,v) - F(v)\right) - \left(\frac{1}{2} a(u,u) - F(u)\right)
&= a(u,w) + \frac{1}{2} a(w,w) - F(w) \\
&= \frac{1}{2} a(w,w) \geq \frac{\alpha}{2} \|w\|^2 \geq 0
\end{aligned}
$$

故 $u$ 是唯一极小元。反之，若 $u$ 极小化上述泛函，取变分方向可得 Euler-Lagrange 方程即弱形式。

---

## 一维两点边值问题

考虑最简单的情形：$-u'' = f$ 在 $(0,1)$ 上，$u(0)=u(1)=0$。

**弱形式**：
$$
a(u, v) = \int_0^1 u' v' \, dx = \int_0^1 f v \, dx = F(v), \quad \forall v \in H_0^1(0,1)
$$

由一维 Poincaré 不等式 $\|u\|_{L^2} \leq \frac{1}{\pi} \|u'\|_{L^2}$，$a$ 是强制的。Lax-Milgram 定理保证解的存在唯一性。

**显式解与 Green 函数的联系**：这类弱解的古典解可由 Green 函数表示为
$$u(x) = \int_0^1 G(x,\xi) f(\xi) d\xi, \quad G(x,\xi) = \begin{cases} x(1-\xi), & x < \xi \\ \xi(1-x), & x > \xi \end{cases}$$

弱形式给出此公式的另一推导：Green 函数 $G(\cdot, \xi)$ 本身是 $a(G(\cdot, \xi), v) = v(\xi)$ 的弱解（$\delta$ 函数的弱实现）。

---

## 习题

1. **Dirichlet 能量的极小元**：证明 Dirichlet 能量 $E[u] = \frac{1}{2} \int_\Omega |\nabla u|^2 dx$ 在有约束 $u|_{\partial\Omega} = g$ 下的 Euler-Lagrange 方程是 $-\Delta u = 0$。（已完成，确认推导的每一步。）

2. **一维弱解计算**：对 $-u'' = 1$ 在 $(0,1)$ 上，$u(0)=u(1)=0$，显式求出古典解。构造两段线性函数 $v_1(x) = x$（$0 \leq x \leq 1/2$），$v_1(x) = 1-x$（$1/2 < x \leq 1$），计算弱形式中 $a(u, v_1)$ 和 $F(v_1)$，验证等式成立。

3. **Poincaré 不等式**：设 $\Omega = (0,L)$，对所有 $u \in H_0^1(0,L)$，证明 $\|u\|_{L^2} \leq \frac{L}{\pi} \|\nabla u\|_{L^2}$。提示：利用 $u(x) = \int_0^x u'(t) dt$ 和 Cauchy-Schwarz，或 Fourier 正弦级数展开。

4. **强制性的条件**：对 Neumann 问题 $-\Delta u = f$ 在 $\Omega$，$\frac{\partial u}{\partial \nu} = 0$ 在 $\partial\Omega$，直接在 $H^1(\Omega)$ 上用 Lax-Milgram 定理是否会失效？如何修正？（提示：解在常数平移下不唯一，相容性条件 $\int_\Omega f = 0$。）

5. **Lax-Milgram 定理的非对称形式**（Nečas 定理）：设 $a(u,v)$ 满足：$|a(u,v)| \leq M \|u\|\|v\|$ 且
   $$\inf_{u \neq 0} \sup_{v \neq 0} \frac{a(u,v)}{\|u\|\|v\|} \geq \alpha > 0, \quad \sup_{u \neq 0} |a(u,v)| > 0\ (\forall v \neq 0)$$
   证明此条件足以保证解的存在唯一性。说明它为什么比强制性更弱。

6. **弱形式的 Petrov-Galerkin 近似**：取有限维子空间 $V_h \subset H_0^1(\Omega)$，$u_h \in V_h$ 满足 $a(u_h, v_h) = F(v_h)$（$\forall v_h \in V_h$）。证明 Céa 引理：$\|u - u_h\|_{H^1} \leq \frac{M}{\alpha} \inf_{v_h \in V_h} \|u - v_h\|_{H^1}$。解释其意义：近似解的误差由最佳近似的误差控制。

7. **Dirichlet 原理的局限性**：给出一个 Dirichlet 能量 $E[u]$ 有下界但下确界不可达的例子（即在容许函数类中不存在极小元）。提示：考虑 $\Omega = (0,1)$，边界条件 $u(0)=0, u(1)=1$，但在 $H^1(0,1)$ 中证明极小元存在（这其实是可解的）；Hadamard 曾举出无界区域上的反例。

> [!hint]- 部分提示
> - 3: 用 $u(x) = \int_0^x u'(t) dt$，则 $|u(x)| \leq \sqrt{x} \|\nabla u\|_{L^2}$，积分得 $\|u\|_{L^2}^2 \leq \frac{L^2}{2} \|\nabla u\|_{L^2}^2$；Fourier 级数法可得最优常数 $\frac{L^2}{\pi^2}$
> - 4: 在 $H^1/\mathbb{R}$ 商空间上（模去常数），Lax-Milgram 定理可正常工作
> - 5: 此即 inf-sup 条件（Banach-Nečas-Babuška 定理），对非对称问题（如对流-扩散方程）至关重要

---

## 相关笔记

- [[Sobolev嵌入定理]] — $H^1$ 紧嵌入 $L^2$，极小化序列的收敛性基础
- [[Laplace方程Green函数]] — 同一问题的积分核表示与弱形式的关系
- [[Sturm-Liouville特征函数正交性]] — 一维 S-L 算子的变分刻画：本征值 = Rayleigh 商的极小值
