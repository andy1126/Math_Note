---
title: 极坐标下的 Laplace 算子
date: 2026-06-18
tags:
  - 题解
  - 多元微积分
  - 偏微分方程
  - Laplace算子
  - 链式法则
  - 极坐标
  - 坐标变换
---

# 极坐标下的 Laplace 算子

## 题目

> 设 $u: \mathbb{R}^2 \to \mathbb{R}$ 为 $C^2$ 函数。引入极坐标变换
> $$x = r\cos\theta, \qquad y = r\sin\theta \quad (r > 0,\; \theta \in \mathbb{R}).$$
> 将二维 Laplace 算子 $\Delta = \dfrac{\partial^2}{\partial x^2} + \dfrac{\partial^2}{\partial y^2}$ 用极坐标变量 $(r, \theta)$ 表示，证明
> $$\Delta = \frac{\partial^2}{\partial r^2} + \frac{1}{r}\frac{\partial}{\partial r} + \frac{1}{r^2}\frac{\partial^2}{\partial \theta^2}.$$

---

## 预备定义与定理

> [!note] Laplace 算子（Laplacian）
> 对 $C^2$ 函数 $u: \mathbb{R}^n \to \mathbb{R}$，其 **Laplace 算子**（Laplacian）定义为各二阶纯偏导之和：
> $$\Delta u = \sum_{i=1}^n \frac{\partial^2 u}{\partial x_i^2}.$$
> 在 $\mathbb{R}^2$ 中，$\Delta u = u_{xx} + u_{yy}$。

> [!note] 极坐标变换
> 平面极坐标 $(r, \theta)$ 与直角坐标 $(x, y)$ 的关系为
> $$x = r\cos\theta, \quad y = r\sin\theta, \qquad r = \sqrt{x^2 + y^2}, \quad \theta = \arctan\frac{y}{x}.$$
> 该变换在 $\mathbb{R}^2 \setminus \{0\}$ 上是 $C^\infty$ 微分同胚（各除去一条射线使 $\theta$ 单值）。

> [!abstract] 定理：多元链式法则
> 若 $w = f(x_1, \ldots, x_n)$ 可微，且每个 $x_i = x_i(t_1, \ldots, t_p)$ 可微，则
> $$\frac{\partial w}{\partial t_j} = \sum_{i=1}^n \frac{\partial w}{\partial x_i} \frac{\partial x_i}{\partial t_j}.$$
> 特别地，**二阶导需对一阶导再次应用链式法则**——这正是本题的核心技术。详见 [[多元链式法则]]。

---

## 解答

### 第一步：计算 $r, \theta$ 关于 $x, y$ 的偏导数

由 $r = \sqrt{x^2 + y^2}$，$\theta = \arctan(y/x)$：

$$
\begin{aligned}
\frac{\partial r}{\partial x} = \frac{x}{r} = \cos\theta, &\qquad
\frac{\partial r}{\partial y} = \frac{y}{r} = \sin\theta, \\[2mm]
\frac{\partial \theta}{\partial x} = \frac{-y}{x^2 + y^2} = -\frac{\sin\theta}{r}, &\qquad
\frac{\partial \theta}{\partial y} = \frac{x}{x^2 + y^2} = \frac{\cos\theta}{r}.
\end{aligned}
$$

### 第二步：写出链式法则的一阶算子关系

由链式法则，对任意 $C^1$ 函数 $u$，将 $u$ 看作 $(x,y)$ 的函数，而 $(x,y)$ 又通过逆变换依赖于 $(r,\theta)$（或等价地，将 $u$ 的偏导用 $r,\theta$ 偏导表示）：

$$
\begin{aligned}
\frac{\partial}{\partial x} &= \frac{\partial r}{\partial x}\frac{\partial}{\partial r} + \frac{\partial \theta}{\partial x}\frac{\partial}{\partial \theta}
= \cos\theta\,\frac{\partial}{\partial r} - \frac{\sin\theta}{r}\,\frac{\partial}{\partial \theta}, \quad \cdots (1) \\[2mm]
\frac{\partial}{\partial y} &= \frac{\partial r}{\partial y}\frac{\partial}{\partial r} + \frac{\partial \theta}{\partial y}\frac{\partial}{\partial \theta}
= \sin\theta\,\frac{\partial}{\partial r} + \frac{\cos\theta}{r}\,\frac{\partial}{\partial \theta}. \quad \cdots (2)
\end{aligned}
$$

> [!info] 算子观点
> 将 $\partial_x$、$\partial_y$ 视为**算子**，则 $(1)(2)$ 给出了它们在极坐标基底 $\{\partial_r, \partial_\theta\}$ 下的表达式。二阶导即是将这些算子**再次作用**于自身（或彼此），这正是第二步链式法则的含义。

