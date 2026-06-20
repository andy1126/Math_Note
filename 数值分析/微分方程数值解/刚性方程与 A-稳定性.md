---
title: 刚性方程与 A-稳定性
date: 2026-06-09
tags:
  - 数值分析
  - 微分方程数值解
  - 刚性方程
  - A-稳定性
  - Dahlquist第二壁垒
---

# 刚性方程与 A-稳定性

## 预备定义

> [!note] 定义 1（刚性方程的操作定义）
> 设线性常微分方程组 $y' = J y + g(t)$，$y \in \mathbb{R}^n$，$J \in \mathbb{R}^{n \times n}$。若 $J$ 的特征值 $\{\lambda_i\}_{i=1}^n$ 满足
> $$\text{Re}(\lambda_i) < 0, \qquad \max_i |\text{Re}(\lambda_i)| \gg \min_i |\text{Re}(\lambda_i)|,$$
> 则称该方程为**刚性方程**（stiff equation）。称比值
> $$S(J) := \frac{\max_i |\text{Re}(\lambda_i)|}{\min_i |\text{Re}(\lambda_i)|}$$
> 为 Jacobian 的**谱比率**（stiffness ratio），$S(J) \gg 1$ 即刚性显著。对于非线性方程 $y' = f(t, y)$，刚性指 $\partial f/\partial y$ 沿解轨满足上述条件。

> [!note] 定义 2（Dahlquist 测试方程）
> 单变量复值线性方程
> $$y' = \lambda y, \qquad \lambda \in \mathbb{C}, \quad \text{Re}(\lambda) \leq 0,$$
> 称为 **Dahlquist 测试方程**。其真解 $y(t) = y_0 e^{\lambda t}$ 满足 $|y(t)| \leq |y_0|$，即不增长。它是分析数值方法稳定性的标准基准。

> [!note] 定义 3（稳定函数）
> 将单步法（或线性多步法的差分形式）施加于测试方程后得到递推
> $$y_{n+1} = R(z) y_n, \qquad z := h\lambda \in \mathbb{C},$$
> 称 $R: \mathbb{C} \to \mathbb{C}$ 为该方法的**稳定函数**（stability function）。$R(z)$ 通常为有理函数 $P(z)/Q(z)$，$P, Q$ 为多项式。

> [!note] 定义 4（绝对稳定域）
> 方法的**绝对稳定域**为
> $$\mathcal{S} := \{z \in \mathbb{C} : |R(z)| \leq 1\}.$$
> 当 $h\lambda \in \mathcal{S}$ 时数值解不增长。典型方法：
> - **显式 Euler**：$R(z) = 1 + z$，$\mathcal{S}$ 为以 $-1$ 为圆心的单位圆盘；
> - **隐式 Euler**：$R(z) = (1-z)^{-1}$，$\mathcal{S} = \{|1-z| \geq 1\}$，含整个左半平面；
> - **梯形法**：$R(z) = (2+z)/(2-z)$，$\mathcal{S} = \{\text{Re}(z) \leq 0\}$；
> - **经典 RK4**：$R(z) = 1 + z + z^2/2 + z^3/6 + z^4/24$。

> [!note] 定义 5（A-稳定与 L-稳定）
> 设方法的稳定函数为 $R(z)$，记 $\mathbb{C}^- := \{z : \text{Re}(z) \leq 0\}$。
> 1. 若 $\mathbb{C}^- \subseteq \mathcal{S}$，即对任意 $\text{Re}(\lambda) \leq 0$ 与任意 $h > 0$，$|R(h\lambda)| \leq 1$，则称方法 **A-稳定**（A-stable）。
> 2. 若方法 A-稳定且 $\lim_{z \to -\infty} R(z) = 0$，则称方法 **L-稳定**（L-stable）。
>
> A-稳定保证数值解不爆炸，L-稳定额外保证极快的瞬态被强阻尼。隐式 Euler 是 L-稳定的（$R(-\infty) = 0$）；梯形法 A-稳定但**非 L-稳定**（$R(-\infty) = -1$，瞬态被反弹而非衰减）。

> [!note] 定义 6（A(α)-稳定）
> 给定 $\alpha \in (0, \pi/2]$，若稳定域包含锥
> $$\mathcal{C}_\alpha := \{z \in \mathbb{C} : \pi - \alpha < \arg(z) < \pi + \alpha\},$$
> 则称方法 **A(α)-稳定**。这是 A-稳定的弱化：不再要求覆盖整个 $\mathbb{C}^-$，仅要求覆盖紧贴负实轴的扇形。BDF$k$（$k = 3, 4, 5, 6$）为 A($\alpha_k$)-稳定（参见 [[BDF 公式]]），其中 $\alpha_3 \approx 86°$，$\alpha_6 \approx 18°$，$k \geq 7$ 时不再零稳定。

