---
title: Baire 范畴定理及其应用
date: 2026-05-23
tags:
  - 泛函分析
  - 实分析
  - 度量空间
  - Baire范畴定理
  - 完备度量空间
---

# Baire 范畴定理及其应用

## 预备定义

> [!note] 完备度量空间
> 称度量空间 $(X, d)$ 为**完备的**（complete），若 $X$ 中每个 Cauchy 序列都收敛于 $X$ 中的点。

> [!note] 闭包与内部
> 设 $(X, d)$ 为度量空间，$A \subseteq X$。
> - $A$ 的**闭包** $\overline{A}$ 为含 $A$ 的最小闭集，等价于 $A \cup \{$ $A$ 的所有极限点 $\}$。
> - $A$ 的**内部** $\operatorname{int}(A)$ 为含于 $A$ 的最大开集，等价于 $\{x \in A : \exists\, r > 0,\ B(x, r) \subseteq A\}$。

> [!note] 稠密集
> 称 $A \subseteq X$ 在 $X$ 中**稠密**（dense），若 $\overline{A} = X$。等价地，$A$ 与 $X$ 中每个非空开集相交。

> [!note] 无处稠密集
> 称 $A \subseteq X$ 为**无处稠密的**（nowhere dense），若 $\operatorname{int}(\overline{A}) = \varnothing$。等价地，$X \setminus \overline{A}$ 在 $X$ 中稠密。
>
> 直观含义：$A$ 的闭包"看不到任何开球"，处处"漏洞百出"。

> [!note] 第一范畴集与第二范畴集
> - 称 $A \subseteq X$ 为**第一范畴集**（meagre / first category），若 $A$ 可表示为可数个无处稠密集的并。
> - 不是第一范畴集的集合称为**第二范畴集**（non-meagre / second category）。

> [!abstract] 引理：闭球的嵌套构造
> 设 $(X, d)$ 为完备度量空间，$\{\overline{B(x_n, r_n)}\}_{n=1}^{\infty}$ 为递降的闭球序列，即 $\overline{B(x_{n+1}, r_{n+1})} \subseteq \overline{B(x_n, r_n)}$，且 $r_n \to 0$。则
> $$\bigcap_{n=1}^{\infty} \overline{B(x_n, r_n)} \neq \varnothing.$$

**证明**：由嵌套关系，对 $m, n \geq N$，有 $x_m, x_n \in \overline{B(x_N, r_N)}$，故 $d(x_m, x_n) \leq 2 r_N \to 0$，即 $\{x_n\}$ 为 Cauchy 序列。由完备性，存在 $x \in X$ 使 $x_n \to x$。对任意固定 $N$，当 $n \geq N$ 时 $x_n \in \overline{B(x_N, r_N)}$，由闭集对极限封闭，$x \in \overline{B(x_N, r_N)}$。故 $x \in \bigcap_n \overline{B(x_n, r_n)}$。$\square$

---

## 定理

**(Baire 范畴定理)** 设 $(X, d)$ 为完备度量空间。则下列等价命题成立：

**(i)** 可数个开稠密集的交在 $X$ 中稠密。即若 $\{U_n\}_{n=1}^\infty$ 为开稠密集列，则 $\bigcap_{n=1}^\infty U_n$ 在 $X$ 中稠密。

**(ii)** $X$ 不能表示为可数个无处稠密集的并，即 $X$ 是第二范畴集。

**(iii)** 若 $X = \bigcup_{n=1}^\infty F_n$，其中每个 $F_n$ 为闭集，则至少存在某个 $F_N$ 满足 $\operatorname{int}(F_N) \neq \varnothing$。

---

## 证明

主要证明 **(i)**；**(ii)** 和 **(iii)** 由 **(i)** 通过取补集容易导出。

### 主要部分：(i) 的证明

**目标**：设 $\{U_n\}_{n=1}^\infty$ 为 $X$ 中的开稠密子集族。需证 $\bigcap_n U_n$ 在 $X$ 中稠密，即对任意非空开集 $V \subseteq X$，有 $V \cap \bigcap_n U_n \neq \varnothing$。

#### 第一步：选取第一个闭球

