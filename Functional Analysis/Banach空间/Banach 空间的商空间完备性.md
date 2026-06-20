---
title: Banach 空间的商空间完备性
date: 2026-04-05
tags:
  - 泛函分析
  - Banach空间
  - 商空间
  - 完备性
---

# Banach 空间的商空间完备性

## 预备定义

> [!note] 商空间与商范数
> 设 $X$ 为赋范空间，$Y$ 为 $X$ 的子空间。**商空间** $X/Y$ 的元素为陪集
> $$[x] = x + Y = \{ x + y : y \in Y \},$$
> 其上定义**商范数**
> $$\|[x]\| = \inf_{y \in Y} \|x - y\| = \text{dist}(x, Y).$$

---

## 定理

设 $X$ 为 Banach 空间，$Y$ 为 $X$ 的闭子空间。则商空间 $X/Y$ 在商范数下是完备的（即 $X/Y$ 也是 Banach 空间）。

---

## 证明

### 前提验证：商范数是范数

在证明完备性之前，先确认商范数确实构成范数（此步骤需要 $Y$ 的封闭性）。

#### (N1) 非负性

$\|[x]\| = \inf_{y \in Y} \|x - y\| \geq 0$，因为 $\|\cdot\|$ 非负。$\square$

#### (N2) 正定性（此处用到 $Y$ 闭）

设 $\|[x]\| = 0$。则 $\inf_{y \in Y} \|x - y\| = 0$，故存在序列 $\{y_n\} \subseteq Y$ 使得

$$\|x - y_n\| \to 0, \quad \text{即} \quad y_n \to x.$$

**由于 $Y$ 是闭子空间**，$Y$ 包含其所有极限点，故 $x \in Y$，即 $[x] = [0]$。

> [!warning] $Y$ 封闭的必要性
> 若 $Y$ 不封闭，可能存在 $x \notin Y$ 但 $\text{dist}(x, Y) = 0$，此时 $\|[x]\| = 0$ 而 $[x] \neq [0]$，正定性失败，商"范数"退化为半范数。

$\square$

#### (N3) 齐次性

对 $\alpha \neq 0$：

$$\|[\alpha x]\| = \inf_{y \in Y} \|\alpha x - y\| = \inf_{y \in Y} \|\alpha x - y\|.$$

由于 $Y$ 是子空间，当 $y$ 遍历 $Y$ 时，$y/\alpha$ 也遍历 $Y$。令 $y' = y/\alpha$：

