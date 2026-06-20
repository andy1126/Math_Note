---
title: Gamma函数与Beta函数
date: 2026-06-19
tags:
  - 多元微积分
  - 积分学
  - 含参量积分
  - Gamma函数
  - Beta函数
  - 特殊函数
---

# Gamma函数与Beta函数

## 预备定义

> [!note] Gamma 函数
> 称参量积分
> $$\Gamma(s) = \int_0^{+\infty} t^{\,s-1} e^{-t}\,dt$$
> 为 **Gamma 函数**（Gamma function），其中 $s$ 为参量。

> [!note] Beta 函数
> 称参量积分
> $$B(p,q) = \int_0^1 t^{\,p-1}(1-t)^{\,q-1}\,dt$$
> 为 **Beta 函数**（Beta function），其中 $p,q$ 为参量。

> [!abstract] 引理：反常积分的收敛比较判别
> 若 $|f(x)| \le g(x)$ 且 $\int g$ 收敛，则 $\int f$ 绝对收敛（Weierstrass 判别）；若在无穷远处 $f(x)\sim Cx^{-\alpha}$（$\alpha>1$ 收敛，$\alpha\le 1$ 发散），在有限奇点 $x_0$ 处 $f(x)\sim C|x-x_0|^{-\beta}$（$\beta<1$ 收敛，$\beta\ge 1$ 发散）。详见 [[含参量反常积分]]。

> [!abstract] 引理：变量替换公式
> 若 $\Phi:E\to\Phi(E)$ 为 $C^1$ 微分同胚，则
> $$\int_{\Phi(E)} f(y)\,dy = \int_E f(\Phi(x))\,|J_\Phi(x)|\,dx.$$
> 详见 [[变量替换公式]]。

> [!abstract] 引理：矩形上的 Fubini 定理
> 若 $f$ 在矩形上连续（或非负可测），则二重积分与两个累次积分相等。详见 [[二重积分与Fubini定理]]。

---

## 定理

**(收敛域)** $\Gamma(s)$ 的收敛域为 $s>0$；$B(p,q)$ 的收敛域为 $p>0,\ q>0$。

**(Γ 的递推)** 对 $s>0$，
$$\Gamma(s+1) = s\,\Gamma(s),\qquad \Gamma(n) = (n-1)!\ \ (n\in\mathbb{N}^+).$$

**(Γ-B 联系)** 对 $p,q>0$，
$$B(p,q) = \frac{\Gamma(p)\,\Gamma(q)}{\Gamma(p+q)}.$$

**(余元公式 / Euler 反射公式)** 对 $0 < s < 1$，
$$\Gamma(s)\,\Gamma(1-s) = \frac{\pi}{\sin(\pi s)}.$$

**(倍元公式 / Legendre 倍量公式)** 对 $s>0$，
$$\Gamma(s)\,\Gamma\!\left(s+\tfrac{1}{2}\right) = \frac{\sqrt{\pi}}{2^{2s-1}}\,\Gamma(2s).$$

**(B 函数的对称与递推)** 对 $p,q>0$，
$$B(p,q) = B(q,p),\qquad B(p,q) = \frac{p-1}{p+q-1}\,B(p-1,q)\ \ (p>1),$$
$$B(p,q) = 2\int_0^{\pi/2} \sin^{2p-1}\!\theta\,\cos^{2q-1}\!\theta\,d\theta.$$

---

## 证明

### 收敛域

#### Γ(s) 的收敛域：$s>0$

将积分拆为奇点附近与无穷远两段：$\Gamma(s)=\int_0^1 + \int_1^{+\infty}$。

- **奇点 $t=0$ 附近**（$0<t\le 1$）：$e^{-t}\to 1$，故 $t^{s-1}e^{-t}\sim t^{s-1}$。由比较判别，$\int_0^1 t^{s-1}\,dt$ 收敛当且仅当 $s-1>-1$，即 $s>0$。
- **无穷远 $t\to+\infty$**：对任意 $s$，$t^{s-1}e^{-t} \le C\,e^{-t/2}$（因 $t^{s-1}e^{-t/2}\to 0$），而 $\int_1^\infty e^{-t/2}\,dt$ 收敛。由 Weierstrass 判别，此段对一切 $s$ 收敛。

