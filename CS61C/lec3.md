# CS61C | lecture3
## 运算优先级
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240607130804.png)
$x\&1==0$ 是 $x\&(1==0)$ 而不是 $(x\&1)==0$

```c
int main() {
	int x = 1;
	int y = ++ x; // y = 2, x = 2
	x --; // x = 1
	int z = x ++; // z = 1, x = 2
	return 0;
}
```

## Struct Alignment
在 32 位架构上，int 为 4 字节，short 为 2 字节，指针为 4 字节。
```c
struct hello {
	int a;
	char b;
	short c;
	char *d;
	char e;
};
```
没有对齐的情况下 sizeof(hello) = 4 + 1 + 2 + 4 + 1 = 12

对齐的情况下，存在填充使得边界都为 2 的倍数。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608003553.png)
sizeof(hello) = 4 + 1 + 1 + 2 + 4 + 1 + 3 = 16

如果更换位置，使得 e 在 b 右侧填充的位置，则可以节约空间。
```c
struct hello {
	int a;
	char b;
	char e;
	short c;
	char *d;
};
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608003818.png)
sizeof(hello) = 4 + 1 + 1 + 2 + 4 = 12

## Arrays and Pointers
ar\[0] = \*ar
ar\[2] = \*(ar + 2)

初始化数组有 3 种方式
```c
for(i = 0; i < SIZE; i ++)
	ar[i] = 0;

for(i = 0; i < SIZE; i ++)
	*(ar + 1) = 0;

for(p = ar; p < ar + SIZE; p ++)
	*p = 0;
```

```c
int foo(int array[], unsigned int size)
{
	printf("%d\n", sizeof(array));
}

int main(void) 
{
	int a[10], b[10];
	... foo(a, 10) ...
	printf("%d\n", sizeof(a));
}
```
在 foo 函数中 sizeof(array) 实际上是 sizeof(int \*)。数组在传递给函数时实际上是以指针传递，编译器永远不知道数组的大小，编译器只是把它当作指针。
在 32 位架构上，foo 函数中 sizeof(array) 为 4。
而在 main 函数中编译器知道数组的大小，所以 sizeof(a) = 40。

字符串数组末尾编译器会自动添加 null 终止符，而字符数组则需我们手动添加。
```c
char letters[] = "abc";
const char letters[] = {'a', 'b', 'c', '\0'};
```

```c
#include <stdio.h>
#include <string.h>

int main() 
{
	char s1[10], s2[10], s3[] = "hello", *s4 = "hola";
	strcpy(s1, "hi");
	strcpy(s2, "hi");

	sizeof(s1); // 10
	strlen(s1); // 2
	s1 == s2; // 地址不同
	strcmp(s1, s2); // 0
	strcmp(s1, s3); // 4 (s1 > s3)
	strcmp(s1, s4); // -6 (s1 < s4)
}
```

\*--p 先对 p 进行自减，再解引用。
++\*p 对 \*p 进行自增。
\*p++ 返回 \*p 再自增 p
```c
char *p = "hi"; // 假设 p 存着 40
char c = *p ++;
c = *p;
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608163707.png)
```c
char c = *p ++; // c = 'h', p = 41;
c = *p; // c = 'i';
```

(\*p) ++ 返回 \*p 并对 (\*p) 自增
```c
char arr[] = "bye";
char *p = arr; // c = 'b'. p = 40;
char c = (*p) ++; // c = 'c',因为 'b' + 1 = 'c'
c = *p;
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608164011.png)
## Pointers and Structures
```c
struct Point {
	int x;
	int y;
	struct Point *p;
};

struct Point pt1;
struct Point pt2;
struct Point *ptaddr;
```
点访问
```c
int h = pt1.x;
pt2.y = pt1.y;
```
箭头访问(专门用于指针)
```c
int h = ptaddr -> x;
int h = (*ptaddr).x;
```

地址的赋值，一个结构体发生改变，另一个也会随之改变。
```c
pt1 = pt2;
```


```c
void IncrementPtr(int *p)
{
	p = p + 1;
}

int A[3] = {50, 60, 70};
int *q = A;
IncrementPtr(q);
printf("*q = &d\n", *q);
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608165333.png)
p 将会被移到下一个位置，但是 q 不变。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608165343.png)

```c
void IncrementPtr(int **h)
{
	*h = *h + 1;
}

int A[3] = {50, 60, 70};
int *q = A;
IncrementPtr(&q);
printf("*q = &d\n", *q);
```
让 h 指向 q 指针，从而让 q 移动。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608165452.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608165506.png)


```c
int x[] = {2, 4, 6, 8, 10};
int *p = x;
int **pp = &p;
(*pp) ++;
(*(*pp)) ++;
printf(“%d\n”, *p);
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608165700.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608165743.png)
(\*(\*pp)) ++ 也就是 (\*p) ++ = 4 ++ = 5
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240608165852.png)
最终输出 5。

