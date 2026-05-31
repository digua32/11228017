# 工商數學作業解答

## 拉普拉斯轉換作業題目：第 (5) 題

**題目：** 用拉普拉斯反轉換求解方程：
$$F(s) = \frac{1 - e^{-3s}}{s(s + 4)}$$

**解答：**

我們可以將 $F(s)$ 拆解為兩部分來處理：

$$F(s) = \frac{1}{s(s+4)} - \frac{e^{-3s}}{s(s+4)}$$

首先，利用**部份分式項展開法 (Partial Fraction Expansion)** 來簡化基本形式：

$$\frac{1}{s(s+4)} = \frac{A}{s} + \frac{B}{s+4}$$

通分後分子相應相等：

$$1 = A(s+4) + Bs$$

* 令 $s = 0 \implies 1 = 4A \implies A = \frac{1}{4}$
* 令 $s = -4 \implies 1 = -4B \implies B = -\frac{1}{4}$

因此：

$$\frac{1}{s(s+4)} = \frac{1}{4}\left(\frac{1}{s} - \frac{1}{s+4}\right)$$

對其進行拉普拉斯反轉換 $\mathcal{L}^{-1}$：

$$\mathcal{L}^{-1}\left\{ \frac{1}{4}\left(\frac{1}{s} - \frac{1}{s+4}\right) \right\} = \frac{1}{4}\left(1 - e^{-4t}\right)u(t)$$

*(其中 $u(t)$ 為單位階梯函數 Unit Step Function)*

接下來處理含有平移因子 $e^{-3s}$ 的第二項。根據**時間平移定理 (Time-Shifting Theorem)**：

$$\mathcal{L}^{-1}\left\{ e^{-as}G(s) \right\} = g(t-a)u(t-a)$$

在此題中 $a = 3$，故：

$$\mathcal{L}^{-1}\left\{ \frac{e^{-3s}}{s(s+4)} \right\} = \frac{1}{4}\left(1 - e^{-4(t-3)}\right)u(t-3)$$

將兩部分合併，即得到最終解 $f(t)$：

$$f(t) = \frac{1}{4}\left(1 - e^{-4t}\right)u(t) - \frac{1}{4}\left(1 - e^{-4(t-3)}\right)u(t-3)$$

---

## 傅立葉變換作業題目：第 (7) 題

**題目：** 令 $f(x) = x + \pi$ ， $x \in [-\pi, \pi]$，求函數 $f$ 之傅立葉級數 (Fourier series)。

**解答：**

在區間 $[-\pi, \pi]$ 上，週期 $2L = 2\pi \implies L = \pi$。傅立葉級數的展開式形式為：

$$f(x) = a_0 + \sum_{n=1}^{\infty} \left( a_n \cos(nx) + b_n \sin(nx) \right)$$

我們可以將 $f(x) = x + \pi$ 拆成兩部分分開計算其係數：

### 1. 計算直流項 $a_0$

$$a_0 = \frac{1}{2\pi} \int_{-\pi}^{\pi} (x + \pi) \, dx$$

因為 $x$ 是奇函數，在對稱區間原點積分為 0；$\pi$ 是偶函數：

$$a_0 = \frac{1}{2\pi} \left[ \frac{1}{2}x^2 + \pi x \right]_{-\pi}^{\pi} = \frac{1}{2\pi} \left( 2\pi^2 \right) = \pi$$

### 2. 計算餘弦項係數 $a_n$ ($n \ge 1$)

$$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \cos(nx) \, dx$$

拆開後：
* $\int_{-\pi}^{\pi} x \cos(nx) \, dx = 0$ （奇函數 $\times$ 偶函數 $=$ 奇函數）
* $\int_{-\pi}^{\pi} \pi \cos(nx) \, dx = 0$ （正弦函數在週期區間積分為 0）

因此：

$$a_n = 0$$

### 3. 計算正弦項係數 $b_n$ ($n \ge 1$)

$$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \sin(nx) \, dx$$

拆開後，$\pi \sin(nx)$ 是奇函數，積分為 0。剩下 $x \sin(nx)$ 為偶函數（奇 $\times$ 奇），可化簡為 2 倍的半區間積分：

$$b_n = \frac{2}{\pi} \int_{0}^{\pi} x \sin(nx) \, dx$$

利用分部積分法，設 $u = x, dv = \sin(nx)dx \implies du = dx, v = -\frac{\cos(nx)}{n}$：

$$b_n = \frac{2}{\pi} \left( \left[ -\frac{x \cos(nx)}{n} \right]_0^{\pi} - \int_{0}^{\pi} -\frac{\cos(nx)}{n} \, dx \right)$$

$$b_n = \frac{2}{\pi} \left( -\frac{\pi \cos(n\pi)}{n} + \left[ \frac{\sin(nx)}{n^2} \right]_0^{\pi} \right)$$

因為 $\sin(n\pi) = 0$ 且 $\cos(n\pi) = (-1)^n$：

$$b_n = \frac{2}{\pi} \left( -\frac{\pi (-1)^n}{n} \right) = -\frac{2(-1)^n}{n} = \frac{2(-1)^{n+1}}{n}$$

### 4. 最終傅立葉級數展開式

將求得的係數帶回原式：

$$f(x) = \pi + \sum_{n=1}^{\infty} \frac{2(-1)^{n+1}}{n} \sin(nx)$$