$$= \inf_{y' \in Y} \|\alpha x - \alpha y'\| = |\alpha| \inf_{y' \in Y} \|x - y'\| = |\alpha| \, \|[x]\|.$$

当 $\alpha = 0$ 时，$[\alpha x] = [0]$，$\|[0]\| = 0 = |0| \cdot \|[x]\|$。$\square$

#### (N4) 三角不等式

设 $[x_1], [x_2] \in X/Y$。对任意 $\varepsilon > 0$，存在 $y_1, y_2 \in Y$ 使得

$$\|x_1 - y_1\| < \|[x_1]\| + \varepsilon, \quad \|x_2 - y_2\| < \|[x_2]\| + \varepsilon.$$

由于 $y_1 + y_2 \in Y$：

$$\|[x_1 + x_2]\| = \inf_{y \in Y} \|x_1 + x_2 - y\| \leq \|(x_1 + x_2) - (y_1 + y_2)\| \leq \|x_1 - y_1\| + \|x_2 - y_2\|.$$

故

$$\|[x_1 + x_2]\| < \|[x_1]\| + \|[x_2]\| + 2\varepsilon.$$

令 $\varepsilon \to 0$，得 $\|[x_1 + x_2]\| \leq \|[x_1]\| + \|[x_2]\|$。$\square$

---

### 完备性的证明

**目标**：证明 $X/Y$ 中每个 Cauchy 序列收敛。

设 $\{[x_n]\}$ 为 $X/Y$ 中的 Cauchy 序列。

#### 第一步：提取快速收敛子列

由于 $\{[x_n]\}$ 为 Cauchy 序列，可提取子列 $\{[x_{n_k}]\}_{k=1}^{\infty}$ 使得

$$\|[x_{n_{k+1}}] - [x_{n_k}]\| < \frac{1}{2^k}, \quad \forall\, k \geq 1.$$

> [!info] 为何可以提取这样的子列
> 对每个 $k$，由 Cauchy 条件存在 $N_k$ 使得 $m, n \geq N_k$ 时 $\|[x_m] - [x_n]\| < 2^{-k}$。取 $n_1 < n_2 < \cdots$ 使得 $n_k \geq N_k$，则 $\|[x_{n_{k+1}}] - [x_{n_k}]\| < 2^{-k}$。

#### 第二步：为子列选取好的代表元

**目标**：在 $X$ 中构造一个 Cauchy 序列 $\{z_k\}$，使得 $[z_k] = [x_{n_k}]$。

取 $z_1 = x_{n_1}$ 为 $[x_{n_1}]$ 的任意代表元。

对每个 $k \geq 1$，由商范数的定义：

$$\|[x_{n_{k+1}} - x_{n_k}]\| = \inf_{y \in Y} \|(x_{n_{k+1}} - x_{n_k}) - y\| < \frac{1}{2^k}.$$

由下确界的性质，存在 $y_k \in Y$ 使得

$$\|x_{n_{k+1}} - x_{n_k} - y_k\| < \frac{1}{2^k}. \quad \cdots (\ast)$$

定义

$$z_k = x_{n_k} - \sum_{j=1}^{k-1} y_j, \quad k \geq 2.$$

（约定 $k = 1$ 时空和为 $0$，即 $z_1 = x_{n_1}$。）

#### 第三步：验证 $[z_k] = [x_{n_k}]$

$$z_k = x_{n_k} - \underbrace{\sum_{j=1}^{k-1} y_j}_{\in\, Y}.$$

由于 $Y$ 为子空间，有限和 $\sum_{j=1}^{k-1} y_j \in Y$，故

$$[z_k] = [x_{n_k}]. \quad \square$$

#### 第四步：验证 $\{z_k\}$ 在 $X$ 中是 Cauchy 序列

计算相邻两项之差：

$$z_{k+1} - z_k = \left(x_{n_{k+1}} - \sum_{j=1}^{k} y_j\right) - \left(x_{n_k} - \sum_{j=1}^{k-1} y_j\right) = x_{n_{k+1}} - x_{n_k} - y_k.$$

由 $(\ast)$：

$$\|z_{k+1} - z_k\| = \|x_{n_{k+1}} - x_{n_k} - y_k\| < \frac{1}{2^k}.$$

对任意 $m > k$，利用伸缩求和：

$$\|z_m - z_k\| = \left\|\sum_{j=k}^{m-1} (z_{j+1} - z_j)\right\| \leq \sum_{j=k}^{m-1} \|z_{j+1} - z_j\| < \sum_{j=k}^{m-1} \frac{1}{2^j} < \sum_{j=k}^{\infty} \frac{1}{2^j} = \frac{1}{2^{k-1}}.$$

当 $k \to \infty$ 时 $\dfrac{1}{2^{k-1}} \to 0$，故 $\{z_k\}$ 为 $X$ 中的 Cauchy 序列。$\square$

#### 第五步：利用 $X$ 的完备性

**$X$ 是 Banach 空间**，故 Cauchy 序列 $\{z_k\}$ 在 $X$ 中收敛。设

$$z_k \to z \in X.$$

> [!important] 完备性的核心运用
> 此步是整个证明的关键：我们在 $X/Y$ 中无法直接构造极限，但通过精心选取代表元，将问题转化为 $X$ 中 Cauchy 序列的收敛性——而 $X$ 的完备性正好保证了这一点。

#### 第六步：证明 $[x_{n_k}] \to [z]$

利用商范数的基本估计：对任意 $[a] \in X/Y$，

$$\|[a]\| = \inf_{y \in Y} \|a - y\| \leq \|a\|$$

（取 $y = 0$ 即得）。因此

$$\|[x_{n_k}] - [z]\| = \|[z_k] - [z]\| = \|[z_k - z]\| \leq \|z_k - z\| \to 0.$$

故子列 $[x_{n_k}] \to [z]$ 在 $X/Y$ 中。$\square$

#### 第七步：由子列收敛推出全列收敛

$\{[x_n]\}$ 为 Cauchy 序列，且其子列 $\{[x_{n_k}]\}$ 收敛于 $[z]$。

> [!abstract] 引理：Cauchy 序列若有收敛子列，则全列收敛于同一极限
> 设 $\{a_n\}$ 为度量空间中的 Cauchy 序列，$\{a_{n_k}\}$ 为其收敛于 $a$ 的子列。对任意 $\varepsilon > 0$，存在 $N$ 使得 $m, n \geq N$ 时 $d(a_m, a_n) < \varepsilon/2$，存在 $K$ 使得 $k \geq K$ 时 $d(a_{n_k}, a) < \varepsilon/2$。取 $n \geq N$ 及 $k$ 使 $n_k \geq N$ 且 $k \geq K$，则 $d(a_n, a) \leq d(a_n, a_{n_k}) + d(a_{n_k}, a) < \varepsilon$。

应用此引理：对任意 $\varepsilon > 0$，

- 存在 $N_1$ 使得 $m, n \geq N_1$ 时 $\|[x_m] - [x_n]\| < \varepsilon/2$（Cauchy 条件）；
- 存在 $K$ 使得 $k \geq K$ 时 $\|[x_{n_k}] - [z]\| < \varepsilon/2$（子列收敛）。

对任意 $n \geq N_1$，取 $k$ 充分大使得 $n_k \geq N_1$ 且 $k \geq K$，则

$$\|[x_n] - [z]\| \leq \|[x_n] - [x_{n_k}]\| + \|[x_{n_k}] - [z]\| < \frac{\varepsilon}{2} + \frac{\varepsilon}{2} = \varepsilon.$$

因此 $[x_n] \to [z]$ 在 $X/Y$ 中。$\square$

---

## 结论

$X/Y$ 中的任意 Cauchy 序列均收敛，故 $X/Y$ 在商范数下完备。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明的核心策略是**将商空间中的收敛问题提升到原空间**：
>
> $$\{[x_{n_k}]\} \text{ (Cauchy in } X/Y) \quad \xrightarrow{\text{选代表元}} \quad \{z_k\} \text{ (Cauchy in } X) \quad \xrightarrow{X \text{ 完备}} \quad z_k \to z \quad \xrightarrow{\text{投影}} \quad [x_{n_k}] \to [z]$$
>
> 1. **提取快速子列**：使相邻项商范数差以几何级数衰减（$< 2^{-k}$）；
> 2. **选取好的代表元**：利用下确界的逼近性，从每个陪集中挑选代表元 $z_k$，使得 $\|z_{k+1} - z_k\|$ 也以 $2^{-k}$ 衰减；
> 3. **在 $X$ 中求极限**：$\{z_k\}$ 绝对收敛，$X$ 完备保证极限 $z$ 存在；
> 4. **投影回商空间**：$\|[a]\| \leq \|a\|$ 保证 $X$ 中的收敛蕴含 $X/Y$ 中的收敛。
>
> $Y$ 的封闭性在**商范数的正定性**中起到关键作用，确保 $\|[x]\| = 0 \Rightarrow x \in Y$。
