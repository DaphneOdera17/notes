ssh: connect to host github.com port 22: Connection refused

默认配置文件在 ~/.ssh/config
如果没有则 touch ~/.ssh/config

vim ~/.ssh/config
在其中添加这几行：

```shell
Host github.com
  Hostname ssh.github.com
  Port 443
```
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240319163811.png)

```

```

