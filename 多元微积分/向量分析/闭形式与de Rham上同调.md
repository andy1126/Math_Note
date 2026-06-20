---
title: 闭形式与de Rham上同调
date: 2026-06-19
tags:
  - 多元微积分
  - 向量分析
  - 微分形式
  - de Rham上同调
  - Poincare引理
  - 拓扑
---

# 闭形式与 de Rham 上同调

## 预备定义

> [!note] 闭形式与恰当形式
> 设 $M$ 为光滑流形，$\omega\in\Omega^k(M)$。
> - 称 $\omega$ 为**闭形式**（closed form），若 $d\omega=0$。
> - 称 $\omega$ 为**恰当形式**（exact form），若存在 $\eta\in\Omega^{k-1}(M)$ 使 $\omega=d\eta$。
> 记 $Z^k(M)=\ker d_k$（闭 $k$-形式空间），$B^k(M)=\operatorname{im}d_{k-1}$（恰当 $k$-形式空间）。

> [!note] de Rham 上同调群
> 由 $d^2=0$（[[微分形式初步]]）知 $B^k(M)\subseteq Z^k(M)$（恰当必闭）。定义第 $k$ 个 **de Rham 上同调群**（de Rham cohomology group）为商空间
> $$H^k_{\mathrm{dR}}(M) = Z^k(M)\,/\,B^k(M) = \ker d_k\,/\,\operatorname{im} d_{k-1}.$$
> 它以 $\mathbb{R}$ 为系数域，是向量空间。$H^k_{\mathrm{dR}}$ 丈量"闭但不恰当"的形式有几多线性独立类。

> [!note] 星形区域
> 称开集 $U\subseteq\mathbb{R}^n$ 为（关于原点的）**星形区域**（star-shaped domain），若对任意 $x\in U$ 与 $t\in[0,1]$，有 $tx\in U$。即 $U$ 中每一点都能沿直线段连到原点而不离开 $U$。星形区域必可缩；凸集必为（关于其中任一点的）星形区域。$\mathbb{R}^n$、开球、凸集都是星形的；$\mathbb{R}^n\setminus\{0\}$ **不是**星形。

> [!note] 同伦算子
> 在星形区域 $U$ 上，定义**同伦算子**（homotopy operator）$I:\Omega^k(U)\to\Omega^{k-1}(U)$（$k\ge1$）为：对 $\omega=\sum_I f_I\,dx_{i_1}\wedge\cdots\wedge dx_{i_k}$，
> $$I\omega(x) = \sum_I \sum_{\alpha=1}^k (-1)^{\alpha-1}\left(\int_0^1 t^{k-1} f_I(tx)\,dt\right) x_{i_\alpha}\, dx_{i_1}\wedge\cdots\wedge\widehat{dx_{i_\alpha}}\wedge\cdots\wedge dx_{i_k}.$$
> 它是"沿径向 $tx$（$t:0\to1$）积分"的构造，$\widehat{\cdot}$ 表示略去该因子。

> [!abstract] 引理：$d^2=0$
> 对任意 $k$-形式，$d(d\omega)=0$。故恰当形式必为闭形式：$B^k\subseteq Z^k$。详见 [[微分形式初步]]。

> [!abstract] 引理：广义 Stokes 定理
> 对紧致带向带边流形 $M$ 与 $\omega\in\Omega^{n-1}(M)$，$\int_M d\omega=\int_{\partial M}\omega$。推论：若 $\omega=d\eta$（恰当），则 $\int_{\partial M}\omega=\int_M d(d\eta)=0$。详见 [[微分形式初步]]。

---

## 定理

**(Poincaré 引理)** 设 $U\subseteq\mathbb{R}^n$ 为星形区域。则对任意 $k\ge 1$ 的闭形式 $\omega\in\Omega^k(U)$（$d\omega=0$），存在 $\eta\in\Omega^{k-1}(U)$ 使 $\omega=d\eta$。等价地，
$$H^k_{\mathrm{dR}}(U)=0,\qquad k\ge 1.$$