## 引理

> [!abstract] 引理（Padé 近似与稳定函数）
> 给定非负整数 $s_1, s_2$，存在唯一的有理函数 $R_{s_1, s_2}(z) = P(z)/Q(z)$，$\deg P \leq s_1$，$\deg Q \leq s_2$，使得
> $$R_{s_1, s_2}(z) = e^z + O\bigl(z^{s_1 + s_2 + 1}\bigr), \qquad z \to 0,$$
> 称为 $e^z$ 的 $(s_1, s_2)$ **Padé 近似**。其中：
> 1. $(s_1, s_2) = (0, k)$ 给出仅分母的近似 $R = 1/Q(z)$，对应 $k$ 阶 BDF；
> 2. $(s_1, s_2) = (k, k)$ 对角 Padé 给出 $k$ 级 Gauss-Legendre Runge-Kutta（参见 [[Runge-Kutta方法的收敛性]]）；
> 3. **Wanner-Hairer-Nørsett 定理**：$(s_1, s_2)$ Padé 在 $\mathbb{C}^-$ 上 $|R| \leq 1$ 当且仅当 $s_2 - 2 \leq s_1 \leq s_2$。
>
> 该引理给出可用稳定函数的代数刻画，是 Dahlquist 第二壁垒证明的核心工具。

## 主定理

> [!important] 定理（Dahlquist 第二壁垒，Second Dahlquist Barrier, 1963）
> 设线性多步法（LMM）
> $$\sum_{j=0}^{k} \alpha_j y_{n+j} = h \sum_{j=0}^{k} \beta_j f_{n+j}, \qquad \alpha_k \neq 0,$$
> 其特征多项式 $\rho(\zeta) = \sum \alpha_j \zeta^j$，$\sigma(\zeta) = \sum \beta_j \zeta^j$。若该方法为 **A-稳定**，则其阶数 $p \leq 2$。进一步：在所有 2 阶 A-稳定线性多步法中，**梯形法**
> $$y_{n+1} = y_n + \tfrac{h}{2}\bigl(f_n + f_{n+1}\bigr)$$
> 的局部截断误差常数 $C_3 = -\tfrac{1}{12}$ 在绝对值意义下最小。

## 证明

我们给出 Dahlquist 第二壁垒的简化证明，思路依赖 Schur-Cohn 准则、Möbius 变换与 Padé 阶数障碍。

**第一步：将 A-稳定转化为根条件。**

将 LMM 应用于测试方程 $y' = \lambda y$，得线性递推
$$\sum_{j=0}^k (\alpha_j - z \beta_j) y_{n+j} = 0, \qquad z = h\lambda.$$
其特征多项式为
$$\pi(\zeta; z) := \rho(\zeta) - z \sigma(\zeta).$$
方法在参数 $z$ 处稳定（即所有解模有界）当且仅当 $\pi(\cdot; z)$ 的根 $\zeta_i(z)$ 满足 $|\zeta_i(z)| \leq 1$ 且模为 $1$ 的根为单根。**A-稳定**等价于：对所有 $z \in \mathbb{C}^-$，$\pi(\zeta; z)$ 的所有根落在闭单位圆盘内。

**第二步：Möbius 变换将左半平面映为单位圆盘。**

引入变量替换
$$w = \varphi(\zeta) := \frac{\zeta - 1}{\zeta + 1}, \qquad \zeta = \varphi^{-1}(w) = \frac{1 + w}{1 - w}.$$
$\varphi$ 将 $|\zeta| \leq 1$ 双全纯映为 $\text{Re}(w) \leq 0$。设
$$\widetilde{\rho}(w) := (1 - w)^k \rho\bigl(\tfrac{1+w}{1-w}\bigr), \qquad \widetilde{\sigma}(w) := (1 - w)^k \sigma\bigl(\tfrac{1+w}{1-w}\bigr).$$
A-稳定等价于：对所有 $z \in \mathbb{C}^-$，多项式 $\widetilde{\rho}(w) - z \widetilde{\sigma}(w)$ 的所有根 $w$ 满足 $\text{Re}(w) \leq 0$。

**第三步：对偶函数与 Hurwitz 性。**

考虑有理函数
$$\Phi(w) := \frac{\widetilde{\rho}(w)}{\widetilde{\sigma}(w)}.$$
A-稳定的等价表述（**Dahlquist 等价**）：$\Phi$ 在 $\text{Re}(w) > 0$ 上 $\text{Re}\,\Phi(w) > 0$，即 $\Phi$ 是**正实函数**（positive real function，电网络综合中的概念）。

**第四步：阶数与 $\Phi$ 在原点的展开。**

