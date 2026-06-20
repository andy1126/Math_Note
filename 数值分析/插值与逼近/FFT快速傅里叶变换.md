---
title: FFT 快速傅里叶变换
date: 2026-06-19
tags:
  - 数值分析
  - 插值与逼近
  - FFT
  - DFT
  - Cooley-Tukey
  - 卷积
  - 采样定理
---

# FFT 快速傅里叶变换

离散 Fourier 变换（DFT）是连续 Fourier 变换在采样信号上的离散对应，也是**等距节点三角插值**的系数变换——这把它纳入插值与逼近的主线。直接计算 DFT 需 $O(N^2)$ 次复数乘法；**快速 Fourier 变换（FFT）** 利用单位根的对称性把它降到 $O(N\log N)$，是 20 世纪最有影响的数值算法之一。配合卷积定理，FFT 把时域卷积转为频域逐点乘，使多项式乘法、大数乘法、滤波等运算获得本质加速。本笔记建立 DFT 与三角插值的对应、Cooley–Tukey 分治、卷积定理，并衔接 [[Shannon-Nyquist 采样定理]]。

## 预备定义

> [!note] 定义 1（离散 Fourier 变换 DFT）
> 设序列 $x=(x_0,\dots,x_{N-1})\in\mathbb C^N$，记主单位根 $\omega_N=e^{-2\pi i/N}$。**DFT** 与**逆 DFT** 为
> $$\hat x_k=\sum_{j=0}^{N-1}x_j\,\omega_N^{jk},\qquad x_j=\frac1N\sum_{k=0}^{N-1}\hat x_k\,\omega_N^{-jk}.$$
> 本笔记采用此约定：**正变换无 $1/N$，逆变换带 $1/N$**。

> [!note] 定义 2（循环卷积）
> 序列 $x,y\in\mathbb C^N$ 的循环卷积 $(x\circledast y)_n=\sum_{j=0}^{N-1}x_j\,y_{(n-j)\bmod N}$。**线性卷积**（多项式乘法对应）则不取模，长度 $2N-1$。

> [!note] 定义 3（运算量）
> 直接按定义算全部 $\hat x_k$ 需 $N$ 个和、每个 $N$ 项，共 $O(N^2)$ 次复数乘加。FFT 把它降为 $O(N\log N)$。

> [!abstract] 引理（单位根的性质）
> $\omega_N^N=1$；$\omega_N^{k+N/2}=-\omega_N^{k}$（**对消引理**，$N$ 偶）；$\omega_N^2=\omega_{N/2}$（**折半引理**）。Cooley–Tukey 全靠后两条。

## 定理

> [!important] 定理（DFT、FFT 与卷积）
>
> 1. **DFT = 等距节点三角插值的系数**：以 $x_j$ 为节点 $t_j=2\pi j/N$ 处的值，三角插值多项式
> $$p(t)=\frac1N\sum_{k=0}^{N-1}\hat x_k\,e^{ikt}$$
> 满足 $p(t_j)=x_j$。即 DFT 解的是等距节点上的三角插值（Vandermonde）系统，对应 [[Lagrange插值误差估计|代数插值]] 的三角版本。
>
> 2. **Cooley–Tukey 分治**：当 $N=2M$，长度 $N$ 的 DFT 可拆为偶、奇下标两个长度 $M$ 的 DFT：
> $$\hat x_k=E_k+\omega_N^k O_k,\qquad \hat x_{k+M}=E_k-\omega_N^k O_k\quad(0\le k<M),$$
> 其中 $E,O$ 分别是 $(x_0,x_2,\dots)$、$(x_1,x_3,\dots)$ 的 DFT。递归到 $N=2^m$ 得复杂度 $T(N)=2T(N/2)+O(N)=O(N\log N)$。
>
> 3. **卷积定理**：$\widehat{x\circledast y}=\hat x\odot\hat y$（逐点乘）。故循环卷积可经 FFT 在 $O(N\log N)$ 算出：$x\circledast y=\text{IDFT}(\hat x\odot\hat y)$。

## 证明

### 第一步：DFT 即三角插值系数

设 $p(t)=\tfrac1N\sum_k \hat x_k e^{ikt}$，在 $t_j=2\pi j/N$ 求值：
$$p(t_j)=\frac1N\sum_{k=0}^{N-1}\hat x_k e^{ik\cdot 2\pi j/N}=\frac1N\sum_k\hat x_k\,\omega_N^{-jk}.$$
代入逆 DFT 定义即 $p(t_j)=x_j$。存在唯一性源于等距节点单位根的**正交性**
$$\sum_{j=0}^{N-1}\omega_N^{j(k-l)}=\begin{cases}N,&k\equiv l\!\!\pmod N\\0,&\text{否则}\end{cases}$$
（几何级数求和），它使 Vandermonde 系统可显式求逆。$\square$

### 第二步：Cooley–Tukey 分解

