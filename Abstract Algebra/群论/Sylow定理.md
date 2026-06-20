---
title: Sylow 定理
date: 2026-04-11
tags:
  - 抽象代数
  - 群论
  - 有限群
  - Sylow子群
  - 群作用
  - p-群
---

# Sylow 定理

## 预备定义

> [!note] $p$-群
> 设 $p$ 为素数。称有限群 $G$ 为 **$p$-群**（$p$-group），若 $|G| = p^k$ 对某个 $k \geq 0$。
>
> 等价地（由 Lagrange 定理），$G$ 中每个元素的阶都是 $p$ 的幂。

> [!note] Sylow $p$-子群
> 设 $|G| = p^n m$，其中 $p \nmid m$（即 $p^n$ 是 $|G|$ 中 $p$ 的最高幂次）。$G$ 的子群 $P$ 称为 **Sylow $p$-子群**（Sylow $p$-subgroup），若 $|P| = p^n$。
>
> 记 $\operatorname{Syl}_p(G)$ 为所有 Sylow $p$-子群的集合，$n_p = |\operatorname{Syl}_p(G)|$。

> [!note] 群作用与轨道
> 群 $G$ **作用**在集合 $X$ 上，若存在映射 $G \times X \to X$（$(g, x) \mapsto g \cdot x$）满足 $e \cdot x = x$ 和 $(gh) \cdot x = g \cdot (h \cdot x)$。
>
> - **轨道**：$\operatorname{Orb}(x) = \{g \cdot x : g \in G\}$；
> - **稳定子**：$\operatorname{Stab}(x) = \{g \in G : g \cdot x = x\}$；
> - **轨道-稳定子定理**：$|\operatorname{Orb}(x)| = [G : \operatorname{Stab}(x)]$。

> [!note] 共轭
> $G$ 的两个子群 $H, K$ 称为**共轭的**（conjugate），若存在 $g \in G$ 使得 $gHg^{-1} = K$。
>
> $G$ 通过共轭作用在其子群集合上：$g \cdot H = gHg^{-1}$。

> [!note] 正规化子
> 子群 $H \leq G$ 的**正规化子**为
> $$N_G(H) = \{g \in G : gHg^{-1} = H\}.$$
> $H \trianglelefteq N_G(H)$，且 $H \trianglelefteq G$ 当且仅当 $N_G(H) = G$。

> [!abstract] 引理：不动点定理（$p$-群作用的基本性质）
> 设 $P$ 为 $p$-群，$P$ 作用在有限集 $X$ 上。设 $X^P = \{x \in X : g \cdot x = x \;\forall g \in P\}$ 为不动点集。则
> $$|X| \equiv |X^P| \pmod{p}.$$

**证明**：将 $X$ 分解为轨道。每个轨道大小 $|\operatorname{Orb}(x)| = [P : \operatorname{Stab}(x)]$ 整除 $|P| = p^k$，故每个轨道大小为 $p$ 的幂。大小为 $1$ 的轨道恰好构成 $X^P$，大小 $> 1$ 的轨道大小被 $p$ 整除。故 $|X| = |X^P| + \sum(\text{非平凡轨道大小}) \equiv |X^P| \pmod{p}$。$\square$

> [!abstract] 引理：Cauchy 定理
> 设 $G$ 为有限群，素数 $p$ 整除 $|G|$。则 $G$ 中存在阶为 $p$ 的元素。

**证明**：考虑集合 $X = \{(g_1, \ldots, g_p) \in G^p : g_1 g_2 \cdots g_p = e\}$。前 $p-1$ 个元素自由选取，第 $p$ 个由 $g_p = (g_1 \cdots g_{p-1})^{-1}$ 确定，故 $|X| = |G|^{p-1}$，被 $p$ 整除。

循环群 $\mathbb{Z}/p\mathbb{Z}$ 作用在 $X$ 上：将 $(g_1, \ldots, g_p)$ 循环移位为 $(g_2, \ldots, g_p, g_1)$（乘积的循环不变性保证仍在 $X$ 中）。

不动点集 $X^{\mathbb{Z}/p} = \{(g, g, \ldots, g) : g^p = e\}$。由不动点定理，$|X^{\mathbb{Z}/p}| \equiv |X| \equiv 0 \pmod{p}$。又 $(e, e, \ldots, e) \in X^{\mathbb{Z}/p}$，故 $|X^{\mathbb{Z}/p}| \geq p$，即存在 $g \neq e$ 使得 $g^p = e$。$\square$

---

## 定理

设 $G$ 为有限群，$|G| = p^n m$，其中 $p$ 为素数，$n \geq 1$，$p \nmid m$。

**(第一 Sylow 定理)** $G$ 存在 Sylow $p$-子群，即存在阶为 $p^n$ 的子群。

**(第二 Sylow 定理)** $G$ 的任意两个 Sylow $p$-子群共轭。特别地，若 $P$ 为 Sylow $p$-子群且 $Q$ 为任意 $p$-子群，则存在 $g \in G$ 使得 $Q \leq gPg^{-1}$。

