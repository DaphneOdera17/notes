# Debian | 更换 Gnome 至 Xfce4
## 更新源
```shell
sudo apt update && sudo apt upgrade
```
## 安装 xfce4
```shell
sudo apt install xfce4
```
我选择 lightdm，回车
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240805232414.png)
## 切换桌面
```shell
sudo update-alternatives --config x-session-manager
```
输入 xfce 所在序号，我这里是 3
## 卸载 Gnome
```shell
sudo apt remove gnome-core
sudo apt remove gnome-shell
```
## 重启
```shell
sudo reboot
```
进入 xfce4 桌面，会有登录验证，输入自己的用户名和密码即可。