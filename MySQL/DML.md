Data Manipulation Language 数据操作语言，用来对数据库中表的数据记录进行增删改操作。

## 添加数据
### 给指定字段添加数据
```mysql
INSERT INTO 表名(字段名1,字段名2,...) VALUES(值1,值2,...);
```

### 给全部字段添加数据
```mysql
INSERT INTO 表名 VALUES(值1,值2,...);
```

### 批量添加数据
```mysql
INSERT INTO 表名(字段名1,字段名2,...) VALUES(值1,值2,...), (值1,值2,...), (值1,值2,...);
```

```mysql
INSERT INTO 表名 VALUES(值1,值2,...), (值1,值2,...), (值1,值2,...);
```

![|525](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250119204544.png)

```mysql
insert into employee(id, workno, name, gender, age, idcard, entrydate) VALUES  
    (1, '1', 'Itcast', '男', 10, '123456789012345678',  
     '2000-01-01');
```
## 修改数据
```mysql
UPDATE 表名 SET 字段名1=值1,字段名2=值2,...[WHERE 条件];
```
修改语句的条件如果没有，则会修改整张表的所有数据。

修改 id=1 的数据的 name 字段为 itheima
```mysql
update employee set name = 'itheima' where id = 1;
```

修改 id=2 的数据的 name 字段为 hhh, gender 为女
```mysql
update employee set name = 'hhh', gender = '女' where id = 2;
```

将所有员工的入职日期修改为 2008-01-01
```mysql
update employee set entrydate = '2008-01-01';
```

## 删除数据
```mysql
DELETE FROM 表名 [WHERE 条件]
```

删除所有性别为女的员工
```mysql
delete from employee where gender = '女';
```

删除所有员工
```mysql
delete from employee;
```