**(第三 Sylow 定理)** Sylow $p$-子群的个数 $n_p$ 满足
$$n_p \equiv 1 \pmod{p} \quad \text{且} \quad n_p \mid m.$$

---

## 第一 Sylow 定理的证明：存在性

### 方法：$G$ 作用在大小为 $p^n$ 的子集上

设 $|G| = p^n m$。令 $\mathcal{X}$ 为 $G$ 的所有大小为 $p^n$ 的子集（不要求是子群）的集合：

$$\mathcal{X} = \{S \subseteq G : |S| = p^n\}.$$

$G$ 通过左平移作用在 $\mathcal{X}$ 上：$g \cdot S = gS = \{gs : s \in S\}$。

#### 第一步：$|\mathcal{X}|$ 不被 $p^{n+1}$ 整除

$$|\mathcal{X}| = \binom{p^n m}{p^n}.$$

> [!important] 组合数中 $p$ 的幂次
> 利用恒等式
> $$\binom{p^n m}{p^n} = \prod_{j=0}^{p^n - 1} \frac{p^n m - j}{p^n - j}.$$
> 对每个 $0 \leq j \leq p^n - 1$，$p^n m - j$ 与 $p^n - j$ 中 $p$ 的幂次相同：设 $j = p^a c$（$p \nmid c$），则 $v_p(p^n m - j) = v_p(j) = a = v_p(p^n - j)$（当 $a < n$ 时；$j = 0$ 时两者均为 $v_p(p^n m) = n + v_p(m)$ 和 $v_p(p^n) = n$，商贡献 $v_p(m)$... 实际上精确计算给出）。
>
> 最终 $v_p\!\left(\binom{p^n m}{p^n}\right) = v_p(m) \cdot 0 = 0$... 更直接地：$p \nmid \binom{p^n m}{p^n} / (\text{某个因子})$。

精确论证：$v_p(p^n m - j) = v_p(p^n - j)$ 对一切 $1 \leq j \leq p^n - 1$（因为 $p^n m - j \equiv -j \equiv p^n - j \pmod{p^n}$，而 $v_p(j) < n$）。$j = 0$ 时商为 $m$。故

$$v_p\!\left(\binom{p^n m}{p^n}\right) = v_p(m) = 0.$$

即 $p \nmid |\mathcal{X}|$。$\square$

#### 第二步：存在大小不被 $p^{n+1}$ 整除的轨道

将 $\mathcal{X}$ 分解为 $G$-轨道。由 $p \nmid |\mathcal{X}|$，至少存在一个轨道 $\operatorname{Orb}(S_0)$，其大小不被 $p^{n+1}$ 整除。

由轨道-稳定子定理，$|\operatorname{Orb}(S_0)| = [G : \operatorname{Stab}(S_0)] = |G|/|\operatorname{Stab}(S_0)|$。

设 $H = \operatorname{Stab}(S_0) = \{g \in G : gS_0 = S_0\}$。由 $p \nmid |\operatorname{Orb}(S_0)|$... 更精确地：由 $|\operatorname{Orb}(S_0)| \cdot |H| = p^n m$ 且 $p \nmid |\operatorname{Orb}(S_0)|$（因为如果 $p^{n+1} \mid |\operatorname{Orb}(S_0)|$ 则... 实际上我们只知道 $p \nmid |\mathcal{X}|$ 故至少一个轨道大小不被 $p$ 整除）。

重新论证：由 $p \nmid |\mathcal{X}|$ 和 $|\mathcal{X}| = \sum |\operatorname{Orb}|$，至少一个轨道大小 $p \nmid |\operatorname{Orb}(S_0)|$。由 $|\operatorname{Orb}(S_0)| = p^n m / |H|$，得 $p^n \mid |H|$。$\square$

#### 第三步：$|H| = p^n$

$H = \operatorname{Stab}(S_0)$ 意味着 $gS_0 = S_0$ 对一切 $g \in H$，即 $H$ 左平移保持 $S_0$ 不变。取任意 $s \in S_0$，则 $Hs \subseteq S_0$，故 $|H| \leq |S_0| = p^n$。

结合第二步的 $p^n \mid |H|$，得 $|H| = p^n$。

故 $H$ 是 $G$ 的阶为 $p^n$ 的子群——即 Sylow $p$-子群。$\square$

---

## 第二 Sylow 定理的证明：共轭性

### 任意 $p$-子群包含在某个 Sylow $p$-子群的共轭中

设 $P \in \operatorname{Syl}_p(G)$，$Q$ 为 $G$ 的任意 $p$-子群。令 $Q$ 通过左平移作用在左陪集集合 $G/P = \{gP : g \in G\}$ 上：

$$q \cdot (gP) = (qg)P.$$

#### 第一步：不动点定理的应用

$|G/P| = [G:P] = m$，$p \nmid m$。由 $Q$ 为 $p$-群，不动点定理给出

