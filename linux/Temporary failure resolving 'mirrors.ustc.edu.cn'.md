# Linux | 修复 Temporary failure resolving 'mirrors.ustc.edu.cn' 等镜像源问题
在执行以下指令(或者在安装东西的时候)
```shell
sudo apt update
```
出现以下报错：
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240428223854.png)
更换镜像源无果。
## 解决方法
```shell
sudo vim /etc/resolv.conf
```
在 nameserver 后添加
```text
nameserver 8.8.8.8  
nameserver 8.8.4.4
```
重启网卡
```shell
sudo nmcli networking off
sudo nmcli networking on
```
再运行
```shell
sudo apt update
```