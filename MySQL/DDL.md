## 数据库操作
### 查询
查询所有数据库：
```mysql
show databases;
```
查询当前数据库：
```mysql
select database();
```

### 使用
```mysql
use 数据库名;
```

### 创建
创建数据库
```mysql
create database 数据库名;
```

若要指定字符集(例如 utf8mb4)，可以加上
```mysql
create database 数据库名 default charset utf8mb4;
```
### 删除
```mysql
drop database 数据库名;
```

## 表操作
### 查询
查询当前数据库所有表
```mysql
show tables;
```
查询表结构
```mysql
desc 表名;
```
查询指定表的建表语句
```mysql
show create table 表名;
```
### 创建
![|300](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250116221900.png)

comment 为注释，可以忽略。
```mysql
create table tb_user(
    id int comment '编号',
    name varchar(50) comment '姓名',
    age int comment '年龄',
    gender varchar(1) comment '性别'
    ) comment '用户表';
```

查看表结构

![|450](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250116222011.png)

### 修改操作
#### 添加字段
![|450](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250116224357.png)

```mysql
alter table emp add nickname varchar(20) comment '昵称';
```
#### 修改数据类型
```mysql
ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);
```
#### 修改字段名和字段类型
```mysql
alter table emp change nickname username varchar(30) comment '用户名';
```

![|450](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250116224605.png)
#### 删除
```mysql
ALTER TABLE 表名 DROP 字段名;
```

![|425](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250116224739.png)
#### 修改表名
```mysql
alter table 表名 rename to 新表名;
```

![|400](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250116224856.png)

### 删除
删除表
```mysql
DROP TABLE [IF EXISTS] 表名;
```
删除指定表，并重新创建该表
```mysql
TRUNCATE TABLE 表名;
```
## 数据类型
### 数值类型

| 类型            | 大小      | 有符号范围           | 无符号范围      |
| ------------- | ------- | --------------- | ---------- |
| TINYINT       | 1 bytes | (-128, 127)     | (0, 255)   |
| SMALLINT      | 2 bytes | (-32768, 32768) | (0, 65535) |
| MEDIUMINT     | 3 bytes |                 |            |
| INT 或 INTEGER | 4 bytes |                 |            |
| BIGINT        | 8 bytes |                 |            |
| FLOAT         | 4 bytes |                 |            |
| DOUBLE        | 8 bytes |                 |            |
| DECIMAL       |         |                 |            |
### 字符串类型

| 类型         | 大小            | 描述                |
| ---------- | ------------- | ----------------- |
| CHAR       | 0-255 bytes   | 定长字符串             |
| VARCHAR    | 0-65535 bytes | 变长字符串             |
| TINYBLOB   | 0-255 bytes   | 不超过 255 个字符的二进制数据 |
| TINYTEXT   | 0-255 bytes   | 短文本字符串            |
| BLOB       |               | 二进制形式的长文本数据       |
| TEXT       |               | 长文本数据             |
| MEDIUMBLOB |               | 二进制形式的中等长度文本数据    |
| MEDIUMTEXT |               | 中等长度文本数据          |
| LONGBLOB   |               | 二进制形式的极大文本数据      |
| LONGTEXT   |               | 极大文本数据            |
### 日期类型

| 类型        | 格式                  | 描述           |
| --------- | ------------------- | ------------ |
| DATE      | YYYY-MM-DD          | 日期值          |
| TIME      | HH:MM:SS            | 时间值或持续时间     |
| YEAR      | YYYY                | 年份值          |
| DATETIME  | YYYY-MM-DD HH:MM:SS | 混合日期和时间值     |
| TIMESTAMP | YYYY-MM-DD HH:MM:SS | 混合日期和时间值，时间戳 |

### Ex
```mysql
create table emp(
    id int comment '编号',
    workno varchar(10) comment '工号',
    name varchar(10) comment '姓名',
    gender char(1) comment '性别',
    age tinyint unsigned comment '年龄',
    idcard char(18) comment '身份证',
    entrydate date comment '入职时间'
) comment '员工表';
```

