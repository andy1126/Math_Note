---
title: 线性多步法与 Dahlquist 等价定理
date: 2026-06-09
tags:
  - 数值分析
  - 微分方程数值解
  - 线性多步法
  - Dahlquist等价定理
  - 零稳定性
  - 收敛性
---

# 线性多步法与 Dahlquist 等价定理

线性多步法（Linear Multistep Method, LMM）是数值求解常微分方程初值问题
$$y'(t) = f(t, y(t)), \quad y(t_0) = y_0$$
的一大类方法。与 [[Runge-Kutta方法的收敛性|Runge-Kutta 方法]]这类**单步法**不同，多步法在每一步利用**多个**先前时刻的信息以提高精度，但代价是引入了更复杂的稳定性结构。本笔记的核心是 **Dahlquist 等价定理**：一个 LMM 收敛当且仅当它**相容**且**零稳定**。

历史背景上，Dahlquist 在 1956 年的博士论文中首次系统建立了线性多步法的相容性、稳定性与收敛性的等价关系。这一结果不仅刻画了 LMM 的本质，也启发了后续偏微分方程有限差分理论中的 Lax 等价定理。理解 Dahlquist 等价定理的关键在于把握三组概念之间的精确关系：
- **相容性**：方法形式上"逼近"微分方程的程度（一种局部性质）；
- **零稳定性**：方法的齐次结构对初始扰动的鲁棒性（一种代数性质）；
- **收敛性**：当步长 $h \to 0$ 时数值解逐点逼近真解（一种全局分析性质）。

定理告诉我们：**局部良好（相容）+ 结构稳定（零稳定）= 全局良好（收敛）**。这种"局部 + 稳定 = 全局"的范式贯穿数值分析始终。

## 预备定义

> [!note] 定义 1：$k$ 步线性多步法
> 设步长 $h > 0$，节点 $t_n = t_0 + nh$。一个 $k$ 步线性多步法的一般形式为
> $$\sum_{j=0}^{k} \alpha_j y_{n+j} = h \sum_{j=0}^{k} \beta_j f(t_{n+j}, y_{n+j}),$$
> 其中 $\alpha_j, \beta_j \in \mathbb{R}$ 为常系数，且约定 $\alpha_k = 1$，$|\alpha_0| + |\beta_0| > 0$。
> - 若 $\beta_k = 0$，方法为**显式**（explicit）；
> - 若 $\beta_k \neq 0$，方法为**隐式**（implicit），每步需求解关于 $y_{n+k}$ 的非线性方程。

> [!note] 定义 2：第一与第二特征多项式
> 与 LMM 相伴的两个多项式定义为
> $$\rho(z) = \sum_{j=0}^{k} \alpha_j z^j, \qquad \sigma(z) = \sum_{j=0}^{k} \beta_j z^j.$$
> $\rho$ 控制方法的**齐次差分结构**（与 $f \equiv 0$ 时的解相关），$\sigma$ 控制**右端项的加权方式**。Dahlquist 理论的基本观察是：稳定性由 $\rho$ 决定，相容性由 $\rho, \sigma$ 联合决定。

