---
title: Legendre 多项式的正交性
date: 2026-04-19
tags:
  - 数学物理方法
  - 特殊函数
  - Legendre多项式
  - 正交性
---

# Legendre 多项式的正交性

## 预备定义

> [!note] Rodrigues 公式
> **Legendre 多项式** $P_n(x)$ 可由 **Rodrigues 公式**定义：
> $$P_n(x) = \frac{1}{2^n\, n!} \frac{d^n}{dx^n}(x^2 - 1)^n, \quad n = 0, 1, 2, \ldots$$
>
> 前几个 Legendre 多项式为：
> - $P_0(x) = 1$
> - $P_1(x) = x$
> - $P_2(x) = \dfrac{1}{2}(3x^2 - 1)$
> - $P_3(x) = \dfrac{1}{2}(5x^3 - 3x)$
>
> $P_n(x)$ 是 $n$ 次多项式，其首项系数为 $\dfrac{(2n)!}{2^n (n!)^2}$。

> [!abstract] 引理：$(x^2 - 1)^n$ 在 $x = \pm 1$ 处的零点阶数
> 记 $u_n(x) = (x^2 - 1)^n$。则 $u_n^{(k)}(\pm 1) = 0$ 对一切 $k = 0, 1, \ldots, n-1$ 成立。

**证明**：因为 $(x^2 - 1)^n = (x-1)^n(x+1)^n$，所以 $x = 1$ 和 $x = -1$ 各是 $u_n(x)$ 的 $n$ 重零点。一个 $n$ 重零点经 $k$ 次求导后仍为 $(n-k)$ 重零点（当 $k < n$ 时）。因此 $u_n^{(k)}(\pm 1) = 0$ 对 $k = 0, 1, \ldots, n-1$ 成立。$\square$

> [!info] Wallis 型积分公式
> $$\int_0^{\pi/2} \cos^{2n+1}\theta\, d\theta = \frac{(2n)!!\,}{(2n+1)!!} = \frac{2^n\, n!}{1 \cdot 3 \cdot 5 \cdots (2n+1)} = \frac{2^{2n}\,(n!)^2}{(2n+1)!},$$
> 其中 $(2n)!! = 2 \cdot 4 \cdots (2n)$，$(2n+1)!! = 1 \cdot 3 \cdots (2n+1)$。
> 由此可得
> $$\int_{-1}^{1} (1 - x^2)^n\, dx = \frac{2^{2n+1}\,(n!)^2}{(2n+1)!}. \quad \cdots (\dagger)$$

---

## 定理

Legendre 多项式族 $\{P_n\}_{n=0}^{\infty}$ 在 $[-1, 1]$ 上关于权函数 $w(x) = 1$ 正交，且

$$\int_{-1}^{1} P_m(x)\, P_n(x)\, dx = \frac{2}{2n+1}\, \delta_{mn},$$

其中 $\delta_{mn}$ 为 Kronecker delta。

即：

**(i)** 当 $m \neq n$ 时，$\displaystyle\int_{-1}^{1} P_m(x)\, P_n(x)\, dx = 0$。

**(ii)** 当 $m = n$ 时，$\displaystyle\int_{-1}^{1} [P_n(x)]^2\, dx = \dfrac{2}{2n+1}$。

---

## 第(i)部分的证明：正交性（$m \neq n$）

不失一般性，设 $m < n$。

### 第一步：用 Rodrigues 公式展开

$$\int_{-1}^{1} P_m(x)\, P_n(x)\, dx = \frac{1}{2^n\, n!} \int_{-1}^{1} P_m(x)\, \frac{d^n}{dx^n}(x^2 - 1)^n\, dx. \quad \cdots (\ast)$$

$\square$

### 第二步：反复分部积分 $n$ 次

对 $(\ast)$ 中的积分施行分部积分，每次将一个导数从 $(x^2 - 1)^n$ 转移到 $P_m(x)$ 上。

