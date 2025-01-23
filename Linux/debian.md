## 命令找不到
```shell
vim /root/.bashrc
```
在里面添加
```shell
export PATH=$PATH:/usr/sbin
```
让配置文件生效
```shell
source /root/.bashrc
```

## 添加用户到 sudoers 组
```shell
usermod -aG sudo 用户名
```

## 下载 gcc 等工具
```shell
sudo update
sudo apt install build-essential
```
