# VsCode | 修改首页启动页 Logo
## 最终效果：
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503202114.png)
## 插件的安装
先安装插件 Custom CSS and JS Loader
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503210221.png)
### 插件配置
Ctrl + Shift + P 输入
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503210258.png)
打开用户设置，在末尾添加
```json
"vscode_custom_css.imports": [""]
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503210455.png)
## 下载 Logo
下载 Logo
[点我下载](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/VSCode-Thick.png)
## 引入图片
创建一个文件夹 Vs_code_config，里面放入 user.css
```cpp
.editor-group-watermark > .letterpress{
  background-image: url("https://raw.githubusercontent.com/Aikoyori/ProgrammingVTuberLogos/main/VSCode/VSCode-Thick.png") !important;
  opacity: .75;
  aspect-ratio: 3/2 !important;
}
```
但是会因为网络原因可能加载不出来。所以我们可以通过将图片转换 base64 来进行访问。
[base64编码在线转换网站](https://tool.chinaz.com/tools/imgtobase)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503202202.png)
然后将这些编码粘贴到 url 里面，替换掉原先的网页链接并保存
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503210845.png)
### 引入 css
回到用户的 settings.json
将之前输入的改为，其中 file:/// 之后是你 user.css 存放的路径
```json
"vscode_custom_css.imports": ["file:///D:/VS_code_config/user.css"]
```
## 让插件生效
Ctrl + Shift + P 输入 >Enable...
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503210126.png)
点击 Enable Custom CSS and JS
重启 VsCode 生效