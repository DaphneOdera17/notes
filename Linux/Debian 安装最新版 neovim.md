# Debian 安装最新版 neovim
## 卸载旧版 neovim
```shell
sudo remove neovim
```
## 下载最新版压缩包
```shell
sudo wget https://github.com/neovim/neovim/releases/download/stable/nvim-linux64.tar.gz
```
## 解压并移动
```shell
sudo tar xzvf nvim-linux64.tar.gz
sudo mv nvim-linux64 /usr/local/nvim
```
## 创建软链接
```shell
sudo ln -s /usr/local/nvim/bin/nvim /usr/bin/nvim
```
## 查看版本
```shell
nvim -v
```