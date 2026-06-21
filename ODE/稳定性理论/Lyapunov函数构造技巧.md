---
title: Lyapunov 函数构造技巧
date: 2026-06-20
tags:
  - 微分方程
  - ODE
  - 稳定性理论
  - Lyapunov函数
  - Lyapunov稳定性
  - 构造方法
---

# Lyapunov 函数构造技巧

## 预备定义

> [!note] Lyapunov 函数
> 对自治系统 $\dot{\mathbf{x}} = \mathbf{f}(\mathbf{x})$（$\mathbf{f}(\mathbf{0}) = \mathbf{0}$），设 $V: U \to \mathbb{R}$ 在原点某邻域 $U$ 上 $C^1$。称 $V$ 为**正定**的，若 $V(\mathbf{0}) = 0$ 且 $V(\mathbf{x}) > 0$（$\mathbf{x} \neq \mathbf{0}$）。$V$ 沿解的时间导数（Lie 导数 / 轨道导数）为
> $$\dot{V}(\mathbf{x}) = \nabla V(\mathbf{x}) \cdot \mathbf{f}(\mathbf{x}).$$

> [!abstract] 定理：Lyapunov 稳定性判据
> 详见 [[Lyapunov稳定性定理]]。简言之：
> - 若存在正定 $V$ 使 $\dot{V} \leq 0$ → 原点稳定；
> - 若 $\dot{V} < 0$（$\mathbf{x} \neq \mathbf{0}$）→ 原点渐近稳定；
> - 若 $V$ 正定、径向无界（$V(\mathbf{x}) \to \infty$ 当 $\|\mathbf{x}\| \to \infty$）且 $\dot{V} < 0$ → 全局渐近稳定。
>
> 本文聚焦于**如何构造 $V$**——这是应用 Lyapunov 方法时最关键也最依赖经验的步骤。

---

## 核心构造方法

### 方法 1：能量法（力学系统）

对来自 Newton 力学的二阶方程 $\ddot{x} + g(x) = 0$（或其含阻尼形式 $\ddot{x} + h(\dot{x}) + g(x) = 0$），自然的 Lyapunov 函数即**总能量**：
$$V(x, \dot{x}) = \frac{1}{2} \dot{x}^2 + G(x), \quad G(x) = \int_0^x g(s)\, ds.$$

一阶系统形式：$\dot{x} = y,\ \dot{y} = -g(x) - h(y)$。则
$$\dot{V} = y \dot{y} + g(x) \dot{x} = y(-g(x) - h(y)) + g(x) y = -y\, h(y).$$

若 $y\, h(y) > 0$（$y \neq 0$）即 $h$ 为"真阻尼"，则 $\dot{V} < 0$（除 $y = 0$ 外即零）。再用 LaSalle 不变性原理排除 $y \equiv 0$ 上的非零解 → 渐近稳定。

> [!info] 适用场景
> $\ddot{x} + c\dot{x} + k x = 0$（$c, k > 0$）→ $V = \frac{1}{2}\dot{x}^2 + \frac{k}{2}x^2$，$\dot{V} = -c \dot{x}^2 \leq 0$。
> $\ddot{x} + \dot{x} + x^3 = 0$ → $V = \frac{1}{2}\dot{x}^2 + \frac{1}{4}x^4$，$\dot{V} = -\dot{x}^2$。详见 [[Lyapunov例题]]。

### 方法 2：二次型试探（线性化系统的 Lyapunov 方程）

对系统 $\dot{\mathbf{x}} = A\mathbf{x} + \mathbf{g}(\mathbf{x})$（$\mathbf{g}(\mathbf{0}) = \mathbf{0}$，$D\mathbf{g}(\mathbf{0}) = \mathbf{0}$），若 $A$ 的所有特征值具负实部（线性化渐近稳定），则对任意正定 $Q$，**Lyapunov 矩阵方程**
$$A^T P + P A = -Q$$
有唯一正定解 $P$。取 $V(\mathbf{x}) = \mathbf{x}^T P \mathbf{x}$，则
$$\dot{V} = \mathbf{x}^T (A^T P + P A) \mathbf{x} + o(\|\mathbf{x}\|^2) = -\mathbf{x}^T Q \mathbf{x} + o(\|\mathbf{x}\|^2) < 0 \ (\text{对充分小 } \|\mathbf{x}\|).$$

$P$ 的计算：对二维系统，令 $P = \begin{pmatrix} p_{11} & p_{12} \\ p_{12} & p_{22} \end{pmatrix}$，取 $Q = I$，解 $2 \times 2$ 线性方程组得 $P$ 各分量。此方法给出**局部渐近稳定的严格 Lyapunov 证明**（不必靠 Hartman-Grobman）。

### 方法 3：分离变量型 $V(x, y) = F(x) + G(y)$

