# 工商數學作業解答

## 拉普拉斯轉換作業題目：第 (5) 題

**題目：**
用拉普拉斯反轉換求解方程：
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

亦可寫成分段函數的形式（當 $t \ge 0$）：
$$f(t) = \begin{cases} \frac{1}{4}\left(1 - e^{-4t}\right), & 0 \le t < 3 \\ \frac{1}{4}\left(e^{-4(t-3)} - e^{-4t}\right), & t \ge 3 \end{cases}$$

---

## 傅立葉變換作業題目：第 (7) 題

**題目：**
令 $f(x) = x + \pi$ ， $x \in [-\pi, \pi]$，求函數 $f$ 之傅立葉級數 (Fourier series)。

**解答：**

在區間 $[-\pi, \pi]$ 上，週期 $2L = 2\pi \implies L = \pi$。傅立葉級數的展開式形式為：
$$f(x) = a_0 + \sum_{n=1}^{\infty} \left( a_n \cos(nx) + b_n \sin(nx) \right)$$

我們可以將 $f(x) = x + \pi$ 拆成兩部分分開計算其係數，或者直接帶入公式求解：

### 1. 計算直流項 $a_0$
$$a_0 = \frac{1}{2\pi} \int_{-\pi}^{\pi} f(x) \, dx = \frac{1}{2\pi} \int_{-\pi}^{\pi} (x + \pi) \, dx$$
因為 $x$ 是奇函數，在對稱區間原點積分為 0；$\pi$ 是偶函數：
$$a_0 = \frac{1}{2\pi} \left[ \frac{1}{2}x^2 + \pi x \right]_{-\pi}^{\pi} = \frac{1}{2\pi} \left( 2\pi^2 \right) = \pi$$

### 2. 計算餘弦項係數 $a_n$ ($n \ge 1$)
$$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \cos(nx) \, dx = \frac{1}{\pi} \int_{-\pi}^{\pi} x \cos(nx) \, dx + \frac{1}{\pi} \int_{-\pi}^{\pi} \pi \cos(nx) \, dx$$
* 第一項：$x \cos(nx)$ 為（奇 $\times$ 偶 $=$ 奇函數），積分結果為 0。
* 第二項：$\int_{-\pi}^{\pi} \cos(nx) \, dx = \left[ \frac{\sin(nx)}{n} \right]_{-\pi}^{\pi} = 0$。

因此，$a_n = 0$。

### 3. 計算正弦項係數 $b_n$ ($n \ge 1$)
$$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \sin(nx) \, dx = \frac{1}{\pi} \int_{-\pi}^{\pi} x \sin(nx) \, dx + \frac{1}{\pi} \int_{-\pi}^{\pi} \pi \sin(nx) \, dx$$
* 第二項：$\pi \sin(nx)$ 為奇函數，積分結果為 0。
* 第一項：$x \sin(nx)$ 為（奇 $\times$ 奇 $=$ 偶函數），可簡化為 2 倍的半區間積分：
$$b_n = \frac{2}{\pi} \int_{0}^{\pi} x \sin(nx) \, dx$$

利用分部積分法 (Integration by parts)，設 $u = x, dv = \sin(nx)dx \implies du = dx, v = -\frac{\cos(nx)}{n}$：
$$b_n = \frac{2}{\pi} \left[ \left. -\frac{x \cos(nx)}{n} \right|_0^{\pi} - \int_{0}^{\pi} \left(-\frac{\cos(nx)}{n}\right) \, dx \right]$$
$$b_n = \frac{2}{\pi} \left[ -\frac{\pi \cos(n\pi)}{n} + 0 + \left. \frac{\sin(nx)}{n^2} \right|_0^{\pi} \right]$$

因為 $\sin(n\pi) = 0$ 且 $\cos(n\pi) = (-1)^n$：
$$b_n = \frac{2}{\pi} \left[ -\frac{\pi (-1)^n}{n} \right] = -\frac{2(-1)^n}{n} = \frac{2(-1)^{n+1}}{n}$$

### 4. 最終傅立葉級數展開式
將求得的係數帶回原式：
$$f(x) = \pi + \sum_{n=1}^{\infty} \frac{2(-1)^{n+1}}{n} \sin(nx)$$