第 $j$ 次分部积分（$j = 1, 2, \ldots, n$）产生的边界项为

$$(-1)^{j-1} \left[P_m^{(j-1)}(x) \cdot \frac{d^{n-j}}{dx^{n-j}}(x^2 - 1)^n\right]_{-1}^{1}.$$

由引理，$\dfrac{d^{n-j}}{dx^{n-j}}(x^2 - 1)^n$ 在 $x = \pm 1$ 处为零（因为 $n - j \leq n - 1$）。

> [!important] 所有边界项均为零
> 分部积分的每一步中，被求值的因子 $\dfrac{d^k}{dx^k}(x^2-1)^n$（$k = n-1, n-2, \ldots, 0$）在 $x = \pm 1$ 处均消失。这正是 $(x^2-1)^n$ 在端点有 $n$ 重零点的威力 — 它"吸收"了全部 $n$ 次分部积分的边界项。

因此，经 $n$ 次分部积分后，

$$\int_{-1}^{1} P_m(x)\, \frac{d^n}{dx^n}(x^2-1)^n\, dx = (-1)^n \int_{-1}^{1} P_m^{(n)}(x)\, (x^2-1)^n\, dx. \quad \cdots (\star)$$

$\square$

### 第三步：利用 $m < n$ 得出结论

$P_m(x)$ 是 $m$ 次多项式。对它求 $n$ 阶导数（$n > m$），

$$P_m^{(n)}(x) = 0.$$

代入 $(\star)$，

$$\int_{-1}^{1} P_m(x)\, P_n(x)\, dx = \frac{(-1)^n}{2^n\, n!} \int_{-1}^{1} 0 \cdot (x^2-1)^n\, dx = 0. \quad \square$$

---

## 第(ii)部分的证明：模的计算（$m = n$）

### 第一步：沿用分部积分的结果

在第(i)部分的推导中取 $m = n$，由 $(\ast)$ 和 $(\star)$，

$$\int_{-1}^{1} [P_n(x)]^2\, dx = \frac{(-1)^n}{2^n\, n!} \int_{-1}^{1} P_n^{(n)}(x)\, (x^2 - 1)^n\, dx. \quad \cdots (1)$$

$\square$

### 第二步：计算 $P_n^{(n)}(x)$

$P_n(x)$ 是 $n$ 次多项式，其首项系数为 $\dfrac{(2n)!}{2^n(n!)^2}$（由 Rodrigues 公式，$(x^2-1)^n$ 的首项 $x^{2n}$ 经 $n$ 次求导后为 $\dfrac{(2n)!}{n!} x^n$，再除以 $2^n n!$）。

> [!info] 首项系数的推导
> $(x^2-1)^n$ 的最高次项为 $x^{2n}$。
> $$\frac{d^n}{dx^n} x^{2n} = \frac{(2n)!}{n!}\, x^n.$$
> 因此 $P_n(x) = \dfrac{1}{2^n n!} \cdot \dfrac{(2n)!}{n!}\, x^n + \text{低次项} = \dfrac{(2n)!}{2^n(n!)^2}\, x^n + \cdots$

对 $n$ 次多项式求 $n$ 阶导数，仅保留首项系数乘以 $n!$：

$$P_n^{(n)}(x) = \frac{(2n)!}{2^n(n!)^2} \cdot n! = \frac{(2n)!}{2^n\, n!}. \quad \cdots (2)$$

这是一个**常数**。$\square$

### 第三步：计算 $\int_{-1}^{1}(x^2 - 1)^n\, dx$

$$\int_{-1}^{1}(x^2-1)^n\, dx = (-1)^n \int_{-1}^{1}(1-x^2)^n\, dx.$$

由 $(\dagger)$，

$$\int_{-1}^{1}(1-x^2)^n\, dx = \frac{2^{2n+1}(n!)^2}{(2n+1)!}.$$

因此

