---
title: Runge-Kutta 方法的相容性与收敛阶
date: 2026-05-28
tags:
  - 数值分析
  - 微分方程数值解
  - Runge-Kutta
  - RK4
  - 收敛阶
  - Gronwall
---

# Runge-Kutta 方法的相容性与收敛阶

## 预备定义

> [!note] 初值问题
> 考虑
> $$y'(t) = f(t, y(t)), \quad y(t_0) = y_0, \quad t \in [t_0, T].$$
> 假设 $f: [t_0, T] \times \mathbb{R}^d \to \mathbb{R}^d$ 关于 $y$ Lipschitz（常数 $L$）：
> $$\|f(t, y) - f(t, z)\| \leq L\,\|y - z\|.$$

> [!note] 一步法
> 给定步长 $h$，节点 $t_n = t_0 + nh$。一步法
> $$y_{n+1} = y_n + h\,\Phi(t_n, y_n, h)$$
> 其中 $\Phi$ 为**增量函数**（incremental function）。

> [!note] 局部截断误差
> 设 $y(t)$ 为真解。**局部截断误差**：
> $$\tau_n(h) := y(t_{n+1}) - y(t_n) - h\,\Phi(t_n, y(t_n), h).$$
> 衡量"从真解出发一步走有多远"。

> [!note] 相容性与阶数
> 一步法 **$p$ 阶相容**（consistent of order $p$），若
> $$|\tau_n(h)| \leq C\,h^{p+1}$$
> 对一切 $n, h$（充分小 $h$）。

> [!note] 经典 RK4
> 取
> $$\begin{aligned}
> k_1 &= f(t_n, y_n), \\
> k_2 &= f(t_n + h/2,\ y_n + h k_1 / 2), \\
> k_3 &= f(t_n + h/2,\ y_n + h k_2 / 2), \\
> k_4 &= f(t_n + h,\ y_n + h k_3), \\
> y_{n+1} &= y_n + \frac{h}{6}(k_1 + 2 k_2 + 2 k_3 + k_4).
> \end{aligned}$$
> 即 $\Phi(t, y, h) = (k_1 + 2k_2 + 2k_3 + k_4)/6$。

> [!abstract] 引理：Gronwall（离散形式）
> 设 $|e_{n+1}| \leq (1 + Ah)\,|e_n| + B\,h^{p+1}$，$|e_0| = 0$，$A, B > 0$。则
> $$|e_n| \leq \frac{B\,h^p}{A}\,(e^{A n h} - 1) \leq \frac{B\,h^p}{A}\,e^{A(T - t_0)}.$$
>
> **证明**：归纳 $|e_n| \leq B h^{p+1} \sum_{k=0}^{n-1}(1+Ah)^k \leq \dfrac{Bh^{p+1}((1+Ah)^n - 1)}{Ah} \leq \dfrac{Bh^p e^{Anh}}{A}$（用 $1 + Ah \leq e^{Ah}$）。$\square$
>
> 这是 [[Gronwall不等式]] 的离散版本。

---

## 定理（RK4 的收敛性）

设初值问题中 $f \in C^4$，关于 $y$ Lipschitz。经典 RK4 满足：

**(i)（相容性）** 局部截断误差 $|\tau_n(h)| \leq C\,h^5$，故 **4 阶相容**。

**(ii)（增量函数 Lipschitz）** $\Phi$ 关于 $y$ 一致 Lipschitz：存在 $\Lambda$ 使
$$\|\Phi(t, y, h) - \Phi(t, z, h)\| \leq \Lambda\,\|y - z\|.$$

**(iii)（全局收敛阶）** 全局误差 $e_n = y(t_n) - y_n$ 满足
$$\max_{0 \leq n \leq N} \|e_n\| \leq K\,h^4,$$
其中 $K$ 仅依赖 $L, T - t_0$ 与 $f$ 的 $C^4$-范数。RK4 **全局 4 阶收敛**。

