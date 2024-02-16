# $static$ 

1. 修饰局部变量，称为静态局部变量
2. 修饰全局变量，称为静态全局变量
3. 修饰函数，称为静态函数



```c
void test()
{
	int a = 1;
	a++;
	printf("%d ", a);
}

int main()
{
	int i = 0;
	while (i++ < 10)
		test();

	return 0;
}
```

![image-20231207160728128](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231207160728128.png)

当没有用 $static$ 修饰，每次调用 $test()$ 函数，都会重新创建一个变量 $a$，并且让他的初始值为 $1$

![image-20231207162019692](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231207162019692.png)

而当我们加入 $static$ 修饰时，输出的结果是 $2\sim 11$

$static$ 修饰局部变量，局部变量出了作用域并不会被销毁。本质上，它修饰局部变量的时候，改变了变量的存储位置。静态区的变量出了程序才会销毁。

那是不是每次进入 $test()$,都会新创建一个 $a$ 呢？

当我们观察反汇编

![image-20231207162918163](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231207162918163.png)

会发现,$static~int~a~=~1$ 没有对应的汇编指令，所以后面使用的都是第一次创建的 $a$

实际上，静态变量在编译期间就给他们分配了空间，而不是在运行期间



修饰全局变量

```

```

