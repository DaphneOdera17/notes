[TOC]



# $Bandit$

## $Level~0$

```shell
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

然后再输入 $password$ 

$bandit0$

输入

```shell
ls
```

![image-20231204110003599](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204110003599.png)

```shell
cat readme
```

![image-20231204110039079](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204110039079.png)

获取密码之后退出登录

```shell
exit
```

## $Level~1$

```shell
ssh -p 2220 bandit1@bandit.labs.overthewire.org
```

复制粘贴 $level~0$ 的密码登入

![image-20231204110220752](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204110220752.png)

此时只发现一个名为 $-$ 的东西

![image-20231204110317288](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204110317288.png)

他并不是一个文件夹名字

当我们使用

```shell
vim -
cat -
```

发现都没什么用

事实上

![image-20231204105452618](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204105452618.png)

当我们使用

```shell
cat < -
cat ./-
```

可以输出结果

![image-20231204110634289](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204110634289.png)



接下来不再重复登录以及登出操作

## $Level~3$

![image-20231204110739583](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204110739583.png)

此时列表下存在一个名为 $spaces~in~this~filename$

如果我们直接

![image-20231204110818042](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204110818042.png)

则会提示错误，他把整个文件名字拆成了 $4$ 个不同的文件名字

我们可以用

```shell
cat spac
```

再键入 Tab 键自动补全

![image-20231204110936509](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204110936509.png)

则文件名中如果有空格要用 \ 符号

### $Level~4$

![image-20231204114550042](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204114550042.png)

当我们进入 $inhere$ 目录并且使用 $ls$ 发现没有任何文件

所以我们用

```shell
ls -a
```

列出当前目录下的所有文件，包括隐藏文件

![image-20231204114711247](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204114711247.png)

```shell
cat .hidden
```

获得密码

## $Level~5$

![image-20231204125856394](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204125856394.png)

需要尝试

![image-20231204125838463](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204125838463.png)

### $Level~6$

### $Solution~1$

使用 $find$ 指令

![image-20231204202656658](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204202656658.png)

```shell
find ./ -type f -readable ! -executable -size 1033c
```

$-size~1033$ 来查找文件大小要求

$-type~f$ 仅查看文件

![image-20231204202738822](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204202738822.png)

再使用 $cat$ 命令获取其中的文本

![image-20231204202812349](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204202812349.png)

### $Solution~2$

```shell
ls -la */*
```

$*/*$ 可以获取所有子文件

![image-20231204203714631](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204203714631.png)

### $Solution~3（ERORR)$

使用 $grep$
$$
<command>~|~grep~<pattern>
$$
获取第一个命令的输出并将其作为输入通过管道传入第二个命令中

$*/*$ 可以获取所有文件，但是不包括隐藏的文件

使用 $\{.,\}$ 来包括以 $.$ 开头的文件

$,$ 表示以其他任何内容 

![image-20231204205804377](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204205804377.png)

当我们使用

```shell
file */{.,}* | grep "ASCII text"
```

打印出人类可读的文件类型

![image-20231204210018183](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204210018183.png)

这些文件分为 $with~very~long~lines$ 和 空

为了过滤出不含非常长的行，使用指令

```shell
file */{.,}* | grep "ASCII text" | grep -v ', with very long lines'
```

![image-20231204210516722](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204210516722.png)

然后可以手动检查这些文件（此时是假设文件不包含 $long~lines$

但是从其他方法可知，答案并不在这些文件中

### $Solution~4$

用 $du$ 命令获取文件的大小

如果要获取以字节为单位的大小，要使用 $-b$ 标志。要获取所有文件（包括隐藏文件），可以用 $-a$ 标志

$ls~-l$ 命令会在第五列显示文件的大小

```shell
du -b -a | grep 
```

![image-20231204211304254](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204211304254.png)

### $Level~7$

```shell
ls -l
```

可以查看文件权限

第三列显示用户，第四列显示拥有该文件的组

$find$ 指令提供了查找特定用户 $-user~<username>$ 和 特定组 $-group~<groupname>$ 拥有的文件的标识



当使用命令

```shell
find / -type f -user bandit7 -group bandit6 -size 33c
```

![image-20231204213606274](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204213606274.png)

我们发现会为我们无权限的文件打印 $Permission~denied$ 的报错

可以加上 $2>/dev/null$ 可以隐藏所有错误信息

![image-20231204214052226](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204214052226.png)



## $Level~8$

### $Solution~1$

```shell
vim data.txt
```

在 $vim$ 中键入 $/$

输入 $millionth$

![image-20231204220343353](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231204220343353.png)

### $Solution~2$

```shell
cat data.txt | grep millionth
```

![image-20231205201905360](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231205201905360.png)

## $Level~9$

$uniq$ 基于相同的行进行过滤。

$-u$ 用于过滤唯一的行

$-c$ 可以计数

$-d$ 可以仅返回重复行



$sort$ 可以对文本文件的行进行排序

$-r$ 反向排序

$-n$ 数字排序

![image-20231205202321003](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231205202321003.png)

## $Level~10$

$strings$ 命令可以用来查找人类可读的字符串

```shell
strings data.txt  | grep ==
```

![image-20231205202943794](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231205202943794.png)

## $Level~11$

$base64~[OPTIONS]~[INFILE]~[OUTFILE]$

$-d~or~-decode$

$-e~or~-encode$ 



```shell
cat data.txt
base64 -d data.txt
```

![image-20231205203648397](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231205203648397.png)

## $Level~12$

#### $Rot13$

![image-20231205204604064](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231205204604064.png)

```shell
# Map upper case A-Z to N-ZA-M and lower case a-z to n-za-m
tr 'A-Za-z' 'N-ZA-Mn-za-m' <<< "The Quick Brown Fox Jumps Over The Lazy Dog"
```

```shell
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

![image-20231205204405660](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231205204405660.png)

## $Level~13$

$mkdir~<path>$ 创建新目录

$cp~<source>~<destination>$ 复制文件

$mv~<source>~<destination>$ 移动或者重命名文件


$mktemp~-d$ 创建一个具有随机名称的文件夹

```shell
cd /tmp
mktemp -d
cd #相应的目录名称
cp ~/data.txt .
mv data.txt hexdump_data
```

![image-20231207212925163](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231207212925163.png)



$xxd~<input\_file>~<output\_file>$ 可以创建十六进制转储

$-r$ 可以恢复十六进制传储
