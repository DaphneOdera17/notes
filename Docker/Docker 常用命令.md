# Docker | 入门：常用命令
## 帮助命令
```shell
docker version # 显示 Docker 版本信息
docker info # 显示 Docker 的系统信息(包括镜像和容器数量)
docker 命令 --help # 万能命令
```
[帮助文档](https://docs.docker.com/manuals/)
## 镜像命令
```shell
docker images # 查看所有本地的主机上的镜像
# REPOSITORY 为镜像的仓库
# TAG 镜像的 标签
# IMAGE ID 镜像的 id
# CREATED 镜像的创建时间
# SIZE 镜像的大小
``
# 可选项
-a, --all          # 列出所有镜像
-q, --quiet        # 只显示镜像的 id
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240515185536.png)
[DockerHub](https://hub.docker.com/)
### 搜索镜像
```shell
docker search mysql # 搜索镜像
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240516124946.png)
```shell
docker search mysql --filter=STARS=3000 # 过滤，使得搜索出来的镜像 STARS 大于 3000
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240516125226.png)
### 下载镜像
```shell
docker pull 镜像名字[:tag] # tag 可以加版本，默认是最新版
docker pull mysql # 等价于 docker pull docker.io/library/mysql:latest
docker pull mysql:5.7 # 指定版本下载
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240516125842.png)
### 删除镜像
```shell
docker rmi -f 镜像ID # 删除指定镜像
docker rmi -f 镜像ID 镜像ID 镜像ID # 删除多个镜像
docker rmi -f $(docker images -aq) # 递归删除所有镜像
```
## 容器命令
有了镜像才可以创建容器。
### 下载一个 centos 的镜像
```shell
docker pull centos
```
### 新建容器并启动
```shell
docker run [可选参数] image
# 参数说明
--name="Name" 容器名字 tomcat01 tomcat02 来区分容器
-d            后台方式运行
-it           使用交互方式运行，进入容器查看内容
-p            指定容器端口 -p 8080:8080
	-p ip:主机端口:容器端口
	-p 主机端口:容器端口(常用)
	-p 容器端口
	容器端口
-P            随机指定端口
```
以交互界面方式进入 centos
```shell
docker run -it centos /bin/bash
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240516131355.png)
### 退出容器
```shell
exit # 直接容器停止并且退出
Ctrl + P + Q # 容器不停止并退出
```
与主机目录比较
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240516131558.png)
### 列出所有运行中容器
```shell
docker ps     # 查看运行中容器
docker ps -a  # 查看运行过的容器
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240516131753.png)
### 删除容器
```shell
docker rm -f 容器id              # 删除指定容器
docker rm -f $(docker ps -aq)    # 删除所有容器
docker ps -a -q|xargs docker rm  # 删除所有容器
```
### 启动和停止容器
```shell
docker start 容器id    # 启动容器
docker restart 容器id  # 重启容器
docker stop 容器id     # 停止容器
docker kill 容器id     # 杀死容器
```
## 常用其它命令
### 后台启动容器
基于一个镜像创建并运行一个容器。
```shell
docker run -d 镜像名字
```
然而，当我们运行
```shell
docker run -d centos

docker ps 
```
却发现 centos 停止了。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609145454.png)
实际上，docker 容器使用后台运行，就必须要有一个前台进程，docker 发现没有应用，就会自动停止。
### 查看日志
```shell
docker logs -tf --tail number 容器ID
```
### 查看容器中进程信息
```shell
docker top 容器ID
```
### 查看容器的元数据
```shell
docker inspect 容器ID
```
### 进入当前正在运行的容器
```shell
docker exec -it 容器id bashShell
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609151847.png)
也可以使用
```shell
docker attach 容器id
```

两者区别在于
**docker exec** 进入容器后打开一个新的终端，可以在里面操作
**docker attach** 进入容器正在执行的终端，不会启动新的进程。
### 从容器内拷贝文件到主机上
```shell
docker cp 容器id:容器内路径 目的路径
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609152639.png)
# 总结
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240609152932.png)