### 第三步：计算 $\partial_{xx}$ —— 将 $\partial_x$ 作用于自身

由 $(1)$，
$$\frac{\partial^2}{\partial x^2} = \left( \cos\theta\,\frac{\partial}{\partial r} - \frac{\sin\theta}{r}\,\frac{\partial}{\partial \theta} \right)\!\left( \cos\theta\,\frac{\partial}{\partial r} - \frac{\sin\theta}{r}\,\frac{\partial}{\partial \theta} \right).$$

展开为四个子项：记
$$
\begin{aligned}
T_1 &= \cos\theta\,\frac{\partial}{\partial r}\!\left( \cos\theta\,\frac{\partial}{\partial r} \right), \\[2mm]
T_2 &= -\cos\theta\,\frac{\partial}{\partial r}\!\left( \frac{\sin\theta}{r}\,\frac{\partial}{\partial \theta} \right), \\[2mm]
T_3 &= -\frac{\sin\theta}{r}\,\frac{\partial}{\partial \theta}\!\left( \cos\theta\,\frac{\partial}{\partial r} \right), \\[2mm]
T_4 &= \frac{\sin\theta}{r}\,\frac{\partial}{\partial \theta}\!\left( \frac{\sin\theta}{r}\,\frac{\partial}{\partial \theta} \right).
\end{aligned}
$$

分别计算（注意 $\partial_r$、$\partial_\theta$ 作用于系数时只对其显式依赖求导）。

#### $T_1$：$\cos\theta\,\partial_r(\cos\theta\,\partial_r)$

$\cos\theta$ 不依赖于 $r$，$\partial_r(\cos\theta) = 0$。故
$$T_1 = \cos\theta \cdot \cos\theta \cdot \partial_{rr} = \cos^2\theta\,\partial_{rr}. \quad \square$$

#### $T_2$：$-\cos\theta\,\partial_r\!\left(\dfrac{\sin\theta}{r}\,\partial_\theta\right)$

应用乘积法则：
$$-\cos\theta\left[ \frac{\partial}{\partial r}\!\left(\frac{\sin\theta}{r}\right) \cdot \partial_\theta + \frac{\sin\theta}{r} \cdot \frac{\partial}{\partial r}\partial_\theta \right].$$

由 $\partial_r(\sin\theta / r) = \sin\theta \cdot (-1/r^2) = -\sin\theta/r^2$，得
$$T_2 = -\cos\theta\left[ -\frac{\sin\theta}{r^2}\,\partial_\theta + \frac{\sin\theta}{r}\,\partial_{r\theta} \right]
= \frac{\cos\theta\sin\theta}{r^2}\,\partial_\theta - \frac{\cos\theta\sin\theta}{r}\,\partial_{r\theta}. \quad \square$$

#### $T_3$：$-\dfrac{\sin\theta}{r}\,\partial_\theta(\cos\theta\,\partial_r)$

应用乘积法则：
$$-\frac{\sin\theta}{r}\left[ \frac{\partial}{\partial\theta}(\cos\theta) \cdot \partial_r + \cos\theta \cdot \frac{\partial}{\partial\theta}\partial_r \right].$$

由 $\partial_\theta(\cos\theta) = -\sin\theta$，得
$$T_3 = -\frac{\sin\theta}{r}\bigl[ -\sin\theta\,\partial_r + \cos\theta\,\partial_{r\theta} \bigr]
= \frac{\sin^2\theta}{r}\,\partial_r - \frac{\sin\theta\cos\theta}{r}\,\partial_{r\theta}. \quad \square$$

#### $T_4$：$\dfrac{\sin\theta}{r}\,\partial_\theta\!\left(\dfrac{\sin\theta}{r}\,\partial_\theta\right)$

应用乘积法则：
$$\frac{\sin\theta}{r}\left[ \frac{\partial}{\partial\theta}\!\left(\frac{\sin\theta}{r}\right) \cdot \partial_\theta + \frac{\sin\theta}{r} \cdot \partial_{\theta\theta} \right].$$

由 $\partial_\theta(\sin\theta/r) = \cos\theta/r$，得
$$T_4 = \frac{\sin\theta}{r}\left[ \frac{\cos\theta}{r}\,\partial_\theta + \frac{\sin\theta}{r}\,\partial_{\theta\theta} \right]
= \frac{\sin\theta\cos\theta}{r^2}\,\partial_\theta + \frac{\sin^2\theta}{r^2}\,\partial_{\theta\theta}. \quad \square$$

