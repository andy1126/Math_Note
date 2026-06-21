---
title: Lyapunov 例题
date: 2026-06-20
tags:
  - 题解
  - 微分方程
  - ODE
  - 稳定性理论
  - Lyapunov函数
  - Lyapunov稳定性
---

# Lyapunov 例题

## 题目

> 为系统
> $$\ddot{x} + \dot{x} + x^3 = 0$$
> 构造一个 **Lyapunov 函数**，证明原点 $(x, \dot{x}) = (0, 0)$ 是**全局渐近稳定**的平衡点。

---

## 预备定义与定理

> [!note] 一阶系统形式
> 令 $y = \dot{x}$，则二阶方程化为二维一阶系统：
> $$\begin{cases} \dot{x} = y, \\ \dot{y} = -y - x^3. \end{cases}$$
> 原点 $(0, 0)$ 为唯一平衡点（$y = 0$ 且 $-y - x^3 \Rightarrow x^3 = 0 \Rightarrow x = 0$）。

> [!abstract] 定理：Lyapunov 渐近稳定性
> 若存在 $C^1$ 函数 $V(x, y)$，满足：
> 1. $V(0, 0) = 0$，$V(x, y) > 0$（$(x, y) \neq (0, 0)$）——正定；
> 2. $\dot{V}(x, y) < 0$（$(x, y) \neq (0, 0)$）——沿解的导数负定；
> 则原点**局部渐近稳定**。若进一步 $V$ 径向无界（$V \to \infty$ 当 $\|(x, y)\| \to \infty$），则原点**全局渐近稳定**。
> 详见 [[Lyapunov稳定性定理]]。

> [!abstract] 引理：LaSalle 不变性原理
> 若 $\dot{V} \leq 0$（半负定），则轨线的 $\omega$-极限集含于 $\{\dot{V} = 0\}$ 的最大不变子集中。若该子集仅为 $\{\mathbf{0}\}$，则渐近稳定仍成立。详见 [[LaSalle不变性原理]]。

> [!abstract] 引理：能量法
> 对 $\ddot{x} + h(\dot{x}) + g(x) = 0$，总能量 $V = \frac{1}{2} \dot{x}^2 + \int_0^x g(s) ds$ 给出 $\dot{V} = -\dot{x}\, h(\dot{x})$。若 $y\, h(y) > 0$（$y \neq 0$），则 $\dot{V} \leq 0$。详见 [[Lyapunov函数构造技巧]]。

---

## 解答

### 第一步：识别系统结构与构造策略

原方程为 $\ddot{x} + \text{阻尼}(\dot{x}) + \text{恢复力}(x) = 0$ 的形式，其中
$$h(y) = y \quad (\text{线性阻尼}), \qquad g(x) = x^3 \quad (\text{非线性恢复力}).$$

这是标准的力学系统，适用**能量法**构造 Lyapunov 函数。

### 第二步：构造总能量作为候选 $V$

力学系统的总能量 = 动能 + 势能：
$$V(x, y) = \frac{1}{2} y^2 + \int_0^x s^3\, ds = \frac{1}{2} y^2 + \frac{1}{4} x^4.$$

**验证正定性**：$V(0, 0) = 0$；$\frac{1}{2} y^2 \geq 0$，$\frac{1}{4} x^4 \geq 0$，且当 $(x, y) \neq (0, 0)$ 时至少有一项严格大于 $0$。故 $V$ **正定**。✓

**验证径向无界性**：当 $\|(x, y)\| \to \infty$，$x^4 \to \infty$ 或 $y^2 \to \infty$，均使 $V \to \infty$。故 $V$ **径向无界**。✓

### 第三步：计算 $\dot{V}$ 沿系统轨线的导数

$$\begin{aligned}
\dot{V} &= \frac{\partial V}{\partial x} \dot{x} + \frac{\partial V}{\partial y} \dot{y} \\
&= x^3 \cdot y + y \cdot (-y - x^3) \\
&= x^3 y - y^2 - x^3 y \\
&= -y^2.
\end{aligned}$$

> [!important] 交叉项自动抵消的魔力
> $x^3 y$ 来自动能对位置求导的部分（$\partial V/\partial x \cdot \dot{x}$），而 $\dot{y}$ 中的 $-x^3$ 项（恢复力）乘以 $y$ 产生 $-x^3 y$——二者恰为相反数，自动互消。这不是巧合：能量法中的 $\dot{V} = -y\, h(y)$ 保证了恢复力的贡献恒被动能梯度的贡献抵消，只剩阻尼项。

### 第四步：分析 $\dot{V}$ 的定性