由于 $U_1$ 在 $X$ 中稠密，$V \cap U_1$ 非空。又 $V$ 和 $U_1$ 均开，$V \cap U_1$ 为非空开集。取 $x_1 \in V \cap U_1$，并取 $r_1 \in (0, 1)$ 使得

$$\overline{B(x_1, r_1)} \subseteq V \cap U_1. \quad \cdots (1)$$

> [!info] 为何能选到这样的闭球
> $V \cap U_1$ 开，故对 $x_1 \in V \cap U_1$，存在 $\rho > 0$ 使 $B(x_1, \rho) \subseteq V \cap U_1$。取 $r_1 = \min\{\rho/2,\ 1/2\}$，则 $\overline{B(x_1, r_1)} \subseteq B(x_1, \rho) \subseteq V \cap U_1$。

#### 第二步：归纳构造闭球嵌套序列

**归纳假设**：已构造 $x_1, \dots, x_n$ 与 $r_1, \dots, r_n$，使得

$$\overline{B(x_k, r_k)} \subseteq B(x_{k-1}, r_{k-1}) \cap U_k, \quad k = 2, \dots, n,$$

且 $r_k < 1/k$。

**归纳步骤**：由 $U_{n+1}$ 稠密，$B(x_n, r_n) \cap U_{n+1}$ 非空；又两者均开，故为非空开集。取

$$x_{n+1} \in B(x_n, r_n) \cap U_{n+1}, \qquad r_{n+1} \in \bigl(0,\ \tfrac{1}{n+1}\bigr),$$

满足

$$\overline{B(x_{n+1}, r_{n+1})} \subseteq B(x_n, r_n) \cap U_{n+1}. \quad \cdots (2)$$

由归纳法，$\{\overline{B(x_n, r_n)}\}$ 为递降闭球序列，$r_n \to 0$。$\square$

#### 第三步：完备性 + 嵌套闭球引理

由完备度量空间中的嵌套闭球引理，

$$\bigcap_{n=1}^\infty \overline{B(x_n, r_n)} \neq \varnothing.$$

取 $x \in \bigcap_n \overline{B(x_n, r_n)}$。

> [!important] 完备性的核心运用
> 第三步是完备性发挥作用的唯一一步。若 $X$ 不完备，构造出的 Cauchy 序列 $\{x_n\}$ 可能在 $X$ 中无极限，整个证明将失败。

#### 第四步：验证 $x \in V \cap \bigcap_n U_n$

由 $(1)$，$x \in \overline{B(x_1, r_1)} \subseteq V \cap U_1$，故 $x \in V$ 且 $x \in U_1$。

由 $(2)$，对每个 $n \geq 2$，$x \in \overline{B(x_n, r_n)} \subseteq U_n$。

综上：$x \in V$ 且 $x \in U_n$ 对一切 $n \in \mathbb{N}$ 成立。故 $x \in V \cap \bigcap_n U_n$。$\square$

### 等价性：(i) $\Leftrightarrow$ (ii) $\Leftrightarrow$ (iii)

#### (i) $\Rightarrow$ (ii)

设 $X = \bigcup_n A_n$，其中每个 $A_n$ 无处稠密。则 $U_n = X \setminus \overline{A_n}$ 开，且因 $\operatorname{int}(\overline{A_n}) = \varnothing$，$U_n$ 稠密。由 (i)，$\bigcap_n U_n$ 稠密，特别非空。但

$$\bigcap_n U_n = \bigcap_n (X \setminus \overline{A_n}) = X \setminus \bigcup_n \overline{A_n} \subseteq X \setminus \bigcup_n A_n = \varnothing.$$

矛盾。故 $X$ 不能表示为可数个无处稠密集的并。$\square$

#### (ii) $\Rightarrow$ (iii)

设 $X = \bigcup_n F_n$，$F_n$ 闭。若所有 $F_n$ 均有 $\operatorname{int}(F_n) = \varnothing$，则因 $F_n$ 闭即 $\overline{F_n} = F_n$，故 $F_n$ 无处稠密。从而 $X$ 是可数个无处稠密集的并，违反 (ii)。$\square$

#### (iii) $\Rightarrow$ (i)