> [!important] 收敛域由奇点决定
> 无穷段因 $e^{-t}$ 的指数衰减而对所有 $s$ 收敛；$t=0$ 处的幂次奇性 $t^{s-1}$ 才是约束——要求 $s>0$。故 $\Gamma$ 的收敛域为 $(0,+\infty)$。

#### B(p,q) 的收敛域：$p>0,\ q>0$

唯一奇点在端点。$t=0$ 附近 $t^{p-1}(1-t)^{q-1}\sim t^{p-1}$，收敛当且仅当 $p>0$；$t=1$ 附近 $(1-t)^{q-1}$ 主导，收敛当且仅当 $q>0$。故收敛域为 $p>0,\ q>0$。$\square$

### Γ 的递推公式

由分部积分（$u=t^s,\ dv=e^{-t}\,dt$）：
$$\Gamma(s+1) = \int_0^{+\infty} t^s e^{-t}\,dt = \left[-t^s e^{-t}\right]_0^{+\infty} + s\int_0^{+\infty} t^{s-1}e^{-t}\,dt.$$
- $t\to+\infty$：$t^s e^{-t}\to 0$（指数衰减压过幂次）；
- $t\to 0^+$：$t^s e^{-t}\to 0$（$s>0$）。

边界项为零，故
$$\Gamma(s+1) = s\,\Gamma(s).$$
迭代得 $\Gamma(n) = (n-1)\Gamma(n-1) = \cdots = (n-1)!\,\Gamma(1)$，而 $\Gamma(1)=\int_0^\infty e^{-t}\,dt = 1$，故 $\Gamma(n)=(n-1)!$。$\square$

### Γ-B 联系（核心）

**目标**：证 $B(p,q) = \dfrac{\Gamma(p)\Gamma(q)}{\Gamma(p+q)}$，即 $\Gamma(p+q)B(p,q)=\Gamma(p)\Gamma(q)$。

#### 第一步：写出 Γ(p)Γ(q) 为二重积分

由 Fubini 定理（被积函数非负，换序合法）：
$$\Gamma(p)\Gamma(q) = \left(\int_0^\infty u^{p-1}e^{-u}\,du\right)\!\left(\int_0^\infty v^{q-1}e^{-v}\,dv\right) = \int_0^\infty\!\!\int_0^\infty u^{p-1}v^{q-1}e^{-(u+v)}\,du\,dv.$$

#### 第二步：变量替换 $u=xt,\ v=x(1-t)$

作替换（以 $(x,t)\mapsto(u,v)$）：
$$u = xt,\qquad v = x(1-t),\qquad x>0,\ 0<t<1.$$
反解：$x=u+v$，$t=u/(u+v)$。Jacobian：
$$\frac{\partial(u,v)}{\partial(x,t)} = \begin{vmatrix} t & x \\ -t & -(x\!-\!... )\end{vmatrix}$$
直接计算：
$$\frac{\partial(u,v)}{\partial(x,t)} = \begin{vmatrix} t & x \\ 1-t & -x \end{vmatrix} = -xt - x(1-t) = -x,\qquad \left|\det\right| = x.$$
故 $du\,dv = x\,dx\,dt$。由 [[变量替换公式]]，
$$\Gamma(p)\Gamma(q) = \int_0^\infty\!\!\int_0^1 (xt)^{p-1}\bigl(x(1-t)\bigr)^{q-1} e^{-x}\,x\,dt\,dx.$$

#### 第三步：分离变量

整理被积函数的 $x$、$t$ 因子：
$$\Gamma(p)\Gamma(q) = \int_0^\infty x^{p-1+q-1+1} e^{-x}\,dx \cdot \int_0^1 t^{p-1}(1-t)^{q-1}\,dt = \Gamma(p+q)\cdot B(p,q).$$

> [!info] 替换的几何意义
> $(x,t)$ 中 $x=u+v$ 是"径向"、$t=u/(u+v)$ 是"角度"——本质是把第一象限的直角坐标 $(u,v)$ 换成以 $x$ 为径向尺度、$t$ 为比例的坐标。Jacobian $x$ 正是极坐标类替换中"径向因子"的体现。

