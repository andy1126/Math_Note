---
title: Leibniz 交错级数判别法
date: 2026-04-11
tags:
  - 实分析
  - 级数
  - 交错级数
  - 条件收敛
  - Leibniz
---

# Leibniz 交错级数判别法

## 预备定义

> [!note] 交错级数
> 形如 $\sum_{n=0}^\infty (-1)^n a_n$ 的级数（其中 $a_n \geq 0$）称为**交错级数**（alternating series）。相邻两项的符号交替变化。

> [!note] 单调递减序列
> 称非负序列 $(a_n)$ **单调递减**（monotone decreasing），若 $a_{n+1} \leq a_n$ 对所有 $n \geq 0$ 成立。

---

## 定理

设 $(a_n)_{n=0}^\infty$ 为非负实数序列，满足：

**(i)** $(a_n)$ 单调递减：$a_{n+1} \leq a_n$，$\forall\, n \geq 0$；

**(ii)** $a_n \to 0$（$n \to \infty$）。

则交错级数 $\sum_{n=0}^\infty (-1)^n a_n$ 收敛。

此外，若 $S = \sum_{n=0}^\infty (-1)^n a_n$，$S_N = \sum_{n=0}^N (-1)^n a_n$，则有**余项估计**：

$$|S - S_N| \leq a_{N+1}.$$

---

## 证明

### 第一步：偶数部分和单调递增且有上界

考虑偶数部分和 $S_{2m} = \sum_{n=0}^{2m} (-1)^n a_n$。

$$S_{2m+2} - S_{2m} = (-1)^{2m+1} a_{2m+1} + (-1)^{2m+2} a_{2m+2} = -a_{2m+1} + a_{2m+2}.$$

由单调递减 $a_{2m+2} \leq a_{2m+1}$，故

$$S_{2m+2} - S_{2m} = -(a_{2m+1} - a_{2m+2}) \leq 0.$$

即 $(S_{2m})$ **单调递减**。$\quad \cdots (\ast)$

另一方面，将 $S_{2m}$ 配对重写：

$$S_{2m} = a_0 - (a_1 - a_2) - (a_3 - a_4) - \cdots - (a_{2m-1} - a_{2m}).$$

每个括号 $a_{2k-1} - a_{2k} \geq 0$（单调递减），故

$$S_{2m} \leq a_0. \quad \cdots (\star)$$

同时，另一种配对：

$$S_{2m} = (a_0 - a_1) + (a_2 - a_3) + \cdots + (a_{2m-2} - a_{2m-1}) + a_{2m} \geq 0. \quad \cdots (\star\star)$$

综合：$(S_{2m})$ 单调递减、有下界 $0$，由**[[单调有界序列收敛|单调有界定理]]**收敛：

$$S_{2m} \to L \quad (m \to \infty). \quad \cdots (1)$$

$\square$

### 第二步：奇数部分和收敛于同一极限

$$S_{2m+1} = S_{2m} + (-1)^{2m+1} a_{2m+1} = S_{2m} - a_{2m+1}.$$

由 $(1)$ 和条件 (ii)（$a_{2m+1} \to 0$）：

$$S_{2m+1} \to L - 0 = L \quad (m \to \infty). \quad \cdots (2)$$

$\square$

### 第三步：全序列收敛

由 $(1)$ 和 $(2)$，偶数项子列和奇数项子列均收敛于 $L$。由此

$$S_N \to L \quad (N \to \infty),$$

即 $\sum_{n=0}^\infty (-1)^n a_n = L$ 收敛。$\square$

> [!info] 为何两个子列收敛于同一极限蕴含全列收敛
> 对任意 $\varepsilon > 0$，存在 $M_1$ 使得 $m \geq M_1 \implies |S_{2m} - L| < \varepsilon$，存在 $M_2$ 使得 $m \geq M_2 \implies |S_{2m+1} - L| < \varepsilon$。取 $N_0 = \max(2M_1, 2M_2+1)$。对 $N \geq N_0$：若 $N$ 为偶数，$N = 2m \geq 2M_1$，故 $|S_N - L| < \varepsilon$；若 $N$ 为奇数，$N = 2m+1 \geq 2M_2+1$，故 $|S_N - L| < \varepsilon$。

---

### 第四步：余项估计

需证 $|S - S_N| \leq a_{N+1}$。

**情形 1**：$N = 2m$（偶数）。则

$$S - S_{2m} = \sum_{n=2m+1}^\infty (-1)^n a_n = -a_{2m+1} + a_{2m+2} - a_{2m+3} + \cdots$$

将此配对为

$$S - S_{2m} = -(a_{2m+1} - a_{2m+2}) - (a_{2m+3} - a_{2m+4}) - \cdots \leq 0.$$

故 $S \leq S_{2m}$。另一种配对：

$$S - S_{2m} = -a_{2m+1} + (a_{2m+2} - a_{2m+3}) + (a_{2m+4} - a_{2m+5}) + \cdots \geq -a_{2m+1}.$$

因此 $-a_{2m+1} \leq S - S_{2m} \leq 0$，即 $|S - S_{2m}| \leq a_{2m+1} = a_{N+1}$。$\square$

**情形 2**：$N = 2m+1$（奇数）。则

$$S - S_{2m+1} = a_{2m+2} - a_{2m+3} + a_{2m+4} - \cdots$$

配对得 $0 \leq S - S_{2m+1} \leq a_{2m+2} = a_{N+1}$。$\square$

两种情形均有 $|S - S_N| \leq a_{N+1}$。

---

### 结论

1. $\sum_{n=0}^\infty (-1)^n a_n$ 收敛。 ✓
2. $|S - S_N| \leq a_{N+1}$。 ✓

$\blacksquare$

---

## 证明思路总结

> [!tip] 关键思想
> 证明的核心是**奇偶分列 + 单调有界定理**：
>
> - 偶数部分和 $(S_{2m})$ 单调递减且有下界（通过交替配对看出）→ 收敛于 $L$；
> - 奇数部分和 $S_{2m+1} = S_{2m} - a_{2m+1}$，由 $a_n \to 0$ 知也收敛于 $L$；
> - 两个子列覆盖了所有 $N$，故 $S_N \to L$。
>
> 余项估计 $|S - S_N| \leq a_{N+1}$ 同样来自配对：截断后的尾部交错和被第一项控制。
>
> 直觉上，交错级数的部分和在 $L$ 的两侧"振荡趋近"：
> $$S_0 \geq S_2 \geq S_4 \geq \cdots \geq L \geq \cdots \geq S_5 \geq S_3 \geq S_1.$$

> [!warning] 条件收敛的典型例子
> 交错调和级数 $\sum_{n=1}^\infty \frac{(-1)^{n+1}}{n} = 1 - \frac{1}{2} + \frac{1}{3} - \frac{1}{4} + \cdots = \ln 2$ 满足两个条件（$1/n$ 递减趋于零），故收敛。但 $\sum |(-1)^{n+1}/n| = \sum 1/n$ 发散——这是**条件收敛**（convergent but not absolutely convergent）的经典例子。
>
> 由 [[绝对收敛判别法|绝对收敛判别法]]，绝对收敛蕴含收敛。反之不然——Leibniz 判别法正是处理这类"靠符号消去而收敛"的级数的工具。
>
> **两个条件缺一不可**：
> - 去掉 $a_n \to 0$：$\sum (-1)^n \cdot 1$ 发散（部分和在 $0$ 和 $1$ 之间振荡）。
> - 去掉单调性：存在 $a_n \to 0$ 但 $\sum (-1)^n a_n$ 发散的反例（需精心构造非单调的 $a_n$ 使得部分和无界）。
