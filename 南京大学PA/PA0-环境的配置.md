# NJU PA0
使用教程提供的源再进行sudo apt install ... 可能会出现 Unmet dependencies 此类报错
可以安装 aptitude 
```shell
sudo apt install aptitude
sudo aptitude install <package>
```
然后它会提示你，选 n 进行降级。再选 Y 确认
或者
将 /etc/apt/sources.list 下的源改为
```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
```
再输入
```shell
sudo apt-get update
sudo apt-get upgrade
```

对于 git，克隆 ssh 仓库
可能会遇到 ssh: connect to host github.com port 22: Connection refused 这样的报错
解决方案是在 ~/.ssh/config
如果没有则 touch ~/.ssh/config
vim ~/.ssh/config
在其中添加这几行：
```shell
Host github.com
  Hostname ssh.github.com
  Port 443
```
然后再进行 git clone 

当我们运行 make menuconfig
出现以下报错
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240321214235.png)
我们需要安装这些缺少项
```shell
sudo apt install bison
```
再尝试输入 make
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240321214424.png)
同理，安装
```shell
sudo apt install flex
```
即可正常编译