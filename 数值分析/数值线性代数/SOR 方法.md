---
title: SOR 方法
date: 2026-06-06
tags:
  - 数值分析
  - 数值线性代数
  - 迭代法
  - SOR
  - 松弛因子
  - 一致排序
---

# SOR 方法

## 预备定义

> [!note] 逐次超松弛 (SOR)
> 设 $A = D - L - U$（与 [[Jacobi 与 Gauss-Seidel 迭代|GS 笔记]] 一致约定）。**逐次超松弛迭代 (Successive Over-Relaxation, SOR)** 引入松弛因子 $\omega > 0$：
> $$x_i^{(k+1)} \;=\; (1 - \omega) x_i^{(k)} + \omega \cdot \underbrace{\frac{1}{a_{ii}}\bigl(b_i - \sum_{j < i} a_{ij} x_j^{(k+1)} - \sum_{j > i} a_{ij} x_j^{(k)}\bigr)}_{\text{Gauss-Seidel 公式}}.$$
>
> 矩阵形式：
> $$(D - \omega L) x^{(k+1)} \;=\; \bigl[(1 - \omega) D + \omega U\bigr] x^{(k)} + \omega b,$$
> 即 $x^{(k+1)} = B_\omega x^{(k)} + c_\omega$，其中
> $$B_\omega \;=\; (D - \omega L)^{-1}\bigl[(1 - \omega) D + \omega U\bigr].$$

> [!info] 退化情形
> - $\omega = 1$：SOR ≡ Gauss-Seidel；
> - $\omega < 1$：**欠松弛**（under-relaxation），稳化不收敛的 GS；
> - $\omega > 1$：**超松弛**（over-relaxation），加速 GS（常用 $1 < \omega < 2$）。

---

## 收敛性定理

### 必要条件：Kahan 定理

> [!abstract] 定理 1（Kahan）
> SOR 收敛的必要条件是
> $$\omega \;\in\; (0, 2).$$

**证明**：$\det B_\omega = \det((D - \omega L)^{-1}) \cdot \det((1-\omega)D + \omega U)$。

$D - \omega L$ 下三角，对角与 $D$ 相同 → $\det((D - \omega L)^{-1}) = 1/\det D$.
$(1-\omega)D + \omega U$ 上三角，对角 $= (1-\omega) a_{ii}$ → $\det = (1-\omega)^n \det D$.

故 $\det B_\omega = (1 - \omega)^n$。

由 $|\det B_\omega| = \prod |\lambda_i(B_\omega)|$ 且 $\rho(B_\omega) \geq |\det B_\omega|^{1/n} = |1 - \omega|$。

收敛需 $\rho(B_\omega) < 1 \Rightarrow |1 - \omega| < 1 \Rightarrow \omega \in (0, 2)$。$\square$

### 充分条件：SPD + $\omega \in (0, 2)$

> [!abstract] 定理 2（Ostrowski-Reich）
> 设 $A$ 对称正定。则 SOR 收敛 $\Leftrightarrow$ $\omega \in (0, 2)$。

**证明梗概**：用 Stein 定理（迭代矩阵 $B = -M^{-1}N$ 的稳定性等价于 $M + M^\top - A$ 正定）。

设 $M = (D - \omega L)/\omega$、$N = ((1-\omega)D + \omega U)/\omega \cdot (-1)$... 详细见 Varga《Matrix Iterative Analysis》第 3 章。$\square$

---

## 最优松弛因子

### 一致排序矩阵 (consistently ordered)

> [!note] 一致排序
> $A$ 称为**一致排序**，若对所有 $\alpha \neq 0$，矩阵
> $$\alpha^{-1} D^{-1} L + \alpha D^{-1} U$$
> 的特征值不依赖于 $\alpha$。

典型一致排序：
- **块三对角**（来自 PDE 的有限差分离散，棋盘排序后）；
- 任何排序后形如"Young's property A"的矩阵。

### Young 定理：最优 $\omega^*$

> [!abstract] 定理 3（Young, 1954）
> 设 $A$ 一致排序、SPD、$B_J = D^{-1}(L+U)$ 谱半径 $\rho_J = \rho(B_J) < 1$。则
> $$\omega^* \;=\; \frac{2}{1 + \sqrt{1 - \rho_J^2}}, \qquad \rho(B_{\omega^*}) \;=\; \omega^* - 1 \;=\; \frac{1 - \sqrt{1 - \rho_J^2}}{1 + \sqrt{1 - \rho_J^2}}.$$

**证明梗概**：用一致排序矩阵的 $\lambda(B_\omega) \leftrightarrow \mu(B_J)$ 函数关系
$$(\lambda + \omega - 1)^2 \;=\; \omega^2 \mu^2 \lambda.$$
对 $\lambda$ 求模最小值——把 $\mu$ 取最大 $\rho_J$，得最优 $\omega^*$。$\square$

### 渐近加速

对 Poisson 方程：$\rho_J \approx 1 - \frac{\pi^2 h^2}{2}$（$h$ 网格距）。则
$$\omega^* \approx 2 - 2\pi h, \qquad \rho(B_{\omega^*}) \approx 1 - 2\pi h.$$

