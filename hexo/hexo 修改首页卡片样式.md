# hexo魔改 | 修改首页卡片样式
## 文章卡片效果预览
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240412214100.png" style="zoom: 50%">
## 新建样式
在主题文件夹下 source/css/ 中新建 color.css
```css
.recent-post-item:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}
  
.card-widget.card-info:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-announcement:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-recent-post:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-categories:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-tags:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-archives:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-webinfo:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}
```
## 引入
在主题配置文件中 inject 的 head 下引入 css
```yml
inject:
    head:
        - <link rel="stylesheet" href="/css/color.css">
    bottom:
```

## 侧边栏效果预览
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240412220233.png" style="zoom:50%">
以下的代码笔者均添加到 color.css 中了。
### 让图片呈现圆角状
```css
img {
    border-radius: 8px;
}
```
### 添加悬浮效果
```css
.aside-list-item:hover {
    background-color: #50ccd5; /* 背景 */
    color: white; /* 白色字体 */
    border-radius: 8px; /* 四个角为圆角 */
    transform: scale(1.05); /* 略微放大 */
}
  
.aside-list-item:hover a.title {
    color: white !important; 
}

.aside-list-item:hover time {
    color: white !important;
}
```
### 添加过渡
```css
#aside-content .aside-list > .aside-list-item {
    transition: background-color 0.3s ease, color 0.3s ease,
        border-radius 0.3s ease, transform 0.2s ease, padding-left 0.3s ease,
        margin-left 0.3s ease; /* 添加过渡效果 */
    padding: 5px 5px !important; /* 让框框变大点 */
}
```
## 最终 css 代码
```css
.recent-post-item:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-info:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-announcement:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-recent-post:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-categories:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-tags:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-archives:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

.card-widget.card-webinfo:hover {
    box-shadow: 0 0 0 3px #50ccd5 !important;
}

#aside-content .aside-list > .aside-list-item {
    transition: background-color 0.3s ease, color 0.3s ease,
        border-radius 0.3s ease, transform 0.2s ease, padding-left 0.3s ease,
        margin-left 0.3s ease; /* 添加过渡效果 */
    padding: 5px 5px !important;
}

.aside-list-item:hover {
    background-color: #50ccd5; /* 蓝色背景 */
    color: white; /* 白色字体 */
    border-radius: 8px; /* 四个角为圆角 */
    transform: scale(1.05); /* 略微放大 */
}

.aside-list-item:hover a.title {
    color: white !important; /* 白色字体 */
}

.aside-list-item:hover time {
    color: white !important; /* 白色字体 */
}

img {
    border-radius: 8px;
}
```

## 最重要的！
别忘了！
```shell
hexo clean
hexo g
hexo d
hexo s
```
