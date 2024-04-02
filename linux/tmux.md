[原文链接](https://www.ruanyifeng.com/blog/2019/10/tmux.html)
### 安装
```shell
sudo apt-get install tmux
```
输入
```shell
tmux
```
进入窗口

退出
ctrl+d / 输入 exit

所有快捷键要通过前缀键唤起 ctrl + b
例如进入帮助页面 ctrl + b + ? 
按 q 或者 ESC 退出

第一个启动的 tmux 窗口编号为 0，第二个为 1， 依次类推。
可以用
```shell
tmux new -s <name>
```
来对窗口命名。

在 tmux 窗口中按下 ctrl+b d 或者输入 tmux detach 可以退出当前 Tmux 窗口，但是会话和进程仍在后台运行。

### 查看所有会话
```shell
tmux ls
```
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240401203933.png)

### 重新接入会话
```shell
tmux attach -t <name>
```

### 杀死会话
```
tmux kill-session -t <name>
```

划分窗格
划分为上下两个：
```shell
tmux split-window
```
划分为左右两个：
```shell
tmux split-window -h
```

快捷键
```
- `Ctrl+b %`：划分左右两个窗格。
- `Ctrl+b "`：划分上下两个窗格。
- `Ctrl+b <arrow key>`：光标切换到其他窗格。`<arrow key>`是指向要切换到的窗格的方向键，比如切换到下方窗格，就按方向键`↓`。
- `Ctrl+b ;`：光标切换到上一个窗格。
- `Ctrl+b o`：光标切换到下一个窗格。
- `Ctrl+b {`：当前窗格与上一个窗格交换位置。
- `Ctrl+b }`：当前窗格与下一个窗格交换位置。
- `Ctrl+b Ctrl+o`：所有窗格向前移动一个位置，第一个窗格变成最后一个窗格。
- `Ctrl+b Alt+o`：所有窗格向后移动一个位置，最后一个窗格变成第一个窗格。
- `Ctrl+b x`：关闭当前窗格。
- `Ctrl+b !`：将当前窗格拆分为一个独立窗口。
- `Ctrl+b z`：当前窗格全屏显示，再使用一次会变回原来大小。
- `Ctrl+b Ctrl+<arrow key>`：按箭头方向调整窗格大小。
- `Ctrl+b q`：显示窗格编号。
```
