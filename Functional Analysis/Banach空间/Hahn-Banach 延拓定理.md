---
title: Hahn-Banach 延拓定理
date: 2026-04-11
tags:
  - 泛函分析
  - 线性泛函
  - Hahn-Banach定理
  - 赋范空间
---

# Hahn-Banach 延拓定理

## 预备定义

> [!note] 次线性泛函
> 设 $X$ 为实线性空间。称函数 $p : X \to \mathbb{R}$ 为**次线性泛函**（sublinear functional），若满足：
> 1. **正齐次性**：$p(\alpha x) = \alpha\, p(x)$，对一切 $x \in X$，$\alpha > 0$；
> 2. **次可加性**：$p(x + y) \leq p(x) + p(y)$，对一切 $x, y \in X$。
>
> 注意次线性泛函不要求对称性，即一般 $p(-x) \neq p(x)$。范数是次线性泛函的特例（额外满足 $p(-x) = p(x)$ 和正定性）。

> [!note] 线性泛函
> 设 $X$ 为实线性空间。称函数 $f : X \to \mathbb{R}$ 为**线性泛函**（linear functional），若满足：
> $$f(\alpha x + \beta y) = \alpha f(x) + \beta f(y), \quad \forall\, x, y \in X,\; \alpha, \beta \in \mathbb{R}.$$

> [!abstract] 引理：Zorn 引理
> 设 $(P, \leq)$ 为非空偏序集，且 $P$ 的每个全序子集（链）都有上界。则 $P$ 中存在极大元。
>
> Zorn 引理等价于选择公理，是 Hahn-Banach 定理在一般情形下证明的关键工具。

> [!abstract] 引理：一维延拓引理
> 设 $X$ 为实线性空间，$p : X \to \mathbb{R}$ 为次线性泛函，$Y \subsetneq X$ 为真子空间，$f : Y \to \mathbb{R}$ 为线性泛函且 $f \leq p$ 在 $Y$ 上成立。取 $z \in X \setminus Y$，令 $Y_1 = Y + \mathbb{R}z = \{y + tz : y \in Y,\, t \in \mathbb{R}\}$。则存在线性泛函 $f_1 : Y_1 \to \mathbb{R}$，使得 $f_1|_Y = f$ 且 $f_1 \leq p$ 在 $Y_1$ 上成立。

**证明**：$Y_1$ 中每个元素可唯一写成 $y + tz$（$y \in Y$，$t \in \mathbb{R}$）。定义

$$f_1(y + tz) = f(y) + tc$$

其中 $c \in \mathbb{R}$ 为待定常数。$f_1$ 显然是线性泛函且 $f_1|_Y = f$。需要选取 $c$ 使得 $f_1 \leq p$ 在 $Y_1$ 上成立。

#### 确定 $c$ 的范围

对 $t > 0$，要求 $f_1(y + tz) \leq p(y + tz)$，即

$$f(y) + tc \leq p(y + tz).$$

由正齐次性，令 $y' = y/t$ 得

$$c \leq p(y' + z) - f(y'), \quad \forall\, y' \in Y. \quad \cdots (1)$$

对 $t < 0$，令 $t = -s$（$s > 0$），要求 $f(y) - sc \leq p(y - sz)$，即

$$f(y'') - p(y'' - z) \leq c, \quad \forall\, y'' \in Y. \quad \cdots (2)$$

#### 验证 $c$ 的存在性

需要 $(2)$ 的上确界 $\leq$ $(1)$ 的下确界。对任意 $y', y'' \in Y$：

$$f(y'') - p(y'' - z) = f(y') + f(y'' - y') - p(y'' - z).$$

由 $f \leq p$ 在 $Y$ 上成立及次可加性：

$$f(y'') - p(y'' - z) \leq p(y'' - y') - p(y'' - z) + f(y').$$

但更直接地：