对比：$\rho(B_{GS}) \approx 1 - \pi^2 h^2$。

**收敛步数估计**（到 $\varepsilon$ 精度）：
- GS: $\sim \log \varepsilon^{-1}/(\pi^2 h^2) \sim n^2$（$n = 1/h$）；
- 最优 SOR: $\sim \log \varepsilon^{-1}/(2 \pi h) \sim n$.

**SOR 比 GS 加速 $n$ 倍**。

---

## 实现细节

### 算法

输入：$A$、$b$、$\omega$、初值 $x^{(0)}$、容差 $\varepsilon$。

```
重复 k = 0, 1, 2, ...
    对 i = 1 到 n：
        s = b_i
        对 j ≠ i：s -= a_{ij} x_j（j < i 用新值，j > i 用旧值）
        x_i^new = (1 - ω) x_i + ω * s / a_{ii}
    若 ||x^new - x|| < ε：停止
```

### $\omega$ 的选择实务

- **理论已知**：用 Young 公式（如 Poisson 方程）；
- **未知 $\rho_J$**：先做几次 Jacobi 估计 $\rho_J$（$\|x^{(k+1)} - x^{(k)}\|/\|x^{(k)} - x^{(k-1)}\|$ 趋近 $\rho_J$）；
- **粗调**：试 $\omega = 1.5$；细调上下扫描。

### 与 Gauss-Seidel 的相同串行性

SOR 与 GS 一样难并行。Red-Black SOR：棋盘染色后同色并行更新，是椭圆 PDE 求解器中的高度成熟技术。

---

## 具体应用

### 应用一：1D Poisson 方程的 SOR

离散
$$\frac{-u_{i-1} + 2 u_i - u_{i+1}}{h^2} \;=\; f(x_i), \quad i = 1, \ldots, n.$$
（$h = 1/(n+1)$）。$\rho_J = \cos(\pi h)$。

最优 $\omega^* = 2/(1 + \sin(\pi h))$，$\rho(B_{\omega^*}) = (1 - \sin \pi h)/(1 + \sin \pi h) \approx 1 - 2 \sin \pi h$.

$n = 100$（$h \approx 0.01$）：
- $\rho_J \approx 0.9995$ → Jacobi $\sim 1.5 \times 10^4$ 步；
- $\rho_{GS} \approx 0.999$ → GS $\sim 7 \times 10^3$ 步；
- $\rho_{\omega^*} \approx 0.94$ → SOR $\sim 100$ 步。

**约百倍加速**。

### 应用二：2D Poisson 方程

二维网格 $n \times n$，$N = n^2$ 未知。SOR 步数 $\sim n = \sqrt{N}$（比 GS 的 $n^2 = N$ 优 $\sqrt{N}$ 倍）。**直到 1980 年代多重网格出现前**，SOR 是椭圆 PDE 求解器的工业标准。

### 应用三：与 CG 的对比

[[共轭梯度法 CG]] 对 SPD 系统收敛速率 $\sqrt{\kappa(A)}$，对 Poisson 方程 $\kappa \sim h^{-2}$ → CG 步数 $\sim h^{-1} = n$。**与最优 SOR 同阶**。

但：
- **SOR 需要调 $\omega^*$**，错调代价大；
- **CG 无超参数**，鲁棒；
- **CG 局部最优**（每步残差最小），SOR 仅渐近最优。

**现代偏好 CG（+ 预条件）**。

### 应用四：作为预条件子

SSOR（对称 SOR：一次 SOR + 一次反向 SOR）作为 SPD 系统的预条件，配合 CG 极有效。代价低（$O(n)$ per app），加速效果好。

### 应用五：非 SPD 与块 SOR

对块 PDE（Navier-Stokes 离散）的耦合系统，**块 SOR** 把 $n$ 维分量打包成块（如 $3 \times 3$ 速度-压力子块），对块用 SOR 思想。CFD 教材主流技术。

---

## 算法关键点

> [!tip] SOR 的"超松弛"为何加速？
> Gauss-Seidel 每步走"全步"。若 $A$ 收敛轨迹的曲率允许"超调一点"（$\omega > 1$）穿过最优然后回拉，整体路径更短。**SOR = GS + 动量**——类似 Nesterov 加速梯度。

> [!important] Young 定理的历史地位
> Young 1954 年博士论文给出最优 $\omega^*$ 公式，是数值线性代数史上的里程碑。**首次精确刻画了迭代法的渐近最优速率**——告诉工程师"理论上最快能多快"。

> [!warning] $\omega$ 选错惩罚大
> $\omega$ 偏离最优 $0.1$ 可使收敛步数翻倍。$\omega$ 选错方向（$\omega > 2$ 或 $\omega < 0$）则发散。**鲁棒性差是 SOR 被 CG/GMRES 取代的主要原因**。

> [!info] 现代角色
> SOR 作为独立求解器在生产代码中已少见。但作为**多重网格的平滑器**与**预条件子**仍广泛使用：
> - **SSOR-PCG**：对称 SOR + 共轭梯度；
> - **Multigrid + GS 平滑器**：$O(N)$ 解 Poisson。

$\blacksquare$