$$\int_{-1}^{1}(x^2-1)^n\, dx = (-1)^n \cdot \frac{2^{2n+1}(n!)^2}{(2n+1)!}. \quad \cdots (3)$$

$\square$

### 第四步：合并计算

将 $(2)$ 和 $(3)$ 代入 $(1)$：

$$\int_{-1}^{1} [P_n(x)]^2\, dx = \frac{(-1)^n}{2^n\, n!} \cdot \frac{(2n)!}{2^n\, n!} \cdot (-1)^n \cdot \frac{2^{2n+1}(n!)^2}{(2n+1)!}.$$

注意 $(-1)^n \cdot (-1)^n = 1$。化简：

$$= \frac{(2n)!}{2^{2n}(n!)^2} \cdot \frac{2^{2n+1}(n!)^2}{(2n+1)!} = \frac{(2n)! \cdot 2}{(2n+1)!} = \frac{2}{2n+1}.$$

> [!info] 化简过程
> 分子：$(2n)! \cdot 2^{2n+1} (n!)^2$。分母：$2^{2n} (n!)^2 \cdot (2n+1)!$。
> $(n!)^2$ 约去，$2^{2n}$ 约去，剩 $\dfrac{(2n)! \cdot 2}{(2n+1)!} = \dfrac{2}{2n+1}$（因为 $(2n+1)! = (2n+1) \cdot (2n)!$）。

因此

$$\|P_n\|^2 = \int_{-1}^{1}[P_n(x)]^2\,dx = \frac{2}{2n+1}. \quad \square$$

---

## 总结

综合两部分：

1. $m \neq n$ 时正交性成立（分部积分 + 多项式次数不够高）。 ✓
2. $m = n$ 时模为 $\sqrt{2/(2n+1)}$。 ✓

因此 $\displaystyle\int_{-1}^{1} P_m(x)\, P_n(x)\, dx = \frac{2}{2n+1}\,\delta_{mn}$。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 整个证明依赖于 **Rodrigues 公式 + 分部积分**这一组合。核心机制是：
>
> 1. 用 Rodrigues 公式将 $P_n$ 写成 $\dfrac{d^n}{dx^n}(x^2-1)^n$ 的形式；
> 2. 对积分施行 $n$ 次分部积分，将全部 $n$ 个导数从 $(x^2-1)^n$ "搬"到 $P_m$ 上；
> 3. $(x^2-1)^n$ 在 $x = \pm 1$ 处的 $n$ 重零点保证**所有边界项消失**；
> 4. 搬完后，$P_m^{(n)} = 0$（当 $m < n$ 时）直接杀死了积分 — 这就是正交性。
>
> 从更高的观点看，Legendre 多项式是 Sturm-Liouville 问题
> $$\frac{d}{dx}\!\left[(1-x^2)\frac{d}{dx}P_n\right] + n(n+1)\,P_n = 0$$
> 的特征函数，正交性是 Sturm-Liouville 理论的一般结论。但上述基于 Rodrigues 公式的直接证明更为初等，且给出了模的显式计算。

### 生成函数与递推关系

> [!abstract] 生成函数
> Legendre 多项式的**生成函数**为：
> $$\frac{1}{\sqrt{1 - 2xt + t^2}} = \sum_{n=0}^\infty P_n(x) t^n, \quad |t| < 1, \; |x| \leq 1$$
> 
> **验证**：在 $t=0$ 附近 Taylor 展开左边，$t^0$ 系数为 $1 = P_0(x)$，$t^1$ 系数为 $x = P_1(x)$，$t^2$ 系数为 $\frac12(3x^2-1) = P_2(x)$。

> [!abstract] Bonnet 递推关系
> $$(n+1)P_{n+1}(x) = (2n+1)x P_n(x) - n P_{n-1}(x), \quad n \geq 1$$
> 
> **证明概要**：对生成函数关于 $t$ 求导：$\frac{\partial}{\partial t} \frac{1}{\sqrt{1-2xt+t^2}} = \frac{x-t}{(1-2xt+t^2)^{3/2}}$。代入级数表达式，比较 $t^n$ 系数即得递推关系。也可由 Rodrigues 公式求导验证。