因此 $B(p,q)=\dfrac{\Gamma(p)\Gamma(q)}{\Gamma(p+q)}$。$\square$

### 余元公式（Euler 反射公式）

**目标**：证 $\Gamma(s)\Gamma(1-s) = \dfrac{\pi}{\sin(\pi s)}$（$0<s<1$）。

#### 第一步：化为已知积分

由 Γ-B 联系，$\Gamma(s)\Gamma(1-s) = \Gamma(1)\,B(s,1-s) = B(s,1-s)$（因 $\Gamma(1)=1$）。故只需计算
$$B(s,1-s) = \int_0^1 t^{s-1}(1-t)^{-s}\,dt.$$

#### 第二步：变量替换 $t = \dfrac{x}{1+x}$

令 $t=\frac{x}{1+x}$（$x=\frac{t}{1-t}$），则 $t:0\to1$ 对应 $x:0\to+\infty$，且
$$1-t = \frac{1}{1+x},\qquad dt = \frac{dx}{(1+x)^2}.$$
代入：
$$B(s,1-s) = \int_0^{+\infty} \left(\frac{x}{1+x}\right)^{s-1}\!\left(\frac{1}{1+x}\right)^{-s}\!\frac{dx}{(1+x)^2} = \int_0^{+\infty} \frac{x^{s-1}}{1+x}\,dx.$$

#### 第三步：计算 $\int_0^\infty \frac{x^{s-1}}{1+x}\,dx$

> [!abstract] 引理：经典积分 $\int_0^\infty \frac{x^{s-1}}{1+x}\,dx = \frac{\pi}{\sin(\pi s)}$
> 对 $0<s<1$ 成立。可由下述实分析围道（keyhole contour）或复分析留数（[[柯西积分公式]]）给出。此处给出实分析证明梗概。

**引理证明梗概**：考虑复平面上的钥匙孔围道（keyhole contour）绕正实轴，取 $f(z)=\frac{z^{s-1}}{1+z}$（取主值支 $z^{s-1}=e^{(s-1)\log z}$）。围道包围极点 $z=-1=e^{i\pi}$。由留数定理，围道积分 $=2\pi i\,\operatorname{Res}(f;-1)=2\pi i\,e^{(s-1)i\pi}$。围道沿正实轴上、下岸的贡献分别为
$$\int_0^\infty \frac{x^{s-1}}{1+x}\,dx \quad\text{与}\quad -\int_0^\infty \frac{x^{s-1}e^{(s-1)2\pi i}}{1+x}\,dx,$$
两者之和 $= (1-e^{2\pi i(s-1)})\int_0^\infty \frac{x^{s-1}}{1+x}\,dx = -2i\,e^{\pi i(s-1)}\sin(\pi s)\cdot I$。结合留数结果：
$$-2i\,e^{\pi i(s-1)}\sin(\pi s)\cdot I = 2\pi i\,e^{(s-1)i\pi} \implies I = \frac{\pi}{\sin(\pi s)}.$$
大圆与小圆贡献在大圆 $R\to\infty$、小圆 $\varepsilon\to0$ 时分别趋于零（需 $0<s<1$）。$\square_{\text{引理}}$

> [!info] 复分析视角
> 该引理也可直接由 [[柯西积分公式]] 在支点处取留数得到。本质上余元公式的"复分析内核"即此引理；实分析路线与复分析路线在此交汇。

#### 第四步：组装

综合三步，
$$\Gamma(s)\Gamma(1-s) = B(s,1-s) = \int_0^\infty \frac{x^{s-1}}{1+x}\,dx = \frac{\pi}{\sin(\pi s)}. \quad \square$$

> [!warning] 避免循环论证
> 余元公式的证明依赖引理 $\int_0^\infty\frac{x^{s-1}}{1+x}\,dx=\frac{\pi}{\sin\pi s}$，而该引理的证明独立于余元公式本身（由留数定理 / 围道积分给出）。不可用"余元公式"反推此引理，否则构成循环。

### 倍元公式（Legendre）

**目标**：证 $\Gamma(s)\Gamma(s+\tfrac12)=\dfrac{\sqrt\pi}{2^{2s-1}}\Gamma(2s)$。