展開前幾項得：
$$f(x) = \pi + 2 \left( \sin x - \frac{1}{2}\sin(2x) + \frac{1}{3}\sin(3x) - \frac{1}{4}\sin(4x) + \cdots \right)$$
* **求 $B$：** 令 $s = -4$，得 $B = \left. \frac{1}{s} \right|_{s=-4} = -\frac{1}{4}$

因此：
$$F(s) = \frac{1}{4} \cdot \frac{1}{s} - \frac{1}{4} \cdot \frac{1}{s+4}$$

對其進行拉普拉斯反轉換，可得基礎函數 $f(t)$：
$$f(t) = \mathcal{L}^{-1} \left\{ \frac{1}{4} \cdot \frac{1}{s} - \frac{1}{4} \cdot \frac{1}{s+4} \right\} = \frac{1}{4} - \frac{1}{4}e^{-4t} = \frac{1}{4}\left(1 - e^{-4t}\right)$$
*(註：此處預設 $t \ge 0$，或可寫成 $\frac{1}{4}(1 - e^{-4t})u(t)$，其中 $u(t)$ 為單位階梯函數)*

#### Step 3: 應用時間平移定理 (Time-Shifting Theorem)
根據拉普拉斯轉換的時間平移定理：
$$\mathcal{L}^{-1} \left\{ e^{-as} F(s) \right\} = f(t-a) \cdot u(t-a)$$

在第二項中，$a = 3$，因此：
$$\mathcal{L}^{-1} \left\{ e^{-3s} \cdot \frac{1}{s(s+4)} \right\} = f(t-3) \cdot u(t-3)$$

將先前求得的 $f(t)$ 代入：
$$f(t-3) = \frac{1}{4}\left(1 - e^{-4(t-3)}\right)$$

#### Step 4: 組合最終答案
將兩項的結果相減，得到最終的拉普拉斯反轉換結果：
$$y(t) = \frac{1}{4}\left(1 - e^{-4t}\right)u(t) - \frac{1}{4}\left(1 - e^{-4(t-3)}\right)u(t-3)$$

亦可寫成分段函數的形式：
$$y(t) = 
\begin{cases} 
0, & t < 0 \\\\[2ex]
\dfrac{1}{4}\left(1 - e^{-4t}\right), & 0 \le t < 3 \\\\[2ex]
\dfrac{1}{4}\left(e^{-4(t-3)} - e^{-4t}\right), & t \ge 3
\end{cases}$$

---

## 傅立葉變換作業題目：(7)（地方特考）

### 題目描述
> **令 $f(x) = x + \pi$ ， $x \in [-\pi, \pi]$，求函數 $f(x)$ 之傅立葉級數 (Fourier series)。**

### 求解步驟

#### Step 1: 傅立葉級數公式定義
在區間 $[-\pi, \pi]$ 上，函數 $f(x)$ 的傅立葉級數展開式為：
$$f(x) = \frac{a_0}{2} + \sum_{n=1}^{\infty} \left( a_n \cos(nx) + b_n \sin(nx) \right)$$

其中各係數公式為：
* $$a_0 = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \, dx$$
* $$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \cos(nx) \, dx$$
* $$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \sin(nx) \, dx$$

#### Step 2: 計算 $a_0$
將 $f(x) = x + \pi$ 代入：
$$a_0 = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \, dx$$

由於 $x$ 是奇函數（在對稱區間 $[-\pi, \pi]$ 積分為 0），$\pi$ 是偶函數，式子可以簡化為：
$$a_0 = \frac{1}{\pi} \left[ \int_{-\pi}^{\pi} x \, dx + \int_{-\pi}^{\pi} \pi \, dx \right] = \frac{1}{\pi} \left[ 0 + \pi \cdot (2\pi) \right] = 2\pi$$

所以，直流項（常數項）為：
$$\frac{a_0}{2} = \pi$$

#### Step 3: 計算 $a_n$ ($n \ge 1$)
$$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \cos(nx) \, dx = \frac{1}{\pi} \int_{-\pi}^{\pi} x \cos(nx) \, dx + \frac{1}{\pi} \int_{-\pi}^{\pi} \pi \cos(nx) \, dx$$

* 第一項：$x$（奇函數）$\times \cos(nx)$（偶函數）$=$ 奇函數，在對稱區間積分結果為 $0$。
* 第二項：$\frac{1}{\pi} \cdot \pi \int_{-\pi}^{\pi} \cos(nx) \, dx = \left[ \frac{\sin(nx)}{n} \right]_{-\pi}^{\pi} = \frac{\sin(n\pi) - \sin(-n\pi)}{n} = 0$（因為當 $n$ 為整數時，$\sin(n\pi) = 0$）。

