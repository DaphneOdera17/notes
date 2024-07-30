# CS61C | Venus 使用指南
下载最新版的 Venus 在 https://venus.cs61c.org/jvm/venus-jvm-latest.jar
同时，需要有 java 环境，最好是 java 11
```shell
sudo apt install default-jdk
```
把它放到项目中，可以放到 lab 外侧也可以
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726231116.png)
在终端进入 lab03 目录
```shell
java -jar tools/venusvm-latest.jar . -dm --poport 6162
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726231314.png)
根据提示，打开 [https://venus.cs61c.org](https://venus.cs61c.org/)
 在网站的终端界面，输入 (后面的 key 具体以自己系统的提示为准)
```shell
mount http://localhost:6162 vmfs DHyBVqpMCJX62QmtyzAT60ryjQj7dwgUK5TWzF16BII=
```
此时本地终端会有提示
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726231527.png)
根据提示，我们在本地终端输入 
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726231622.png)
在网页上的 Files 下
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726231709.png)
点击 vmfs 右侧的 Open 即可打开文件目录
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726231807.png)
其它请参考 https://cs61c.org/su24/resources/venus-reference/