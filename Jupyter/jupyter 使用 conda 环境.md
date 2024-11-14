# Jupyter | jupyter notebook 使用 conda 环境
## 创建虚拟环境
在 Anaconda Prompt 里面输入：
```shell
conda create -n env-name
```
并且输入 y 确认。例如我们创建环境名为 jupyter
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240929205221.png" style="zoom:80%">
## 激活环境
```shell
conda activate env-name
```
激活之后发现环境从 base 变为 jupyter(笔者用的 env-name 为 jupyter)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240929205434.png)
## 安装内核
在创建的环境下
```shell
conda install ipykernel
python -m ipykernel install --user --name env-name --display-name "name"
```
比如我们的
```shell
python -m ipykernel install --user --name jupyter --display-name "Python (jupyter)"
```
显示这个说明安装成功
![1061e6e092fa0b6bafb4e35f25edecb.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/1061e6e092fa0b6bafb4e35f25edecb.png)
在创建虚拟环境的文件夹下打开 jupyter notebook
```shell
jupyter notebook
```
创建一个新的 notebook，选择内核的时候看到我们刚才安装的 jupyter 说明成功了。然后选中它进行切换。
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/bbc9a635e229b4007fa0127799a9749.png" style="zoom:70%">
也可以在这里进行切换内核
![e984e0a58bc17bd34be87549603cce9.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/e984e0a58bc17bd34be87549603cce9.png)

下载一些 python 包，在这个虚拟环境下进行下载
例如我们要安装 numpy 
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240929210644.png)
测试
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240929210728.png)
并没有报错，说明安装成功