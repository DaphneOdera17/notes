编写一个简单的程序
```c
#include<stdio.h>

int main()
{
	printf("hello world!\n");
	return 0;
}
```
在它的目录下编写一个 $Makefile$ 文件
```makefile
hello:hello.c
	gcc hello.c -o hello

.PHONY: clean

clean:
	rm hello
```

```shell
make
```
会发现通过 gcc 生成了可执行文件 hello
```shell
./hello 
```
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240401211944.png)

Makefile 的编写规则:
	目标文件名:依赖文件列表
	    用于生成目标文件的命令序列   **# 注意开头的tab, 而不是空格**

.PHONY: clean 用于指示 **clean 是一个伪目标**

### 程序的编译
将源代码编译为中间代码文件。例如 Windows 系统下的 .obj 文件，Linux 系统下的 .o 文件(Object File)。
### 程序的链接
将大量 Object File 合成可执行文件的过程