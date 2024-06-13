# $Base64$ 编码
[Wiki](https://en.wikipedia.org/wiki/Base64)
![base64编码表](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240121092628109.png)

$Base64$ 用 $6$ 位表示

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240121091417546.png)

将  $echo$ "$HelloWorld$" 的结果作为 $Base64$ 命令的输入来执行一个 $Base64$ 编码操作

## 编码的原理和过程

#### 1.转换编码对象为二进制

$H：01001000$

$e：01100101$

$l：01101100$

$l：01101100$

$o：01101111$

$W：01010111$

$o：01101111$

$r：01110010$

$l：01101100$

$d：01100100$

$\n：00001010$$

再将二进制位从左往右排列，得到字符串的二进制表示

#### 2.把二进制的字符串按照每六位一组来分组

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240121091749052.png)

如果最后一组二进制位不足 $6$ 位，用 $0$ 来补齐

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240121091857123.png)

#### 3.把每一组的二进制位转换成十进制的数字并映射

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240121092008188.png)

就得到了编码之后的结果

$SGVsbG9Xb3JsZAo$

但是需要注意的是，$\textcolor{red}{编码之后的长度必须为 4 的倍数}$

如果不是的话，需要在结尾的位置用 $=$ 来补齐。

因此，结果为

$SGVsbG9Xb3JsZAo=$

## 解码

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240121092530681.png)