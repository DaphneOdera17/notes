# Lecture11 | Combinational Logic
## 1 iff one(not both) a, b = 1

| a   | b   | y   |
| --- | --- | --- |
| 0   | 0   | 0   |
| 0   | 1   | 1   |
| 1   | 0   | 1   |
| 1   | 1   | 0   |

| a   | y              |
| --- | -------------- |
| 0   | b              |
| 1   | $\overline{b}$ |
## 2-bit adder
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731155609.png" style="zoom:70%">

| A<br>$a_1a_0$ | B<br>$b_1b_0$ | C<br>$c_2c_1c_0$ |
| ------------- | ------------- | ---------------- |
| 00            | 00            | 000              |
| 00            | 01            | 001              |
| 00            | 10            | 010              |
| 00            | 11            | 011              |
| 01            | 00            | 001              |
| 01            | 01            | 010              |
| 01            | 10            | 011              |
| 01            | 11            | 100              |
| 10            | 00            | 010              |
| 10            | 01            | 011              |
| 10            | 10            | 100              |
| 10            | 11            | 101              |
| 11            | 00            | 011              |
| 11            | 01            | 100              |
| 11            | 10            | 101              |
| 11            | 11            | 110              |
## Logical Gates
### AND
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731160553.png" style="zoom: 50%">

| ab  | c   |
| --- | --- |
| 00  | 0   |
| 01  | 0   |
| 10  | 0   |
| 11  | 1   |
### OR
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731161615.png" style="zoom:50%">

| ab  | c   |
| --- | --- |
| 00  | 0   |
| 01  | 1   |
| 10  | 1   |
| 11  | 1   |
### NOT
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731161717.png" style="zoom:50%">

| a   | b   |
| --- | --- |
| 0   | 1   |
| 1   | 0   |
### XOR
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731162226.png" style="zoom:50%">

| ab  | c   |
| --- | --- |
| 00  | 0   |
| 01  | 1   |
| 10  | 1   |
| 11  | 0   |
对于异或，如果有$\textcolor{red}{奇数}$个 1 最后结果就是 1
### NAND
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731162433.png" style="zoom:50%">

| ab  | c   |
| --- | --- |
| 00  | 1   |
| 01  | 1   |
| 10  | 1   |
| 11  | 0   |
### NOR
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731162506.png" style="zoom:50%">

| ab  | c   |
| --- | --- |
| 00  | 1   |
| 01  | 0   |
| 10  | 0   |
| 11  | 0   |
## Example
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731163032.png" style="zoom:70%">

| PS  | Input | NS  | Output |
| --- | ----- | --- | ------ |
| 00  | 0     | 00  | 0      |
| 00  | 1     | 01  | 0      |
| 01  | 0     | 00  | 0      |
| 01  | 1     | 10  | 0      |
| 10  | 0     | 00  | 0      |
| 11  | 1     | 00  | 1      |
$PS_0$ 是右边一列，$PS_1$ 是左边的一列
## Boolean Algebra
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731171150.png)
$$
y = a \cdot b + a \cdot c + b \cdot c
$$
### Algebraic Simplification
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731172431.png)
$$
\begin{aligned}
y &= ab + a + c \\
 & = a(b + 1) + c \\
 & = a(1) + c \\
 & = a + c
\end{aligned}
$$
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731172818.png" style="zoom:70%">
$$
\begin{aligned}
x \cdot \overline {x} &= 0  ~~~~~~~~~~~~~~~~~~ &x + \overline {x} &= 1\\   
x \cdot 0 &= 0 ~~~~~~~~~~~~~~~~~~ &x + 1 &= 1\\
x \cdot 1 &= x ~~~~~~~~~~~~~~~~~~  &x + 0 &= x\\
x \cdot x &= x ~~~~~~~~~~~~~~~~~~  &x + x &= x\\
x \cdot y &= y \cdot x ~~~~~~~~~~~~~~~~~~  &x + y &= y + x\\
(xy)z &= x(yz) ~~~~~~~~~~~~~~~~~~  &(x + y) + z &= x + (y + z)\\
x(y + z) &= xy + xz ~~~~~~~~~~~~~~~~~~  &x + yz &= (x + y)(x + z)\\
xy + x &= x ~~~~~~~~~~~~~~~~~~ &(x + y)x &= x\\
\overline{x \cdot y} &= \overline{x} + \overline{y} ~~~~~~~~~~~~~~~~~~ &\overline{(x + y)} &= \overline{x} \cdot \overline{y}\\
\end{aligned}
$$
## Data Multiplexor 
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731191634.png" style="zoom:50%">
当 S 为 0 时，A 路可行。当 S 为 1 时，B 路可行。
可以将 n 位输入多路复用器看做 n 个 1 位输入的多路复用器。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731191838.png)

