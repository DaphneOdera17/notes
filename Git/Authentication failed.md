
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20241030233257.png)

## 解决方法一：
将 HTTPS 改为 SSH
```shell
git remote -v
git remote set-url origin git@github.com:USERNAME/REPONAME.git
```

## 方法二
```shell
git config --global --unset credential.helper
git config credential.helper store
```
