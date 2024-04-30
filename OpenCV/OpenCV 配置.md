# OpenCV | 逆天坑
笔者亲身经历。网上 OpenCV 相关教程太多，但是发现会有漏洞，然后就折腾了半天。。
## 安装 libjasper-dev 出错
$Unable to locate package$
输入：
```shell
sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
```
然而，又会报错。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427233004.png)
需要添加两个 key
```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 40976EAF437D05B5

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427233036.png)
更新
```shell
sudo apt-get update
```
此时再下载就会成功。
```shell
sudo apt install libjasper1 libjasper-dev
```
## CMake 时出错 CMake Warning at cmake/OpenCVDownload.cmake:248 (message):
  data: Download failed: 7;"Couldn't connect to server"

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240428202901.png)
```shell
#使用socks5代理（推荐）
git config --global http.https://github.com.proxy socks5://127.0.0.1:7890
#使用http代理（不推荐）
git config --global http.https://github.com.proxy http://127.0.0.1:7890
```
[参考文章: 设置代理解决github被墙](https://zhuanlan.zhihu.com/p/481574024)
## Undefined reference to 
https://stackoverflow.com/questions/71799459/undefined-reference-to-cvmatmat

## Vscode: undefined symbol: __libc_pthread_init, version GLIBC_PRIVATE
在 vscode 下 make 之后运行


视频教学：
https://www.youtube.com/watch?v=Nn5OfJjBGmg