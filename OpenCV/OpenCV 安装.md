# Ubuntu 22.04 安装 OpenCV 4.7.0 C++ and Python
## 镜像源的替换
```shell
sudo apt-get update
sudo apt-get upgrade
```
## 安装依赖
```shell
sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
```
### 添加 key
```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 40976EAF437D05B5

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32
```
```shell
sudo apt-get update
```
```shell
sudo apt-get install build-essential cmake python3-numpy python3-dev python3-tk libavcodec-dev libavformat-dev libavutil-dev libswscale-dev libdc1394-dev libeigen3-dev libgtk-3-dev libvtk7-qt-dev
```
## 配置代理
```shell
#使用socks5代理（推荐）
git config --global http.https://github.com.proxy socks5://127.0.0.1:51837

#使用http代理（不推荐）
git config --global http.https://github.com.proxy http://127.0.0.1:58591
```
