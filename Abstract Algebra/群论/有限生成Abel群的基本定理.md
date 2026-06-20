---
title: 有限生成 Abel 群的基本定理
date: 2026-04-11
tags:
  - 抽象代数
  - 群论
  - Abel群
  - 有限生成群
  - Smith标准形
  - 不变因子
  - 初等因子
---

# 有限生成 Abel 群的基本定理

## 预备定义

> [!note] 有限生成 Abel 群
> Abel 群 $G$（加法记号）称为**有限生成的**（finitely generated），若存在有限子集 $\{g_1, \ldots, g_k\} \subset G$，使得
> $$G = \langle g_1, \ldots, g_k \rangle = \left\{\sum_{i=1}^k n_i g_i : n_i \in \mathbb{Z}\right\}.$$

> [!note] 自由 Abel 群与关系
> **秩 $k$ 的自由 Abel 群**为 $\mathbb{Z}^k = \mathbb{Z} \oplus \cdots \oplus \mathbb{Z}$（$k$ 个副本）。
>
> 任何有限生成 Abel 群 $G$ 可表示为
> $$G \cong \mathbb{Z}^k / H,$$
> 其中 $H$ 为 $\mathbb{Z}^k$ 的子群（**关系子群**）。选取 $H$ 的生成元 $h_1, \ldots, h_l$，将它们按列排成**关系矩阵** $A \in \mathbb{Z}^{k \times l}$。

> [!note] Smith 标准形
> 设 $A \in \mathbb{Z}^{k \times l}$ 为整数矩阵。通过以下三种**初等行列变换**（对应 $\mathbb{Z}^k$ 和 $\mathbb{Z}^l$ 的基变换）：
> 1. 交换两行（或两列）；
> 2. 将某行（或某列）乘以 $-1$；
> 3. 将某行的整数倍加到另一行（或列类似），
>
> $A$ 可化为**Smith 标准形**：
> $$S = PAQ = \operatorname{diag}(d_1, d_2, \ldots, d_r, 0, \ldots, 0),$$
> 其中 $P \in GL_k(\mathbb{Z})$，$Q \in GL_l(\mathbb{Z})$，$d_i \geq 1$，且 $d_1 \mid d_2 \mid \cdots \mid d_r$。
>
> $d_1, \ldots, d_r$ 称为 $A$ 的**不变因子**（invariant factors），由 $A$ 唯一确定。

> [!abstract] 引理：$\mathbb{Z}^n$ 的子群仍是自由的
> $\mathbb{Z}^n$ 的任何子群 $H$ 同构于 $\mathbb{Z}^m$（$m \leq n$），即 $H$ 是秩 $\leq n$ 的自由 Abel 群。

**证明概要**：对 $n$ 归纳。$n = 1$ 时 $H \leq \mathbb{Z}$ 为 $d\mathbb{Z}$（$\cong \mathbb{Z}$ 或 $\{0\}$）。一般地，投影 $\pi: \mathbb{Z}^n \to \mathbb{Z}$（取最后一个坐标），$\pi(H) = d\mathbb{Z}$。取 $h \in H$ 使得 $\pi(h) = d$。则 $H = (H \cap \ker\pi) \oplus \mathbb{Z}h$，$\ker\pi \cong \mathbb{Z}^{n-1}$，由归纳假设 $H \cap \ker\pi$ 自由。$\square$

---

## 定理

### 不变因子形式

每个有限生成 Abel 群 $G$ 同构于

$$G \cong \mathbb{Z}^r \oplus \mathbb{Z}/d_1\mathbb{Z} \oplus \mathbb{Z}/d_2\mathbb{Z} \oplus \cdots \oplus \mathbb{Z}/d_s\mathbb{Z},$$

其中 $r \geq 0$，$d_i \geq 2$，且 $d_1 \mid d_2 \mid \cdots \mid d_s$。

$r$ 称为**自由秩**（free rank），$d_1, \ldots, d_s$ 称为**不变因子**。它们由 $G$ 唯一确定。

### 初等因子形式

等价地，

$$G \cong \mathbb{Z}^r \oplus \bigoplus_{i} \mathbb{Z}/p_i^{a_i}\mathbb{Z},$$

