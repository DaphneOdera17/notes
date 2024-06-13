# Java Compilation
编译器获取 java 文件并把它转换为类文件。
解释器再获取类文件。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240516185425.png)
```shell
javac Hello.java
```
发现生成了 Hello.class 文件
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240516191448.png)
运行程序
```shell
java Hello
```
## public static void main(String\[] agrs)
args 是 commandline arguments 命令行参数。
```java
public class ArgsDemo {
	public static void main(String[] args) {
		System.out.println(args[0]);
	}
}
```
在命令行输入
```shell
javac ArgsDemo
java ArgsDemo hello some args
>> hello
```

```java
public class ArgsSum {
	public static void main(String[] args) {
		int idx = 0;
		int sum = 0;
		while(idx < args.length) {
			sum += Integer.parseInt(args[idx]);
			idx ++;
		}
		System.out.println(sum);
	}
}
```
```shell
java ArgsSum 1 2 3 4 5 6 7 8 
>> 36
```