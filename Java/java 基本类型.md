
## String
```java
String str = "嘿嘿";  
System.out.println(100 + str);  
System.out.println(str + 100);  
System.out.println(100 + 3 + str);  
System.out.println(str + 100 + 3);  
System.out.println(100 + str + 3);
```
输出：
```
100嘿嘿
嘿嘿100
103嘿嘿
嘿嘿1003
100嘿嘿3
```
### 基本类型转换为 String
```java
int i = 10;  
double d = 10.0;  
float f = 10.0f;  
String s1 = i + "";  
String s2 = d + "";  
String s3 = f + "";  
System.out.println(s1);  
System.out.println(s2);  
System.out.println(s3);
```
输出为
```
10
10.0
10.0
```
### String 转换为基本类型
```java
String S1 = "123";  
int i1 = Integer.parseInt(S1);  
double d1 = Double.parseDouble(S1);  
float f1 = Float.parseFloat(S1);  
  
System.out.println(i1);  
System.out.println(d1);  
System.out.println(f1);
```
输出为
```
123
123.0
123.0
```
而对于转化为 char 类型，要用到 charAt
```java
System.out.println(S1.charAt(0));  
System.out.println(S1.charAt(1));  
System.out.println(S1.charAt(2));
```
输出
```
1
2
3
```
charAt 传入的是索引。
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240915220617.png" style="zoom:70%">

## Float 和 Double
```java
double n1 = 3.1415926535;  
float n2 = 3.1415926535f;  
System.out.println(n1 + "\n" + n2);  
double num1 = 2.7;  
double num2 = 8.1 / 3;  
System.out.println(num1 == num2);  
System.out.println(num1 + "\n" + num2);
```
结果为
```
3.1415926535
3.1415927
false
2.7
2.6999999999999997
```
float 类型精度有限，只能显示大约 7 位有效数字。
对于为什么 8.1 / 3 不是 2.7，是因为数存储在计算机是以二进制形式，8.1 用二进制无法精确表示，在二进制下是一个无限循环的小数，1000.0001100110011...，只能被近似表示，会有精度损失。所以 8.1 / 3 最后的结果也会是个近似值。

注意不能写成
```java
float n2 = 3.1415926535;
```
因为 3.1415926535 是 double 类型，java 默认将所有小数字面视为 double 类型。高精度类型不能自动向低精度类型转换，得强制进行类型转换，所以要在最后加上 f 或 F 来显式指定它是 float 类型。
## 类型转换
(byte, short) 和 char 之间不会相互**自动转换**
从低精度到高精度排序：
```java
char -> int -> long -> float -> double
byte -> short -> int -> long -> float -> double
```
对于：
```java
double d = 100;  
int i = 'a';  
System.out.println(d);  
System.out.println(i);
```
输出结果为
```
100.0
97
```
低精度会向高精度进行转化。100 为 int 类型，而 d 是 double 类型，所以被转换为 double 类型。而 'a' 是 char 类型，i 是 int 类型，所以会转换成 97。
```java
double d = 100;  
int i = 100;  
float f = 10.1f;  
System.out.println(d + i + f);
```
最后打印结果为 210.10000038146973。最终类型取决于 d、i、f 谁的类型精度最大。
### 强制类型转换
```java
int a = (int)1.9;  
System.out.println(a);
```
这样输出就是 1，直接进行截断。
## Byte
byte 范围在 ~128 ~ 127 之间。
当把具体数赋给 byte 时，吸纳判断该数是否在 byte 范围内，如果是就可以。
如果是变量赋值，判断类型。
```java
byte b1 = 10; // 正确，在 -128~127
int n2 = 1;   // n2 是 int，4 个字节
byte b2 = n2; // 错误

char c1 = b1; // 错误，byte 不能自动转成 char
```
## 强制类型转换
数据从高精度->低精度，要用到强制转换。

char 类型可以保存 int 的常量值，但不能保存 int 的变量值
```java
char c1 = 100;     // 正确
int m = 100;   
char c2 = n;       // 错误
cahr c3 = (char)m; // 正确
```
## 自动转换类型细节
byte，short, char 三者可以计算，在计算时首先转换为 int 类型。
```java
byte b2 = 1;
short s1 = 1;
short s2 = b2 + s1;
```

boolean 不参与自动转换
```java
boolean pass = true;
int num100 = pass; // 错误，boolean 不参与类型的转换。
```

