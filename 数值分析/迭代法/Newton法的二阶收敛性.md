---
title: Newton 法的局部二阶收敛性
date: 2026-05-28
tags:
  - 数值分析
  - 迭代法
  - Newton法
  - 二阶收敛
  - 不动点迭代
---

# Newton 法的局部二阶收敛性

## 预备定义

> [!note] Newton 迭代
> 求解 $f(x) = 0$（$f \in C^2(I)$）的 **Newton 迭代**：
> $$x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)}, \quad k = 0, 1, 2, \ldots$$

> [!note] 收敛阶
> 称序列 $x_k \to x^\ast$ **$p$ 阶收敛**，若存在 $C > 0$ 使
> $$|x_{k+1} - x^\ast| \leq C\, |x_k - x^\ast|^p$$
> 对充分大的 $k$ 成立。$p = 2$ 称**二阶**（平方）收敛。

> [!abstract] 引理：带余项的 Taylor 展开
> 设 $f \in C^2[a, b]$，$x, x^\ast \in [a, b]$。则
> $$f(x) = f(x^\ast) + f'(x^\ast)(x - x^\ast) + \frac{1}{2} f''(\xi)(x - x^\ast)^2$$
> 其中 $\xi$ 介于 $x, x^\ast$ 之间。详见 [[Taylor定理]]（实分析中的版本）。

> [!abstract] 引理：不动点迭代收敛阶
> 设 $\varphi \in C^1$，$x^\ast$ 为不动点。若 $|\varphi'(x^\ast)| < 1$，则 $\{x_k\}$ 局部至少线性收敛，且渐近率 $= |\varphi'(x^\ast)|$。详见 [[不动点迭代收敛定理]]。

---

## 定理

设 $f \in C^2(I)$，$x^\ast \in I$ 为 $f$ 的根（即 $f(x^\ast) = 0$），且 $f'(x^\ast) \neq 0$（即 $x^\ast$ 为**单根**）。则：

**(i)（局部存在性）** 存在 $\delta > 0$，使对任意初值 $x_0 \in [x^\ast - \delta, x^\ast + \delta]$，Newton 迭代 $\{x_k\}$ 良定（不会触及 $f'(x_k) = 0$），且 $x_k \to x^\ast$。