| s   | ab  | c   |
| --- | --- | --- |
| 0   | 00  | 0   |
| 0   | 01  | 0   |
| 0   | 10  | 1   |
| 0   | 11  | 1   |
| 1   | 00  | 0   |
| 1   | 01  | 1   |
| 1   | 10  | 0   |
| 1   | 11  | 1   |
s 为 0 时 c 实际上是 a 的值。s 为 1 时 c 实际上是 b 的值。
$$
\begin{aligned}
c &= \overline{s}a\overline{b} + \overline{s}ab + s\overline{a}b + sab \\
 &= \overline{s}(a\overline{b} + ab) + s(\overline{a}b + ab) \\
 &= \overline{s}(a(\overline{b} + b)) + s((\overline{a} + a)b) \\
 &= \overline{s}(a(1)+s(1)b) \\
 &= \overline{s}a + sb
\end{aligned}
$$
也就是
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731192502.png" style="zoom:50%">
### 4-to-1 Multiplexor
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731192610.png" style="zoom:60%">
$e=\overline{s_1}\cdot\overline{s_0}a+\overline{s_1}\cdot s_0b+s_1\cdot\overline{s_0}c+s_1s_0d$
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731194140.png" style="zoom:50%">
## Arithmetic Logic Unit(ALU)
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731194637.png" style="zoom:50%">

| S   | R      |
| --- | ------ |
| 00  | A + B  |
| 01  | A - B  |
| 10  | A & B  |
| 11  | A \| B |
### Our Simple ALU
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731194938.png" style="zoom:60%">
## Adder
$s_0 = a_0~ ~XOR~ ~b_0$
$c_1=a_0~~ AND ~~b_0$ 进位

| $a_0$ | $b_0$ | $s_0$ | $c_1$ |
| ----- | ----- | ----- | ----- |
| 0     | 0     | 0     | 0     |
| 0     | 1     | 1     | 0     |
| 1     | 0     | 1     | 0     |
| 1     | 1     | 0     | 1     |

| $a_i$ | $b_i$ | $c_i$ | $s_i$ | $c_{i+1}$ |
| ----- | ----- | ----- | ----- | --------- |
| 0     | 0     | 0     | 0     | 0         |
| 0     | 0     | 1     | 1     | 0         |
| 0     | 1     | 0     | 1     | 0         |
| 0     | 1     | 1     | 0     | 1         |
| 1     | 0     | 0     | 1     | 0         |
| 1     | 0     | 1     | 0     | 1         |
| 1     | 1     | 0     | 0     | 1         |
| 1     | 1     | 1     | 1     | 1         |
$s_i=XOR(a_i,b_i,c_i)$
$c_{i+1}=MAJ(a_i,b_i,c_i)=a_ib_i+a_ic_i+b_ic_i$
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731200916.png" style="zoom:50%">
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731200944.png" style="zoom:50%">
### N 1-bit adders -> 1 N-bit adder
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731201100.png" style="zoom:50%">
对于 unsigned 来说，$overflow = c_n$
对于 signed 来说
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731201440.png" style="zoom:50%">
#### Highest adder
- $C_{in} = Carry-in=c_1, ~~C_{out} = Carry-out = c_2$
- $No~ ~C_{out} ~or~ ~C_{in}~ ~->~ ~NO~~overflow$
- $C_{out} ~and~ ~C_{in}~ ~->~ ~NO~~overflow$
- $C_{in}~~but~~no~~C_{out}~~->~~A,B~~both~~>~~0,~~\textcolor{red}{overflow}!$
- $C_{out}~~but~~no~~C_{in}~~->~~A~~or~~B~~are~~-2,~~\textcolor{red}{overflow}!$
$~~\textcolor{red}{overflow} = c_n~~XOR~~c_{n+1}$
## Subtractor
$A-B=A+(-B)$
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240731203459.png)










