Data Control Language 数据控制语言，用来管理数据库用户、控制数据库的访问权限。
## 管理用户
### 查询用户
```mysql
USE mysql;
SELECT * FROM user;
```
### 创建用户
```mysql
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
```
### 修改用户密码
```mysql
CREATE USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';
```
### 删除用户
```mysql
DROP USER '用户名'@'主机名';
```

## 权限控制
![|600](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250125191646.png)