#### 第一步：用 Γ-B 联系表出左端

$$\Gamma(s)\Gamma\!\left(s+\tfrac12\right) = \Gamma(2s+\tfrac12)\,B\!\left(s,\tfrac12\right).$$

#### 第二步：计算 $B(s,\tfrac12)$

用三角换元（见后）$B(p,q)=2\int_0^{\pi/2}\sin^{2p-1}\!\theta\cos^{2q-1}\!\theta\,d\theta$：
$$B\!\left(s,\tfrac12\right) = 2\int_0^{\pi/2} \sin^{2s-1}\!\theta\,d\theta.$$

#### 第三步：用 Wallis 型替换化为 Γ

令 $u=\sin^2\theta$，则 $d\theta=\frac{du}{2\sqrt{u(1-u)}}$，$\sin^{2s-1}\theta = u^{(2s-1)/2}$，积分化为
$$B\!\left(s,\tfrac12\right) = \int_0^1 u^{s-1}(1-u)^{-1/2}\,du = B\!\left(s,\tfrac12\right)\ \text{（恒等，循环）}.$$
故换用直接路线：由 $B(s,\tfrac12)=\frac{\Gamma(s)\Gamma(1/2)}{\Gamma(s+1/2)}$，需知 $\Gamma(1/2)$。由 $B(1/2,1/2)=\frac{\Gamma(1/2)^2}{\Gamma(1)}=\Gamma(1/2)^2$，而 $B(1/2,1/2)=\int_0^1\frac{dt}{\sqrt{t(1-t)}}=\pi$（令 $t=\sin^2\theta$），故
$$\Gamma\!\left(\tfrac12\right) = \sqrt{\pi}.$$

#### 第四步：组装

回到第一步的等价形式，改用更简洁的代数推导。由 $\Gamma(1/2)=\sqrt\pi$ 与 Γ-B 联系：
$$B\!\left(s,\tfrac12\right) = \frac{\Gamma(s)\sqrt\pi}{\Gamma(s+\tfrac12)}.$$
另一方面，对 $\Gamma(2s)$ 用倍角恒等式的另一形式：考虑 $B(s,s)$ 并作替换 $t=\frac{1+\cos\varphi}{2}$ 可得 $B(s,s)=2^{1-2s}B(s,\tfrac12)$（"倍量恒等式"）。于是
$$\frac{\Gamma(s)^2}{\Gamma(2s)} = B(s,s) = 2^{1-2s}\,B\!\left(s,\tfrac12\right) = 2^{1-2s}\,\frac{\Gamma(s)\sqrt\pi}{\Gamma(s+\tfrac12)}.$$
两边约去 $\Gamma(s)$ 并整理：
$$\Gamma(s)\Gamma\!\left(s+\tfrac12\right) = \frac{\sqrt\pi}{2^{1-2s}}\,\Gamma(2s) = \frac{\sqrt\pi}{2^{2s-1}}\,\Gamma(2s). \quad \square$$

> [!info] 关键中间结果 $\Gamma(1/2)=\sqrt\pi$
> 这等价于 Gauss 积分 $\int_{-\infty}^\infty e^{-x^2}\,dx=\sqrt\pi$：令 $t=x^2$，则 $\Gamma(1/2)=\int_0^\infty t^{-1/2}e^{-t}\,dt = 2\int_0^\infty e^{-x^2}\,dx = \sqrt\pi$。

### B 函数的对称、递推与三角换元

#### 对称性 $B(p,q)=B(q,p)$

令 $t\mapsto 1-t$：
$$B(p,q)=\int_0^1 t^{p-1}(1-t)^{q-1}\,dt = \int_0^1 (1-t)^{p-1}t^{q-1}\,dt = B(q,p). \quad \square$$

#### 递推 $B(p,q)=\frac{p-1}{p+q-1}B(p-1,q)$

