/etc/passwd
/etc/shadow
/etc/group 

## 文件
用 su - 切换身份至 root 并查看文件详细权限和属性等(包括隐藏文件)
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609164316.png" style="zoom:50%">
依次为

| 权限         | 链接  | 拥有者  | 用户组  | 文件容量 | 修改日期         | 文件名 |
| ---------- | --- | ---- | ---- | ---- | ------------ | --- |
| drwx------ | 4   | root | root | 4096 | Apr 16 22:58 | .   |
退回到原先身份用 exit
### 文件类型与权限
上述第一列尤为重要，一共有 10 个字符
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609165251.png" style="zoom:70%">
第一个字符代表是目录、文件或链接文件等
d 表示目录
\- 表示文件
| 表示链接文件
b 表示设备文件里面的可供存储的周边设备
c 表示设备文件里面的串行端口设备，如键盘、鼠标

接下来字符每三个为一组，其中：
r 表示可读，w 表示可写，x 表示可执行，没有权限则是 -。
第一组是文件拥有者可具备的权限，第二组为加入此用户组的账号的权限，第三组为非本人且没有加入本用户组的其他账号的权限。

文件名前面多个 . 表示是隐藏文件。
```shell
drwxr-xr-- 
# 文件拥有者可以在本目录进行任何工作
# 用户组可以进入本目录工作但不能进行写入
# 其他用户没有 x 的权限，并不能进入此目录
```
### 修改文件属性和权限
chgrp: 修改文件所属用户组
chown: 修改文件所有者
chmod: 修改文件的权限
#### chmod
各个权限的数字对照表：

|     |     |
| --- | --- |
| r   | 4   |
| w   | 2   |
| x   | 1   |
| rwx | 7   |
| rw- | 6   |
| r-x | 5   |
| r-- | 4   |
| -wx | 3   |
| -w- | 2   |
| --x | 1   |
-rwxr-xr--:
```shell
chmod 754 filename
```
## FHS
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609174924.png)