按下标奇偶拆分：
$$\hat x_k=\sum_{j=0}^{N-1}x_j\omega_N^{jk}=\sum_{r=0}^{M-1}x_{2r}\omega_N^{2rk}+\sum_{r=0}^{M-1}x_{2r+1}\omega_N^{(2r+1)k}.$$
由折半引理 $\omega_N^{2rk}=\omega_M^{rk}$：
$$\hat x_k=\underbrace{\sum_r x_{2r}\omega_M^{rk}}_{E_k}+\omega_N^{k}\underbrace{\sum_r x_{2r+1}\omega_M^{rk}}_{O_k}=E_k+\omega_N^k O_k.$$
$E_k,O_k$ 以 $M$ 为周期。对 $k+M$，用对消引理 $\omega_N^{k+M}=-\omega_N^k$、$E_{k+M}=E_k$、$O_{k+M}=O_k$：
$$\hat x_{k+M}=E_k-\omega_N^k O_k.$$
一次"蝶形"运算由 $E_k,O_k$ 同时产出 $\hat x_k,\hat x_{k+M}$。递归 $T(N)=2T(N/2)+cN\Rightarrow T(N)=O(N\log N)$。$\square$

### 第三步：卷积定理

$$\widehat{(x\circledast y)}_k=\sum_{n=0}^{N-1}\Bigl(\sum_{j}x_j y_{(n-j)\bmod N}\Bigr)\omega_N^{nk}.$$
令 $m=(n-j)\bmod N$，换序（利用 $\omega_N^{nk}=\omega_N^{jk}\omega_N^{mk}$，模 $N$ 周期性保证求和范围不变）：
$$=\sum_j x_j\omega_N^{jk}\sum_m y_m\omega_N^{mk}=\hat x_k\,\hat y_k.\ \blacksquare$$
连续背景（采样、混叠）见 [[Shannon-Nyquist 采样定理]]；能量守恒的离散版（Parseval）对应 [[Parseval 定理（Fourier 变换的能量守恒）]]。

## 应用

> [!example] 例题 1：FFT 多项式乘法
> 求 $A(x)=\sum_{k=0}^{n-1}a_kx^k$ 与 $B(x)$ 之积 $C=A\cdot B$（次数 $\le 2n-2$）。步骤：
> 1. **补零**：把 $a,b$ 补零到长度 $L\ge 2n-1$ 且为 $2$ 的幂（防止循环卷积混叠，见警告）。
> 2. **正变换**：$\hat a=\text{FFT}(a)$，$\hat b=\text{FFT}(b)$，各 $O(L\log L)$。
> 3. **逐点乘**：$\hat c_k=\hat a_k\hat b_k$，$O(L)$。
> 4. **逆变换**：$c=\text{IFFT}(\hat c)$，取实部/四舍五入得整系数。
>
> 总复杂度 $O(L\log L)=O(n\log n)$，对比直接卷积 $O(n^2)$。例如 $n=1024$：直接约 $10^6$ 次乘，FFT 约 $L\log_2 L=2048\cdot 11\approx 2.3\times10^4$ 次——快约 **40 倍**，且 $n$ 越大优势越显著。

> [!example] 例题 2：频谱分析与混叠
> 信号 $s(t)=\cos(2\pi\cdot 5t)+\cos(2\pi\cdot 50t)$，采样率 $f_s=128\,$Hz，$N=128$ 点（$1$ 秒）。DFT $\hat s_k$ 的模 $|\hat s_k|$ 在 $k=5$ 与 $k=50$（及共轭镜像 $k=123,78$）出现尖峰，正确识别两个频率分量。
>
> **混叠**：若改用 $f_s=64\,$Hz 采样，则 $50\,$Hz 超过 Nyquist 频率 $32\,$Hz，被混叠到 $64-50=14\,$Hz，频谱在 $k=14$ 处出现**虚假**峰。这是 [[Shannon-Nyquist 采样定理]] 失效（欠采样）的直接数值表现：采样率须 $>2f_{\max}$ 方能无失真还原。

## 证明思路总结

> [!tip] 关键思想
> - **DFT 是等距三角插值的系数**：把 FFT 接回插值主线——代数插值用单项式基（Vandermonde 病态），三角插值用单位根基（正交、良态）。
> - **Cooley–Tukey = 对称性分治**：折半引理 $\omega_N^2=\omega_{N/2}$ 把 $N$ 点 DFT 拆成两个 $N/2$ 点 DFT，对消引理 $\omega_N^{k+N/2}=-\omega_N^k$ 让一次蝶形同时产出两个输出，$O(N^2)\to O(N\log N)$。
> - **卷积定理是 FFT 的威力之源**：时域卷积 = 频域逐点乘，使多项式/大数乘法、滤波、相关都降到 $O(N\log N)$。

> [!warning] 补零与归一化陷阱
> - **线性 vs 循环卷积**：FFT 算的是**循环**卷积。要得长度 $2n-1$ 的线性卷积（多项式乘法），必须补零至 $L\ge 2n-1$，否则尾部回卷（wrap-around）混入低次项。
> - **归一化约定**：$1/N$ 放在正变换、逆变换还是对称分摊（$1/\sqrt N$），全篇必须统一；卷积定理 $\widehat{x\circledast y}=\hat x\hat y$ 在"正变换无 $1/N$"约定下成立，换约定会带入额外 $N$ 因子。
> - 整系数结果应在 IFFT 后四舍五入，以消除浮点舍入残差。

## 相关笔记

- [[Shannon-Nyquist 采样定理]] — DFT 的连续背景，采样与混叠
- [[Parseval 定理（Fourier 变换的能量守恒）]] — 能量守恒的离散对应
- [[Lagrange插值误差估计]] — 代数插值 vs 三角插值的对比
- [[Gauss 求积]] — 同为"选节点"的数值方法
- [[Newton-Cotes 数值积分]] — 等距节点的另一应用
- [[Fourier变换的时移性质]] — 时移 ↔ 频域相位旋转，对应 DFT 的移位定理