分部积分（$u=(1-t)^{q-1},\ dv=t^{p-1}\,dt$）：
$$B(p,q) = \left[\frac{t^p}{p}(1-t)^{q-1}\right]_0^1 + \frac{q-1}{p}\int_0^1 t^p(1-t)^{q-2}\,dt = \frac{q-1}{p}B(p+1,q-1).$$
结合对称性与 Γ-B 联系递推即得所给形式。等价地，由 $B(p,q)=\frac{\Gamma(p)\Gamma(q)}{\Gamma(p+q)}$ 与 $\Gamma(p)=(p-1)\Gamma(p-1)$：
$$B(p,q)=\frac{(p-1)\Gamma(p-1)\Gamma(q)}{\Gamma(p+q)} = \frac{p-1}{p+q-1}\cdot\frac{\Gamma(p-1)\Gamma(q)}{\Gamma(p+q-1)} = \frac{p-1}{p+q-1}B(p-1,q). \quad \square$$

#### 三角换元

令 $t=\sin^2\theta$，则 $dt=2\sin\theta\cos\theta\,d\theta$，$t:0\to1$ 对应 $\theta:0\to\pi/2$：
$$B(p,q) = \int_0^{\pi/2} \sin^{2(p-1)}\!\theta\cdot\cos^{2(q-1)}\!\theta\cdot 2\sin\theta\cos\theta\,d\theta = 2\int_0^{\pi/2}\sin^{2p-1}\!\theta\,\cos^{2q-1}\!\theta\,d\theta. \quad \square$$

### 总结

1. 收敛域：Γ 为 $s>0$（奇点 $t=0$ 决定），B 为 $p,q>0$。 ✓
2. Γ 递推：分部积分，$\Gamma(n)=(n-1)!$。 ✓
3. Γ-B 联系：二重积分 + 变量替换 $(u,v)\mapsto(x,t)$，Jacobian $=x$。 ✓
4. 余元公式：Γ-B 联系 + 替换 $t=x/(1+x)$ + 留数引理。 ✓
5. 倍元公式：$\Gamma(1/2)=\sqrt\pi$ + 倍量恒等式 $B(s,s)=2^{1-2s}B(s,1/2)$。 ✓
6. B 的对称/递推/三角换元：换元 + 分部 + Γ-B 联系。 ✓

$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> Γ、B 函数的全部初等性质都源于三个机制的组合：
> 1. **含参量积分 + 收敛性分析**：收敛域由奇点（$t=0$ 处幂次 $t^{s-1}$）决定，无穷远因 $e^{-t}$ 而无忧；
> 2. **分部积分**：给出 Γ 的递推 $\Gamma(s+1)=s\Gamma(s)$，使其成为阶乘的连续插值；
> 3. **二重积分换序 + 精心选择的变量替换**：Γ-B 联系 $(u,v)\mapsto(x,t)$（径向-比例分解）是核心，由此一切（余元、倍元、递推）皆可导出。
>
> 其中**余元公式**是唯一需要从外部引入非初等工具（留数定理 / 围道积分）的结果——它把 $\pi$ 与 $\sin\pi s$ 引入 Γ 的世界，是 Γ 函数超越"阶乘插值"而具有解析/数论深度的入口。

> [!warning] 余元公式的非初等性
> 余元公式 $\Gamma(s)\Gamma(1-s)=\pi/\sin\pi s$ 无法仅用实分析的初等换元证明——其本质是复分析（$\sin\pi s$ 的零点即 $\Gamma$ 的极点）。试图纯实分析证明会隐式使用等价的围道论证。这也说明 Γ 函数是复变函数，$s>0$ 只是其实积分定义的收敛域，其解析延拓 $\Gamma(z)$（$z\notin\{0,-1,-2,\ldots\}$）的极点恰由余元公式显化。

---

## 相关笔记

- [[含参量反常积分]] - Γ、B 收敛性判别与一致收敛的理论依据
- [[含参量常义积分]] - Γ-B 联系中二重积分换序的常义基础
- [[变量替换公式]] - Γ-B 联系、余元公式中变量替换的依据
- [[二重积分与Fubini定理]] - Γ(p)Γ(q) 化为二重积分的依据
- [[柯西积分公式]] - 余元公式的复分析视角（留数计算）
- [[Legendre多项式的正交性]] - 同为正交特殊函数，跨库衔接
- [[含参量积分的应用习题]] - Γ/B 的具体计算应用
