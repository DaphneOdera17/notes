# Github | curl Failed
curl: (7) Failed to connect to raw.githubusercontent.com port 443 after 1 ms: Connection refused
```shell
sudo vim /etc/hosts
```
在里面添加：
```
185.199.110.133 raw.githubusercontent.com
```
之后又遇到
Failed to connect to github.com port 443 after 133217 ms: Connection timed out
再在 /etc/hosts 里面添加
```
140.82.113.4 github.com
```