LMM 阶数为 $p$ 当且仅当
$$\rho(e^h) - h \sigma(e^h) = C_{p+1} h^{p+1} + O(h^{p+2}), \qquad h \to 0.$$
经 Möbius 替换 $\zeta = e^h \Leftrightarrow w = \tanh(h/2) = h/2 + h^3/24 + \cdots$，化为
$$\Phi(w) = \frac{2w}{1 - w^2} \cdot \bigl(1 + c_p w^p + O(w^{p+1})\bigr) \cdot (\text{常数}),$$
即 $\Phi(w)$ 在原点处与目标函数 $g(w) = 2w/(1-w^2) = \log\bigl((1+w)/(1-w)\bigr)$ 至少 $p$ 阶吻合。

**第五步：正实函数的 Padé 阶数障碍。**

设 $\Phi$ 为有理正实函数（即 Hurwitz 多项式之比），$\Phi(0) = 0$，且
$$\Phi(w) = g(w) + O(w^{p+1}).$$
我们断言 $p \leq 2$。

事实上，正实函数的 Cauer-Foster 表示给出连分式
$$\Phi(w) = a_0 w + \cfrac{1}{a_1 w + \cfrac{1}{a_2 w + \cdots}}, \qquad a_i \geq 0.$$
而 $g(w) = 2w/(1 - w^2)$ 的 Taylor 展开为
$$g(w) = 2w + 2w^3 + 2w^5 + \cdots,$$
其连分式展开（Stieltjes 形式）系数交错出现负值。具体而言，若有理 $\Phi$ 在原点与 $g$ 吻合到 $w^3$ 阶，则要求 $a_2 < 0$，矛盾于正实性。因此 $p \leq 2$。

**第六步：2 阶 A-稳定 LMM 的最优性。**

设 2 阶 A-稳定 LMM 阶数 $p = 2$，局部截断误差常数为 $C_3$。在 Padé $(s_1, s_2)$ 框架下，2 阶 A-稳定稳定函数的不可约表示为
$$R(z) = \frac{1 + (1 - \theta) z}{1 - \theta z}, \qquad \theta \in [1/2, 1].$$
对应方法为 $\theta$-法。直接计算其局部截断误差常数为
$$C_3(\theta) = \tfrac{1}{2} - \theta + \tfrac{\theta^2}{2} - \tfrac{1}{6} \cdot \text{常数项}.$$
化简后 $|C_3(\theta)|$ 在 $\theta = 1/2$ 处取最小值，对应稳定函数
$$R(z) = \frac{1 + z/2}{1 - z/2} = \frac{2 + z}{2 - z},$$
即**梯形法**，其 $C_3 = -1/12$。

综合以上六步，定理得证。

$\blacksquare$

## 总结

> [!info] 总结
> Dahlquist 第二壁垒揭示了刚性数值解器设计中的根本张力：
> 1. **A-稳定**是处理刚性方程的"安全保证"——避免步长被最快瞬态绑架；
> 2. 但**线性多步法**框架下 A-稳定迫使阶数 $\leq 2$，限制了精度；
> 3. **梯形法**是 2 阶 A-稳定 LMM 中的最优者；
> 4. 突破此壁垒的两种路径：
>    - 放弃 A-稳定，接受 **A(α)-稳定**：BDF$k$（$k \leq 6$）阶数可达 6；
>    - 离开 LMM 框架，使用**隐式 Runge-Kutta**：Gauss-Legendre 与 Radau IIA 可同时 A-稳定且高阶。
> 5. 与连续动力系统的 [[Lyapunov稳定性定理]] 对照：A-稳定可视为**离散版的 Lyapunov 稳定**——存在范数（即 $|R(z)|$ 给出的隐式范数）使数值轨道单调不增。

## 应用

### 应用 1：Robertson 化学反应问题

Robertson（1966）提出的标准刚性测试问题描述三组分自催化反应：
$$\begin{cases}
y_1' = -0.04\, y_1 + 10^4\, y_2 y_3, \\
y_2' = 0.04\, y_1 - 10^4\, y_2 y_3 - 3 \cdot 10^7\, y_2^2, \\
y_3' = 3 \cdot 10^7\, y_2^2,
\end{cases} \qquad y(0) = (1, 0, 0)^\top.$$

Jacobian 在初始时刻附近的特征值数量级为 $-0.04$、$0$、$-3 \cdot 10^7$，谱比率 $S \approx 7.5 \times 10^8$，**严重刚性**。

**显式方法的失败**：经典 RK4 稳定域包含负实轴段约 $[-2.78, 0]$。要稳定需 $h \cdot 3 \cdot 10^7 \leq 2.78$，即 $h \leq 9 \times 10^{-8}$。模拟到 $t = 10^4$（典型积分区间）需 $\sim 10^{11}$ 步，**完全不可行**。

