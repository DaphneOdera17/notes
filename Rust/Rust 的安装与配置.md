[Rust 官网](https://www.rust-lang.org/learn/get-started)

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240315235528.png)

双击运行 rustup-init.exe
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240315235608.png)
在终端，选择推荐安装方式，等待安装完成。



```shell
rustc --vesion
cargo --vesion
```

如果能成功查看版本号则成功。

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240316001303.png)


如果要更新 rust, 可以在命令行输入
```shell
rustup update
```

添加国内镜像：
在系统环境变量中
RUSTUP_DIST_SERVER 设置为 https://mirrors.ustc.edu.cn/rust-static

<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240316001107.png"/>
RUSTUP_UPDATE_ROOT 设置为 https://mirrors.ustc.edu.cn/rust-static/rustup

![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240316001214.png)

在 C:\Users\(Username)\.cargo\config 添加： 
```
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"

# 设置源
replace-with = 'ustc' 

# 清华大学
[source.tuna]
registry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"

# 中国科学技术大学
[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"

# 上海交通大学
[source.sjtu]
registry = "https://mirrors.sjtug.sjtu.edu.cn/git/crates.io-index"

# rustcc社区
[source.rustcc]
registry = "git://crates.rustcc.cn/crates.io-index"
```

使用 $cargo$ 指令创建一个新的项目
```shell
cargo new hello_world
```