因此：
$$a_n = 0$$

#### Step 4: 計算 $b_n$ ($n \ge 1$)
$$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \sin(nx) \, dx = \frac{1}{\pi} \int_{-\pi}^{\pi} x \sin(nx) \, dx + \frac{1}{\pi} \int_{-\pi}^{\pi} \pi \sin(nx) \, dx$$

* 第二項：$\pi$（偶函數）$\times \sin(nx)$（奇函數）$=$ 奇函數，在對稱區間積分結果為 $0$。
* 第一項：$x$（奇函數）$\times \sin(nx)$（奇函數）$=$ 偶函數，可以簡化為 $0$ 到 $\pi$ 積分的 2 倍：
    $$b_n = \frac{2}{\pi} \int_{0}^{\pi} x \sin(nx) \, dx$$

使用分部積分法 (Integration by parts)，令 $u = x \implies du = dx$， $dv = \sin(nx)dx \implies v = -\frac{\cos(nx)}{n}$：
$$\int_{0}^{\pi} x \sin(nx) \, dx = \left[ -x \frac{\cos(nx)}{n} \right]_{0}^{\pi} - \int_{0}^{\pi} \left( -\frac{\cos(nx)}{n} \right) \, dx$$
$$= \left( -\pi \frac{\cos(n\pi)}{n} - 0 \right) + \left[ \frac{\sin(nx)}{n^2} \right]_{0}^{\pi}$$
$$= -\frac{\pi (-1)^n}{n} + 0 = -\frac{\pi (-1)^n}{n}$$

將此結果帶回 $b_n$：
$$b_n = \frac{2}{\pi} \cdot \left( -\frac{\pi (-1)^n}{n} \right) = -\frac{2(-1)^n}{n} = \frac{2 \cdot (-1)^{n+1}}{n}$$

我們可以列出前幾項看看：
* $b_1 = 2$
* $b_2 = -1$
* $b_3 = \frac{2}{3}$
* $b_4 = -\frac{1}{2}$

#### Step 5: 組合最終答案
將求得的係數 $\frac{a_0}{2} = \pi$，$a_n = 0$，$b_n = \frac{2(-1)^{n+1}}{n}$ 代入展開式：
$$f(x) = \pi + \sum_{n=1}^{\infty} \frac{2(-1)^{n+1}}{n} \sin(nx)$$

展開前幾項形式為：
$$f(x) = \pi + 2 \left( \sin(x) - \frac{1}{2}\sin(2x) + \frac{1}{3}\sin(3x) - \frac{1}{4}\sin(4x) + \cdots \right)$$
* **求 $B$：** 令 $s = -4$，得 $B = \left. \frac{1}{s} \right|_{s=-4} = -\frac{1}{4}$

因此：
$$F(s) = \frac{1}{4} \cdot \frac{1}{s} - \frac{1}{4} \cdot \frac{1}{s+4}$$

對其進行拉普拉斯反轉換，可得基礎函數 $f(t)$：
$$f(t) = \mathcal{L}^{-1} \left[ \frac{1}{4} \cdot \frac{1}{s} - \frac{1}{4} \cdot \frac{1}{s+4} \right] = \frac{1}{4} - \frac{1}{4}e^{-4t} = \frac{1}{4}(1 - e^{-4t})$$
*(註：此處預設 $t \ge 0$，或可寫成 $\frac{1}{4}(1 - e^{-4t})u(t)$，其中 $u(t)$ 為單位梯度函數)*

#### Step 3: 應用時間平移定理 (時移定理)
根據拉普拉斯轉換的時間平移定理：
$$\mathcal{L}^{-1} \left[ e^{-as} F(s) \right] = f(t-a) \cdot u(t-a)$$

在第二項中，$a = 3$，因此：
$$\mathcal{L}^{-1} \left[ e^{-3s} \cdot \frac{1}{s(s+4)} \right] = f(t-3) \cdot u(t-3)$$

將先前求得的 $f(t)$ 代入：
$$f(t-3) = \frac{1}{4}(1 - e^{-4(t-3)})$$

#### Step 4: 組合最終答案
將裝兩項的結果相減，得到最終的拉普拉斯反轉換結果：
$$y(t) = \frac{1}{4}(1 - e^{-4t})u(t) - \frac{1}{4}(1 - e^{-4(t-3)})u(t-3)$$

