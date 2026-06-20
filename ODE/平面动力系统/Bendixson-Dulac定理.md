---
title: Bendixson-Dulac 定理
date: 2026-04-11
tags:
  - 常微分方程
  - 动力系统
  - 平面系统
  - 周期轨道
  - Green定理
  - 散度
---

# Bendixson-Dulac 定理

## 预备定义

> [!note] 平面自治系统
> 考虑 $\mathbb{R}^2$ 上的自治系统
> $$x' = P(x, y), \quad y' = Q(x, y), \quad \cdots (S)$$
> 其中 $P, Q: D \to \mathbb{R}$（$D \subseteq \mathbb{R}^2$ 为单连通开集）连续可微。

> [!note] 周期轨道
> 称 $(S)$ 的解 $\gamma(t) = (x(t), y(t))$ 为**周期轨道**（periodic orbit），若存在 $T > 0$ 使得 $\gamma(t + T) = \gamma(t)$ 对一切 $t$ 成立，且 $\gamma$ 不是平衡点。
>
> 周期轨道的像是 $D$ 中的一条简单闭曲线。

> [!note] 散度
> 向量场 $(P, Q)$ 的**散度**（divergence）为
> $$\operatorname{div}(P, Q) = \frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y}.$$

> [!abstract] Green 定理
> 设 $\Gamma$ 为 $\mathbb{R}^2$ 中分段光滑的简单闭曲线（正向），$\Omega$ 为其围成的区域。设 $P, Q$ 在包含 $\overline{\Omega}$ 的开集上连续可微。则
> $$\oint_\Gamma (P\, dx + Q\, dy) = \iint_\Omega \left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right) dA.$$
> 等价地（散度形式）：
> $$\oint_\Gamma (P\, dy - Q\, dx) = \iint_\Omega \left(\frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y}\right) dA = \iint_\Omega \operatorname{div}(P, Q)\, dA.$$

---

## 定理

### Bendixson 判据

设 $D \subseteq \mathbb{R}^2$ 为单连通开集，$P, Q \in C^1(D)$。若

$$\frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y} \quad \text{在 } D \text{ 上不变号（即 } \geq 0 \text{ 或 } \leq 0\text{）且不恒为零},$$

则系统 $(S)$ 在 $D$ 中**没有周期轨道**。

### Bendixson-Dulac 推广

更一般地，若存在 $C^1$ 函数 $\rho: D \to \mathbb{R}$（称为 **Dulac 函数**），使得

$$\frac{\partial(\rho P)}{\partial x} + \frac{\partial(\rho Q)}{\partial y} \quad \text{在 } D \text{ 上不变号且不恒为零},$$

则系统 $(S)$ 在 $D$ 中没有周期轨道。

> [!info] Dulac 函数的作用
> Bendixson 判据是 $\rho \equiv 1$ 的特殊情形。引入 $\rho$ 相当于对向量场 $(P, Q)$ 做"加权"，有时原始散度变号但加权后不变号。选取合适的 $\rho$ 是一门技巧。

---

## 证明

证明 Bendixson-Dulac 推广形式（Bendixson 判据令 $\rho \equiv 1$ 即得）。

**反证法**：假设 $(S)$ 在 $D$ 中存在周期轨道 $\Gamma$。

### 第一步：周期轨道围成的区域

$\Gamma$ 是 $D$ 中的简单闭曲线。由 $D$ 单连通，$\Gamma$ 围成的区域 $\Omega$ 满足 $\overline{\Omega} \subset D$。

$\square$

### 第二步：沿 $\Gamma$ 的线积分为零

设 $\Gamma$ 的参数化为 $(x(t), y(t))$，周期为 $T$。沿 $\Gamma$ 计算：

$$\oint_\Gamma (\rho P\, dy - \rho Q\, dx) = \int_0^T \left[\rho P \cdot y' - \rho Q \cdot x'\right] dt.$$

代入 $(S)$：$x' = P$，$y' = Q$，得

$$= \int_0^T \rho(x(t), y(t)) \left[P \cdot Q - Q \cdot P\right] dt = \int_0^T 0 \, dt = 0. \quad \cdots (\ast)$$

