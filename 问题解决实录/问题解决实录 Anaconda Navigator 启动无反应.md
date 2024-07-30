# 问题解决实录 | Anaconda | Anaconda Navigator 启动无反应
以管理员身份运行 Anaconda Prompt
```shell
conda update -n root conda
conda update --all
```
如果执行完以上步骤
碰到 AttributeError: module 'pkgutil' has no attribute 'ImpImporter'. Did you mean: 'zipimporter'? 这个问题
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
之后我们要重新进行上述两个步骤(如果没问题的则不用输入了)
```cmd
conda update -n root conda
conda update --all
```
最后输入
```shell
anaconda-navigator --reset
anaconda-navigator
```
还不行的试试卸载 anaconda-navigator 再进行安装。
此时终于能成功启动！
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240722030103.png)
