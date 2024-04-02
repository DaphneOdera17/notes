themes\\butterfly\\source\\css\\_page\\common.styl
```styl
.layout
  display: flex
  flex: 1 auto
  margin: 0 auto
  padding: 40px 15px
  max-width: 1500px
  width: 100%

  +maxWidth900()
    flex-direction: column

  +maxWidth768()
    padding: 20px 5px

  +minWidth2000()
    max-width: 70%

  & > div:first-child:not(.recent-posts)
    @extend .cardHover
    align-self: flex-start
    padding: 50px 40px

    +maxWidth768()
      padding: 36px 14px

  & > div:first-child
    width: 90% // 默认为 74%
    transition: all .3s

    +maxWidth900()
      width: 100% !important

    if hexo-config('aside.position') == 'left'
      +minWidth900()
        order: 2

  // 隱藏aside
  &.hide-aside
    max-width: 1000px
```

将 & > div:first-child 下的 width 调大