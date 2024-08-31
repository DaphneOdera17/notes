# Gitlet
[Project 2: Gitlet](https://sp21.datastructur.es/materials/proj/proj2/proj2)
# 参考资料
[Gitlet 之我见](https://qiushao-e.github.io/2024/08/21/gitlet/)
[Gitlet 完结记录](https://eimy.ink/zh/posts/2023/gitlet-fin/)
## 前期准备
### String[ ] args
考虑以下程序
```java
public class test {
	public static void main(String[] args) {
		System.out.println(args[0]);
	}
}
```
在命令行
```shell
javac test.java
java test one two three
```
命令行将输出 one
### Git 底层原理分析
[深入理解 Git 底层实现原理](http://chuquan.me/2022/05/21/understand-principle-of-git/)
#### Git 结构图
图源 [Git底层原理与分析模型](https://www.cnblogs.com/liqinglucky/p/18239066/git)
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240829200702.png" style="zoom:50%">
#### 数据结构
##### 仓库
当我们在终端输入
```shell
git init
```
便会在该目录下生成文件夹 .git，也就是初始化仓库
##### 分区
Git 
##### 对象 Blob, tree, commit
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240829212124.png)
#### git-SHA1 hash
对于两个内容相同的文件，他们的 git-SHA1 hash 值是相同的。
可以使用
```shell
git hash-object 文件名
```
来查看文件的 git-SHA1 hash 值。
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240829213846.png" style="zoom:70%">
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240829222018.png" style="zoom:50%">
### Git Commit
每次提交 git 至少要存储
```
An author
A date
A commit message
A list of all files and their versions
The parent's commit ID
```
### Serializable 
Java 内置的 Serializable 可以让我们存储任意的 objects。
只需要让我们的 class implement Serializable。
```java
public class Commit implements Serializable {
	...
}
```