也可以寫成分段函數的形式：
$$y(t) = \begin{cases} 0, & t < 0 \\ \dfrac{1}{4}(1 - e^{-4t}), & 0 \le t < 3 \\ \dfrac{1}{4}(e^{-4(t-3)} - e^{-4t}), & t \ge 3 \end{cases}$$

---

## 傳立葉變換作業題目：(7)（地方特考）

### 題目描述
> **令 $f(x) = x + \pi$ ， $x \in [-\pi, \pi]$，求函數 $f(x)$ 之傳立葉級數 (Fourier series)。**

### 求解步驟

#### Step 1: 傳立葉級數公式定義
在區間 $[-\pi, \pi]$ 上，函數 $f(x)$ 的傳立葉級數展開式為：
$$f(x) = \frac{a_0}{2} + \sum_{n=1}^{\infty} ( a_n \cos(nx) + b_n \sin(nx) )$$

其中各係數公式為：
* $$a_0 = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \, dx$$
* $$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \cos(nx) \, dx$$
* $$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \sin(nx) \, dx$$

#### Step 2: 計算 $a_0$
將 $f(x) = x + \pi$ 代入：
$$a_0 = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \, dx$$

由於 $x$ 是奇函數（在對稱區間 $[-\pi, \pi]$ 積分為 0），$\pi$ 是偶函數，式子可以簡化為：
$$a_0 = \frac{1}{\pi} \left[ \int_{-\pi}^{\pi} x \, dx + \int_{-\pi}^{\pi} \pi \, dx \right] = \frac{1}{\pi} [ 0 + \pi \cdot (2\pi) ] = 2\pi$$

所以，直流項（常數項）為：
$$\frac{a_0}{2} = \pi$$

#### Step 3: 計算 $a_n$ ($n \ge 1$)
$$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \cos(nx) \, dx = \frac{1}{\pi} \int_{-\pi}^{\pi} x \cos(nx) \, dx + \frac{1}{\pi} \int_{-\pi}^{\pi} \pi \cos(nx) \, dx$$

* 第一項：$x$（奇函數）$\times \cos(nx)$（偶函數）$=$ 奇函數，在對稱區間積分結果為 $0$。
* 第二項：$\frac{1}{\pi} \cdot \pi \int_{-\pi}^{\pi} \cos(nx) \, dx = \left[ \frac{\sin(nx)}{n} \right]_{-\pi}^{\pi} = \frac{\sin(n\pi) - \sin(-n\pi)}{n} = 0$（因為當 $n$ 為整數時，$\sin(n\pi) = 0$）。

因此：
$$a_n = 0$$

#### Step 4: 計算 $b_n$ ($n \ge 1$)
$$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \sin(nx) \, dx = \frac{1}{\pi} \int_{-\pi}^{\pi} x \sin(nx) \, dx + \frac{1}{\pi} \int_{-\pi}^{\pi} \pi \sin(nx) \, dx$$

* 第二項：$\pi$（偶函數）$\times \sin(nx)$（奇函數）$=$ 奇函數，在對稱區間積分結果為 $0$。
* 第一項：$x$（奇函數）$\times \sin(nx)$（奇函數）$=$ 偶函數，可以簡化為 $0$ 到 $\pi$ 積分的 2倍：
    $$b_n = \frac{2}{\pi} \int_{0}^{\pi} x \sin(nx) \, dx$$

使用分部積分法 (Integration by parts)，令 $u = x \implies du = dx$， $dv = \sin(nx)dx \implies v = -\frac{\cos(nx)}{n}$：
$$\int_{0}^{\pi} x \sin(nx) \, dx = \left[ -x \frac{\cos(nx)}{n} \right]_{0}^{\pi} - \int_{0}^{\pi} \left( -\frac{\cos(nx)}{n} \right) \, dx$$
$$= \left( -\pi \frac{\cos(n\pi)}{n} - 0 \right) + \left[ \frac{\sin(nx)}{n^2} \right]_{0}^{\pi}$$
$$= -\frac{\pi (-1)^n}{n} + 0 = -\frac{\pi (-1)^n}{n}$$

將此結果帶回 $b_n$：
$$b_n = \frac{2}{\pi} \cdot \left( -\frac{\pi (-1)^n}{n} \right) = -\frac{2(-1)^n}{n} = \frac{2 \cdot (-1)^{n+1}}{n}$$

