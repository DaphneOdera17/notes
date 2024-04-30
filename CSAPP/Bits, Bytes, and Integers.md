# CSAPP | Bits, Bytes, and Integers
## Great Reality
### **Ints are not Integers, Floats are not Reals**
对于 (x + y) + z = x + (y + z)，无符号整形和有符号整形是成立的。
但是对于浮点数, (1e20 + -1e20) + 3.14 -> 3.14，而 1.e20 + (-1e20 + 3.14) = 0
```c
typedef struct {
	int a[2];
	double d;
}struct_t;

double fun(int i) {
	volatile struct_t s;
	s.d = 3.14;
	s.a[i] = 1073741824; /* Possibly out of bounds */
	return s.d;
}
```
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240413142810.png" style="zoom:50%" >
我们发现，当 i = 5 时，程序会崩溃。
### Explanation:
C 语言不会在运行中做任何边界检查
对于下图，垂直链的每个块代表 4 字节。a 数组的两个元素都是 4 字节，d 是 8 个字节
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240413142922.png" style="zoom:75%">
当 i 大于 1 时，赋值 a[2] 会赋值给 d3 ... d0，赋值 a[3] 会赋值给 d4 ... d7，所以 i = 4 的时候正常，后面报不报错看栈的空间等。
## Memory System Performance Example
下面有两端函数。
```c
void copyij(int src[2048][2048], int dst[2048][2048])
{
	int i, j;
	for(int i = 0; i < 2048; i ++)
		for(int j = 0; j < 2048; j ++)
			dst[i][j] = src[i][j];
}
```
```c
void copyji(int src[2048][2048], int dst[2048][2048])
{
	int i, j;
	for(int j = 0; j < 2048; j ++)
		for(int i = 0; i < 2048; i ++)
			dst[i][j] = src[i][j];
}
```
可以看出它们的区别在于一个行优先，一个列优先。而第一段代码运行速度远远快于第二段代码。以行优先代码的运行速度快于一列一列运行。
## Everything is bits
整数、浮点数等都可以表示为二进制。
### Data Representations

| C Data Type | Typical 32-bit | Typical 64-bit | x86-64 |
| :---------: | :------------: | :------------: | :----: |
|    char     |       1        |       1        |   1    |
|    short    |       2        |       2        |   2    |
|     int     |       4        |       4        |   4    |
|    long     |       4        |       8        |   8    |
|    float    |       4        |       4        |   4    |
|   double    |       8        |       8        |   8    |
| long double |       -        |       -        | 10/16  |
|   pointer   |       4        |       8        |   8    |
|             |                |                |        |
## Boolean Algebra
And: A & B = 1 when both A = 1 and B = 1
Or: A | B = 1 when either A = 1 or B = 1
Not: ~A = 1 when A = 0
Exclusive-Or(Xor): A^B = 1 when either A = 1 or B = 1, but not both 相同为 0，相异为 1
### Representing & Manipulating
#### Representation
Width w bit vector represents subsets of {0, ..., w - 1}
$a_j = 1~ ~if~ ~j~ ~\in A$

01101001 代表 {0, 3, 5, 6}
7**65**4**3**21**0**

01010101 代表 {0, 2, 4, 6}
7**6**5**4**3**2**1**0**
#### Operations

| 符号  |            操作             |  二进制序列   |         集合         |
| :-: | :-----------------------: | :------: | :----------------: |
|  &  |      Intersection 交       | 01000001 |       {0, 6}       |
| \|  |          Union 并          | 01111101 | {0, 2 ,3, 4, 5, 6} |
|  ^  | Symmetric difference 对称差异 | 00111100 |    {2, 3, 4, 5}    |
|  ~  |       Complement 补        | 10101010 |    {1, 3, 5, 7}    |
### Bit-Level Operations in C
位运算
#### Examples(Char data type)
$\sim0x41 -> 0xBE$
	$\sim01000001_2 -> 10111110_2$ 
$\sim0x00 -> 0xFF$
	$\sim0000 0000_2 -> 1111 1111_2$
$\sim0x69~ ~\&~ ~0x55 -> 0x41$
	$\sim0110 1001_2 ~~\&~~ 0101 0101_2-> 0100 0001_2$
$\sim0x69 ~~| ~~0x55 ->  0x7D$
	$\sim0110 1001_2 ~~|~~ 0101 0101_2 -> 0111 1101_2$
### Logic Operations in C
$\&\&, ||, !$
	view 0 as "False"
	Anythings nonzero as "True"
	**Always return 0 or 1**
	**Early termination**
