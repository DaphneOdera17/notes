# $Level13 -> Level14$
在目录下有 sshkey.private 文件，意味我们可以通过 ssh 连接登录。
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240417203628.png)
```shell
cat sshkey.private
```
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240417203704.png)
退出登录。
## $scp$
[菜鸟教程 Linux scp](https://www.runoob.com/linux/linux-comm-scp.html)
scp 即为 Secure copy. 可以基于 ssh 登录进行安全的远程文件拷贝。
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240417205301.png)
参考 scp 从本地复制到远程指令:
```shell
scp local_file remote_username@remote_ip:remote_file
```
将远程服务器 bandit13 中的 sshkey.private 复制到本地根目录。
```shell
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
```
此时会提示登录 bandit13，登录成功之后我们查看本地根目录，发现文件夹下产生了 sshkey.private
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240417205643.png)
## $ssh$
[Linux SSH](http://linux.51yip.com/search/ssh)
> -i identity_file  
    指定一个 RSA 或 DSA 认证所需的身份(私钥)文件. 默认文件是协议第一版的 $HOME/.ssh/identity 以及协议第二版的 $HOME/.ssh/id_rsa 和 $HOME/.ssh/id_dsa 文件. 也可以在配置文件中对每个主机单独指定身份文件. 可以同时使用多个 -i 选项 (也可以在配置文件中指定多个身份文件).

我们通过 sshkey.private 密钥登录
```shell
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```
发现报错
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240417210035.png)
因为该文件的权限除了拥有者，其它组也可以访问。
我们需要修改它的权限。
## $chmod$
[Linux chmod](https://cloud.tencent.com/developer/article/2098260)
Linux 权限共有 3 个组：拥有者、群组、其他组
每个组都可以设置三个权限：r(读)、w(写)、x(执行)。用二进制表示这个权限是否拥有。如下所示。最终我们在指令中用三位八进制表示，每位分别对应权限组。如 777 对应 -rwxrwxrwx
```shell
r-- = 100
-w- = 010 
--x = 001 
--- = 000
```
```shell
rwx = 111 = 7 
rw- = 110 = 6 
r-x = 101 = 5 
r-- = 100 = 4 
-wx = 011 = 3 
-w- = 010 = 2 
--x = 001 = 1 
--- = 000 = 0
```
我们修改他的权限使得只能拥有者访问。700 代表 -rwx------。
```shell
chmod 700 sshkey.private
```

最后，再用指令即可登录。
```shell
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```