其中 $p_i$ 为素数，$a_i \geq 1$。素数幂 $p_i^{a_i}$（含重复）称为**初等因子**（elementary divisors），由 $G$ 唯一确定（至多排列顺序）。

> [!info] 两种形式的等价性
> 由中国剩余定理，$\mathbb{Z}/d\mathbb{Z} \cong \bigoplus_{p^a \| d} \mathbb{Z}/p^a\mathbb{Z}$（其中 $p^a \| d$ 表示 $p^a$ 是 $d$ 的素幂因子）。故不变因子形式与初等因子形式可互相转化。

---

## 存在性的证明

### 第一步：表示为商群

$G$ 有限生成，设有 $k$ 个生成元。定义满同态 $\pi: \mathbb{Z}^k \twoheadrightarrow G$（将标准基映到生成元）。令 $H = \ker\pi$，由第一同构定理：

$$G \cong \mathbb{Z}^k / H. \quad \cdots (\ast)$$

由引理，$H \cong \mathbb{Z}^m$（$m \leq k$）。选取 $H$ 的基 $h_1, \ldots, h_m$，关系矩阵为 $A \in \mathbb{Z}^{k \times m}$（$h_j$ 为第 $j$ 列）。$\square$

### 第二步：Smith 标准形化简

将 $A$ 化为 Smith 标准形 $S = PAQ = \operatorname{diag}(d_1, \ldots, d_r, 0, \ldots, 0)$，其中 $P \in GL_k(\mathbb{Z})$，$Q \in GL_m(\mathbb{Z})$，$d_1 \mid d_2 \mid \cdots \mid d_r$，$d_i \geq 1$。

$P$ 对应 $\mathbb{Z}^k$ 的基变换（新基 $e_1', \ldots, e_k'$），$Q$ 对应 $H$ 的基变换。在新基下，$H$ 由列 $d_1 e_1', \ldots, d_r e_r'$ 生成。$\square$

### 第三步：直和分解

在新基下：

$$\mathbb{Z}^k = \mathbb{Z} e_1' \oplus \cdots \oplus \mathbb{Z} e_k', \quad H = \mathbb{Z}(d_1 e_1') \oplus \cdots \oplus \mathbb{Z}(d_r e_r').$$

商群逐分量计算：

$$G \cong \mathbb{Z}^k / H \cong \frac{\mathbb{Z} e_1'}{\mathbb{Z}(d_1 e_1')} \oplus \cdots \oplus \frac{\mathbb{Z} e_r'}{\mathbb{Z}(d_r e_r')} \oplus \mathbb{Z} e_{r+1}' \oplus \cdots \oplus \mathbb{Z} e_k'.$$

即

$$G \cong \mathbb{Z}/d_1\mathbb{Z} \oplus \cdots \oplus \mathbb{Z}/d_r\mathbb{Z} \oplus \mathbb{Z}^{k-r}. \quad \cdots (\star)$$

去掉 $d_i = 1$ 的项（$\mathbb{Z}/1\mathbb{Z} = 0$），剩余的 $d_i \geq 2$ 即为不变因子，$k - r$ 即为自由秩。$\square$

---

## 唯一性的证明

### 自由秩 $r$ 的唯一性

**$r = \dim_{\mathbb{Q}}(G \otimes_{\mathbb{Z}} \mathbb{Q})$**。

对分解式张量 $\mathbb{Q}$：$\mathbb{Z} \otimes \mathbb{Q} \cong \mathbb{Q}$，$\mathbb{Z}/d\mathbb{Z} \otimes \mathbb{Q} = 0$（因 $d$ 在 $\mathbb{Q}$ 中可逆）。故

$$G \otimes_{\mathbb{Z}} \mathbb{Q} \cong \mathbb{Q}^r.$$

$r$ 由 $G$ 唯一确定。$\square$

### 初等因子的唯一性

对每个素数 $p$ 和 $k \geq 1$，定义

$$G[p^k] = \{g \in G : p^k g = 0\}, \quad U_p^{(k)} = p^{k-1}G[p^k] / p^k G[p^{k+1}].$$

> [!important] 用 $p$-挠提取初等因子
> 更初等的方法：对有限 Abel 群 $G$（自由部分已去除），考虑 $p$-初等分量
> $$G_p = \{g \in G : p^N g = 0 \text{ 对某个 } N\}.$$
> 由中国剩余定理，$G = \bigoplus_p G_p$。故只需证明每个 $p$-群 $G_p$ 的分解唯一。

