# Python 3.12: AttributeError: module 'pkgutil' has no attribute 'ImpImporter'. Did you mean: 'zipimporter'?
我是在运行 anaconda navigator 时遇到的问题。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240722025940.png)
用管理员模式启动终端(一定要管理员模式)。
先进行更新 pip(大概版本更新到 23 以上)
```cmd
python -m ensurepip --upgrade
```
用 pip --version 查看自己的版本
接着更新 setuptools
```cmd
pip uninstall -y setuptools
pip install setuptools
```
此时应该下载了最新版的 setuptools
```cmd
pip show setuptools
```
目前最新版是 71.1.0
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240722030456.png)
之后就可以解决问题了。