C 语言的逻辑运算只有 2 种结果， 0x00 和 0x01
取反是**按结果取反**，不是按位取反！
#### Examples(Char data type)
$!0x41 -> 0x00$ 相当于对 true 取反，结果为 false, 为 0x00
$!0x00 -> 0x01$
$!!0x41-> 0x01$

$0x69~ ~\&\&~ ~0x55 -> 0x01$
$0x69~ ~||~ ~0x55 -> 0x01$
$p~~\&\&~~*p$ (avoids null pointer access) 在访问之前先判断是否为空指针，如果是空指针，会提前终止。
### Shift Operation
#### Left Shift: x << y
Shift bit-vector x left y positions, Throw away extra bits on left
Fill with 0's on right
#### Right Shift: x >> y
Shift bit-vector x right y position, Throw away extra bits on right
Logical Shift
	Fill with 0's on left
Arithmetic Shift
	Replicate(复制) most significant bit on left
对于右移运算，分为算数右移和逻辑右移。他们的填充规则不一样。算数右移填充的是符号位的数字。

| Argument x  | 0110 0010 |
| :---------: | :-------: |
|    << 3     | 0001 0000 |
|  Log. >> 2  | 0001 1000 |
| Arith. >> 2 | 0001 1000 |

| Argument x  | 1010 0010 |
| :---------: | :-------: |
|    << 3     | 0001 0000 |
|  Log. >> 2  | 0010 1000 |
| Arith. >> 2 | 1110 1000 |
#### Undefined Behavior
Shift amount < 0 or >= word size
### Numeric Ranges
#### Unsigned Values
$UMin = 0 -> 000...0$
$UMax = 2^w - 1 -> 111...1$ 
$UMax = 2 \times TMax + 1$
#### Two's Complement Values (补码)
$TMin = -2^{w - 1} -> 100...0$
$TMax = w^{w - 1} - 1 -> 011...1$
$|TMin| = TMax + 1$
#### Other Values
$Minus~1 -> 111...1$
##### Values for W = 16

|      | Decimal |  Hex  |      Binary       |     |
| :--: | :-----: | :---: | :---------------: | --- |
| UMax |  65535  | FF FF | 11111111 11111111 |     |
| TMax |  32767  | 7F FF | 01111111 11111111 |     |
| TMin | -32768  | 80 00 | 10000000 00000000 |     |
|  -1  |   -1    | FF FF | 11111111 11111111 |     |
|  0   |    0    | 00 00 | 00000000 00000000 |     |
$UMax = 2 \times TMax + 1$
#### From Binary to Unsigned
$B2U(X) = \sum_{i = 0}^{w - 1}x_i 2^i$
#### From Binary to Two's complement
$B2T(X) = -x_{w - 1} 2^{w - 1} + \sum_{i = 0}^{w - 2} x_i 2^i$
对于补码，最高位称为符号位，为 1 代表负数。
#### Unsigned & Signed Numeric Values

| X    | B2U(X) | B2T(X) |
| ---- | ------ | ------ |
| 0000 | 0      | 0      |
| 0001 | 1      | 1      |
| 0010 | 2      | 2      |
| 0011 | 3      | 3      |
| 0100 | 4      | 4      |
| 0101 | 5      | 5      |
| 0110 | 6      | 6      |
| 0111 | 7      | 7      |
| 1000 | 8      | -8     |
| 1001 | 9      | -7     |
| 1010 | 10     | -6     |
| 1011 | 11     | -5     |
| 1100 | 12     | -4     |
| 1101 | 13     | -3     |
| 1110 | 14     | -2     |
| 1111 | 15     | -1     |
观察可知，负数与对应的正数关系是，正数取反加 1
#### Casting
如果有符号数和无符号数混合，有符号数会被隐式转换为无符号数。
$-1 > 0U$ 因为 $-1$ 会被转换为无符号数 $1111~ ~1111$ 也就变成 $UMax$
$W =32,~TMIN = -2147483647, ~TMAX=2147483647$
$2147483647U < -2147483647 - 1$
$(unsigned)-1 > -2$
$2147483647 < 2147483648U$
$2147483647 > (int)2147483648U$, 对于 32 位系统来说，$int$ 范围是 $-2147483648 \sim 2147483647$,$unsigned~int$ 范围是 $0 \sim 4294967295$，所以将 $2147483648U$ 转换为 $int$, 会溢出。

