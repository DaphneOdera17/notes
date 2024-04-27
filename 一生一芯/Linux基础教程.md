# Linux基础教程
## 比较文件
文本文件的比较：
```shell
vimdiff file1 file2
```
非文本文件的比较
```SHELL
diff file1 file2
```
很大的文件比较, 通过计算出哈希码
```shell
md5sum file1 file2
```
还可以在一个目录下算出所有文件的哈希值
```shell
md5sum *
```