$$|{(G/P)}^Q| \equiv |G/P| = m \not\equiv 0 \pmod{p}.$$

故至少存在一个不动点 $g_0 P$。$\square$

#### 第二步：不动点意味着包含

$g_0 P$ 是 $Q$ 的不动点意味着 $q(g_0 P) = g_0 P$ 对一切 $q \in Q$，即 $g_0^{-1}Qg_0 \subseteq P$，即

$$Q \leq g_0 P g_0^{-1}. \quad \square$$

#### 第三步：两个 Sylow $p$-子群共轭

若 $Q$ 本身也是 Sylow $p$-子群（$|Q| = p^n$），则 $Q \leq g_0 P g_0^{-1}$ 且 $|Q| = |g_0 P g_0^{-1}| = p^n$，故

$$Q = g_0 P g_0^{-1}. \quad \square$$

---

## 第三 Sylow 定理的证明：计数

### $n_p \mid m$

由第二 Sylow 定理，$G$ 通过共轭在 $\operatorname{Syl}_p(G)$ 上传递地作用。由轨道-稳定子定理，

$$n_p = |\operatorname{Syl}_p(G)| = [G : N_G(P)]$$

对任意 $P \in \operatorname{Syl}_p(G)$。由 $P \leq N_G(P)$，$n_p = [G:N_G(P)]$ 整除 $[G:P] = m$。$\square$

### $n_p \equiv 1 \pmod{p}$

固定 $P \in \operatorname{Syl}_p(G)$，令 $P$ 通过共轭作用在 $\operatorname{Syl}_p(G)$ 上：$g \cdot Q = gQg^{-1}$。

由不动点定理：

$$n_p \equiv |\operatorname{Syl}_p(G)^P| \pmod{p}.$$

**断言**：$\operatorname{Syl}_p(G)^P = \{P\}$，即 $P$ 是自身共轭作用下的唯一不动点。

**证明**：设 $Q \in \operatorname{Syl}_p(G)$ 是 $P$-不动点，即 $gQg^{-1} = Q$ 对一切 $g \in P$，即 $P \leq N_G(Q)$。

在 $N_G(Q)$ 中，$P$ 和 $Q$ 都是 Sylow $p$-子群（$|P| = |Q| = p^n$，且 $p^n$ 是 $|N_G(Q)|$ 中 $p$ 的最高幂次，因为 $N_G(Q) \leq G$）。

由第二 Sylow 定理应用于 $N_G(Q)$：$P$ 和 $Q$ 在 $N_G(Q)$ 中共轭。但 $Q \trianglelefteq N_G(Q)$（$Q$ 在其正规化子中正规），故 $Q$ 是 $N_G(Q)$ 中唯一的与 $Q$ 共轭的子群，即 $P = Q$。$\square$

故 $n_p \equiv |\{P\}| = 1 \pmod{p}$。$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 三条 Sylow 定理的证明统一于一个方法：**群作用 + $p$-群的不动点定理**。
>
> | Sylow 定理 | 作用空间 | 谁在作用 | 关键推论 |
> |-----------|---------|---------|---------|
> | 第一（存在性） | $\binom{G}{p^n}$（大小为 $p^n$ 的子集） | $G$ 左平移 | $p \nmid |\mathcal{X}|$ → 存在小轨道 → 稳定子即为 Sylow 子群 |
> | 第二（共轭性） | $G/P$（左陪集） | $p$-子群 $Q$ | $p \nmid m$ → 不动点存在 → $Q \leq gPg^{-1}$ |
> | 第三（$n_p \equiv 1$） | $\operatorname{Syl}_p(G)$ | $P$ 共轭 | 不动点仅 $P$ 自身 → $n_p \equiv 1 \pmod{p}$ |
>
> 核心工具是**不动点定理**（$|X| \equiv |X^P| \pmod{p}$），它将模 $p$ 的算术约束注入群的结构理论。

> [!warning] 应用与推论
> - **分类小阶群**：Sylow 定理是分类低阶群的主力工具。例如，$|G| = 15 = 3 \times 5$：$n_3 \mid 5$ 且 $n_3 \equiv 1\!\pmod{3}$，故 $n_3 = 1$；$n_5 \mid 3$ 且 $n_5 \equiv 1\!\pmod{5}$，故 $n_5 = 1$。Sylow 子群均正规，$G \cong \mathbb{Z}/3 \times \mathbb{Z}/5 \cong \mathbb{Z}/15$。
> - **正规 Sylow 子群**：$n_p = 1$ 当且仅当唯一的 Sylow $p$-子群正规于 $G$。
> - **非单群判据**：若 $n_p = 1$ 对某个 $p$，则 $G$ 有非平凡正规子群，故不是非 Abel 单群。这用于排除特定阶的单群存在。
> - **推广**：Sylow 定理可推广到无限群的局部有限情形（每个有限生成子群有限）。对一般无限群，Sylow 子群的类比是 $p$-Prüfer 群和 $p$-进整数群。