#### 合并 $T_1 + T_2 + T_3 + T_4$

$$
\begin{aligned}
\frac{\partial^2}{\partial x^2} &= \cos^2\theta\,\partial_{rr} \\[2mm]
&\quad + \left( \frac{\cos\theta\sin\theta}{r^2} + \frac{\sin\theta\cos\theta}{r^2} \right)\partial_\theta
   + \left( -\frac{\cos\theta\sin\theta}{r} - \frac{\sin\theta\cos\theta}{r} \right)\partial_{r\theta} \\[2mm]
&\quad + \frac{\sin^2\theta}{r}\,\partial_r + \frac{\sin^2\theta}{r^2}\,\partial_{\theta\theta} \\[2mm]
&= \cos^2\theta\,\partial_{rr} + \frac{\sin^2\theta}{r}\,\partial_r + \frac{\sin^2\theta}{r^2}\,\partial_{\theta\theta}
   + \frac{2\sin\theta\cos\theta}{r^2}\,\partial_\theta - \frac{2\sin\theta\cos\theta}{r}\,\partial_{r\theta}. \quad \cdots (3)
\end{aligned}
$$

### 第四步：计算 $\partial_{yy}$ —— 将 $\partial_y$ 作用于自身

由 $(2)$，
$$\frac{\partial^2}{\partial y^2} = \left( \sin\theta\,\frac{\partial}{\partial r} + \frac{\cos\theta}{r}\,\frac{\partial}{\partial \theta} \right)\!\left( \sin\theta\,\frac{\partial}{\partial r} + \frac{\cos\theta}{r}\,\frac{\partial}{\partial \theta} \right).$$

展开为四个子项：
$$
\begin{aligned}
S_1 &= \sin\theta\,\frac{\partial}{\partial r}\!\left( \sin\theta\,\frac{\partial}{\partial r} \right), \\[2mm]
S_2 &= \sin\theta\,\frac{\partial}{\partial r}\!\left( \frac{\cos\theta}{r}\,\frac{\partial}{\partial \theta} \right), \\[2mm]
S_3 &= \frac{\cos\theta}{r}\,\frac{\partial}{\partial \theta}\!\left( \sin\theta\,\frac{\partial}{\partial r} \right), \\[2mm]
S_4 &= \frac{\cos\theta}{r}\,\frac{\partial}{\partial \theta}\!\left( \frac{\cos\theta}{r}\,\frac{\partial}{\partial \theta} \right).
\end{aligned}
$$

分别计算：

#### $S_1$：$\sin\theta\,\partial_r(\sin\theta\,\partial_r)$

$\partial_r(\sin\theta) = 0$，故
$$S_1 = \sin^2\theta\,\partial_{rr}. \quad \square$$

#### $S_2$：$\sin\theta\,\partial_r\!\left(\dfrac{\cos\theta}{r}\,\partial_\theta\right)$

$\partial_r(\cos\theta/r) = -\cos\theta/r^2$，故
$$S_2 = \sin\theta\left[ -\frac{\cos\theta}{r^2}\,\partial_\theta + \frac{\cos\theta}{r}\,\partial_{r\theta} \right]
= -\frac{\sin\theta\cos\theta}{r^2}\,\partial_\theta + \frac{\sin\theta\cos\theta}{r}\,\partial_{r\theta}. \quad \square$$

#### $S_3$：$\dfrac{\cos\theta}{r}\,\partial_\theta(\sin\theta\,\partial_r)$

$\partial_\theta(\sin\theta) = \cos\theta$，故
$$S_3 = \frac{\cos\theta}{r}\bigl[ \cos\theta\,\partial_r + \sin\theta\,\partial_{r\theta} \bigr]
= \frac{\cos^2\theta}{r}\,\partial_r + \frac{\sin\theta\cos\theta}{r}\,\partial_{r\theta}. \quad \square$$

#### $S_4$：$\dfrac{\cos\theta}{r}\,\partial_\theta\!\left(\dfrac{\cos\theta}{r}\,\partial_\theta\right)$

$\partial_\theta(\cos\theta/r) = -\sin\theta/r$，故
$$S_4 = \frac{\cos\theta}{r}\left[ -\frac{\sin\theta}{r}\,\partial_\theta + \frac{\cos\theta}{r}\,\partial_{\theta\theta} \right]
= -\frac{\sin\theta\cos\theta}{r^2}\,\partial_\theta + \frac{\cos^2\theta}{r^2}\,\partial_{\theta\theta}. \quad \square$$

#### 合并 $S_1 + S_2 + S_3 + S_4$