> [!note] 定义 3：局部截断误差与相容性
> 将真解 $y(t)$ 代入差分公式，定义局部截断误差
> $$\tau_n(h) = \frac{1}{h}\left[\sum_{j=0}^{k} \alpha_j y(t_{n+j}) - h \sum_{j=0}^{k} \beta_j y'(t_{n+j})\right].$$
> 称方法**$p$ 阶相容**，若对充分光滑的 $y$ 有 $\tau_n(h) = O(h^p)$。等价的代数条件为
> $$\sum_{j=0}^{k} \alpha_j j^q = q \sum_{j=0}^{k} \beta_j j^{q-1}, \quad q = 0, 1, \ldots, p,$$
> 其中 $q = 0$ 给出 $\rho(1) = 0$，$q = 1$ 给出 $\rho'(1) = \sigma(1)$。**1 阶相容**仅指前两条同时成立。

> [!note] 定义 4：零稳定（Dahlquist 稳定）
> 称 LMM **零稳定**（zero-stable），若 $\rho(z)$ 满足**根条件**（root condition）：
> 1. $\rho$ 的所有零点 $z_i$ 满足 $|z_i| \leq 1$；
> 2. 模为 $1$ 的零点必为单根。
>
> 直观地，这保证齐次差分方程 $\sum_j \alpha_j u_{n+j} = 0$ 的所有解都**有界**。

> [!note] 定义 5：收敛性
> 称 LMM **收敛**，若对任意 Lipschitz 右端 $f$、任意初值 $y_0$、任意启动值 $y_j(h) \to y_0$（$j = 0, 1, \ldots, k-1$，$h \to 0$），固定 $t^* > t_0$，当 $nh \to t^* - t_0$ 时
> $$y_n \longrightarrow y(t^*).$$
> 等价地，固定时间区间 $[t_0, t^*]$，
> $$\max_{0 \leq n \leq N(h)} \|y_n - y(t_n)\| \to 0, \quad h \to 0,$$
> 其中 $N(h) = \lfloor (t^* - t_0)/h \rfloor$。注意收敛性要求**对所有合法启动**成立——不能依赖某种特殊的初值生成。

> [!note] 定义 6：Lipschitz 条件与解的存在唯一性
> 在以下分析中始终假设 $f$ 关于 $y$ 满足 Lipschitz 条件：存在 $L > 0$ 使
> $$\|f(t, y_1) - f(t, y_2)\| \leq L \|y_1 - y_2\|, \quad \forall t \in [t_0, t^*], \forall y_1, y_2.$$
> 由 Picard-Lindelöf 定理，初值问题在 $[t_0, t^*]$ 上有唯一 $C^1$ 解 $y(t)$；若 $f$ 进一步 $C^p$ 则 $y \in C^{p+1}$，这是 $p$ 阶相容性所需的光滑度。

## 引理

> [!abstract] 引理 1：齐次差分方程的通解结构
> 设 $\rho(z) = \prod_{i=1}^{s} (z - z_i)^{m_i}$，则齐次差分方程 $\sum_j \alpha_j u_{n+j} = 0$ 的通解为
> $$u_n = \sum_{i=1}^{s} \sum_{l=0}^{m_i - 1} c_{i,l}\, n^l z_i^n.$$
> 因此通解有界 $\iff$ 满足根条件 $\iff$ 方法零稳定。

> [!abstract] 引理 2：Spijker / 离散稳定性引理
> 若 $\rho$ 满足根条件，则存在常数 $K > 0$，使得对差分方程
> $$\sum_{j=0}^{k} \alpha_j u_{n+j} = \varphi_n$$
> 的任意解，
> $$\max_{0 \leq m \leq N} |u_m| \leq K\left(\max_{0 \leq j < k} |u_j| + \sum_{n=0}^{N-k} |\varphi_n|\right).$$
> 此引理把"$\rho$ 根条件"翻译为定量的解的稳定性估计，是充分性证明的关键。

> [!abstract] 引理 3：离散 Gronwall 不等式
> 见 [[Gronwall不等式]]。设非负序列 $\{a_n\}$ 满足
> $$a_n \leq A + B h \sum_{m=0}^{n-1} a_m, \quad n = 0, 1, \ldots, N,$$
> 其中 $A, B \geq 0$，$h > 0$。则
> $$a_n \leq A \exp(B n h).$$
> 在固定时间区间 $[t_0, t^*]$ 上，$n h \leq t^* - t_0$，故指数因子有界，最终估计为 $a_n \leq A \exp(B(t^* - t_0))$。

> [!abstract] 引理 4：局部截断误差与 Taylor 展开
> 若方法 $p$ 阶相容且 $y \in C^{p+1}([t_0, t^*])$，则
> $$\tau_n(h) = C_{p+1}\, h^p\, y^{(p+1)}(t_n) + O(h^{p+1}),$$
> 其中 $C_{p+1}$ 称为**误差常数**（error constant），仅依赖于 $\rho, \sigma$ 的系数与 $p$。误差常数越小，相同阶的方法精度越高。AM 家族的 $|C_{p+1}|$ 通常显著小于同阶 AB，这是隐式方法的额外优势。

## 主定理

> [!important] 定理（Dahlquist 等价定理，1956）
> 对于 $k$ 步线性多步法，
> $$\boxed{\text{收敛} \;\iff\; \text{相容}\;(\text{至少 1 阶})\; \text{且}\; \text{零稳定}.}$$
> 进一步，若方法 $p$ 阶相容且零稳定，启动误差 $\max_{0 \leq j < k} \|y_j - y(t_j)\| = O(h^p)$，则全局误差
> $$\max_{0 \leq n \leq N}\|y_n - y(t_n)\| = O(h^p).$$
> 这一精度结果说明：**LMM 的全局阶 = 局部阶**，没有"一阶损失"现象（对比有些隐式 Runge-Kutta 方法在刚性问题上的阶降）。

定理的证明分**必要性**与**充分性**两部分。必要性通过精心选取的反例（特殊 $f$、扰动启动）逼出每一条件；充分性则把局部截断误差通过零稳定的"放大控制"与 Gronwall 不等式拼接为全局误差。下面分别给出。

## 证明

### 必要性：收敛 $\Rightarrow$ 相容 + 零稳定

**(a) 收敛 $\Rightarrow$ 0 阶相容（$\rho(1) = 0$）**：取 $f \equiv 0$，则真解恒为 $y(t) \equiv y_0$。取启动值 $y_j = y_0$，差分公式化为 $\sum_j \alpha_j y_{n+j} = 0$。设序列 $y_n \equiv c$（常数）满足此式，则 $c\sum_j \alpha_j = 0$。要求收敛意味着 $y_n \to y_0$，配合启动 $y_0 = y_0$ 得 $c = y_0$ 任意，故 $\sum_j \alpha_j = \rho(1) = 0$。

**(b) 收敛 $\Rightarrow$ 1 阶相容（$\rho'(1) = \sigma(1)$）**：考虑 $f \equiv 1$，$y(t) = t$。代入差分公式（启动 $y_j = t_j$）应当至少在 $h \to 0$ 极限下相容。直接计算
$$\sum_j \alpha_j (n+j)h - h \sum_j \beta_j = h\left[(n)\rho(1) + \rho'(1) - \sigma(1)\right] + (\text{高阶}).$$
由 (a) $\rho(1) = 0$，故余项为 $h[\rho'(1) - \sigma(1)]$。若 $\rho'(1) \neq \sigma(1)$，则数值解与 $y(t) = t$ 在 $O(1)$ 量级偏离，矛盾收敛性。

**(c) 收敛 $\Rightarrow$ 零稳定**：再取 $f \equiv 0$，$y \equiv 0$。考虑启动值 $y_j = h \cdot v_j$，$v_j$ 任取 $O(1)$。数值解满足齐次差分 $\sum_j \alpha_j y_{n+j} = 0$，由引理 1，
$$y_n = h \sum_{i, l} c_{i,l}\, n^l z_i^n.$$
若某 $|z_i| > 1$ 或某 $|z_i| = 1$ 处为重根，则 $y_n / h$ 关于 $n$ 无界。固定 $t^* = nh$，$h \to 0$ 时 $n \to \infty$，故 $|y_n|$ 不收敛于 $0$，与收敛矛盾。因此根条件成立。

### 充分性：相容 + 零稳定 $\Rightarrow$ 收敛

设方法 $p$ 阶相容且零稳定。设 $f$ 关于 $y$ 的 Lipschitz 常数为 $L$。令 $e_n = y_n - y(t_n)$。

**第一步：误差的差分方程**。把数值方程与真解方程相减：
$$\sum_j \alpha_j e_{n+j} = h \sum_j \beta_j [f(t_{n+j}, y_{n+j}) - f(t_{n+j}, y(t_{n+j}))] - h \tau_n.$$
由 Lipschitz 性，
$$\left|\sum_j \alpha_j e_{n+j}\right| \leq h L \sum_j |\beta_j|\, \|e_{n+j}\| + h |\tau_n|.$$
记 $\varphi_n := h \sum_j \beta_j [f(t_{n+j}, y_{n+j}) - f(t_{n+j}, y(t_{n+j}))] - h\tau_n$。

**第二步：套用 Spijker 引理**。由零稳定与引理 2，
$$\max_{0 \leq m \leq N} \|e_m\| \leq K\left(\max_{0 \leq j < k} \|e_j\| + \sum_{n=0}^{N-k} \|\varphi_n\|\right).$$
将 $\|\varphi_n\| \leq h L \sum_j |\beta_j| \max_{0 \leq i \leq k} \|e_{n+i}\| + h |\tau_n|$ 代入，记 $E_N = \max_{m \leq N}\|e_m\|$、$B = L K \sum_j |\beta_j|$，
$$E_N \leq K \cdot (\text{启动误差}) + K \cdot N h \cdot \max_n |\tau_n| + B h \sum_{n=0}^{N} E_n.$$

**第三步：Gronwall**。由 $p$ 阶相容 $|\tau_n| = O(h^p)$，启动误差 $O(h^p)$，故
$$E_N \leq C_1 h^p + B h \sum_{n=0}^{N-1} E_n.$$
由离散 Gronwall（引理 3）
$$E_N \leq C_1 h^p \exp(B \cdot N h) \leq C_1 h^p \exp(B(t^* - t_0)) = O(h^p).$$
$N h$ 在固定时间区间上有界，故指数因子是常数。证毕。

**关于充分性证明的几点说明**：
1. **常数 $K$ 的来源**：引理 2 中的常数 $K$ 仅依赖于 $\rho$ 的根结构与多步法的步数 $k$，与时间区间长度无关。这是零稳定性的核心定量化体现。
2. **隐式情形的处理**：若 $\beta_k \neq 0$（隐式），上述 $\|\varphi_n\|$ 的估计会在右侧出现 $\|e_{n+k}\|$，须将其移到左侧并要求 $h L |\beta_k| < 1$（即步长足够小）以保持估计可逆。这一限制对收敛性分析只是技术细节，并不削弱定理。
3. **启动误差**：若仅有 $O(h^{p-1})$ 的启动误差，则全局阶降至 $O(h^{p-1})$。在工程实践中通常使用更高阶的 [[Runge-Kutta方法的收敛性|Runge-Kutta 方法]]启动 LMM，保证启动阶不构成精度瓶颈。

## 总结

> [!info] 核心思想
> Dahlquist 等价定理把"收敛"这个**分析**概念精确等价于两个**代数/可计算**条件：
> 1. **相容性** —— 通过 $\rho, \sigma$ 系数的线性方程组刻画，决定**精度阶**；
> 2. **零稳定性** —— 通过 $\rho$ 的**根条件**刻画，决定**误差不放大**。
>
> 这一等价定理的精神延续到偏微分方程的有限差分理论中，即著名的 **Lax 等价定理**：相容性 + 稳定性 $\Leftrightarrow$ 收敛性。

> [!warning] 常见陷阱
> - 相容 + 高阶**并不**自动蕴含零稳定。Dahlquist 第一壁垒：$k$ 步零稳定 LMM 的最高阶为 $p \leq k+1$（$k$ 偶）或 $p \leq k+2$（$k$ 奇，且仅当方法是某些特殊形式）。
> - 多步法**启动**不当（$y_1, \ldots, y_{k-1}$ 误差 $> O(h^p)$）会破坏整体收敛阶。
> - 即便方法零稳定，对**刚性问题**仍可能要求很小的步长，需要进一步的 A-稳定性分析（见 [[BDF 公式]]、[[刚性方程与 A-稳定性]]）。

## 应用

### 应用 1：Adams-Bashforth 与 Adams-Moulton 家族

**Adams-Bashforth (AB)** 取 $\rho(z) = z^k - z^{k-1}$（即 $\alpha_k = 1, \alpha_{k-1} = -1$，其余 $\alpha = 0$），$\sigma$ 由 $p = k$ 阶相容确定，$\beta_k = 0$（显式）。
- **AB1**（即 [[Euler 法|显式 Euler]]）：$y_{n+1} = y_n + h f_n$，1 阶；
- **AB2**：$y_{n+2} = y_{n+1} + \dfrac{h}{2}(3 f_{n+1} - f_n)$，2 阶；
- **AB3**：$y_{n+3} = y_{n+2} + \dfrac{h}{12}(23 f_{n+2} - 16 f_{n+1} + 5 f_n)$，3 阶。

**Adams-Moulton (AM)** 同样的 $\rho$，但 $\beta_k \neq 0$（隐式），可达 $p = k+1$ 阶。
- **AM1**（隐式 Euler）：$y_{n+1} = y_n + h f_{n+1}$，1 阶；
- **AM2**（梯形法）：$y_{n+1} = y_n + \dfrac{h}{2}(f_{n+1} + f_n)$，2 阶；
- **AM3**：$y_{n+2} = y_{n+1} + \dfrac{h}{12}(5 f_{n+2} + 8 f_{n+1} - f_n)$，3 阶。

由于 $\rho(z) = z^k - z^{k-1} = z^{k-1}(z-1)$，根为 $z = 1$（单根）和 $z = 0$（$k-1$ 重）—— Adams 家族**自动零稳定**，所以收敛性完全由相容性决定。

### 应用 2：AB2 数值实验 $y' = -y$，$y(0) = 1$

真解 $y(t) = e^{-t}$。AB2 是 2 步法，需要 $y_0 = 1$ 与 $y_1$。用经典 4 阶 Runge-Kutta 自启动得 $y_1 \approx e^{-h}$（误差 $O(h^5)$，远好于 AB2 自身的 $O(h^2)$）。

| $h$    | $\|y_N - y(t_N)\|_\infty$ ($t_N = 1$) | 误差比 |
|--------|-----------------|--------|
| $0.10$ | $\sim 4 \times 10^{-3}$ | —      |
| $0.05$ | $\sim 1 \times 10^{-3}$ | $\approx 4$ |
| $0.025$| $\sim 2.5 \times 10^{-4}$ | $\approx 4$ |

误差比约为 $4$，验证 $O(h^2)$ 收敛——这正是 Dahlquist 等价定理充分性的实验体现。

### 应用 3：零不稳定方法的反例

考虑 2 步法
$$y_{n+2} - 3 y_{n+1} + 2 y_n = h \left[\beta_2 f_{n+2} + \beta_1 f_{n+1} + \beta_0 f_n\right].$$
这里 $\rho(z) = z^2 - 3z + 2 = (z-1)(z-2)$，根 $z = 2 > 1$，**违反根条件**。

可以选取 $\beta_j$ 使其满足任意高阶相容（例如 $\beta_2 = 0, \beta_1 = -2, \beta_0 = -1$ 满足 $\rho'(1) = -1 = \sigma(1)$，达到 1 阶相容；继续调可达更高阶）。但即使如此，数值实验显示：在 $f \equiv 0$ 下，扰动启动 $y_0 = 0, y_1 = \varepsilon$ 给出 $y_n = \varepsilon (2^n - 1)$，误差**指数爆炸**。这正是 Dahlquist 定理必要性 (c) 的现实意义：**相容不足以保证收敛**。

### 应用 4：预测-校正格式（PECE）

实际计算中常将 AB$k$（显式预测）与 AM$k$（隐式校正）配对：
$$\text{P:}\; y_{n+k}^{[0]} = \text{AB}k(y_n, \ldots, y_{n+k-1}); \quad \text{E:}\; \tilde f_{n+k} = f(t_{n+k}, y_{n+k}^{[0]});$$
$$\text{C:}\; y_{n+k} = \text{AM}k(\tilde f_{n+k}, f_{n+k-1}, \ldots); \quad \text{E:}\; f_{n+k} = f(t_{n+k}, y_{n+k}).$$
这样既避免了纯 AM 的非线性方程求解（除非 $f$ 强非线性），又获得 AM 的稳定性优势。整体阶取 $\min(p_{\text{AB}}, p_{\text{AM}})$，对 AB$k$/AM$k$ 配对为 $k$ 阶。

PECE 的阶分析需要小心：单次校正后，整体阶为 $\min(p_{\text{P}} + 1, p_{\text{C}})$（因为校正吸收了一阶预测误差）；多次校正趋向纯隐式 AM 的精度。误差常数也比纯 AM 略大，但因实现简单仍是经典策略。

### 应用 5：Dahlquist 第一壁垒的现实意义

Dahlquist 第一壁垒（first barrier）指出：$k$ 步**零稳定**线性多步法的最高相容阶 $p$ 满足
$$p \leq \begin{cases} k+2, & k\text{ 为偶数，} \\ k+1, & k\text{ 为奇数，} \\ k, & \text{显式情形。}\end{cases}$$
这意味着，单纯通过增加步数 $k$ 并不能任意提高精度——**精度与稳定性互相制约**。这正是 Dahlquist 等价定理"**收敛 = 相容 + 零稳定**"的反面表达：要保持收敛性的精度，方法的复杂度受根条件硬约束。

第一壁垒在工程上的含义：当用户希望同时获得高阶（如 $p = 8$）与零稳定性时，必须接受相当多的步数 $k$ 与复杂的根分布；而对于刚性问题，零稳定甚至并不足够，还需进一步的 A-稳定（这又导出 Dahlquist **第二壁垒**：A-稳定的 LMM 阶 $\leq 2$，详见 [[BDF 公式]]）。

## 证明思路总结

> [!tip] 一图说清 Dahlquist 等价定理
> - **相容** $\iff$ 局部截断误差 $\tau = O(h^{p+1})$，决定**精度阶**；
> - **零稳定** $\iff \rho$ 满足根条件 $\iff$ 齐次差分解有界，决定**误差不放大**；
> - 二者通过 **Spijker 引理 + 离散 Gronwall** 在固定时间区间上"积分"成全局误差 $O(h^p)$。
>
> 必要性反过来：用特殊的 $f$（恒零、恒一）与扰动启动检验，违反任一条件都能构造发散数值解。
>
> 该定理是线性多步法理论的基石，把后续所有关于 LMM 的研究（Dahlquist 第一/第二壁垒、$A$-稳定性、$A(\alpha)$-稳定、刚性问题专用方法等）都建立在"相容 + 零稳定"这一最低要求之上。具体到 [[BDF 公式]]，正是放弃高阶 $A$-稳定（第二壁垒禁止）改求 $A(\alpha)$-稳定的代表案例。

$\blacksquare$
