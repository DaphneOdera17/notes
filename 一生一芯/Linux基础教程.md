# 一生一芯 | Linux基础教程
![7d715e514169b2c29076babdc485420.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/7d715e514169b2c29076babdc485420.png)
## 比较文件
文本文件的比较：
```shell
vimdiff file1 file2
```
非文本文件的比较
```SHELL
diff file1 file2
```
很大的文件比较, 通过计算出哈希码
```shell
md5sum file1 file2
```
还可以在一个目录下算出所有文件的哈希值
```shell
md5sum *
```

## 踪迹工具
利用 strace
### ls 如何运行
```shell
strace ls
```
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609210223.png" style="zoom:70%">
同理，查看 ls -l 的踪迹
```shell
strace ls -l
```
可以看到最后面有很多 write 的操作，也就是最终显示到屏幕上的内容。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609211833.png)
### ls 如何被寻找
```shell
strace -f bash -c "ls"
```
当我们输入
```shell
strace -f bash -c "abcd"
```
输出的最后确实会有显示 "abcd: command not found"
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609212545.png)
#### PATH 环境变量
当我们用 echo 输出 PATH，可以发现几个路径用冒号隔开。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609213225.png)
当我们终端输入 "abcd" 命令，strace 上显示的查找是在这几个路径之下进行查找。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609213412.png)
若将 PATH 改变，再追踪 ls 命令
```shell
strace -f bash -c "PATH='aaa:bbb:ccc' ls"
```
会发现它确实去 aaa，bbb，ccc 这些路径下去寻找 ls 命令了。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609215510.png)
### 用户如何与 man 交互
```shell
strace -o strace.log -f man ls
tail -f strace.log # 另一个终端输入
```
这样就可以实时追踪。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609222647.png)
## shell 方便的功能
期中 A-f 和 A-b 是 Alt+f 或者 Alt+b
![05b3792178f3b6f03fca324b8054e1c.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/05b3792178f3b6f03fca324b8054e1c.png)
## 通过 alias 为常用命令设置别名
```shell
alias ls="ls --color" # 设置 ls 为彩色输出
```
写入 ~/.bashrc 文件就可以打开终端生效。
### 将 ll 设置为 ls -l
在 ~/.bashrc 中添加：
```text
alias ll='ls -l'
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609224849.png)
保存并使之生效
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609224910.png)
## 正则表达式
[正则表达式 Wiki](https://zh.wikipedia.org/wiki/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609225258.png)
## 任务管理
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609230556.png)
查看进程
```shell
ps aux
```
强制关闭进程
```shell
kill -9 进程号
```
### 进程管理
比如输入 
```shell
yes
```
在系统下会无限输出 y。我们通过另一个终端界面，
```shell
ps aux | grep yes
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609230142.png)
输入
```shell
kill -9 5845
```
可以看到进程被强制关闭。
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609230208.png" style="zoom:50%">
### 查看后台任务
```shell
jobs
```
### 最大化最小化
通过 vim 打开 1.txt 文件，再 Ctrl + Z 将它最小化
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609231147.png)
再打开
```shell
fg %1
```
### 输入输出重定向
将 abc 输入到 temp.txt 文件中
```shell
echo abc > temp.txt 
```
#### 向文件追加输出
```shell
ls >> result.txt
```
#### 将标准错误重定向到文件
```shell
ls 2> /dev/null
```
#### 将标准输入重定向到文件
```shell
sort < result.txt
```