对于形如
$$\begin{cases} \dot{x} = f_1(x) + f_2(y), \\ \dot{y} = g_1(x) + g_2(y) \end{cases}$$
的系统，尝试 $V = \int_0^x \phi(s)\, ds + \int_0^y \psi(s)\, ds$，并选取 $\phi, \psi$ 使 $\dot{V}$ 中交叉项抵消：
$$\dot{V} = \phi(x) [f_1(x) + f_2(y)] + \psi(y) [g_1(x) + g_2(y)].$$

目标是使 $\dot{V}$ 只含负定 / 半负定的 $x$-项与 $y$-项。一个经典且有效的选取是 $\phi(x) = -g_1(x)$、$\psi(y) = f_2(y)$，此时交叉项 $\phi f_2 + \psi g_1 = -g_1 f_2 + f_2 g_1 = 0$ 自动抵消。

### 方法 4：梯度系统（$V$ = 势函数）

若系统可写为梯度形式 $\dot{\mathbf{x}} = -\nabla V(\mathbf{x})$，则 $V$ 本身即为 Lyapunov 函数：
$$\dot{V} = \nabla V \cdot \dot{\mathbf{x}} = -\|\nabla V\|^2 \leq 0.$$
等号仅当 $\nabla V = \mathbf{0}$ 时成立。此时平衡点恰为 $V$ 的临界点，渐近稳定性由 $V$ 在该点的 Hessian 正定性保证。

反过来，若系统非梯度型，可用**复合梯度**思路：猜一个 $V$，尽量使 $\mathbf{f} \approx -\nabla V +$ 小扰动。

### 方法 5：齐次系统的广义能量

若 $\mathbf{f}$ 是齐次向量场（$f_i(\lambda \mathbf{x}) = \lambda^m f_i(\mathbf{x})$），可试 $m+1$ 次齐次形式 $V = \sum c_{ij} x^i y^j$（$i+j = m+1$）。匹配系数使 $\dot{V}$ 降次为更负定的形式。

### 方法 6：LaSalle 不变性原理配合半负定 $\dot{V}$

当 $\dot{V} \leq 0$（仅半负定而非严格负定）时，单靠 $\dot{V} \leq 0$ 不够保证渐近稳定。此时需调用 **LaSalle 不变性原理**（见 [[LaSalle不变性原理]]）：轨线的 $\omega$-极限集必含于 $\{\mathbf{x} : \dot{V}(\mathbf{x}) = 0\}$ 的最大不变子集中。若该子集仅为 $\{\mathbf{0}\}$，则原点渐近稳定。

---

## 构造策略总结

| 系统类型 | 推荐方法 | $V$ 的形式 |
|---|---|---|
| 力学系统（二阶 Newton 型） | 能量法 | $\frac{1}{2}\dot{x}^2 + \int g(x) dx$ |
| 线性化渐近稳定 + 小非线性 | 二次型（Lyapunov 方程） | $\mathbf{x}^T P \mathbf{x}$，$A^T P + P A = -Q$ |
| 分离变量型 | $F(x) + G(y)$ + 交叉项抵消 | $\int \phi = -\int g_1$、$\int \psi = \int f_2$ |
| 梯度系统 | $V$ = 势函数 | $\dot{\mathbf{x}} = -\nabla V$ |
| 齐次向量场 | 齐次广义能量 | $m+1$ 次齐次 $V$ |
| $\dot{V} = 0$ 上的最大不变集 | LaSalle 原理 | 从能量法得到半负定 $\dot{V}$ |

---

## 证明思路总结

> [!tip] 关键思想
> Lyapunov 函数构造 = "为动力系统寻找一个单调递减的广义能量"。没有自动化的公式——但每种典型**物理或代数结构**（保守力 → 机械能、线性稳定 → 二次型矩阵方程、梯度流 → 势函数、分离变量 → 积分求和）都提供了自然的候选。核心技巧是**让 $V$ 沿非线性流下降，而非仅沿线性化流下降**：因此 $V$ 通常包含非线性的积分项（$\int g(s) ds$），使 $\dot{V}$ 中的非线性充分暴露。
>
> 最通用的一句话口诀：**$V$ 取系统的某个"守恒律"（当阻尼为零时），则加入阻尼后 $\dot{V}$ 自然负定。**

> [!warning] 构造与验证的鸿沟
> Lyapunov 定理本身不负责构造 $V$——它只负责"一旦你找到了 $V$，我就能给你结论"。本文的六种方法是实践中反复成功的手段，但**不存在万能构造法**。偶数维力学系统是最"友好"的；奇数维和高维系统往往需要结合物理对称性（Noether 定理的 Lyapunov 对应）或借助数值分析猜测。

> [!info] 与相关笔记的衔接
> - [[Lyapunov稳定性定理]] — 本文构造出的 $V$ 直接代入其定理使用；
> - [[LaSalle不变性原理]] — 当 $\dot{V} \leq 0$ 仅为半负定时调用；
> - [[Hartman-Grobman定理]] — 线性化分析的局限性（仅局部、仅双曲），反衬出 Lyapunov 直证（可覆盖非线性大范围）的价值；
> - [[Lyapunov例题]] — 本文方法的完整推演实例。