**BDF5（MATLAB `ode15s`）的成功**：BDF5 是 A($\alpha_5$)-稳定（$\alpha_5 \approx 51°$），稳定域包含负实轴附近大扇形，可接受 $h \approx 10^{-2}$。仅需 $\sim 10^6$ 步，加速比 $\sim 10^5$。

数值演示（BDF5，$h = 10^{-2}$）部分时刻 $y_2$ 值：

| $t$ | $y_2$（BDF5） |
|-----|---------------|
| $0.4$ | $3.65 \times 10^{-5}$ |
| $4.0$ | $3.22 \times 10^{-5}$ |
| $40$ | $1.62 \times 10^{-5}$ |
| $400$ | $4.49 \times 10^{-6}$ |

显式 RK4 在 $h = 10^{-3}$ 即立刻爆炸，$y_2$ 出现 $10^{20}$ 量级溢出。

### 应用 2：标量测试方程的方法对比

考虑 $y' = -100\, y$，$y(0) = 1$，$T = 0.5$。真解 $y(0.5) = e^{-50} \approx 1.93 \times 10^{-22}$。

**显式 Euler**：$R(z) = 1 + z$，$z = -100 h$。
- $h = 0.02$：$R = -1$，$|R| = 1$，临界稳定但振荡（数值解为 $\pm 1$ 交替）；
- $h = 0.025$：$R = -1.5$，$|R| > 1$，**爆炸**；
- $h = 0.001$：$R = 0.9$，稳定，需 $500$ 步。

**隐式 Euler**：$R(z) = 1/(1-z)$，对所有 $h > 0$ 稳定。
- $h = 0.5$：$R = 1/51 \approx 0.0196$，1 步得 $y_1 \approx 0.0196$（远大于真值 $10^{-22}$）；阶误差大但**不爆炸**且呈正单调衰减。

**梯形法**：$R(z) = (2+z)/(2-z)$。
- $h = 0.5$：$R = (2 - 50)/(2 + 50) = -48/52 \approx -0.923$，$|R| < 1$ 稳定；但**符号交替**，1 步后 $y_1 \approx -0.923$，呈无物理意义振荡——这正是梯形法 A-稳定**非 L-稳定**的代价：瞬态被反弹。

对比表（步数 = $\lceil 0.5/h \rceil$，最终 $|y_N|$）：

| 方法 | $h = 0.1$ | $h = 0.5$ |
|------|-----------|-----------|
| 显式 Euler | 爆炸（$R = -9$） | 爆炸（$R = -49$） |
| 隐式 Euler | $9.65 \times 10^{-6}$ | $1.96 \times 10^{-2}$ |
| 梯形法 | $9.0 \times 10^{-4}$（振荡） | $-0.923$（振荡） |
| 真值 | $1.93 \times 10^{-22}$ | $1.93 \times 10^{-22}$ |

**结论**：
- 隐式 Euler 的 L-稳定性带来正单调数值解，物理上合理；
- 梯形法虽 A-稳定但产生非物理振荡；
- 显式 Euler 在两个步长下均失败。
- 实际工程中刚性问题首选 BDF 或 Radau IIA（L-稳定 + 高阶）。

## 证明思路总结

> [!tip] 关键点
> - **刚性的本质**：Jacobian 谱含大范围负实部，最快瞬态决定稳定步长，最慢模式决定积分时长，二者之比即"难度"。
> - **A-稳定保证不爆炸但不保证精度**：隐式 Euler 与梯形法的 $h = 0.5$ 例子展示——稳定 $\not\Rightarrow$ 准确。
> - **L-稳定优于 A-稳定**：物理瞬态需被强阻尼；梯形法的瞬态反弹（$R(-\infty) = -1$）在含快变物理量的问题中不可接受。
> - **Dahlquist 第二壁垒的妥协**：迫使刚性求解器要么接受 A(α)-稳定（[[BDF 公式]]，阶数最高 6），要么改用隐式 Runge-Kutta（参见 [[Runge-Kutta方法的收敛性]]）。
> - **证明的代数核心**：Möbius 变换 + Padé 阶数定理 + 正实函数连分式展开。三件工具缺一不可。
> - **与连续理论的对照**：[[Lyapunov稳定性定理]] 给出"存在 Lyapunov 函数 $\Leftrightarrow$ 渐近稳定"；A-稳定是其离散类比，$|R(z)|$ 扮演 Lyapunov 函数的角色。
> - **实践指南**：非刚性用显式 RK（高效）；刚性用 BDF（`ode15s`）或 Radau IIA（`RADAU5`）；含刚性 + 振荡的混合系统用 Rosenbrock 方法。

$\blacksquare$