**(ii)（二阶收敛）** 误差满足
$$|x_{k+1} - x^\ast| \leq C\, |x_k - x^\ast|^2,\quad C = \frac{\sup |f''|}{2\, \inf |f'|}$$
其中 sup/inf 取在 $x^\ast$ 的某邻域上。特别地
$$\lim_{k \to \infty} \frac{x_{k+1} - x^\ast}{(x_k - x^\ast)^2} = \frac{f''(x^\ast)}{2\, f'(x^\ast)}.$$

---

## 证明

### 前提验证：邻域的可控性

由 $f' \in C(I)$ 与 $f'(x^\ast) \neq 0$，存在 $\delta_0 > 0$ 使
$$|f'(x)| \geq \frac{|f'(x^\ast)|}{2} =: m > 0, \quad x \in J := [x^\ast - \delta_0, x^\ast + \delta_0].$$

设 $M := \sup_{x \in J} |f''(x)| < \infty$（由 $f'' \in C(J)$ 紧致连续）。

### 第一步：建立误差递推

由 Taylor 展开：
$$0 = f(x^\ast) = f(x_k) + f'(x_k)(x^\ast - x_k) + \frac{1}{2} f''(\xi_k)(x^\ast - x_k)^2, \quad \cdots (\ast)$$

其中 $\xi_k$ 介于 $x_k, x^\ast$ 之间。

整理：
$$f(x_k) + f'(x_k)(x^\ast - x_k) = -\frac{1}{2} f''(\xi_k)(x^\ast - x_k)^2.$$

设 $f'(x_k) \neq 0$。两边除以 $f'(x_k)$：
$$\frac{f(x_k)}{f'(x_k)} + (x^\ast - x_k) = -\frac{f''(\xi_k)}{2 f'(x_k)}(x^\ast - x_k)^2.$$

由 Newton 迭代定义 $x_{k+1} - x_k = -f(x_k)/f'(x_k)$，左端 $= -(x_{k+1} - x_k) + (x^\ast - x_k) = x^\ast - x_{k+1}$。故

$$x^\ast - x_{k+1} = -\frac{f''(\xi_k)}{2 f'(x_k)}(x^\ast - x_k)^2.$$

即
$$x_{k+1} - x^\ast = \frac{f''(\xi_k)}{2 f'(x_k)}(x_k - x^\ast)^2. \quad \cdots (\sharp)$$

### 第二步：归纳证明迭代留在 $J$ 内

设 $|x_k - x^\ast| \leq \delta$（$\delta$ 待定）。由 $(\sharp)$ 与 $x_k \in J$：
$$|x_{k+1} - x^\ast| \leq \frac{M}{2 m}\, |x_k - x^\ast|^2 \leq \frac{M}{2m}\, \delta \cdot |x_k - x^\ast|. \quad \cdots (\flat)$$

> [!important] 邻域选取
> 取
> $$\delta := \min\!\left(\delta_0,\ \frac{m}{M}\right).$$
> 则 $\dfrac{M}{2m}\,\delta \leq \dfrac{1}{2}$，从而 $(\flat)$ 给出
> $$|x_{k+1} - x^\ast| \leq \frac{1}{2}\, |x_k - x^\ast| \leq \frac{\delta}{2} < \delta.$$
> 故 $x_{k+1} \in J$，归纳完成。

### 第三步：收敛性

由归纳，$|x_k - x^\ast| \leq (1/2)^k \delta \to 0$，故 $x_k \to x^\ast$。$\square$（(i)）

### 第四步：二阶收敛

直接由 $(\sharp)$：
$$|x_{k+1} - x^\ast| \leq \frac{M}{2 m}\, |x_k - x^\ast|^2 = C\, |x_k - x^\ast|^2. \quad \square$$

### 第五步：渐近率精确

由 $x_k \to x^\ast$ 与 $\xi_k$ 夹在 $x_k, x^\ast$ 间，$\xi_k \to x^\ast$。由 $f'' \in C$，$f''(\xi_k) \to f''(x^\ast)$；类似 $f'(x_k) \to f'(x^\ast)$。$(\sharp)$ 取极限：
$$\frac{x_{k+1} - x^\ast}{(x_k - x^\ast)^2} = \frac{f''(\xi_k)}{2 f'(x_k)} \longrightarrow \frac{f''(x^\ast)}{2 f'(x^\ast)}. \quad \blacksquare$$

---

## 证明思路总结

> [!tip] 关键思想
> Newton 法可视为**沿切线代替函数**：在 $x_k$ 处用切线 $L(x) = f(x_k) + f'(x_k)(x - x_k)$ 逼近 $f$，求 $L(x) = 0$ 得 $x_{k+1}$。
>
> 二阶收敛源于 Taylor 展开的**二阶余项**——切线丢掉的部分恰为 $\frac{1}{2}f''(\xi)(x-x^\ast)^2$，故误差从 $|x_k - x^\ast|$ 缩到 $|x_k - x^\ast|^2$。
>
> **不动点视角**：写 $\varphi(x) = x - f(x)/f'(x)$。则 $x^\ast$ 为 $\varphi$ 不动点。计算
> $$\varphi'(x) = \frac{f(x)\, f''(x)}{f'(x)^2}.$$
> 在 $x^\ast$ 处 $f(x^\ast) = 0$，故 $\varphi'(x^\ast) = 0$——压缩系数瞬时为 0，超线性收敛。由 [[不动点迭代收敛定理]] 一般理论的极限：$\varphi'(x^\ast) = 0$ 即至少二阶收敛。

> [!warning] $f'(x^\ast) \neq 0$（单根）不可省
> 反例（**重根**）：$f(x) = x^2$，$x^\ast = 0$。Newton 迭代 $x_{k+1} = x_k - x_k^2 / (2 x_k) = x_k / 2$。**仅线性收敛**（率 $1/2$），非二阶。
>
> 对 $m$ 重根（$f(x^\ast) = f'(x^\ast) = \cdots = f^{(m-1)}(x^\ast) = 0$，$f^{(m)}(x^\ast) \neq 0$），标准 Newton 退化为线性收敛，率 $1 - 1/m$。修正 Newton $x_{k+1} = x_k - m\, f(x_k)/f'(x_k)$ 可恢复二阶。

> [!warning] 局部性不可省
> Newton 的收敛只在 $x_0$ 充分接近 $x^\ast$ 时保证。远初值可能：
> - **发散**：$f(x) = \arctan x$ 取 $x_0$ 过大时迭代振荡发散；
> - **进入循环**：$f(x) = x^3 - 2x + 2$ 在 $x_0 = 0$ 处陷入周期 2 循环 $0 \to 1 \to 0 \to \cdots$；
> - **穿过奇点**：迭代撞上 $f'(x_k) = 0$。

> [!info] 多维推广
> 求解 $F: \mathbb{R}^n \to \mathbb{R}^n$，$F(\mathbf{x}^\ast) = 0$，Jacobian $F'(\mathbf{x}^\ast)$ 非奇异。多维 Newton：
> $$\mathbf{x}_{k+1} = \mathbf{x}_k - F'(\mathbf{x}_k)^{-1} F(\mathbf{x}_k).$$
> 类似证明（用 Taylor + 反函数定理保证 $F'(\mathbf{x})$ 局部可逆，详见 [[反函数定理]]）给出
> $$\|\mathbf{x}_{k+1} - \mathbf{x}^\ast\| \leq C\, \|\mathbf{x}_k - \mathbf{x}^\ast\|^2.$$

> [!info] 在数值优化中
> 求 $\min g(\mathbf{x})$ 等价于 $\nabla g = 0$。Newton 应用于 $F = \nabla g$ 即**Hessian Newton 法**：
> $$\mathbf{x}_{k+1} = \mathbf{x}_k - [\nabla^2 g(\mathbf{x}_k)]^{-1} \nabla g(\mathbf{x}_k).$$
> Hessian 正定时局部二阶收敛；远初值要配合阻尼或信赖域。
