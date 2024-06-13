# CS61C | lecture2
C 语言是一种编译语言。C 编译器将 C 程序映射到特定与体系结构的机器代码(实际上是一串 0 和 1)。
而 Java 会通过 JVM(Java 虚拟机) 将代码转换为独立于架构的字节码。
Python 则会直接解释代码。C 不会直接解释代码，而是将其编译成机器代码之后，CPU 直接解释并运行。
## 编译优点
C 的编译优势在于：
1.有很出色的运行性能，通常比 Python 和 Java 快。
2.编译的时候可以允许我们仅重新编译修改了的文件。
## 编译缺点
1.编译文件包括可执行文件是特定于体系结构的，也就是特定于 CPU 类型和操作系统类型。
2.编译过程通常是 编辑、编译、运行 的重复
## 类型转换
C 是一种弱类型语言。
## 结构对齐与填充
```c
struct foo {
	int a;
	char b;
	struct foo *c;
}
```
这段代码在 32 位架构上：

|                    | 字节  |
| :----------------: | :-: |
|         a          |  4  |
|         b          |  1  |
|    unused bytes    |  3  |
|         c          |  4  |
| sizeof(struct foo) | 12  |

32 位计算机上的指针是 32 位，也就是 4 字节。
## Unions
union 可以让元素共享存储空间。同时会占用空间最大的元素提供了充足的空间。


```shell
./foo hello 87
```

|          |         |
| -------- | ------- |
| argv\[0] | "./foo" |
| argv\[1] | "hello" |
| argv\[2] | "87"    |
| argv\[3] | null    |
## 指针
将内存视为一个很大的数组，每个元素有个地址并且存储这一定的值。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240531232124.png)
上图中，p 为指针，指向 x，所以要存储 x 的地址 104
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240531232222.png)
传统在函数中传递参数是通过复制参数的方式，不会对原始变量进行改变。但通过传递引用的方式可以进行修改。
```c
void addOne(int *p) {
	*p = *p + 1;
}

int main() {
	int y = 3;
	addOne(&y); /* y 将变成 4 */
}
```