设 $\{U_n\}$ 为开稠密集列。令 $V$ 为非空开集。假设 $V \cap \bigcap_n U_n = \varnothing$，则 $V \subseteq \bigcup_n (X \setminus U_n)$。但 $X \setminus U_n$ 闭，$V$ 视为完备度量子空间（开子集的闭包问题更细，此处采用直接论证）……（标准论证：将 $V$ 配上原度量，不一定完备；故 (iii) $\Rightarrow$ (i) 通常借助 (i) $\Leftrightarrow$ (ii) 与 (ii) $\Leftrightarrow$ (iii) 闭合循环。）

> [!info] 等价性的注解
> 通常的教科书路径是 (i) $\Rightarrow$ (ii) $\Rightarrow$ (iii)，然后 (iii) $\Rightarrow$ (i) 再次借助补集与稠密性的对偶（在开集 $V$ 上考虑 $\{U_n \cap V\}$ 作为 $\overline{V}$ 中的稠密开集，并对 $\overline{V}$ 应用 (iii)）。三者本质等价。

三个命题等价，故 **(ii)** 与 **(iii)** 亦成立。$\blacksquare$

---

## 应用

### 应用一：完备无孤立点度量空间不可数

> [!abstract] 推论
> 设 $(X, d)$ 为非空完备度量空间且无孤立点（即每个点都是极限点）。则 $X$ 不可数。

**证明**：反证。假设 $X = \{x_1, x_2, \dots\}$ 可数。

#### 单点集 $\{x_n\}$ 无处稠密

$\{x_n\}$ 闭，故 $\overline{\{x_n\}} = \{x_n\}$。由 $X$ 无孤立点，对任意 $r > 0$，$B(x_n, r) \setminus \{x_n\} \neq \varnothing$，故 $\{x_n\}$ 不包含任何开球，即 $\operatorname{int}(\{x_n\}) = \varnothing$。故 $\{x_n\}$ 无处稠密。$\square$

#### 应用 Baire 定理

$X = \bigcup_n \{x_n\}$ 为可数个无处稠密集的并，与 Baire 范畴定理 (ii) 矛盾。故 $X$ 不可数。$\blacksquare$

> [!tip] 推论的特例
> - $\mathbb{R}$（实数集）完备、无孤立点，故 $\mathbb{R}$ 不可数（无需 Cantor 对角线论证）。
> - 任意完备非空 Banach 空间（非平凡）均不可数。
> - Cantor 三分集 $\mathcal{C} \subseteq [0,1]$ 完备（作为 $\mathbb{R}$ 的闭子集）且无孤立点，故不可数。

### 应用二：$\mathbb{Q}$ 不是 $G_\delta$ 集

> [!abstract] 推论
> $\mathbb{R}$ 中的有理数集 $\mathbb{Q}$ 不是 $G_\delta$ 集（即不能表示为可数个开集的交）。

**证明**：反证。假设 $\mathbb{Q} = \bigcap_n U_n$，其中 $U_n$ 为 $\mathbb{R}$ 中的开集。

#### 第一步：$U_n$ 在 $\mathbb{R}$ 中稠密

由 $\mathbb{Q} \subseteq U_n$ 及 $\mathbb{Q}$ 在 $\mathbb{R}$ 中稠密，得 $U_n$ 稠密。$\square$

#### 第二步：构造稠密开集列

设 $\mathbb{Q} = \{q_1, q_2, \dots\}$ 为有理数的一个枚举。令

$$V_n = U_n \setminus \{q_n\} = U_n \cap (\mathbb{R} \setminus \{q_n\}).$$

由于 $\{q_n\}$ 闭，$\mathbb{R} \setminus \{q_n\}$ 开稠密。故 $V_n$ 仍为开稠密集。

#### 第三步：应用 Baire 定理导出矛盾

由 Baire 定理 (i)，$\bigcap_n V_n$ 在 $\mathbb{R}$ 中稠密，特别非空。设 $x \in \bigcap_n V_n$。

则 $x \in \bigcap_n U_n = \mathbb{Q}$，故 $x = q_k$ 某 $k$。但 $x \in V_k = U_k \setminus \{q_k\}$ 蕴含 $x \neq q_k$。**矛盾！** $\blacksquare$