**$p$-群的唯一性**：设 $G_p \cong \bigoplus_{i=1}^s \mathbb{Z}/p^{a_i}\mathbb{Z}$，$a_1 \leq a_2 \leq \cdots \leq a_s$。

定义 $\varphi_k = \dim_{\mathbb{F}_p}(p^{k-1}G_p / p^k G_p)$（将 $p^{k-1}G_p / p^k G_p$ 视为 $\mathbb{F}_p$-向量空间）。

对 $\mathbb{Z}/p^a\mathbb{Z}$ 的直和，直接计算：

$$\varphi_k = |\{i : a_i \geq k\}|.$$

> [!info] 计算细节
> 在 $\mathbb{Z}/p^a\mathbb{Z}$ 中，$p^{k-1}(\mathbb{Z}/p^a) = p^{k-1}\mathbb{Z}/p^a\mathbb{Z}$，当 $k \leq a$ 时同构于 $\mathbb{Z}/p^{a-k+1}\mathbb{Z}$；当 $k > a$ 时为零。故 $p^{k-1}(\mathbb{Z}/p^a)/p^k(\mathbb{Z}/p^a) \cong \mathbb{Z}/p\mathbb{Z}$ 当 $k \leq a$，$= 0$ 当 $k > a$。对直和逐项计算即得。

由 $\varphi_k$ 的值可逐步恢复 $a_i$：

$$s = \varphi_1, \quad |\{i : a_i \geq k\}| = \varphi_k, \quad \text{故 } |\{i : a_i = k\}| = \varphi_k - \varphi_{k+1}.$$

$\varphi_k$ 仅依赖 $G_p$ 的群结构（不依赖分解的选取），故初等因子 $p^{a_i}$ 由 $G$ 唯一确定。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 本定理的证明分两大块：
>
> **存在性（Smith 标准形）**：
> $$G \cong \mathbb{Z}^k/H \;\xrightarrow{\text{Smith 标准形}}\; \bigoplus \mathbb{Z}/d_i\mathbb{Z} \oplus \mathbb{Z}^{k-r}.$$
> 核心是将关系矩阵 $A$ 通过整数初等变换对角化。对角元素 $d_1 \mid d_2 \mid \cdots \mid d_r$ 就是不变因子。整个过程是**构造性的**——给定生成元和关系，Smith 标准形算法直接计算出分解。
>
> **唯一性（不变量提取）**：
> - 自由秩 $r$：张量 $\mathbb{Q}$ 杀死所有挠，剩余 $\mathbb{Q}^r$；
> - 初等因子 $p^{a_i}$：通过 $\varphi_k = \dim(p^{k-1}G_p/p^kG_p)$ 逐层"剥离"，恢复每个素数幂的重数。
>
> 本质上，$\mathbb{Z}$-模的分类归结为**整数矩阵在初等变换下的标准形**，这与线性代数中矩阵对角化的思想完全平行。

> [!warning] 推广与联系
> - **主理想整环上的有限生成模**：本定理是其特殊情形（$R = \mathbb{Z}$）。一般地，PID $R$ 上的有限生成模 $M \cong R^r \oplus \bigoplus R/(d_i)$，$d_1 \mid d_2 \mid \cdots$。当 $R = F[x]$（多项式环）时，这给出**有理标准形**和 **Jordan 标准形**。
> - **有限 Abel 群的计数**：阶为 $n$ 的 Abel 群的同构类个数等于 $n$ 的各素幂因子的分拆数之积。例如，阶 $36 = 2^2 \cdot 3^2$ 的 Abel 群有 $p(2) \times p(2) = 2 \times 2 = 4$ 种：$\mathbb{Z}/36$，$\mathbb{Z}/2 \oplus \mathbb{Z}/18$，$\mathbb{Z}/6 \oplus \mathbb{Z}/6$，$\mathbb{Z}/2 \oplus \mathbb{Z}/2 \oplus \mathbb{Z}/9$... 实际上需仔细枚举。
> - **非 Abel 情形**：有限生成非 Abel 群没有如此简洁的分类。甚至有限 $p$-群的分类在阶增大时迅速变得极其复杂（wild classification problem）。
