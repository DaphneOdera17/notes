# LazyVim

将缩进从 $2$ 个空格改为 $4$ 个空格

$/nvim/lua/config/options.lua$ 文件添加

```
local opt = vim.opt
opt.shiftwidth = 4 -- Size of an indent
```