> [!note] S-L 形式推导
> Legendre 微分方程 $((1-x^2)P_n')' + n(n+1)P_n = 0$ 的 S-L 形式为：$p(x) = 1-x^2$，$q(x) = 0$，$w(x) = 1$，$\lambda_n = n(n+1)$。注意 $p(\pm 1) = 0$，这是**奇异 S-L 问题**（在端点处权函数退化），但 $P_n(x)$ 在 $x = \pm 1$ 处保持有限，正交性仍成立。

> [!warning] 归一化约定
> 物理文献中有时使用**归一化 Legendre 多项式** $\tilde{P}_n(x) = \sqrt{\dfrac{2n+1}{2}}\, P_n(x)$，使得 $\|\tilde{P}_n\| = 1$。在量子力学的球谐函数 $Y_l^m(\theta, \varphi)$ 中，归一化系数 $\sqrt{\dfrac{2l+1}{4\pi} \cdot \dfrac{(l-m)!}{(l+m)!}}$ 正是从此处的 $\dfrac{2}{2n+1}$ 出发推导的。

---

## 习题

1. **正交性验证**：对前三个 Legendre 多项式 $P_0(x)=1, P_1(x)=x, P_2(x)=\frac12(3x^2-1)$，直接计算验证 $\int_{-1}^1 P_0 P_2 dx = 0$ 和 $\int_{-1}^1 P_1 P_2 dx = 0$。

2. **模的计算**：验证 $\int_{-1}^1 P_3^2(x) dx = 2/7$。$P_3(x) = \frac12(5x^3 - 3x)$。

3. **Rodrigues 公式练习**：用 Rodrigues 公式计算 $P_3(x)$，并与已知表达式对比。

4. **生成函数**：Legendre 多项式的生成函数为 $\frac{1}{\sqrt{1-2xt+t^2}} = \sum_{n=0}^\infty P_n(x) t^n$（$|t| < 1$）。验证当 $|t| \ll 1$ 时，展开到 $t^2$ 项得到 $P_0, P_1, P_2$。

5. **Legendre 微分方程**：验证 $P_2(x) = \frac12(3x^2-1)$ 满足 Legendre 方程 $(1-x^2)y'' - 2xy' + 6y = 0$。

6. **递推关系**：证明 Bonnet 递推关系 $(n+1)P_{n+1}(x) = (2n+1)x P_n(x) - n P_{n-1}(x)$。提示：用生成函数或 Rodrigues 公式。

7. **球坐标分离变量**：三维 Laplace 方程在球坐标 $(r,\theta,\varphi)$ 下分离变量时，极角 $\theta$ 部分归结为 Legendre 方程。写出分离假设 $u(r,\theta,\varphi) = R(r)\Theta(\theta)\Phi(\varphi)$，推导 Legendre 方程来源于 $x = \cos\theta$ 代换。

> [!hint]- 部分提示
> - 4: $\frac{1}{\sqrt{1-2xt+t^2}} = 1 + xt + \frac{3x^2-1}{2}t^2 + O(t^3)$
> - 6: 对 Rodrigues 公式求导或使用生成函数
> - 7: $\Theta$ 满足 $\frac{1}{\sin\theta}\frac{d}{d\theta}(\sin\theta\frac{d\Theta}{d\theta}) + [l(l+1) - \frac{m^2}{\sin^2\theta}]\Theta = 0$，当 $m=0$ 时为 Legendre 方程

---

## 相关笔记

- [[球面调和函数]] — Legendre 多项式是球面调和函数 $Y_l^m$ 的 $m=0$ 特例
- [[Sturm-Liouville特征函数正交性]] — Legendre 方程的正交性源于 S-L 理论
- [[Bessel函数]] — 柱坐标分离产生的另一类特殊函数
