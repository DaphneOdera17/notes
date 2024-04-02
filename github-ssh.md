# $github~ssh$

在终端输入

```shell
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

生成密钥

默认在 $\sim/.ssh$ 文件夹下

```shell
cd ~/.ssh
```

会生成 $id\_rsa$ 和 $id\_rsa.pub$ 这两个文件 

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240309183457913.png)

```shell
cat id_rsa.pub
```

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240309183611993.png)

再将这一串密钥复制下来

登陆到 [SSH and GPG keys](https://github.com/settings/keys) 该链接

点击 $New~SSH~key$

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240309183930916.png)

在该界面下输入密钥的名字，在 $Key$ 栏中粘贴刚才复制的密钥

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240309184004773.png)

点击 $Add~SSH~key$ 即可添加成功

在终端，可以用

```shell
ssh -T git@github.com
```

来测试能否连接



克隆仓库的 $SSH$ 地址

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240309184330682.png)

```shell
git clone git@github.com:...
```

即可