我們可以列出前幾項看看：
* $b_1 = 2$
* $b_2 = -1$
* $b_3 = \frac{2}{3}$
* $b_4 = -\frac{1}{2}$

#### Step 5: 組合最終答案
將求得的係數 $\frac{a_0}{2} = \pi$，$a_n = 0$，$b_n = \frac{2(-1)^{n+1}}{n}$ 代入展開式：
$$f(x) = \pi + \sum_{n=1}^{\infty} \frac{2(-1)^{n+1}}{n} \sin(nx)$$

展開前幾項形式為：
$$f(x) = \pi + 2 \left( \sin(x) - \frac{1}{2}\sin(2x) + \frac{1}{3}\sin(3x) - \frac{1}{4}\sin(4x) + \cdots \right)$$
* **求 $A$：** 令 $s = 0$，得 $A = \left. \frac{1}{s+4} \right|_{s=0} = \frac{1}{4}$
* **求 $B$：** 令 $s = -4$，得 $B = \left. \frac{1}{s} \right|_{s=-4} = -\frac{1}{4}$

因此：
$$F(s) = \frac{1}{4} \cdot \frac{1}{s} - \frac{1}{4} \cdot \frac{1}{s+4}$$

對其進行拉普拉斯反轉換，可得基礎函數 $f(t)$：
$$f(t) = \mathcal{L}^{-1} \left( \frac{1}{4} \cdot \frac{1}{s} - \frac{1}{4} \cdot \frac{1}{s+4} \right) = \frac{1}{4} - \frac{1}{4}e^{-4t} = \frac{1}{4}\left(1 - e^{-4t}\right)$$
*(註：此處預設 $t \ge 0$，或可寫成 $\frac{1}{4}(1 - e^{-4t})u(t)$，其中 $u(t)$ 為單位階梯函數)*

#### Step 3: 應用時間平移定理 (Time-Shifting Theorem)
根據拉普拉斯轉換的時間平移定理：
$$\mathcal{L}^{-1} \left( e^{-as} F(s) \right) = f(t-a) \cdot u(t-a)$$

在第二項中，$a = 3$，因此：
$$\mathcal{L}^{-1} \left( e^{-3s} \cdot \frac{1}{s(s+4)} \right) = f(t-3) \cdot u(t-3)$$

將先前求得的 $f(t)$ 代入：
$$f(t-3) = \frac{1}{4}\left(1 - e^{-4(t-3)}\right)$$

#### Step 4: 組合最終答案
將兩項的結果相減，得到最終的拉普拉斯反轉換結果：
$$y(t) = \frac{1}{4}\left(1 - e^{-4t}\right)u(t) - \frac{1}{4}\left(1 - e^{-4(t-3)}\right)u(t-3)$$

亦可寫成分段函數的形式（此處已嚴格修正 `\left\{` 與 `\right.` 的閉合）：
$$y(t) = 
\begin{cases} 
0, & t < 0 \\
\dfrac{1}{4}\left(1 - e^{-4t}\right), & 0 \le t < 3 \\
\dfrac{1}{4}\left(e^{-4(t-3)} - e^{-4t}\right), & t \ge 3
\end{cases}$$

---

## 傳立葉變換作業題目：(7)（地方特考）

### 題目描述
> **令 $f(x) = x + \pi$ ， $x \in [-\pi, \pi]$，求函數 $f(x)$ 之傳立葉級數 (Fourier series)。**

### 求解步驟

#### Step 1: 傳立葉級數公式定義
在區間 $[-\pi, \pi]$ 上，函數 $f(x)$ 的傳立葉級數展開式為：
$$f(x) = \frac{a_0}{2} + \sum_{n=1}^{\infty} \left( a_n \cos(nx) + b_n \sin(nx) \right)$$

其中各係數公式為：
* $$a_0 = \frac{1}{\pi} \intInner_{-\pi}^{\pi} f(x) \, dx$$
* $$a_n = \frac{1}{\pi} \intInner_{-\pi}^{\pi} f(x) \cos(nx) \, dx$$
* $$b_n = \frac{1}{\pi} \intInner_{-\pi}^{\pi} f(x) \sin(nx) \, dx$$

#### Step 2: 計算 $a_0$
將 $f(x) = x + \pi$ 代入：
$$a_0 = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \, dx$$