$\dot{V} = -y^2 \leq 0$（半负定）。仅当 $y = 0$ 时 $\dot{V} = 0$。在集合 $\{y = 0\}$（$x$ 轴）上，系统给出 $\dot{y} = -x^3$——除非 $x = 0$（原点），否则系统的演化会立即离开 $y = 0$。

> [!info] 使用 LaSalle 不变性原理
> 最大不变集含于 $\{\dot{V} = 0\} = \{(x, 0) : x \in \mathbb{R}\}$。若 $(x(t), y(t))$ 是整条含于此集的轨线，则 $y \equiv 0$，进而 $\dot{y} \equiv 0$。由系统运动方程 $0 = \dot{y} = -0 - x^3 = -x^3$，得 $x \equiv 0$。故 $\{\dot{V} = 0\}$ 中的最大不变子集仅为单点 $\{(0, 0)\}$。
>
> 由 **LaSalle 不变性原理**（[[LaSalle不变性原理]]），所有轨线当 $t \to \infty$ 时趋向 $\{(0, 0)\}$。

### 第五步：全局渐近稳定性的结论

$V$ 正定 + $V$ 径向无界 + 所有轨线收敛至原点。由 Lyapunov 定理 + LaSalle 原理（或直接由标准 Lyapunov 全局渐近稳定性定理），原点**全局渐近稳定**。

> [!info] 线性化视角的失效
> 线性化矩阵 $A = \begin{pmatrix} 0 & 1 \\ -3x^2 & -1 \end{pmatrix}$ 在原点处为 $A = \begin{pmatrix} 0 & 1 \\ 0 & -1 \end{pmatrix}$，特征值 $\lambda = 0, -1$。因存在零特征值，**线性化不能判定**原点的稳定性（非双曲情形，Hartman-Grobman 不适用）。这正是 Lyapunov 直接法胜过线性化分析的标准场景——非线性项（这里是 $x^3$）决定了稳定性。

---

## 答案

$$\boxed{ V(x, y) = \frac{1}{2} y^2 + \frac{1}{4} x^4 }$$

$\dot{V} = -y^2 \leq 0$，仅原点为 $\{\dot{V} = 0\}$ 中的不变子集，由 LaSalle 原理得原点**全局渐近稳定**。

---

## 变形与延伸

> [!info] 变形 1（无阻尼极限——中心）
> 对 $\ddot{x} + x^3 = 0$（去掉阻尼项），同样的 $V = \frac{1}{2}\dot{x}^2 + \frac{1}{4}x^4$ 是**守恒量**（$\dot{V} \equiv 0$），所有轨线为闭轨（周期轨），原点为中心（稳定但非渐近稳定）。
>
> **提示**：对比有无阻尼时 $V$ 表现的差异，体现了阻尼将守恒系统"耗散化"的作用——能量函数从首次积分变成严格的 Lyapunov 函数。

> [!info] 变形 2（非线性阻尼）
> 讨论 $\ddot{x} + \dot{x}^3 + x^3 = 0$ 的稳定性。同样的 $V = \frac{1}{2}\dot{x}^2 + \frac{1}{4}x^4$ 给出 $\dot{V} = -\dot{x}^4 \leq 0$。结论有何不同？
>
> **提示**：$\dot{V} = -y^4$ 的衰减比 $-y^2$ 在原点附近更弱（高阶零点），收敛速率更慢。但全局渐近稳定性结论仍然成立，LaSalle 论证完全相同。

> [!info] 变形 3（负阻尼——不稳定）
> $\ddot{x} - \dot{x} + x^3 = 0$：同样 $V = \frac{1}{2}\dot{x}^2 + \frac{1}{4}x^4$ 给出 $\dot{V} = +\dot{x}^2 \geq 0$（非正定，实为"正"）。Lyapunov 不稳定性定理在此适用——这是 Chetaev 型不稳定性（正阻尼 ⇒ 稳定，负阻尼 ⇒ 不稳定）。
>
> **提示**：Chetaev 定理：若在原点的任意小邻域内 $V > 0$ 且 $\dot{V} > 0$，则原点不稳定。这是 Lyapunov 稳定性定理的不稳定对偶版本。

> [!info] 延伸（Lyapunov 函数在控制设计中的应用）
> Lyapunov 函数 $V$ 本身可用作**控制 Lyapunov 函数**（Control Lyapunov Function, CLF）：若可通过选择控制律 $u$ 使 $\dot{V} < 0$ 对任意非平衡点成立，则系统在反馈 $u = k(\mathbf{x})$ 下全局渐近稳定。本文中阻尼 $- \dot{x}$ 即天然扮演了使 $\dot{V} \leq 0$ 的反馈角色。
