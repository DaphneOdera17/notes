# 问题解决实录 | Python | Failed building wheel for matplotlib
朋友遇到 python 安装 matplotlib 时的问题，笔者帮忙远程调试(踩了不少坑)。网上的解决方案有很多无效，以此来记录以下个人解决方案。
在使用指令
```shell
pip install matplotlib
```
出现如下报错：
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427174142.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427174113.png)
"which is required to install pyproject.toml-based projects"
笔者尝试过使用以下指令无果。
```shell
pip install wheel
```
进入 matplotlib 官网
https://pypi.org/project/matplotlib/
下载最新版 matplotlib
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427174448.png)

在文件夹下有 pyproject.toml 文件
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427174601.png)
终端进入该文件夹，并且在命令行输入
```shell
pip install pyproject.toml
```
(PS: 笔者看见过网上一个解决方案，用 poerty install 但是会有 build-system 的报错，就没有用了)。
当然这时候进行 install matplotlib 是没有用的。因为我们缺乏 Microsoft Visual C++ 14.0

因为缺乏 Microsoft Visual C++ 14.0,需要下载相应的 Build-Tools。最简单的方法是通过 Visual Studio Installer 下载。
进入官网并下载 Visual Studio.
https://visualstudio.microsoft.com/zh-hans/#vs-section
在软件安装界面选择 “使用 C++ 的桌面开发” 并保持右侧勾选项不变。等待其安装完毕。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427175001.png)
此时再运行以下指令，未报错。安装成功。
```shell
pip install pyproject.toml
pip install matplotlib

python -i
>>> import matplotlib as plt
```
(我不知道不在本文件夹下安装会不会出错，我是帮朋友弄完凭记忆写的文章，难免会有漏洞 > _ < )
如果该方案有误或者有更好的建议，欢迎交流~。