由於 $x$ 是奇函數（在對稱區間 $[-\pi, \pi]$ 積分為 0），$\pi$ 是偶函數，式子可以簡化為：
$$a_0 = \frac{1}{\pi} \left[ \int_{-\pi}^{\pi} x \, dx + \int_{-\pi}^{\pi} \pi \, dx \right] = \frac{1}{\pi} \left[ 0 + \pi \cdot (2\pi) \right] = 2\pi$$

所以，直流項（常數項）為：
$$\frac{a_0}{2} = \pi$$

#### Step 3: 計算 $a_n$ ($n \ge 1$)
$$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \cos(nx) \, dx = \frac{1}{\pi} \int_{-\pi}^{\pi} x \cos(nx) \, dx + \frac{1}{\pi} \int_{-\pi}^{\pi} \pi \cos(nx) \, dx$$

* 第一項：$x$（奇函數）$\times \cos(nx)$（偶函數）$=$ 奇函數，在對稱區間積分結果為 $0$。
* 第二項：$\frac{1}{\pi} \cdot \pi \int_{-\pi}^{\pi} \cos(nx) \, dx = \left[ \frac{\sin(nx)}{n} \right]_{-\pi}^{\pi} = \frac{\sin(n\pi) - \sin(-n\pi)}{n} = 0$（因為當 $n$ 為整數時，$\sin(n\pi) = 0$）。

因此：
$$a_n = 0$$

#### Step 4: 計算 $b_n$ ($n \ge 1$)
$$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \sin(nx) \, dx = \frac{1}{\pi} \int_{-\pi}^{\pi} x \sin(nx) \, dx + \frac{1}{\pi} \int_{-\pi}^{\pi} \pi \sin(nx) \, dx$$

* 第二項：$\pi$（偶函數）$\times \sin(nx)$（奇函數）$=$ 奇函數，在對稱區間積分結果為 $0$。
* 第一項：$x$（奇函數）$\times \sin(nx)$（奇函數）$=$ 偶函數，可以簡化為 $0$ 到 $\pi$ 積分的 2 倍：
    $$b_n = \frac{2}{\pi} \int_{0}^{\pi} x \sin(nx) \, dx$$

使用分部積分法 (Integration by parts)，令 $u = x \implies du = dx$， $dv = \sin(nx)dx \implies v = -\frac{\cos(nx)}{n}$：
$$\int_{0}^{\pi} x \sin(nx) \, dx = \left[ -x \frac{\cos(nx)}{n} \right]_{0}^{\pi} - \int_{0}^{\pi} \left( -\frac{\cos(nx)}{n} \right) \, dx$$
$$= \left( -\pi \frac{\cos(n\pi)}{n} - 0 \right) + \left[ \frac{\sin(nx)}{n^2} \right]_{0}^{\pi}$$
$$= -\frac{\pi (-1)^n}{n} + 0 = -\frac{\pi (-1)^n}{n}$$

將此結果帶回 $b_n$：
$$b_n = \frac{2}{\pi} \cdot \left( -\frac{\pi (-1)^n}{n} \right) = -\frac{2(-1)^n}{n} = \frac{2 \cdot (-1)^{n+1}}{n}$$

我們可以列出前幾項看看：
* $b_1 = 2$
* $b_2 = -1$
* $b_3 = \frac{2}{3}$
* $b_4 = -\frac{1}{2}$

#### Step 5: 組合最終答案
將求得的係數 $\frac{a_0}{2} = \pi$，$a_n = 0$，$b_n = \frac{2(-1)^{n+1}}{n}$ 代入展開式：
$$f(x) = \pi + \sum_{n=1}^{\infty} \frac{2(-1)^{n+1}}{n} \sin(nx)$$

展開前幾項形式為：
$$f(x) = \pi + 2 \left( \sin(x) - \frac{1}{2}\sin(2x) + \frac{1}{3}\sin(3x) - \frac{1}{4}\sin(4x) + \cdots \right)$$
\[
\mathcal{L}^{-1}\{e^{-as}F(s)\} = f(t-a)u(t-a)
\]

所以：
\[
\mathcal{L}^{-1} \left\{ \frac{e^{-3s}}{s(s+4)} \right\}
=
\frac{1}{4}(1 - e^{-4(t-3)})u(t-3)
\]

---

