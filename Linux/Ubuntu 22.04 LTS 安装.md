# Linux | 安装并配置 Ubuntu 22.04 LTS
笔者采用的是 VMware Workstation 软件。
## 前期准备
## VMware Workstation 软件
[官方下载网址](https://www.vmware.com/products/workstation-pro.html)
该软件似乎是需要破解的，请读者自行解决。
### 镜像下载
[Ubuntu 官网](https://ubuntu.com/desktop?gad_source=1&gclid=CjwKCAjw57exBhAsEiwAaIxaZsMPkLdcWOm7d0kcc6l1SEcZdaj86yHpSRbbqQ-3MLEWqbyIc0kIERoCipcQAvD_BwE)
点击并下载镜像。
笔者用的是 22.04 版本的镜像，当然也可以选择最新版。安装步骤应该差不多。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240428205949.png)
## 安装系统
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202202.png)
勾选稍后安装操作系统
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202243.png)
版本选择 Ubuntu 64位
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202336.png)
名称和位置根据自己偏好设置
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202446.png)
处理器根据自己电脑情况来，后续也可以进行调整
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202521.png)
内存默认 4GB，也可以调整
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202559.png)
选择 网络地址转换(NAT)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202645.png)

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202710.png)

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202722.png)

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202735.png)
个人认为磁盘大小 50GB 比较合理
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202851.png)
磁盘文件根据给出的来就行
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202931.png)

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427202945.png)

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427203112.png)

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427203144.png)
找到你 iso 的下载路径
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427203222.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427203233.png)
设置完成后打开虚拟机
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427203254.png)
选择第一个并回车（或者等待它自动跳转）
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427203345.png)
语言自行选择，尽量选英文
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427204626.png)
选择键盘布局
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427204704.png)
选择正常安装即可
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427204740.png)
选择清空整个磁盘文件并安装系统
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427204835.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427204903.png)
地区选在上海
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427205007.png)
自行配置名字和密码。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427205108.png)
安装完成后选择重启
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427211442.png)

#### Please remove the installation medium, then reboot
重启的时候如果停留在一个界面显示要移除安装介质并且按下 Enter 的，**直接按 Enter** 就行（笔者忘记截图了）。
输入密码进入系统。

## 更新镜像源
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427212347.png)
找到 Terminal 并打开
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427212605.png)
进入终端界面后，我们先安装 Vim 文本编辑器
```shell
sudo apt install vim
```
提示输入密码，输入并回车（此时输入密码是不显示出来的）
安装完成后输入以下指令备份一份存储镜像源的文件。
```shell
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```
```shell
cd /etc/apt
ls
```
替换镜像：
```shell
sudo vim /etc/apt/sources.list
```
在 vim 文本编辑器中，我们在默认模式下，按下： gg（也就是连按两下 g），跳到行首，然后按下 dG(先按下小写 d, 再按大写 G)。即可清空文本。
然后我们复制进去（可以通过右键找到粘贴）
下面是阿里源，当然你也可以用清华源、中科大源等，别的请自行百度。我们以阿里源作为示范：
[其它镜像源](https://midoq.github.io/2022/05/30/Ubuntu20-04%E6%9B%B4%E6%8D%A2%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F%E6%BA%90/)
```
deb https://mirrors.aliyun.com/ubuntu/ jammy main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ jammy main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ jammy-security main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ jammy-security main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ jammy-updates main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ jammy-updates main restricted universe multiverse

# deb https://mirrors.aliyun.com/ubuntu/ jammy-proposed main restricted universe multiverse
# deb-src https://mirrors.aliyun.com/ubuntu/ jammy-proposed main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ jammy-backports main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ jammy-backports main restricted universe multiverse
```
再按下 :wq (先按下 冒号键:, 再输入 wq) 即可保存。
然后更新(需要进入漫长的等待):
```shell
sudo apt-get update
sudo apt-get upgrade
```

## 更改终端字体、界面
### 更改字体大小
我们会发现终端的字体太小了。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427214123.png)
找到 Preference
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427214156.png)
在 Profiles 下的 Unnamed 
勾选 Custom font:
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427214240.png)
调整字体大小
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427214332.png)
### 更改终端大小
更改 columns 和 rows 即可（需要重启终端才可生效）
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240427214431.png)

## 安装必须工具
```shell
sudo apt install build-essential
```
安装的时候可能会提示：Do you want to continue? 记得输入 Y 然后回车。
安装完成后，g++、gcc、make 等都已安装。
```shell
sudo apt install git
```
## 安装中文输入法
### 安装中文语言包
先在终端输入：
```shell
sudo apt-get remove thunderbird
sudo apt-get install language-pack-zh-han*
```
打开设置进入 Region & Language。选择 Manage installed Languages。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240524225230.png)
不过会出现此报错，忽略即可。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240524225505.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240524225608.png)
找到 Chinese 双击选择并应用。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240524225641.png)
等待系统安装完中文语言包，我们进入下个阶段。
### 安装中文输入法
先在终端输入
```shell
sudo apt-get install ibus-pinyin
```
进入设置。

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240524224319.png)

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240524224343.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240524225816.png)
如果此处没有这个选项，可能需要重启。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240524225832.png)
**$\textcolor{red}{添加后记得重启，否则可能无效!!!}$**
之后即可正常使用中文输入法。
按 win + 空格键 可以切换中英文输入法。