$$
\begin{aligned}
\frac{\partial^2}{\partial y^2} &= \sin^2\theta\,\partial_{rr} \\[2mm]
&\quad + \left( -\frac{\sin\theta\cos\theta}{r^2} - \frac{\sin\theta\cos\theta}{r^2} \right)\partial_\theta
   + \left( \frac{\sin\theta\cos\theta}{r} + \frac{\sin\theta\cos\theta}{r} \right)\partial_{r\theta} \\[2mm]
&\quad + \frac{\cos^2\theta}{r}\,\partial_r + \frac{\cos^2\theta}{r^2}\,\partial_{\theta\theta} \\[2mm]
&= \sin^2\theta\,\partial_{rr} + \frac{\cos^2\theta}{r}\,\partial_r + \frac{\cos^2\theta}{r^2}\,\partial_{\theta\theta}
   - \frac{2\sin\theta\cos\theta}{r^2}\,\partial_\theta + \frac{2\sin\theta\cos\theta}{r}\,\partial_{r\theta}. \quad \cdots (4)
\end{aligned}
$$

### 第五步：求和 $\Delta = \partial_{xx} + \partial_{yy}$

将 $(3)$ 与 $(4)$ 逐项相加：

$$
\begin{aligned}
\Delta &= (\cos^2\theta + \sin^2\theta)\,\partial_{rr} \\[2mm]
&\quad + \left(\frac{\sin^2\theta}{r} + \frac{\cos^2\theta}{r}\right)\partial_r \\[2mm]
&\quad + \left(\frac{\sin^2\theta}{r^2} + \frac{\cos^2\theta}{r^2}\right)\partial_{\theta\theta} \\[2mm]
&\quad + \left(\frac{2\sin\theta\cos\theta}{r^2} - \frac{2\sin\theta\cos\theta}{r^2}\right)\partial_\theta \\[2mm]
&\quad + \left(-\frac{2\sin\theta\cos\theta}{r} + \frac{2\sin\theta\cos\theta}{r}\right)\partial_{r\theta}.
\end{aligned}
$$

利用 $\cos^2\theta + \sin^2\theta = 1$，交叉项全部抵消：

- $\partial_{rr}$ 系数：$\cos^2\theta + \sin^2\theta = 1$
- $\partial_r$ 系数：$\dfrac{\sin^2\theta + \cos^2\theta}{r} = \dfrac{1}{r}$
- $\partial_{\theta\theta}$ 系数：$\dfrac{\sin^2\theta + \cos^2\theta}{r^2} = \dfrac{1}{r^2}$
- $\partial_\theta$ 系数：$0$
- $\partial_{r\theta}$ 系数：$0$

故
$$\Delta = \frac{\partial^2}{\partial r^2} + \frac{1}{r}\frac{\partial}{\partial r} + \frac{1}{r^2}\frac{\partial^2}{\partial \theta^2}. \quad \blacksquare$$

> [!important] 交叉项为何抵消？
> 从 $(3)(4)$ 可见，$\partial_{xx}$ 含 $+2sc/r^2\,\partial_\theta$ 和 $-2sc/r\,\partial_{r\theta}$，而 $\partial_{yy}$ 含 $-2sc/r^2\,\partial_\theta$ 和 $+2sc/r\,\partial_{r\theta}$（其中 $s = \sin\theta$, $c = \cos\theta$）。二者**恰好反号**，相加归零。这不是巧合——它反映了 Laplace 算子在旋转下的不变性：极坐标仅是坐标系的旋转伸缩，$\Delta$ 作为旋转不变算子，不应出现混合导数项。

---

## 答案

将 Laplace 算子作用于 $C^2$ 函数 $u$：

$$\boxed{\;\Delta u = u_{rr} + \frac{1}{r}\,u_r + \frac{1}{r^2}\,u_{\theta\theta}\;}$$

或等价地写成紧凑形式：
$$\boxed{\;\Delta = \frac{1}{r}\frac{\partial}{\partial r}\!\left(r\frac{\partial}{\partial r}\right) + \frac{1}{r^2}\frac{\partial^2}{\partial \theta^2}\;}$$

---

## 变形与延伸

