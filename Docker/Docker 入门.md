# Docker | 入门：安装与配置
## Docker 和传统虚拟机区别
对于传统虚拟机：
	虚拟出一套硬件，运行一个完整的操作系统，并在这个操作系统上安装和运行软件。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240428211106.png)
对于 Docker: 将一个个容器隔离开。
	容器内的应用直接运行在宿主机的内容，容器没有自己的内核。每个容器内都有一个属于自己的文件系统，互不影响。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240428211304.png)
## Docker 的基本组成
镜像(Image):
	类似于一个模板，通过它来创建容器服务。可以创建多个容器，并且最终服务运行或者项目运行就是在容器中。
容器(container):
	容器通过镜像来创建。Docker 通过容器技术，独立运行一个或一组应用。
仓库(repository):
	存放镜像的地方。
## Docker 安装
### Linux 系统安装
[官方文档](https://docs.docker.com/engine/install/ubuntu/)
### 卸载旧版本
```shell
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
### Add Docker's official GPG key:
```shell
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
### Add the repository to Apt sources:
```shell
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
```
### 安装最新版 Docker 软件包
```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
### 测试
查看 Docker 是否安装成功
```shell
docker --version
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240428231218.png)
测试 hello-world
```shell
sudo docker run hello-world
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240428231030.png)
从上图可以看出。Docker run 做的事情：先寻找 hello-world 镜像，如果没找到，就去远程拉取。拉取成功后就运行，输出 Hello from Docker.
### 查看镜像
```shell
docker images
```
会发现存在 hello-world 镜像。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240428231447.png)
### 配置阿里云镜像加速
```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF' 
{ 
	"registry-mirrors":["https://ur5v53mu.mirror.aliyuncs.com"] 
} 
EOF 
sudo systemctl daemon-reload 
sudo systemctl restart docker
```
