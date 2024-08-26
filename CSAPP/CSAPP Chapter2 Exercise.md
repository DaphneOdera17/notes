# CSAPP | Exercise | Chapter2
## Ex 2.23
```c
#include<stdio.h>

int fun1(unsigned word){
    return (int) ((word << 24) >> 24);
}

int fun2(unsigned word){
    return ((int) word << 24) >> 24;
}

int main()
{
    unsigned int a = 0x00000076;
    unsigned int b = 0x87654321;
    unsigned int c = 0x000000C9;
    unsigned int d = 0xEDCBA987;
    printf("fun1(a) = %x, fun2(a) = %x \n", fun1(a), fun2(a));
    printf("fun1(b) = %x, fun2(b) = %x \n", fun1(b), fun2(b));
    printf("fun1(c) = %x, fun2(c) = %x \n", fun1(c), fun2(c));
    printf("fun1(d) = %x, fun2(d) = %x \n", fun1(d), fun2(d));

    return 0;
}    
```
运行结果如下：
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240806151730.png)
由于 $fun1$ 先对无符号数 $word$ 进行左移，然后右移，此时因为是无符号数，所以右移用 0 填充。
而对于 $fun2$，先将 $word$ 转换成了有符号数，所以右移用符号位填充。
$7_{10}=0111_2,2_{10}=0010_2,C_{10}=1100_2,8_{10}=1000_2$，可以看到对于 C 和 8，符号位都是 1，所以用 1 填充。

|     $w$      |  $fun1(w)$   |  $fun2(w)$   |
| :----------: | :----------: | :----------: |
| $0x00000076$ | $0x00000076$ | $0x00000076$ |
| $0x87654321$ | $0x00000021$ | $0x00000021$ |
| $0x000000C9$ | $0x000000C9$ | $0xFFFFFFC9$ |
| $0xEDCBA987$ | $0x00000087$ | $0xFFFFFF87$ |
## Ex 2.24
对于无符号数，截断成 $k$ 位，也就是 $mod~~2^k$
对于补码数，则是先无符号 $mod~~2^k$，再将结果转换为有符号数

| 十六进制 | 十进制 | 四位二进制 | 三位二进制 |
| :--: | :-: | :---: | :---: |
|  0   |  0  | 0000  |  000  |
|  2   |  2  | 0010  |  010  |
|  9   |  9  | 1001  |  001  |
|  B   | 11  | 1011  |  011  |
|  F   | 15  | 1111  |  111  |

| 十六进制原始值 | 十六进制截断值 | 无符号原始值 | 无符号截断值 | 补码原始值 | 补码截断值 |
| :-----: | :-----: | :----: | :----: | :---: | :---: |
|    0    |    0    |   0    |   0    |   0   |   0   |
|    2    |    2    |   2    |   2    |   2   |   2   |
|    9    |    1    |   9    |   1    |  -7   |   1   |
|    B    |    3    |   11   |   3    |  -5   |   3   |
|    F    |    7    |   15   |   7    |  -1   |  -1   |
## Ex 2.25
错误代码
```c
#include<stdio.h>

float sum_elements(float a[], unsigned length){
    int i;
    float result = 0;

    for(i = 0; i <= length - 1; i ++)
        result += a[i];

    return result;   
}

int main()
{
    float a[5] = {0.0, 1.1, 2.1, 3.1, 4.1};
    printf("%f", sum_elements(a, 0));
    return 0;
}
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240806155211.png)
出现段错误。
添加一行输出 $length-1$ 的值，
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240806155448.png" style="zoom:50%">
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240806160001.png)

$length-1=42949672950$，实际上，因为 $length$ 为 $unsigned$，无符号类型，当 $length$ 传入为 $0$ 时，$0-1=-1$，$-1$ 被转换成 $unsigned$ 类型，则变为 $UMax$，从而造成 $i$ 过大，数组下标访问越界。
修改为正确的代码为，将 unsigned length 改为 int length:
```c
#include<stdio.h>

float sum_elements(float a[], int length){
    int i;
    float result = 0;

    printf("%u\n", length - 1);

    for(i = 0; i <= length - 1; i ++)
        result += a[i];

    return result;   
}

int main()
{
    float a[5] = {0.0, 1.1, 2.1, 3.1, 4.1};
    printf("%.1f", sum_elements(a, 0));
    return 0;
}
```
## Ex 2.26
由于 size_t 为 unsigned int 即无符号类型，strlen() 的结果也相应为无符号类型。当 s 的长度小于 t 的长度时，$strlen(s)<strlen(t)$，相减本应该小于 0。但因为是无符号类型，负数会被转换为无符号类型，则变为正的。所以 $strlen(s)-strlen(t)$ 恒 $\geq 0$。
要让结果正确，需要改为
```c
return strlen(s) > strlen(t);
```
## Ex 2.27
```c
#include<stdio.h>

int uadd_ok(unsigned x, unsigned y)
{
    unsigned sum = x + y;
    return sum >= x;
}

int main()
{
    unsigned a, b;
    scanf("%u %u", &a, &b);
    if(uadd_ok(a, b))
        puts("uadd_ok");
    else
        puts("overflow");
    return 0;
}
```
## Ex 2.30
```c
#include<stdio.h>

int tadd_ok(int x, int y)
{
    int sum = x + y;
    int pos_flow = x >=0 && y >= 0 && sum < 0;
    int neg_flow = x < 0 && y < 0 && sum >= 0;
    return !pos_flow && !neg_flow;
}

int main()
{
    int a, b;
    scanf("%d %d", &a, &b);
    if(tadd_ok(a, b))
        puts("normal");
    else
        puts("overflow");

    return 0;
}
```
## Ex 2.52
对于 $\frac{25}{32}$，25 为 11001，32 为 $2^5$，所以 $\frac{25}{32}=0.11001_2=1.1001_2\times2^{-1}$，又因为 B 格式只能表示 3 个小数位，所以要舍去 1 位小数，中间值为 $2^1/2=1$，末尾正好是 1，所以向偶数舍入，也就是 $1.100\times2^{-1}$
小数部分为 100，$e=E+bias=-1+7=6=0110_2$
所以为 $0110100_2$

对于 $\frac{31}{2}=11111_2\div2=1111.1_2=1.1111\times2^{3}$，要舍去 1 为小数，所以 $1.000_2\times2^4$，小数部分为 000, $e=4+7=11=1011_2$
所以为 $1011000_2$

对于 $\frac{1}{64}=1.000\times2^{-6}$，小数部分为 000，$e=-6+7=1=0001_2$
所以为 $0001000_2$


