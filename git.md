git add . 添加到暂存区

git commit -m "消息内容"

git push

git pull

<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/090103ec08e0c2708c66b1fa25abe90.png" alt="git" style="zoom:67%;" />



忽略文件 .gitignore

![image-20231027201126231](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231027201126231.png)



列出所有本地分支

```
git branch 
```

列出所有远程分支

```
git branch -r
```

新建一个分支，但是依旧停留在当前分支

```
git branch [branch-name]
```

新建一个分支，并且切换到该分支

```
git checkout -b [branch]
```

合并指定分支到当前分支

```
git merge [branch]
```

删除分支

```
git branch -d [branch-name]
```

删除远程分支

```
git push origin --delete [branch-name]
git branch -dr [remote/branch]
```



多个分支如果并行执行，就会导致我们的代码不冲突，也就是同时存在多个版本

![image-20231029103818384](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231029103818384.png)



![image-20231208232158990](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231208232158990.png)

```shell
git pull origin main --allow-unrelated-histories
```