$$f(y'') + f(y') = f(y'' + y') \leq p(y'' + y') = p((y'' - z) + (y' + z)) \leq p(y'' - z) + p(y' + z).$$

故 $f(y'') - p(y'' - z) \leq p(y' + z) - f(y')$。因此

$$\sup_{y'' \in Y} \bigl[f(y'') - p(y'' - z)\bigr] \leq \inf_{y' \in Y} \bigl[p(y' + z) - f(y')\bigr].$$

取 $c$ 为此闭区间中任一值即可。$\square$

---

## 定理

**(i) 次线性泛函形式（实空间）**：设 $X$ 为实线性空间，$p : X \to \mathbb{R}$ 为次线性泛函，$Y \subseteq X$ 为子空间，$f : Y \to \mathbb{R}$ 为线性泛函且满足

$$f(y) \leq p(y), \quad \forall\, y \in Y.$$

则存在线性泛函 $F : X \to \mathbb{R}$，使得 $F|_Y = f$ 且

$$F(x) \leq p(x), \quad \forall\, x \in X.$$

**(ii) 赋范空间形式**：设 $X$ 为赋范空间（实或复），$Y \subseteq X$ 为子空间，$f \in Y^*$（即 $f$ 是 $Y$ 上的有界线性泛函）。则存在 $F \in X^*$，使得 $F|_Y = f$ 且 $\|F\|_{X^*} = \|f\|_{Y^*}$。

---

## 第(i)部分的证明：次线性泛函形式

### 构造偏序集

设 $\mathcal{F}$ 为所有满足以下条件的有序对 $(Z, g)$ 的集合：

1. $Z$ 是 $X$ 的子空间，$Y \subseteq Z$；
2. $g : Z \to \mathbb{R}$ 是线性泛函；
3. $g|_Y = f$；
4. $g(z) \leq p(z)$，对一切 $z \in Z$。

在 $\mathcal{F}$ 上定义偏序：$(Z_1, g_1) \leq (Z_2, g_2)$ 当且仅当 $Z_1 \subseteq Z_2$ 且 $g_2|_{Z_1} = g_1$。

由 $(Y, f) \in \mathcal{F}$，$\mathcal{F}$ 非空。

### 验证 Zorn 引理的条件

设 $\{(Z_\alpha, g_\alpha)\}_{\alpha \in \Lambda}$ 为 $\mathcal{F}$ 中的全序链。令

$$Z_0 = \bigcup_{\alpha \in \Lambda} Z_\alpha, \qquad g_0(x) = g_\alpha(x) \quad \text{若 } x \in Z_\alpha.$$

#### $Z_0$ 是子空间

设 $x, y \in Z_0$，则 $x \in Z_\alpha$，$y \in Z_\beta$ 对某 $\alpha, \beta$。由全序性，不妨设 $Z_\alpha \subseteq Z_\beta$，则 $x, y \in Z_\beta$，故 $\lambda x + \mu y \in Z_\beta \subseteq Z_0$。$\square$

#### $g_0$ 定义良好且为线性泛函

若 $x \in Z_\alpha \cap Z_\beta$ 且 $Z_\alpha \subseteq Z_\beta$，则 $g_\beta|_{Z_\alpha} = g_\alpha$，故 $g_\alpha(x) = g_\beta(x)$。线性性同理由链的相容性保证。$\square$

#### $g_0 \leq p$ 在 $Z_0$ 上成立

对 $x \in Z_0$，取 $\alpha$ 使 $x \in Z_\alpha$，则 $g_0(x) = g_\alpha(x) \leq p(x)$。$\square$

因此 $(Z_0, g_0) \in \mathcal{F}$ 是链的上界。

### 应用 Zorn 引理

由 Zorn 引理，$\mathcal{F}$ 存在极大元 $(Z^*, F)$。

### 证明 $Z^* = X$

**反证法**：假设 $Z^* \neq X$，则存在 $z \in X \setminus Z^*$。由一维延拓引理，存在线性泛函 $F_1 : Z^* + \mathbb{R}z \to \mathbb{R}$，使得 $F_1|_{Z^*} = F$ 且 $F_1 \leq p$。

则 $(Z^* + \mathbb{R}z, F_1) \in \mathcal{F}$ 且严格大于 $(Z^*, F)$，与 $(Z^*, F)$ 的极大性矛盾。$\square$

因此 $Z^* = X$，即 $F : X \to \mathbb{R}$ 是满足 $F|_Y = f$ 且 $F \leq p$ 的线性延拓。$\blacksquare$

---

## 第(ii)部分的证明：赋范空间形式

### 实赋范空间的情形

令 $p(x) = \|f\|_{Y^*} \cdot \|x\|$。则 $p$ 是次线性泛函。对 $y \in Y$：

$$f(y) \leq |f(y)| \leq \|f\|_{Y^*} \cdot \|y\| = p(y).$$

由第(i)部分，存在线性泛函 $F : X \to \mathbb{R}$，使得 $F|_Y = f$ 且 $F(x) \leq \|f\|_{Y^*} \cdot \|x\|$ 对一切 $x \in X$。

将 $x$ 替换为 $-x$，得 $-F(x) = F(-x) \leq \|f\|_{Y^*} \cdot \|{-x}\| = \|f\|_{Y^*} \cdot \|x\|$，故

$$|F(x)| \leq \|f\|_{Y^*} \cdot \|x\|, \quad \forall\, x \in X.$$

因此 $F$ 有界且 $\|F\|_{X^*} \leq \|f\|_{Y^*}$。又 $F|_Y = f$ 蕴含 $\|F\|_{X^*} \geq \|f\|_{Y^*}$。

综合得 $\|F\|_{X^*} = \|f\|_{Y^*}$。$\square$

### 复赋范空间的情形

设 $X$ 为复赋范空间，$f \in Y^*$。令 $u = \operatorname{Re} f$，则 $u$ 是 $Y$（视为实空间）上的实线性泛函，且

$$f(y) = u(y) - i\, u(iy), \quad \forall\, y \in Y. \quad \cdots (\star)$$

> [!info] 为何 $(\star)$ 成立
> 设 $f(y) = u(y) + iv(y)$。由 $f$ 的复线性性，$f(iy) = if(y) = iu(y) - v(y)$。取实部得 $u(iy) = -v(y)$，故 $v(y) = -u(iy)$。

对 $y \in Y$，$u(y) = \operatorname{Re} f(y) \leq |f(y)| \leq \|f\| \cdot \|y\|$。

由实空间的 Hahn-Banach 定理，将 $u$ 延拓为 $U : X \to \mathbb{R}$，使得 $U|_Y = u$ 且 $|U(x)| \leq \|f\| \cdot \|x\|$。定义

$$F(x) = U(x) - i\, U(ix), \quad \forall\, x \in X.$$

#### 验证 $F$ 是复线性泛函

$F$ 是实线性的（直接验证）。对复线性性，需验证 $F(ix) = iF(x)$：

$$F(ix) = U(ix) - i\, U(i \cdot ix) = U(ix) - i\, U(-x) = U(ix) + i\, U(x).$$
$$iF(x) = i\bigl(U(x) - i\, U(ix)\bigr) = iU(x) + U(ix).$$

两者相等。$\square$

#### 验证 $F|_Y = f$

对 $y \in Y$，$F(y) = U(y) - iU(iy) = u(y) - iu(iy) = f(y)$（由 $(\star)$）。$\square$

#### 验证 $\|F\| = \|f\|$

对任意 $x \in X$，写 $F(x) = |F(x)| e^{i\theta}$，则

$$|F(x)| = e^{-i\theta} F(x) = F(e^{-i\theta} x) = U(e^{-i\theta} x) \leq \|f\| \cdot \|e^{-i\theta} x\| = \|f\| \cdot \|x\|.$$

> [!info] 上式第三个等号的理由
> $F(e^{-i\theta}x)$ 是实数（等于 $|F(x)| \geq 0$），故 $F(e^{-i\theta}x) = \operatorname{Re} F(e^{-i\theta}x) = U(e^{-i\theta}x)$。

故 $\|F\| \leq \|f\|$。又 $F|_Y = f$ 蕴含 $\|F\| \geq \|f\|$。

因此 $\|F\|_{X^*} = \|f\|_{Y^*}$。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明分为两个层次：
>
> **代数层（次线性泛函形式）**：
> 1. **一维延拓**：先证明可以沿一个方向延拓一步——核心是找到常数 $c$ 使得延拓后仍被 $p$ 控制；
> 2. **Zorn 引理**：将所有合法延拓构成偏序集，链有上界（取并），故存在极大元；
> 3. **极大即全空间**：若极大元的定义域不是全空间，则可再延拓一步，矛盾。
>
> **分析层（赋范空间形式）**：
> - **实情形**：取 $p(x) = \|f\| \cdot \|x\|$ 直接归结为代数形式；
> - **复情形**：利用 $f = \operatorname{Re} f - i\operatorname{Re}(f \circ (i\cdot))$ 将复泛函还原为实部，延拓实部后重构复泛函。

> [!warning] Hahn-Banach 延拓的非唯一性
> 延拓 $F$ 一般**不唯一**。唯一性仅在特殊空间（如严格凸的对偶空间）中成立。此外，该定理的证明依赖于 Zorn 引理（等价于选择公理），延拓的存在是非构造性的。

> [!tip] 重要推论
> Hahn-Banach 定理有许多深远的推论：
> 1. **对偶空间足够大**：对任意 $x \neq 0$，存在 $F \in X^*$ 使得 $F(x) = \|x\|$ 且 $\|F\| = 1$；
> 2. **对偶空间分离点**：若 $f(x) = f(y)$ 对一切 $f \in X^*$ 成立，则 $x = y$；
> 3. **范数的对偶表示**：$\|x\| = \sup_{\|f\| \leq 1} |f(x)|$。
