# **hexo 添加 aplayer 播放器**
## 安装插件
先安装插件 [hexo-tag-aplayer](https://github.com/MoePlayer/hexo-tag-aplayer)
```shell
npm install --save hexo-tag-aplayer
```
## 修改配置
在 hexo 的根目录配置文件 \_config.yml 添加
```yml
aplayer:
  meting: true
  asset_inject: false
```
再在主题配置文件中，以 \_config.butterfly.yml 中找到  aplayerInject
将 enable, per_page 改为 true
```yml
# Inject the css and script (aplayer/meting)
aplayerInject:
    enable: true
    per_page: true
```
再找到 inject 在 bottom 下面添加
```yml
- <div class="aplayer no-destroy" data-id="2740999019" data-server="netease" data-type="playlist" data-fixed="true" data-autoplay="true"> </div>
```
```yml
inject:
    head:
    bottom:
        - <div class="aplayer no-destroy" data-id="2740999019" data-server="netease" data-type="playlist" data-fixed="true" data-autoplay="true"> </div>
```
# 这里的 data-id 对应相应音乐软件播放列表的 id
以网易云为例子，在官网的界面打开，看链接可以找到 id
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240406194433.png)

为了让切换页面之后音乐不会暂停。
在主题配置文件中启用 pjax
```yml
pjax:
    enable: true
```

## 效果
最后 hexo clean & hexo g & hexo s 三连，即可看到播放器。
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240406194841.png)

## 参考链接
[butterfly 官方文档](https://butterfly.js.org/posts/507c070f/#%E6%8F%92%E5%85%A5-Aplayer-html)