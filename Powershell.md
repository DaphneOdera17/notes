# Powershell 
## 进入管理员模式
```powershell
Start-Process powershell -Verb runAs
```
## 在此系统上禁止运行脚本
管理员模式下输入
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
```
再输入 Y 并 Enter
## 开放防火墙端口
如果开放端口 7474
```powershell
New-NetFirewallRule -DisplayName "Open Port 7474" -Direction Inbound -Protocol TCP -Action Allow -LocalPort 7474
```

## 取别名
比如给 redis-server 取别名 redis
```shell
Set-Alias -Name redis -Value redis-server
```