# 问题解决实录 | bash 中 tmux 颜色显示不全
如下图，tmux 中颜色显示不全:
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240928125100.png)
```shell
echo $TERM
```
输出的是 screen
但在 bash 里面输出的是 xterm-256 color
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240928125245.png)

在 bash 里面输入：
```shell
touch  ~/.tmux.conf
vim ~/.tmux.conf 
set -g default-terminal "xterm-256color"
```
使之生效
```shell
source  ~/.tmux.conf
```
再打开 tmux 现在显示正常
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240928125445.png)
