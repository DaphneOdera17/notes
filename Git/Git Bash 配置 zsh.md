## 安装 zsh
[安装 Zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)

![|450](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250121215315.png)

## 安装 Oh-my-zsh
[github仓库](https://github.com/ohmyzsh/ohmyzsh)

```bash
sh -c "$(curl -fsSL https://install.ohmyz.sh/)"
```

![|550](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250121204633.png)

## 让 zsh 成为 git bash 默认终端
```bash
vi ~/.bashrc
```

写入：
```.bashrc
if [ -t 1 ]; then
  exec zsh
fi
```

```bash
source ~/.bashrc
```
再重启即可。
## 更换主题
[主题选择](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)

### 安装主题 powerlevel10k
```bash 
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

打开配置文件
```bash
vi ~/.zshrc
```

```.zshrc
ZSH_THEME="powerlevel10k/powerlevel10k"
```

使得主题生效
```bash
source ~/.zshrc
```

如果想重新配置 powerlevel10k 界面
```bash
p10k configure
```

## 插件安装
### 高亮插件
zsh-syntax-highlighting
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### 自动补全插件
zsh-autosuggestions
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

### 使插件生效
```bash
vi ~/.zshrc
```
插件生效
```bash
plugins=( git zsh-syntax-highlighting zsh-autosuggestions )
```

```bash
source ~/.zshrc
```

## 使用 lsd 配色
[官方仓库](https://github.com/lsd-rs/lsd)

![|575](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250121214626.png)

### 安装 lsd
可以使用 scoop 方式，其他方式见官方文档
```bash
scoop install lsd
```

在 `$HOME/.config/lsd ` 下创建配置文件 `config. yml`

![|325](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250121214829.png)

```yml
# == Classic ==
# This is a shorthand to override some of the options to be backwards compatible
# with `ls`. It affects the "color"->"when", "sorting"->"dir-grouping", "date"
# and "icons"->"when" options.
# Possible values: false, true
classic: false

# == Blocks ==
# This specifies the columns and their order when using the long and the tree
# layout.
# Possible values: permission, user, group, context, size, date, name, inode, links, git
blocks:
    - permission
    - user
    - group
    - size
    - date
    - name

# == Color ==
# This has various color options. (Will be expanded in the future.)
color:
    # When to colorize the output.
    # When "classic" is set, this is set to "never".
    # Possible values: never, auto, always
    when: auto
    # How to colorize the output.
    # When "classic" is set, this is set to "no-color".
    # Possible values: default, custom
    # When "custom" is set, lsd will look in the config directory for `colors.yaml`.
    theme: default

# == Date ==
# This specifies the date format for the date column. The freeform format
# accepts a strftime like string.
# When "classic" is set, this is set to "date".
# Possible values: date, locale, relative, '+<date_format>'
# `date_format` will be a `strftime` formatted value. e.g. `date: '+%d %b %y %X'` will give you a date like this: 17 Jun 21 20:14:55
date: date

# == Dereference ==
# Whether to dereference symbolic links.
# Possible values: false, true
dereference: false

# == Display ==
# What items to display. Do not specify this for the default behavior.
# Possible values: all, almost-all, directory-only
# display: all

# == Icons ==
icons:
    # When to use icons.
    # When "classic" is set, this is set to "never".
    # Possible values: always, auto, never
    when: auto
    # Which icon theme to use.
    # Possible values: fancy, unicode
    theme: fancy
    # Separator between icon and the name
    # Default to 1 space
    separator: " "

# == Ignore Globs ==
# A list of globs to ignore when listing.
# ignore-globs:
#   - .git

# == Indicators ==
# Whether to add indicator characters to certain listed files.
# Possible values: false, true
indicators: false

# == Layout ==
# Which layout to use. "oneline" might be a bit confusing here and should be
# called "one-per-line". It might be changed in the future.
# Possible values: grid, tree, oneline
layout: grid

# == Recursion ==
recursion:
    # Whether to enable recursion.
    # Possible values: false, true
    enabled: false
    # How deep the recursion should go. This has to be a positive integer. Leave
    # it unspecified for (virtually) infinite.
    # depth: 3

# == Size ==
# Specifies the format of the size column.
# Possible values: default, short, bytes
size: default

# == Permission ==
# Specify the format of the permission column
# Possible value: rwx, octal, attributes (windows only), disable
permission: rwx

# == Sorting ==
sorting:
    # Specify what to sort by.
    # Possible values: extension, name, time, size, version
    column: name
    # Whether to reverse the sorting.
    # Possible values: false, true
    reverse: false
    # Whether to group directories together and where.
    # When "classic" is set, this is set to "none".
    # Possible values: first, last, none
    dir-grouping: none

# == No Symlink ==
# Whether to omit showing symlink targets
# Possible values: false, true
no-symlink: false

# == Total size ==
# Whether to display the total size of directories.
# Possible values: false, true
total-size: false

# == Hyperlink ==
# Attach hyperlink to filenames
# Possible values: always, auto, never
hyperlink: never

# == Symlink arrow ==
# Specifies how the symlink arrow display, chars in both ascii and utf8
symlink-arrow: ⇒

# == Header ==
# Whether to display block headers.
# Possible values: false, true
header: true

# == Literal ==
# Whether to show quotes on filenames.
# Possible values: false, true
literal: false

# == Truncate owner ==
# How to truncate the username and group names for a file if they exceed a certain
# number of characters.
truncate-owner:
    # Number of characters to keep. By default, no truncation is done (empty value).
    after:
    # String to be appended to a name if truncated.
    marker: ""

```

要注意 permission，改成其他的可能会导致用户名和组别显示 ?

```bash
vi ~/.zshrc
```

添加别名
```
alias ls='lsd'
alias l='ls -l'
alias la='ls -a'
alias lla='ls -la'
alias lt='ls --tree'
```


