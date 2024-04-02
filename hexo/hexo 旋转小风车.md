
[参考链接](https://zhuanlan.zhihu.com/p/584833753)

打开 \_config.butterfly.yml
找到 Beautify，将 enable 设置为 true，title-prefix-icon 设置为 '\f863'
```yaml
# Beautify (美化頁面顯示)
beautify:
    enable: true
    field: post # site/post
    title-prefix-icon: '\f863' # '\f0c1'
    title-prefix-icon-color: "#F47466"
```

在主题文件夹 source/css/ 中创建一个 icon.css
内容如下：
```css
/* 文章页H1-H6图标样式效果 */
/* 控制风车转动速度 4s那里可以自己调节快慢 */
h1::before,
h2::before,
h3::before,
h4::before,
h5::before,
h6::before {
  -webkit-animation: ccc 4s linear infinite;
  animation: ccc 4s linear infinite;
}
/* 控制风车转动方向 -1turn 为逆时针转动，1turn 为顺时针转动，相同数字部分记得统一修改 */
@-webkit-keyframes ccc {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  to {
    -webkit-transform: rotate(-1turn);
    transform: rotate(-1turn);
  }
}
@keyframes ccc {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  to {
    -webkit-transform: rotate(-1turn);
    transform: rotate(-1turn);
  }
}
/* 设置风车颜色 */
#content-inner.layout h1::before {
  color: #ef50a8;
  margin-left: -1.55rem;
  font-size: 1.3rem;
  margin-top: -0.23rem;
}
#content-inner.layout h2::before {
  color: #fb7061;
  margin-left: -1.35rem;
  font-size: 1.1rem;
  margin-top: -0.12rem;
}
#content-inner.layout h3::before {
  color: #ffbf00;
  margin-left: -1.22rem;
  font-size: 0.95rem;
  margin-top: -0.09rem;
}
#content-inner.layout h4::before {
  color: #a9e000;
  margin-left: -1.05rem;
  font-size: 0.8rem;
  margin-top: -0.09rem;
}
#content-inner.layout h5::before {
  color: #57c850;
  margin-left: -0.9rem;
  font-size: 0.7rem;
  margin-top: 0rem;
}
#content-inner.layout h6::before {
  color: #5ec1e0;
  margin-left: -0.9rem;
  font-size: 0.66rem;
  margin-top: 0rem;
}
/* s设置风车hover动效 6s那里可以自己调节快慢*/
#content-inner.layout h1:hover,
#content-inner.layout h2:hover,
#content-inner.layout h3:hover,
#content-inner.layout h4:hover,
#content-inner.layout h5:hover,
#content-inner.layout h6:hover {
  color: var(--theme-color);
}
#content-inner.layout h1:hover::before,
#content-inner.layout h2:hover::before,
#content-inner.layout h3:hover::before,
#content-inner.layout h4:hover::before,
#content-inner.layout h5:hover::before,
#content-inner.layout h6:hover::before {
  color: var(--theme-color);
  -webkit-animation: ccc 6s linear infinite;
  animation: ccc 6s linear infinite;
}
```

并在 \_config.butterfly.yml 中找到 inject，在 head 下添加 
```css
- <link rel="stylesheet" href="/css/icon.css">
```
也就是
```css
# Inject
# Insert the code to head (before '</head>' tag) and the bottom (before '</body>' tag)
# 插入代码到头部 </head> 之前 和 底部 </body> 之前
inject:
    head:
        - <link rel="stylesheet" href="/css/icon.css">
    bottom:
```

最后
```shell
hexo clean
hexo g
hexo d
```