> [!info] 变形 1（三维球坐标 Laplace 算子）
> 在 $\mathbb{R}^3$ 中引入球坐标
> $$x = r\sin\varphi\cos\theta,\quad y = r\sin\varphi\sin\theta,\quad z = r\cos\varphi \quad (r > 0,\; \varphi \in [0,\pi],\; \theta \in [0, 2\pi)).$$
> 用类似的二次链式法则推导三维 Laplace 算子在球坐标下的表达式：
> $$\Delta = \frac{1}{r^2}\frac{\partial}{\partial r}\!\left(r^2\frac{\partial}{\partial r}\right) + \frac{1}{r^2\sin\varphi}\frac{\partial}{\partial\varphi}\!\left(\sin\varphi\,\frac{\partial}{\partial\varphi}\right) + \frac{1}{r^2\sin^2\varphi}\frac{\partial^2}{\partial\theta^2}.$$
> 或展开形式：
> $$\Delta = \partial_{rr} + \frac{2}{r}\partial_r + \frac{1}{r^2}\partial_{\varphi\varphi} + \frac{\cot\varphi}{r^2}\partial_\varphi + \frac{1}{r^2\sin^2\varphi}\partial_{\theta\theta}.$$
>
> **提示**：计算步骤与本题完全平行，但中间变量有三个（$r, \varphi, \theta$），计算量更大。关键技巧是先算 Jacobian 矩阵 $\partial(r,\varphi,\theta)/\partial(x,y,z)$，再套链式法则。特别注意 $\varphi$ 的导数会产生 $\cot\varphi$ 项。

> [!info] 变形 2（连接调和函数）
> 若 $u$ 满足 **Laplace 方程** $\Delta u = 0$（即 $u$ 为调和函数），则极坐标形式给出
> $$u_{rr} + \frac{1}{r}u_r + \frac{1}{r^2}u_{\theta\theta} = 0.$$
> 利用此形式讨论：若 $u$ 是单位圆盘上的调和函数，其边界值 $u(1, \theta)$ 的 Fourier 系数与 $u$ 的幂级数展开（即 $u(r,\theta) = a_0/2 + \sum_{n=1}^\infty r^n(a_n\cos n\theta + b_n\sin n\theta)$）之间的关系是什么？
>
> **提示**：用分离变量法 $u(r,\theta) = R(r)\Theta(\theta)$，代入极坐标 Laplace 方程得 $r^2R''/R + rR'/R = -\Theta''/\Theta = \lambda$（常数）。解出 $R(r) = r^{\pm\sqrt{\lambda}}$ 及 $\Theta$ 的三角函数形式，结合边界条件的周期性（$\Theta(\theta+2\pi)=\Theta(\theta)$）得 $\lambda = n^2$。与调和函数的 Poisson 积分公式对比。详见 [[调和函数的均值性质与极值原理]]。

> [!info] 变形 3（径向对称调和函数——二维 $\ln r$）
> 若 $u$ 在圆环（不含原点）上是**径向对称**的（即 $u = u(r)$），则 Laplace 方程退化为 ODE：
> $$u_{rr} + \frac{1}{r}u_r = 0 \;\Longleftrightarrow\; \frac{1}{r}(r u_r)_r = 0.$$
> 积分两次得 $u(r) = C\ln r + D$（$C, D$ 为常数）。这给出二维 Laplace 方程的**基本解** $\ln r$。
>
> **问题**：验证 $u(x,y) = \ln\sqrt{x^2+y^2}$ 满足 $\Delta u = 0$（在 $\mathbb{R}^2 \setminus \{0\}$ 上），并计算其在单位圆上的 Dirichlet 能量 $\int_{B_1} \|\nabla u\|^2$（注意原点处的奇性）。
>
> **提示**：直接用直角坐标验证 $\Delta \ln r = 0$ 也是好的练习——用本题公式则 $u_{\theta\theta} = 0$，剩下 $u_{rr} + u_r/r = -1/r^2 + (1/r)(1/r) = 0$。能量积分在原点对数发散，需挖去小圆盘取极限。

> [!info] 变形 4（三维径向调和函数——$1/r$）
> 类似地，三维球对称调和函数满足 $u_{rr} + \dfrac{2}{r}u_r = 0$，解得 $u(r) = \dfrac{C}{r} + D$。函数 $\dfrac{1}{r} = \dfrac{1}{\sqrt{x^2+y^2+z^2}}$ 是三维 Laplace 方程的**基本解**（即 $\Delta(1/r) = -4\pi\delta$ 在分布意义下）。
>
> **问题**：用变形 1 的球坐标公式验证 $\Delta(1/r) = 0$（在 $\mathbb{R}^3 \setminus \{0\}$ 上）；并对比二维与三维径向调和函数在原点的奇性差异（$\ln r$ vs $1/r$）。
>
> **提示**：$u = r^{-1}$，$u_r = -r^{-2}$，$u_{rr} = 2r^{-3}$，代入 $\partial_{rr} + \frac{2}{r}\partial_r$ 得 $2r^{-3} + \frac{2}{r}(-r^{-2}) = 0$。物理上，二维对应线源（对数势），三维对应点源（Coulomb 势）。
