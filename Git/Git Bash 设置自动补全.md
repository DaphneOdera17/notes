
在 github 仓库下下载git-completion.bash:
[git-completion](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash)

将文件名改为(也就是在最前面加上一个 .):
.git-completion.bash
将文件放入到 Git 安装目录的 etc 文件夹下

以管理员身份打开同目录下的 bash.bashrc文件
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20241010170548.png)

在文件末尾添加
```bash
source /etc/.git-completion.bash
```