---

## 第(i)部分的证明：相容性

### 第一步：真解的 Taylor 展开

将 $y(t_n + h)$ 在 $t_n$ 处 Taylor 展开至 5 阶：
$$y(t_n + h) = y(t_n) + h\,y'(t_n) + \frac{h^2}{2} y''(t_n) + \frac{h^3}{6} y'''(t_n) + \frac{h^4}{24} y^{(4)}(t_n) + O(h^5). \quad \cdots (\mathrm{T})$$

用 $y' = f$ 反复求导（链式法则）：
$$y'' = f_t + f_y f,\qquad y''' = f_{tt} + 2 f_{ty} f + f_{yy} f^2 + f_y(f_t + f_y f),$$
$y^{(4)}$ 类似但更冗长。所有项均为 $f$ 及其偏导在 $(t_n, y(t_n))$ 处的取值。

### 第二步：RK4 增量函数的 Taylor 展开

分别 Taylor 展开 $k_2, k_3, k_4$（在 $(t_n, y(t_n))$ 处）：
$$\begin{aligned}
k_1 &= f, \\
k_2 &= f + \frac{h}{2}(f_t + f_y f) + \frac{h^2}{8}(f_{tt} + 2 f_{ty} f + f_{yy} f^2) + O(h^3), \\
k_3 &= f + \frac{h}{2}(f_t + f_y f) + \frac{h^2}{8}(f_{tt} + 2 f_{ty} f + f_{yy} f^2) + \frac{h^2}{4} f_y(f_t + f_y f) + O(h^3), \\
k_4 &= f + h(f_t + f_y f) + \frac{h^2}{2}(\cdots) + h^2 f_y(f_t + f_y f) + O(h^3).
\end{aligned}$$

> [!info] 系数选取的"魔术"
> RK4 的系数 $1, 2, 2, 1$ 与节点 $0, 1/2, 1/2, 1$ **精确选取**，使得 $\Phi = (k_1 + 2k_2 + 2k_3 + k_4)/6$ 的 Taylor 展开恰与 $y(t_n + h) - y(t_n)$ 在 $h^4$ 阶之前完全匹配。这一匹配需要满足 **8 个非线性代数条件**（Butcher 1964）。RK4 是这些条件最简洁的 4 阶解。

### 第三步：相消

经直接（繁但机械）的代数验证：
$$y(t_n + h) - y(t_n) = h\,\Phi(t_n, y(t_n), h) + O(h^5).$$

即
$$|\tau_n(h)| = O(h^5). \quad \square$$

---

## 第(ii)部分的证明：$\Phi$ 的 Lipschitz 性

固定 $t, h$。下证 $\|\Phi(t, y, h) - \Phi(t, z, h)\| \leq \Lambda\,\|y - z\|$。

设
$$k_1^y = f(t, y),\quad k_1^z = f(t, z).$$
则 $\|k_1^y - k_1^z\| \leq L\,\|y - z\|$（Lipschitz of $f$）。

类似估计 $k_2$：
$$\|k_2^y - k_2^z\| \leq L\,\|y - z + h(k_1^y - k_1^z)/2\| \leq L\,(1 + hL/2)\,\|y - z\|.$$

迭代得 $\|k_j^y - k_j^z\| \leq L_j(h)\,\|y - z\|$，其中 $L_j(h)$ 为依赖 $L, h$ 的多项式（$h \to 0$ 时 $L_j \to L$）。

故
$$\|\Phi(t, y, h) - \Phi(t, z, h)\| \leq \frac{L_1 + 2L_2 + 2L_3 + L_4}{6}\,\|y - z\| =: \Lambda(h)\,\|y - z\|.$$

对 $h \leq h_0$，$\Lambda(h)$ 一致有界于 $\Lambda$。$\square$

---

## 第(iii)部分的证明：全局收敛

### 第一步：误差递推

$$e_{n+1} = y(t_{n+1}) - y_{n+1}.$$

由真解：$y(t_{n+1}) = y(t_n) + h\,\Phi(t_n, y(t_n), h) + \tau_n(h)$。
由 RK4：$y_{n+1} = y_n + h\,\Phi(t_n, y_n, h)$。

相减：
$$e_{n+1} = e_n + h\,[\Phi(t_n, y(t_n), h) - \Phi(t_n, y_n, h)] + \tau_n(h).$$

### 第二步：用 (ii) 与 (i) 取模

$$\|e_{n+1}\| \leq \|e_n\| + h\,\Lambda\,\|e_n\| + |\tau_n(h)| \leq (1 + h\Lambda)\,\|e_n\| + C\,h^5.$$

### 第三步：应用离散 Gronwall

由 $e_0 = 0$、$A = \Lambda$、$B = C$、$p = 4$，引理给出
$$\|e_n\| \leq \frac{C\,h^4}{\Lambda}\,e^{\Lambda(T - t_0)} = K\,h^4.$$

故 $\max_n \|e_n\| = O(h^4)$，**全局 4 阶收敛**。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> RK4 收敛性的核心是 **Dahlquist 等价定理**的具体实现：
> $$\text{相容（局部）} + \text{零稳定（Lipschitz 增量）} \Longrightarrow \text{收敛（全局）}.$$
>
> 三步骤：
> 1. **局部截断误差**：用 Taylor 展开真解与 RK4 增量函数，验证 RK4 的系数恰好匹配到 $h^4$，给出 $|\tau_n| = O(h^5)$；
> 2. **增量函数 Lipschitz**：由 $f$ 的 Lipschitz 性逐级传递到 $k_2, k_3, k_4$，再到 $\Phi$；
> 3. **误差传播**：局部误差经过 $N \sim 1/h$ 步累积。直接估计给 $O(h^5) \cdot N = O(h^4)$，但需 Gronwall 防止指数爆炸。
>
> **直观图像**：每步丢失 $h^5$ 的精度，走 $1/h$ 步累积到 $h^4$；Gronwall 把"累积放大率"控制为指数有限。

> [!important] Butcher 阶条件的作用
> RK4 系数 $1, 2, 2, 1$ 不是任意——它们满足 8 条非线性方程（"Butcher 阶条件"），确保 $h^1, h^2, h^3, h^4$ 项全部匹配。这是 4 阶相容的代数本质。
>
> Butcher 1964 用**树论**（rooted trees）系统地枚举所有阶条件，奠定了高阶 RK 方法的统一理论。

> [!warning] $f$ 的光滑性不可降
> 第(i)步用到了 Taylor 展开至 5 阶——需 $f \in C^4$。若 $f$ 仅 Lipschitz（$C^{0,1}$），RK4 退化为 Euler 阶。光滑性与阶数严格对应。

> [!info] 应用：自适应步长
> 实际计算中使用 **嵌入式 RK 对**：RK4(5) 公式（Dormand-Prince DOPRI5），同时计算 4 阶与 5 阶解，二者之差即局部误差估计器，据此自适应调整 $h$。MATLAB `ode45`、SciPy `solve_ivp` 默认即此法。

> [!info] 与其他工具的衔接
> - **离散 Gronwall** ← [[Gronwall不等式]]（积分形式）的离散化；
> - **Lipschitz $f$** ← [[Picard-Lindelöf定理]] 中保证 ODE 解唯一存在的条件；
> - **不动点迭代** → 隐式 RK（如 Gauss-Legendre）每步需解非线性系统，用 [[不动点迭代收敛定理]] 或 [[Newton法的二阶收敛性]]；
> - **稳定性区域** → 把 RK 应用到 $y' = \lambda y$ 给出多项式 $R(z)$；$|R(z)| \leq 1$ 的 $z = \lambda h$ 区域即稳定性区。RK4 的稳定区有限——对 stiff 问题（$|\lambda|$ 大）需隐式方法。
