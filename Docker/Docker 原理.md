# Docker | 入门：原理探究
## Run 的运行流程
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240515171336.png)
## Docker 底层原理
### Docker 是怎么工作的？
> Docker 是一个 Client-Server 结构的系统，Docker 的守护进程运行在主机上，通过 Socket 从客户端访问。DockerServer 接受到 Docker-Client 的指令，就会执行这个命令。

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240515172243.png)
### Docker 为什么比 VM 虚拟机快？
1.Docker 比虚拟机的抽象层少。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240515172602.png)
2.Docker 与宿主机共享 OS，而 VM 是在宿主机 OS 上运行虚拟机 OS。也就是说，Docker 用的是宿主机的内核，而 VM 用的是操作系统内核。