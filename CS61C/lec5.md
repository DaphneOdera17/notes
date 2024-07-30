# CS61C | lecture5
## 浮点数的表示
用一个小数点作为边界分隔整数部分和小数部分。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240613131804.png)
$$
10.1010_{2}=1\times2^1+1\times2^{-1}+1\times2^{-3}=2.625_{10}
$$
## Scientific Notation(Binary)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240613132206.png)
## 单精度
$$
+{1.xxx...x_{2}\times2^{yyy...y}}_2
$$
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240613132623.png)

Bias = 127
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240613184150.png)
$$
(-1)^S \times (1.\textcolor{red}{Significand})\times 2^{\textcolor{blue}{Exponent}-127}
$$
$$
\begin{aligned}
&\textcolor{green}{0}\textcolor{blue}{011~~1111~~1}\textcolor{red}{100~~0000~~0000~~0000~~0000~~0000}_2  \\
=&(-1)^{\textcolor{green}{0}}\times(1.\textcolor{red}{1}_2) \times 2^{\textcolor{blue}{127} - 127} \\
=&(1.\textcolor{red}{1}_2) \times 2(\textcolor{blue}{0}) \\ \\
&1.1_2 = 1\times 2^0 + 1 \times 2^{-1} = 1.5_{10} \\
\end{aligned}
$$
注意有一个隐式的 1 在 Significand 前面，所以是 $1.5_{10}$ 而不是 $0.5_{10}$
## 双精度
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240613185203.png)
