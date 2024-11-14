# git | 基础教程

| 命令名称                                | 作用          |
| ----------------------------------- | ----------- |
| git config --global user.name "用户名" |             |
| git config --global user.email 邮箱   |             |
| git init                            | 初始化本地仓库     |
| git status                          | 查看本地库状态     |
| git add 文件名                         | 添加到暂存区      |
| git commit -m "日志信息" 文件名            |             |
| git reflog                          | 查看版本信息      |
| git log                             | 查看版本详细信息    |
| git push                            |             |
| git pull                            |             |
| git reset --hard 版本号                |             |
| git status                          | 查看状态        |
| git config -l                       | 查看 git 所有配置 |
|                                     |             |
|                                     |             |
git 的配置文件一般在 C:\\Users\\用户名\\.gitconfig
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/090103ec08e0c2708c66b1fa25abe90.png" alt="git" style="zoom:67%;" />

忽略文件 .gitignore
![image-20231027201126231](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231027201126231.png)

列出所有本地分支
```shell
git branch 
```

列出所有远程分支
```shell
git branch -r
```

新建一个分支，但是依旧停留在当前分支
```shell
git branch [branch-name]
```

切换分支
```shell
git checkout [branch-name]
```

新建一个分支，并且切换到该分支
```shell
git checkout -b [branch]
```

查看分支
```shell
git branch -v
```

合并指定分支到当前分支
```shell
git merge [branch]
```

删除分支
```shell
git branch -d [branch-name]
```

删除远程分支
```shell
git push origin --delete [branch-name]
git branch -dr [remote/branch]
```

冲突合并的话，执行 git commit 语句最后不能带文件名。

多个分支如果并行执行，就会导致我们的代码不冲突，也就是同时存在多个版本
![image-20231029103818384](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231029103818384.png)

## fatal: refusing to merge unrelated histories
![image-20231208232158990](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231208232158990.png)

```shell
git pull origin main --allow-unrelated-histories
```

## gitignore
忽略根目录下的文件夹 CMakeFiles
忽略 build 文件夹下的 CMakeCache.txt
忽略根目录下的 .vscode 文件夹
```txt
build/CMakeFiles/
build/CMakeCache.txt
.vscode
```
### 清空缓存
```shell
git rm -r --cached .
git add .
git commit -m "update"
git push
```