考虑以下的代码：
对于 x = TMin, 他的输出还是 TMin。
因为 $-x = \sim x + 1$
对于 TMin 1000...0 取反 0111...1 再加 1， 1000...0 所以结果还是 TMin
```c
if(x < 0)
	return -x;
else
	return x;
```
以下代码会造成无限循环。 $i$ 会从 $0$ 变为 $UMax$ (个人认为是 0 减 1 为 -1, 表示为全 1，则解释为 UMax)
```c
unsigned int i;
for(i = n - 1; i >= 0; i --) {
	f(a[i]);
}
```
对于下面的代码, $sizeof(char)$ 实际上返回的是 无符号数。$i$ 为有符号数，有符号数和无符号数比较会被转换为无符号数。$i - sizeof(char) >= 0$ 这个条件就会一直成立，无限循环。
```c
int i;
for(i = n - 1; i - sizeof(char) >= 0; i --) {
	f(a[i]);
}
```
### Sign Extension
Task:
	Given w-bit signed integer x
	Convert it to (w+k)-bit integer with same value
Rule:
	Make k copies of sign bit
	$X' = x_{w-1}, ..., x_{w-1}, x_{w - 2}, ..., x_0$
对于 $1110$，符号位权重为 $-2^3=-8$，将它左移一位，变为 $11110$，原先符号位位置上的权重变为了 $8$，而新的符号位权重为 $-2^4=-16$, $-16 + 8 = -8$, 所以并不改变总和的效应。
Converting from smaller to larger integer data type, C automatically performs sign extension.
```c
short int x = 15213;
int ix = (int) x;
short int y = -15213;
int iy = (int) y;
```
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240424105410.png)
### Two's Complement Addition
-5 + 3
 1011
+0011
1110  -> -2

-3 + 5
 1101
+0101
10010 -> 0010 -> 2 

-3 + -5
 1101
+1011
10000 -> 0 负溢出
## 位运算
移位指令比乘法指令花的时间更少。
$u << k$ 相当于 $u \times 2^k$
$u >> k$ 相当于 $\lfloor {u / 2^k} \rfloor$
前面介绍过算数右移与逻辑右移。算数右移**可以保持符号位**。例如 1010 为 -6，算数右移 1 位，则为 1101 为 -3。但是此时如果再右移 1 位，得到 1110 为 -2。结果出现问题。
特别的，对于负数的除法，如果需要右移 $k$ 位，我们需要先加上偏移量 $2^k - 1$。
1101 + 1 = 1110 此时再右移 1 位，得到 1111 为 -1。
## 正数变负数
$x -> -x$ 需要对所有位取反，再 + 1。
0101 -> 5
1010 + 1 = 1011 -> -5
## 使用 Unsigned 一些方式
```c
unsigned i;
for(i = cnt - 2; i < cnt; i --)
	a[i] += a[i + 1];
```
Better Version:
```c
size_t i;
for(i = cnt - 2; i < cnt; i --)
	a[i] += a[i + 1];
/*
1. Data type size_t defined as unsigned value with length = word size
2. Code will work even if cnt = UMax
*/
```
然而，当 cnt 为 signed 并且小于 0 时。会有问题。cnt 会被转换为无符号数，就会变得非常大，导致无限循环。
## 大端序和小端序
#### Big Endian
高位字节存入低地址，低位字节存入高地址。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240430134050.png)
上图从左往右 01234567
#### Little Endian
低位字节存入低地址，高位字节存入高地址。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240430134057.png)
从右往左 01234567
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240430134509.png)
## 字符串
字符串以 null 结尾，也就是 '0'
```c
char S[6] = '18213';
```
字符 '0' 为 0x30，数字字符 i 为 0x30 + i
对于字符串数组来说，大端法和小端法存储没有区别。因为字符是一个字节一个字节存储，而每个都是一个整体。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240430182303.png)
> [!NOTE]
> 例如对于 0x12345678 来说，这是一个整体，0x12 是整体的高位，0x78 是整体的低位，存储就是 0x78 0x56 0x34 0x12。而对于字符数组，内部组织形式是一个字节一个字节，数组相当于是 0x12 0x34 0x56 0x78，每个字符是一个整体。

## 易错
1. 如果 x < 0, 那么 ((x * 2) < 0) 吗？ 
	错误，因为可能会负溢出，x * 2 可能会是一个正数。
2. 如果一个数 x，x & 7 == 7，也就是最低的 3 位为 111，如果 (x << 30) 那么结果 < 0。
3. Is ux > -1? 错的。无符号数和有符号数作比较，有符号数被隐式转换为无符号数。-1 就会被转换为 UMax。
4. 如果 x > y，那么 -x < -y 一定成立吗？
	错误的，因为如果 y 为 TMin，我们直到 $|TMin| = TMax + 1$。对 TMin 取相反数，也就是 TMin 的位取反再 + 1，那就变成 TMax + 1，发生正溢出。又变回了 TMin。
5. x >= 0 那么 -x <= 0 吗？ 正确的
6. x <= 0 那么 -x >= 0 吗？ 错误的，比如 TMin。
	