### Step 4：最終答案
\[
y(t) =
\frac{1}{4}(1 - e^{-4t})u(t)
-
\frac{1}{4}(1 - e^{-4(t-3)})u(t-3)
\]

---

### 分段形式
\[
y(t)=
\begin{cases}
0, & t < 0 \\
\frac{1}{4}(1 - e^{-4t}), & 0 \le t < 3 \\
\frac{1}{4}(e^{-4(t-3)} - e^{-4t}), & t \ge 3
\end{cases}
\]

---

## 二、傅立葉級數作業：(7)

### 題目
\[
f(x) = x + \pi,\quad x \in [-\pi, \pi]
\]

---

### Step 1：基本形式
\[
f(x) = \frac{a_0}{2} + \sum_{n=1}^{\infty}(a_n \cos nx + b_n \sin nx)
\]

---

### Step 2：計算 \(a_0\)
\[
a_0 = \frac{1}{\pi}\int_{-\pi}^{\pi}(x+\pi)\,dx = 2\pi
\]

\[
\frac{a_0}{2} = \pi
\]

---

### Step 3：計算 \(a_n\)
\[
a_n = 0
\]

---

### Step 4：計算 \(b_n\)
\[
b_n = \frac{2}{\pi}\int_0^\pi x\sin(nx)\,dx
\]

結果：
\[
b_n = \frac{2(-1)^{n+1}}{n}
\]

---

### Step 5：最終傅立葉級數
\[
f(x) = \pi + \sum_{n=1}^{\infty} \frac{2(-1)^{n+1}}{n}\sin(nx)
\]

---

### 展開前幾項
\[
f(x)=\pi + 2\left(\sin x - \frac{1}{2}\sin 2x + \frac{1}{3}\sin 3x - \cdots \right)
\]* **求 $B$：** 令 $s = -4$，得 $B = \left. \frac{1}{s} \right|_{s=-4} = -\frac{1}{4}$

因此：
$$F(s) = \frac{1}{4} \cdot \frac{1}{s} - \frac{1}{4} \cdot \frac{1}{s+4}$$

對其進行拉普拉斯反轉換，可得基礎函數 $f(t)$：
$$f(t) = \mathcal{L}^{-1} \left\{ \frac{1}{4} \cdot \frac{1}{s} - \frac{1}{4} \cdot \frac{1}{s+4} \right\} = \frac{1}{4} - \frac{1}{4}e^{-4t} = \frac{1}{4}\left(1 - e^{-4t}\right)$$
*(註：此處預設 $t \ge 0$，或可寫成 $\frac{1}{4}(1 - e^{-4t})u(t)$，其中 $u(t)$ 為單位階梯函數)*

#### Step 3: 應用時間平移定理 (Time-Shifting Theorem)
根據拉普拉斯轉換的時間平移定理：
$$\mathcal{L}^{-1} \left\{ e^{-as} F(s) \right\} = f(t-a) \cdot u(t-a)$$

在第二項中，$a = 3$，因此：
$$\mathcal{L}^{-1} \left\{ e^{-3s} \cdot \frac{1}{s(s+4)} \right\} = f(t-3) \cdot u(t-3)$$

將先前求得的 $f(t)$ 代入：
$$f(t-3) = \frac{1}{4}\left(1 - e^{-4(t-3)}\right)$$

#### Step 4: 組合最終答案
將兩項的結果相減，得到最終的拉普拉斯反轉換結果：
$$y(t) = \frac{1}{4}\left(1 - e^{-4t}\right)u(t) - \frac{1}{4}\left(1 - e^{-4(t-3)}\right)u(t-3)$$

亦可寫成分段函數的形式：
$$y(t) = 
\begin{cases} 
0, & t < 0 \\\\[2ex]
\dfrac{1}{4}\left(1 - e^{-4t}\right), & 0 \le t < 3 \\\\[2ex]
\dfrac{1}{4}\left(e^{-4(t-3)} - e^{-4t}\right), & t \ge 3
\end{cases}$$

---

## 傅立葉變換作業題目：(7)（地方特考）

### 題目描述
> **令 $f(x) = x + \pi$ ， $x \in [-\pi, \pi]$，求函數 $f(x)$ 之傅立葉級數 (Fourier series)。**

### 求解步驟

#### Step 1: 傅立葉級數公式定義
在區間 $[-\pi, \pi]$ 上，函數 $f(x)$ 的傅立葉級數展開式為：
$$f(x) = \frac{a_0}{2} + \sum_{n=1}^{\infty} \left( a_n \cos(nx) + b_n \sin(nx) \right)$$

