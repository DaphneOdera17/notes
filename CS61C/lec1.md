# CS61C | lecture1
## 计算机系统抽象
## 二进制可以表示任何东西
n 位数字(base B) 可以表示 <= $B^n$ 个事物
### 数字
计算机中，用二进制表示数字
$$
\begin{aligned}
& d_{n-1}d_{n-2}...d_1d_0(n位数字由B为基) \\
=& ~~d_{n-1} \times B^{n-1} + d_{n-2} \times B^{n-2} + .. d_1 \times B^1
 + d_0 \times B^0
\end{aligned}
$$
### 字符
26 个字符用 5 bits 可以表示
ASCII: 7 bits
### 布尔值
0 -> False
1 -> True
### unsigned
$$
\begin{aligned}
x &= 0b1010 \\
& = 2^3 + 2^1 = 10
\end{aligned}
$$
### sign and magnitude
将第一位作为符号，剩下的作为无符号数。
$$
\begin{aligned}
\textcolor{red}{0}00_{two} &= \textcolor{red}{+}0_{ten} \\
\textcolor{red}{0}01_{two} &= \textcolor{red}{+}1_{ten} \\
\textcolor{red}{0}10_{two} &= \textcolor{red}{+}2_{ten} \\
\textcolor{red}{0}11_{two} &= \textcolor{red}{+}3_{ten} \\
\\
\textcolor{blue}{1}00_{two} &= \textcolor{blue}{-}0_{ten} \\
\textcolor{blue}{1}01_{two} &= \textcolor{blue}{-}1_{ten} \\
\textcolor{blue}{1}10_{two} &= \textcolor{blue}{-}2_{ten} \\
\textcolor{blue}{1}11_{two} &= \textcolor{blue}{-}3_{ten} \\
\end{aligned}
$$
这样就会导致存在两个 0，$0...0_{two}~and~10...0_{two} = \pm 0_{ten}$
最大的正数 $01...1_{two}= (2^{(n-1)}-1)_{ten}$
最小的负数 $1...1_{two}=-(2^{(n-1)} - 1)_{ten}$
$$
\begin{aligned}
x &= 0b1010 \\
& = -1 \times 2^1 = -2
\end{aligned}
$$
### biased notation
类似于 unsigned，但是会有偏移从而让 0 粗略的在中间。值 = "unsigned value" - bias
传统偏移量 $(2^{(n-1)} - 1)$
$$
\begin{aligned}
000_{two} &= -3_{ten} \\
001_{two} &= -2_{ten} \\
010_{two} &= -1_{ten} \\
\textcolor{red}{011_{two}} &\textcolor{red}{= 0_{ten}} \\
100_{two} &= +1_{ten} \\
101_{two} &= +2_{ten} \\
110_{two} &= +3_{ten} \\
111_{two} &= +4_{ten} \\
\end{aligned}
$$
此时，0 为 $01...1_{two}=0_{ten}$
最大的正数 $1...1_{two} = (2^{(n-1)})_{ten}$
最小的负数 $0...0_{two}=-(2^{(n-1)} - 1)_{ten}$

$$
\begin{aligned}
x &= 0b1010 \\
& = 2^3 + 2^1 - (2^3 - 1) = 3
\end{aligned}
$$
### one's complement
$$
\begin{aligned}
000_{two} &= +0_{ten} \\
001_{two} &= +1_{ten} \\
010_{two} &= +2_{ten} \\
011_{two} &= +3_{ten} \\
\\
100_{two} &= -3_{ten} \\
101_{two} &= -2_{ten} \\
110_{two} &= -1_{ten} \\
111_{two} &= -0_{ten} \\
\end{aligned}
$$
然而此时 0 有两个 $0...0_{two}~and~1...1_{two} = \pm0_{ten}$
最大的正数 $01...1_{two} = (2^{(n-1)}-1)_{ten}$
最小的负数 $10...0_{two} = -(2^{(n-1)}-1)_{ten}$
$$
\begin{aligned}
x &= 0b1010 \\
-x& = \sim x = 0b0101 = 5 \\ 
x &= -5
\end{aligned}
$$
### two's complement
$$
\begin{aligned}
000_{two} &= +0_{ten} \\
001_{two} &= +1_{ten} \\
010_{two} &= +2_{ten} \\
011_{two} &= +3_{ten} \\
\\
100_{two} &= -4_{ten} \\
101_{two} &= -3_{ten} \\
110_{two} &= -2_{ten} \\
111_{two} &= -1_{ten} \\
\end{aligned}
$$
对于 0，只有 $0...0_{two} = 0_{ten}$
最大的正数 $01...1_{two} = (2^{(n-1)} - 1)_{ten}$
最小的负数 $10...0_{two}=(-2^{(n-1)})_{ten}$

正数翻转所有位并加 1 可以得到负数。

$$
\begin{aligned}
x &= 0b1010 \\
-x& = \sim x + 1= 0b0101 + 1  = 0b0110 = 6 \\
 x & = -6 \\
 & = -2^3 + 2^1 = -8 + 2 = -6
\end{aligned}
$$

对于补码来说

|  会溢出  | 不会溢出  |
| :---: | :---: |
| + + + | - + + |
| - + - | + + - |