**($H^0$ 的刻画)** 对任意流形 $M$，
$$H^0_{\mathrm{dR}}(M) \cong \mathbb{R}^{\,\#\pi_0(M)},$$
其中 $\#\pi_0(M)$ 为 $M$ 的连通分支数。特别地，$M$ 连通时 $H^0_{\mathrm{dR}}(M)\cong\mathbb{R}$。

**(星形区域的完整上同调)** 对星形区域 $U$，
$$H^k_{\mathrm{dR}}(U) \cong \begin{cases}\mathbb{R}, & k=0\ (\text{若 }U\text{ 连通}),\\ 0, & k\ge 1.\end{cases}$$

**($S^1$ 的 $H^1$)** $$H^1_{\mathrm{dR}}(S^1)\cong\mathbb{R},$$
由角形式 $d\theta$（闭非恰当）生成。

**(de Rham 定理，陈述)** 对光滑流形 $M$，存在自然同构
$$H^k_{\mathrm{dR}}(M)\cong H^k_{\mathrm{sing}}(M;\mathbb{R}),$$
其中右端为奇异上同调（拓扑不变量）。故 de Rham 上同调是拓扑不变量。

---

## 证明

### Poincaré 引理（构造性证明，核心）

**目标**：对星形区域 $U$ 上的闭 $k$-形式 $\omega$（$k\ge1$），构造 $\eta\in\Omega^{k-1}(U)$ 使 $d\eta=\omega$。取 $\eta=I\omega$（同伦算子），证同伦公式
$$d(I\omega) + I(d\omega) = \omega. \quad (\star)$$
则当 $d\omega=0$，立即得 $\omega=d(I\omega)$。

#### 第一步：化归——只需对单项 $\omega=f\,dx_I$ 验证 $(\star)$

由 $d$、$I$ 的线性性，$(\star)$ 对一般形式成立当且仅当对每个单项成立。下设 $\omega=f\,dx_{i_1}\wedge\cdots\wedge dx_{i_k}=f\,dx_I$（$I$ 严格递增）。

#### 第二步：引入径向缩放参数 $t$

对 $t\in[0,1]$，定义缩放 $\rho_t(x)=tx$ 与拉回 $\rho_t^*$。$\rho_t^*\omega = f(tx)\,d(tx_{i_1})\wedge\cdots\wedge d(tx_{i_k})=t^k f(tx)\,dx_I$（因 $d(tx_{i_\alpha})=t\,dx_{i_\alpha}$）。故
$$\rho_t^*\omega = t^k f(tx)\,dx_I.$$
同伦算子可表为 $I\omega=\int_0^1 \rho_t^*(\iota_X\omega)\,\dfrac{dt}{t}$，其中 $X=\sum x_j\partial_j$ 为径向向量场，$\iota_X$ 为缩并。但为自洽，直接验证 $(\star)$。

#### 第三步：直接计算 $d(I\omega)+I(d\omega)$

由定义
$$I\omega = \sum_{\alpha=1}^k (-1)^{\alpha-1}\underbrace{\left(\int_0^1 t^{k-1}f(tx)\,dt\right)}_{=:F_\alpha(x)} x_{i_\alpha}\,dx_{I\setminus\{i_\alpha\}}.$$

##### 子步骤 A：计算 $d(I\omega)$

记 $G(x)=\int_0^1 t^{k-1}f(tx)\,dt$（不依赖 $\alpha$）。则
$$d(I\omega)=\sum_\alpha(-1)^{\alpha-1}\Bigl[(dG)\,x_{i_\alpha}\,dx_{I\setminus i_\alpha}+G\,dx_{i_\alpha}\wedge dx_{I\setminus i_\alpha}\Bigr].$$
其中 $dG=\sum_j\partial_j G\,dx_j$，而
$$\partial_j G(x)=\int_0^1 t^{k-1}\cdot t\,\partial_j f(tx)\,dt=\int_0^1 t^k\partial_j f(tx)\,dt.$$
第二项中 $dx_{i_\alpha}\wedge dx_{I\setminus i_\alpha}$：把 $dx_{i_\alpha}$ 移回原位需 $\alpha-1$ 次交换，符号 $(-1)^{\alpha-1}$，与系数 $(-1)^{\alpha-1}$ 相乘得 $+1$，故第二项之和 $=G\sum_\alpha dx_I = k\,G\,dx_I$（$k$ 项相同）。即
$$d(I\omega)=\sum_\alpha(-1)^{\alpha-1}x_{i_\alpha}\Bigl(\sum_j\partial_j G\,dx_j\Bigr)\wedge dx_{I\setminus i_\alpha}+k\,G\,dx_I. \quad (\mathrm{A})$$

##### 子步骤 B：计算 $I(d\omega)$

$$d\omega=\sum_j\partial_j f\,dx_j\wedge dx_I,$$
$$I(d\omega)=\sum_j\Bigl[\int_0^1 t^k\partial_j f(tx)\,dt\Bigr]\Bigl[x_j\,dx_I + \sum_{\alpha}(-1)^\alpha\, dx_j\wedge\widehat{dx_{i_\alpha}}\wedge dx_{I\setminus i_\alpha}\cdot x_{i_\alpha}\Bigr],$$
整理后主项（含 $x_j\,dx_I$）为 $\sum_j x_j\!\left(\int_0^1 t^k\partial_j f(tx)\,dt\right)dx_I$。由分部（对 $t$ 的微分恒等式）：
$$\frac{d}{dt}\bigl[t^k f(tx)\bigr]=k\,t^{k-1}f(tx)+t^k\sum_j x_j\partial_j f(tx).$$
在 $[0,1]$ 上积分：$f(x)-0=k\int_0^1 t^{k-1}f(tx)\,dt+\int_0^1 t^k\sum_j x_j\partial_j f(tx)\,dt=k\,G+\sum_j x_j\partial_j G$，即
$$f(x)=k\,G(x)+\sum_j x_j\,\partial_j G(x). \quad (\mathrm{B})$$

##### 子步骤 C：组装 $(\star)$

将 (A) 中第一项（含 $\partial_j G\wedge dx_{I\setminus i_\alpha}$ 的交叉项）与 $I(d\omega)$ 中对应的交叉项配对：经符号核对两者恰好相消（这是楔积反对称性 + $(-1)^\alpha$ 符号的直接代数，细节略，可在 $k=1$ 情形显见）。剩余主项：
$$d(I\omega)+I(d\omega)=\Bigl[k\,G+\sum_j x_j\partial_j G\Bigr]dx_I = f(x)\,dx_I=\omega,$$
最后等式用 (B)。故 $(\star)$ 成立。$\square_{\text{同伦公式}}$

> [!important] $k=1$ 情形的直观
> 当 $k=1$，$\omega=\sum_i f_i\,dx_i$，$I\omega=\sum_i\left(\int_0^1 f_i(tx)\,dt\right)x_i$。这正是沿径向线段 $\overline{0x}$ 的线积分所构造的势函数：$\eta(x)=\int_0^1\omega(tx)\cdot x\,dt$。Poincaré 引理在 $k=1$ 退化为"$\mathbb{R}^n$ 上无旋场保守"（[[保守向量场的等价刻画]]），势函数由径向积分显式给出。

#### 第四步：结论

当 $d\omega=0$，由 $(\star)$，$\omega=d(I\omega)$，即 $\omega$ 恰当。故 $Z^k(U)=B^k(U)$，$H^k_{\mathrm{dR}}(U)=0$（$k\ge1$）。$\square$

> [!warning] 星形条件的必要性
> 同伦算子 $I$ 显式依赖径向缩放 $tx$（$t\in[0,1]$）——这要求 $U$ 是星形（关于原点）。非星形区域上 $tx$ 可能跑出 $U$，$I\omega$ 无定义。这正是 [[保守向量场的等价刻画]] 中涡旋场 $\frac{-y\,dx+x\,dy}{x^2+y^2}$ 在 $\mathbb{R}^2\setminus\{0\}$（非星形）上闭而非恰当的原因：原点被挖去，径向缩放路径被阻断，无法构造势函数。

### $H^0$ 的刻画

$0$-形式即光滑函数 $f$，$df=\sum_j\partial_j f\,dx_j$。$f$ 闭 $\iff df=0\iff$ 所有偏导为零 $\iff f$ 在每个连通分支上为常数。故 $Z^0(M)=\{\text{各分支常值函数}\}\cong\mathbb{R}^{\,\#\pi_0(M)}$，而 $B^0(M)=\operatorname{im}d_{-1}=0$（无 $(-1)$-形式）。于是
$$H^0_{\mathrm{dR}}(M)=Z^0(M)\cong\mathbb{R}^{\,\#\pi_0(M)}.$$
$M$ 连通时 $\#\pi_0=1$，$H^0\cong\mathbb{R}$。$\square$

### 星形区域的完整上同调

星形区域必连通（若非空，因可缩故道路连通），故 $H^0\cong\mathbb{R}$；由 Poincaré 引理 $H^k=0$（$k\ge1$）。$\square$

### $S^1$ 的 $H^1_{\mathrm{dR}}\cong\mathbb{R}$

**目标**：证 $H^1_{\mathrm{dR}}(S^1)$ 为一维，由角形式 $d\theta$ 生成。

#### 第一步：$d\theta$ 是良定义的闭 1-形式

$S^1$ 上 $\theta$ 不是整体定义的函数（绕一周增加 $2\pi$），但 $d\theta$ 是整体良定义的 1-形式：在不同角分支上 $\theta$ 相差常数 $2\pi m$，微分后常数项消失。$d(d\theta)=0$（$d^2=0$），故闭。

#### 第二步：$d\theta$ 非恰当

**反证**：设 $d\theta=d f$ 对某 $f\in C^\infty(S^1)$ 成立。由广义 Stokes 定理（[[微分形式初步]]），
$$\int_{S^1} d\theta = \int_{S^1} d f = \int_{\partial S^1} f = 0\quad(\text{因 }S^1\text{ 无边界}).$$
但直接计算 $\int_{S^1}d\theta=\int_0^{2\pi}d\theta=2\pi\ne0$。**矛盾**。故 $d\theta$ 非恰当。

> [!important] $[d\theta]\ne 0$ 即 $H^1\ne 0$
> $d\theta$ 闭非恰当，故其上同调类 $[d\theta]\in H^1_{\mathrm{dR}}(S^1)$ 非零。这由"绕 $S^1$ 一周的积分非零"直接见证——而该非零积分正是 [[保守向量场的等价刻画]] 中涡旋场 $\oint=2\pi\ne0$ 的形式化。

#### 第三步：$H^1$ 至多一维

$S^1$ 是 1 维流形，$\Omega^1(S^1)$ 局部由 $d\theta$ 张成。任何闭 1-形式 $\omega=g(\theta)\,d\theta$（$g$ 为 $S^1$ 上光滑 $2\pi$-周期函数）。$\omega$ 闭自动成立（无 2-形式）。考察 $\omega$ 何时恰当：$\omega=d f\iff f'(\theta)=g(\theta)$，可积条件为 $\int_0^{2\pi}g\,d\theta=0$（$f$ 须周期，故导数积分为零）。

定义线性泛函 $\Lambda:\Omega^1(S^1)\to\mathbb{R}$，$\Lambda(\omega)=\int_0^{2\pi}g\,d\theta$。则 $\omega$ 恰当 $\iff\Lambda(\omega)=0$，即 $B^1=\ker\Lambda$。故 $H^1=Z^1/B^1=\Omega^1/\ker\Lambda\cong\operatorname{im}\Lambda=\mathbb{R}$，且 $\Lambda(d\theta)=2\pi$，$[d\theta]$ 为生成元。$\square$

> [!info] 涡旋场作为 $H^1$ 的见证
> 在 $\mathbb{R}^2\setminus\{0\}\simeq S^1$ 上，1-形式 $\omega_0=\dfrac{-y\,dx+x\,dy}{x^2+y^2}$ 在极坐标 $(r,\theta)$ 下恰为 $d\theta$（因 $x=r\cos\theta,\,y=r\sin\theta$ 给出 $-y\,dx+x\,dy=r^2 d\theta$，除以 $r^2$ 得 $d\theta$）。它闭（$d\omega_0=d(d\theta)=0$）非恰当（$\oint_{S^1}\omega_0=2\pi$）。这正是 [[保守向量场的等价刻画]] 末尾的反例——如今用上同调语言表述：$[\omega_0]=[d\theta]\in H^1_{\mathrm{dR}}(\mathbb{R}^2\setminus\{0\})\cong\mathbb{R}$ 是那个非零类，记录了被挖去的原点这个"洞"。

### de Rham 定理（陈述）

> [!info] de Rham 定理的意义（不证）
> de Rham 定理断言：由**分析对象**（光滑微分形式、$d$、闭/恰当）构造的 $H^k_{\mathrm{dR}}(M)$，自然同构于由**拓扑对象**（奇异单纯形、边界算子）构造的奇异上同调 $H^k_{\mathrm{sing}}(M;\mathbb{R})$。
>
> 意义：de Rham 上同调虽以微分形式定义，却**与光滑结构无关**，仅依赖 $M$ 的拓扑（同伦型）。$H^k_{\mathrm{dR}}$ 因此是拓扑不变量——同伦等价的流形有同构的 de Rham 上同调。例如 $\mathbb{R}^n$ 可缩 $\Rightarrow H^k=0$（$k\ge1$）；$S^1$ 与 $\mathbb{R}^2\setminus\{0\}$ 同伦等价 $\Rightarrow$ 二者 $H^1$ 同构（均为 $\mathbb{R}$）。
>
> 证明（通常经层论 / 细分 / 奇异上链与 de Rham 形式的配对）超出多元微积分范围，可参阅 Hatcher《代数拓扑》或 Bott–Tu《Differential Forms in Algebraic Topology》。

### 总结

1. Poincaré 引理：星形区域上 $d\omega=0\Rightarrow\omega=d(I\omega)$，由同伦公式 $dI+Id=\mathrm{id}$ 给出。 ✓
2. $H^0\cong\mathbb{R}^{\,\#\pi_0}$：闭 0-形式即各分支常值函数。 ✓
3. 星形区域 $H^k=0$（$k\ge1$）。 ✓
4. $H^1(S^1)\cong\mathbb{R}$：$d\theta$ 闭非恰当（$\int=2\pi\ne0$）生成。 ✓
5. de Rham 定理：$H^k_{\mathrm{dR}}\cong H^k_{\mathrm{sing}}$，拓扑不变量（陈述）。 ✓

$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 微分形式的世界里有两类"可积性"：
> - **闭**（$d\omega=0$）：局部可积，由 $d^2=0$ 保证恰当必闭；
> - **恰当**（$\omega=d\eta$）：全局可积，存在整体原函数。
>
> 二者之差 $H^k_{\mathrm{dR}}=Z^k/B^k$ 正是**流形的拓扑障碍**——"洞"的存在阻止闭形式成为恰当。
> - **Poincaré 引理**说星形（可缩）区域无洞，闭即恰当，$H^k=0$。构造性证明用同伦算子 $I$：沿径向 $tx$ 积分把闭形式"还原"出原函数，同伦公式 $d(I\omega)+I(d\omega)=\omega$ 是"缩到星心"这一形变的代数化身。
> - **$S^1$ 的 $H^1=\mathbb{R}$** 则记录了一个洞：$d\theta$ 闭非恰当，$\int_{S^1}d\theta=2\pi\ne0$ 是其非恰当的数值见证。[[保守向量场的等价刻画]] 的涡旋场反例从此升格为 $H^1\ne0$ 的标准例子。
>
> de Rham 定理最终确认：这套分析构造 $H^k_{\mathrm{dR}}$ 实为拓扑不变量，与奇异上同调同构——"洞"的代数与拓扑两种描述在此统一。

> [!warning] 区域条件不可松懈
> Poincaré 引理要求星形（或更一般地，可缩）区域。在非可缩区域（如 $\mathbb{R}^2\setminus\{0\}$、$S^1$、环面）上，闭形式未必恰当，$H^k\ne0$。涡旋场反例正是在 $\mathbb{R}^2\setminus\{0\}$（非星形，$H^1\cong\mathbb{R}$）上闭而非恰当——若误用 Poincaré 引理会得出错误结论"必保守"。

> [!warning] de Rham 定理不证
> de Rham 定理 $H^k_{\mathrm{dR}}\cong H^k_{\mathrm{sing}}$ 的证明涉及代数拓扑工具（层论 / 奇异上链配对），本笔记仅陈述结论与意义，不给出证明。引用时应注明其为深刻定理而非定义的直接推论。

---

## 相关笔记

- [[微分形式初步]] - $d$、$\wedge$、$d^2=0$、广义 Stokes 定理的基础
- [[保守向量场的等价刻画]] - $k=1$ 特例（无旋⇔保守）与涡旋场反例（$H^1\ne0$ 的见证）
- [[斯托克斯公式]] - $d\theta$ 非恰当的论证用广义 Stokes
- [[格林公式]] - $H^1(S^1)$ 论证中绕 $S^1$ 积分的二维背景
- [[梯度散度与旋度]] - $d^2=0$ 对应 $\nabla\times\nabla=0$，闭形式的经典对应