其中各係數公式為：
* $$a_0 = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \, dx$$
* $$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \cos(nx) \, dx$$
* $$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \sin(nx) \, dx$$

#### Step 2: 計算 $a_0$
將 $f(x) = x + \pi$ 代入：
$$a_0 = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \, dx$$

由於 $x$ 是奇函數（在對稱區間 $[-\pi, \pi]$ 積分為 0），$\pi$ 是偶函數，式子可以簡化為：
$$a_0 = \frac{1}{\pi} \left[ \int_{-\pi}^{\pi} x \, dx + \int_{-\pi}^{\pi} \pi \, dx \right] = \frac{1}{\pi} \left[ 0 + \pi \cdot (2\pi) \right] = 2\pi$$

所以，直流項（常數項）為：
$$\frac{a_0}{2} = \pi$$

#### Step 3: 計算 $a_n$ ($n \ge 1$)
$$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \cos(nx) \, dx = \frac{1}{\pi} \int_{-\pi}^{\pi} x \cos(nx) \, dx + \frac{1}{\pi} \int_{-\pi}^{\pi} \pi \cos(nx) \, dx$$

* 第一項：$x$（奇函數）$\times \cos(nx)$（偶函數）$=$ 奇函數，在對稱區間積分結果為 $0$。
* 第二項：$\frac{1}{\pi} \cdot \pi \int_{-\pi}^{\pi} \cos(nx) \, dx = \left[ \frac{\sin(nx)}{n} \right]_{-\pi}^{\pi} = \frac{\sin(n\pi) - \sin(-n\pi)}{n} = 0$（因為當 $n$ 為整數時，$\sin(n\pi) = 0$）。

因此：
$$a_n = 0$$

#### Step 4: 計算 $b_n$ ($n \ge 1$)
$$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} (x + \pi) \sin(nx) \, dx = \frac{1}{\pi} \int_{-\pi}^{\pi} x \sin(nx) \, dx + \frac{1}{\pi} \int_{-\pi}^{\pi} \pi \sin(nx) \, dx$$

* 第二項：$\pi$（偶函數）$\times \sin(nx)$（奇函數）$=$ 奇函數，在對稱區間積分結果為 $0$。
* 第一項：$x$（奇函數）$\times \sin(nx)$（奇函數）$=$ 偶函數，可以簡化為 $0$ 到 $\pi$ 積分的 2 倍：
    $$b_n = \frac{2}{\pi} \int_{0}^{\pi} x \sin(nx) \, dx$$

使用分部積分法 (Integration by parts)，令 $u = x \implies du = dx$， $dv = \sin(nx)dx \implies v = -\frac{\cos(nx)}{n}$：
$$\int_{0}^{\pi} x \sin(nx) \, dx = \left[ -x \frac{\cos(nx)}{n} \right]_{0}^{\pi} - \int_{0}^{\pi} \left( -\frac{\cos(nx)}{n} \right) \, dx$$
$$= \left( -\pi \frac{\cos(n\pi)}{n} - 0 \right) + \left[ \frac{\sin(nx)}{n^2} \right]_{0}^{\pi}$$
$$= -\frac{\pi (-1)^n}{n} + 0 = -\frac{\pi (-1)^n}{n}$$

將此結果帶回 $b_n$：
$$b_n = \frac{2}{\pi} \cdot \left( -\frac{\pi (-1)^n}{n} \right) = -\frac{2(-1)^n}{n} = \frac{2 \cdot (-1)^{n+1}}{n}$$

我們可以列出前幾項看看：
* $b_1 = 2$
* $b_2 = -1$
* $b_3 = \frac{2}{3}$
* $b_4 = -\frac{1}{2}$

#### Step 5: 組合最終答案
將求得的係數 $\frac{a_0}{2} = \pi$，$a_n = 0$，$b_n = \frac{2(-1)^{n+1}}{n}$ 代入展開式：
$$f(x) = \pi + \sum_{n=1}^{\infty} \frac{2(-1)^{n+1}}{n} \sin(nx)$$

展開前幾項形式為：
$$f(x) = \pi + 2 \left( \sin(x) - \frac{1}{2}\sin(2x) + \frac{1}{3}\sin(3x) - \frac{1}{4}\sin(4x) + \cdots \right)$$