> [!warning] 对偶事实：$\mathbb{R} \setminus \mathbb{Q}$ 是 $G_\delta$
> 无理数集 $\mathbb{R} \setminus \mathbb{Q} = \bigcap_{q \in \mathbb{Q}} (\mathbb{R} \setminus \{q\})$ 是可数个开集的交，故为 $G_\delta$ 集。这与 $\mathbb{Q}$ 不是 $G_\delta$ 形成鲜明对比，本质上反映了 $\mathbb{Q}$ 的"复杂程度高于" $\mathbb{R} \setminus \mathbb{Q}$。

### 应用三：一致有界性原理的证明骨架

> [!abstract] Banach-Steinhaus 定理
> 设 $X$ 为 Banach 空间，$Y$ 为赋范空间，$\{T_\alpha\}_{\alpha \in \Lambda} \subseteq \mathcal{B}(X, Y)$。若对每个 $x \in X$，$\sup_\alpha \|T_\alpha x\| < \infty$，则 $\sup_\alpha \|T_\alpha\| < \infty$。

**证明思路**：

#### 闭集覆盖

令 $F_n = \{x \in X : \sup_\alpha \|T_\alpha x\| \leq n\}$。由 $T_\alpha$ 连续，$F_n$ 为闭集。由逐点有界，$X = \bigcup_n F_n$。

#### 应用 Baire 定理 (iii)

$X$ 完备，故存在 $F_N$ 有非空内部，即存在 $B(x_0, r) \subseteq F_N$。由线性性，将单位球中的任意 $x$ 平移到该球内可推出 $\|T_\alpha\| \leq 2N/r$。

完整证明见 [[一致有界性原理（Banach-Steinhaus 定理）]]。$\blacksquare$

> [!important] 三大定理的共同根源
> 泛函分析的三大经典定理——**一致有界性原理**、**开映射定理**、**闭图像定理**——均建立在 Baire 范畴定理之上。Baire 是连接"完备性"与"几何丰富性"的桥梁。

---

## 证明思路总结

> [!tip] 关键思想
> Baire 范畴定理的证明核心是**完备性 + 闭球嵌套构造**：
> 1. 给定可数个开稠密集 $\{U_n\}$ 和初始非空开集 $V$；
> 2. 在 $V \cap U_1$ 中放入闭球 $\overline{B_1}$；
> 3. 在 $B_1 \cap U_2$ 中放入更小的闭球 $\overline{B_2}$；
> 4. 依此构造嵌套闭球序列，半径 $\to 0$；
> 5. 完备性保证嵌套交集非空，交集中的点同时落在 $V$ 与所有 $U_n$ 内。
>
> 这是"在每一步只损失一个 $U_n$ 的稠密性条件，但保留一个开球的余地"的精妙平衡。

> [!tip] 应用的统一模式
> Baire 定理的应用通常采用**反证法**：
> 1. 假设结论不成立（如 $X$ 可数，$\mathbb{Q}$ 是 $G_\delta$ 等）；
> 2. 构造一个**可数个无处稠密集（或闭集无内部）的并表达**；
> 3. 由 Baire 定理导出矛盾。
>
> 关键技巧是识别隐藏在反设中的"可数分解"结构。

> [!warning] 完备性的不可省略
> Baire 定理对一般度量空间**不成立**。例如：
> - $\mathbb{Q}$ 是可数的度量空间，且 $\mathbb{Q} = \bigcup_{q \in \mathbb{Q}} \{q\}$ 是可数个无处稠密集的并（在 $\mathbb{Q}$ 内每个单点集无内部）。$\mathbb{Q}$ 不完备，故 Baire 定理不适用。
> - 这也解释了为何"完备无孤立点 $\Rightarrow$ 不可数"中**完备性不可省**。

> [!info] 推广
> Baire 范畴定理对**局部紧 Hausdorff 空间**亦成立（如 $\mathbb{R}^n$ 任意闭子集、流形等）。完备度量空间与局部紧 Hausdorff 空间是 Baire 空间（满足 Baire 性质的空间）的两类典型代表。