> [!important] 关键消去
> 被积函数 $PQ - QP \equiv 0$。这是因为轨道的切向量 $(x', y') = (P, Q)$ 与向量场 $(P, Q)$ **平行**，故加权通量为零。这一消去与 $\rho$ 的选取无关。

$\square$

### 第三步：用 Green 定理计算同一积分

由 Green 定理（散度形式）：

$$\oint_\Gamma (\rho P\, dy - \rho Q\, dx) = \iint_\Omega \left[\frac{\partial(\rho P)}{\partial x} + \frac{\partial(\rho Q)}{\partial y}\right] dA. \quad \cdots (\star)$$

$\square$

### 第四步：矛盾

由假设，被积函数 $\dfrac{\partial(\rho P)}{\partial x} + \dfrac{\partial(\rho Q)}{\partial y}$ 在 $D$ 上不变号且不恒为零。

- 若 $\geq 0$ 且不恒为零：右端面积积分 $> 0$；
- 若 $\leq 0$ 且不恒为零：右端面积积分 $< 0$。

两种情形均与 $(\ast)$ 中左端 $= 0$ **矛盾！**

故 $(S)$ 在 $D$ 中不存在周期轨道。$\blacksquare$

---

## 应用示例

> [!info] 示例 1：Glycolysis 模型
> 考虑 Selkov 模型的一个变体：
> $$x' = -x + ay + x^2 y, \quad y' = b - ay - x^2 y,$$
> 其中 $a, b > 0$。取 $\rho \equiv 1$，则
> $$\frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y} = (-1 + 2xy) + (-a - x^2) = -(1 + a) + 2xy - x^2.$$
> 在适当的参数范围和区域 $D$ 中若此式不变号，则可排除周期轨道。

> [!info] 示例 2：Lotka-Volterra 竞争模型
> $$x' = x(a - bx - cy), \quad y' = y(d - ex - fy),$$
> 在第一象限 $D = \{x > 0, y > 0\}$ 中，取 Dulac 函数 $\rho(x,y) = \dfrac{1}{xy}$，则
> $$\frac{\partial}{\partial x}\!\left(\frac{a - bx - cy}{y}\right) + \frac{\partial}{\partial y}\!\left(\frac{d - ex - fy}{x}\right) = \frac{-b}{y} + \frac{-f}{x} < 0.$$
> 由 Bendixson-Dulac 定理，第一象限中不存在周期轨道。

---

## 证明思路总结

> [!tip] 关键思想
> 本证明是 **Green 定理**在动力系统中的精妙应用，仅用三行核心论证：
> 1. 轨道与向量场平行 $\Rightarrow$ $\oint_\Gamma (\rho P\, dy - \rho Q\, dx) = 0$；
> 2. Green 定理 $\Rightarrow$ 同一积分等于 $\iint_\Omega \operatorname{div}(\rho P, \rho Q)\, dA$；
> 3. 散度不变号 $\Rightarrow$ 面积积分非零 $\Rightarrow$ 矛盾。
>
> 直观图景：散度度量向量场的"膨胀率"。若散度处处 $\leq 0$，流将任何区域的面积压缩，但周期轨道围成的区域在一个周期后必须回到原样（面积不变）——矛盾。

> [!warning] 条件的必要性与局限
> - **单连通性是必需的**：在非单连通区域中（如环形域），Green 定理不直接适用。周期轨道可以"围住"区域的洞，此时 $\Omega \not\subset D$。
> - **"不恒为零"是必需的**：若散度恒为零（如 Hamilton 系统 $x' = H_y, y' = -H_x$），Bendixson-Dulac 无法排除周期轨道——事实上 Hamilton 系统的周期轨道是泛函的。
> - **Dulac 函数没有系统性构造方法**：和 Lyapunov 函数类似，找到合适的 $\rho$ 需要经验与技巧。常见尝试：$\rho = x^a y^b$，$\rho = e^{\alpha x + \beta y}$，$\rho = 1/(PQ)$ 等。
> - **与 [[Poincaré-Bendixson定理]] 的对偶**：Poincaré-Bendixson 给出周期轨道存在的充分条件（有界 + 无平衡点 $\Rightarrow$ 存在周期轨道），Bendixson-Dulac 给出不存在的充分条件（散度不变号 $\Rightarrow$ 无周期轨道）。两者配合使用，可以精确刻画平面系统的定性行为。
