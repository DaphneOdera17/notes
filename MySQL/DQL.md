Data Query Language 数据查询语言，用来查询数据库中表的记录。

```mysql
SELECT
	字段列表
FROM
	表名列表
WHERE
	条件列表
GROUP BY
	分组字段列表
HAVING
	分组后条件列表
ORDER BY
	排序字段列表
LIMIT
	分页参数
```

## 基本查询
### 查询多个字段
```mysql
SELECT 字段1, 字段2,... FROM 表名;
```

```mysql
SELECT * FROM 表名;
```

### 设置别名
```mysql
SELECT 字段1 [AS 别名1], 字段2 [AS 别名2] ... FROM 表名;
```
设置别名的时候 as 可以省略
```mysql
select name xingming From employee;
```
等同于
```mysql
select name as xingming From employee;
```

![|325](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250119215543.png)

### 去除重复记录
```mysql
SELECT DISTINCT 字段列表 FROM 表名;
```

## 条件查询
```mysql
SELECT 字段列表 FROM 表名 WHERE 条件列表;
```

### 条件

| 比较运算符               | 功能                         |
| ------------------- | -------------------------- |
| >                   | 大于                         |
| > =                 | 大于等于                       |
| <                   | 小于                         |
| <=                  | 小于等于                       |
| =                   | 等于                         |
| <> 或 !=             | 不等于                        |
| BETWEEN ... AND ... | 在某个范围之内 (含最小、最大值)          |
| IN(...)             | 在 in 之后的列表中的值，多选一          |
| LIKE 占位符            | 模糊匹配 (\_匹配单个字符, %匹配任意多个字符) |
| IS NULL             | 是 NULL                     |

| 逻辑运算符     | 功能   |
| --------- | ---- |
| AND 或 &&  | 并且   |
| OR 或 \|\| | 或者   |
| NOT 或 ！   | 非，不是 |

### Ex
查询没有身份证号的员工信息
```mysql
select * from emp where idcard is null;
```

查询有身份证号的员工信息
```mysql
select * from emp where idcard is not null;
```

查询年龄在 15 岁 (包含) 到 20 岁 (包含) 的员工信息
```mysql
select * from emp where age between 15 and 20;
```

```mysql
select * from emp where age >= 15 and age <= 20;
```

查询年龄等于 18 或 20 或 40 的员工信息
```mysql
select * from emp where age = 18 or age = 20 or age = 40;
```

```mysql
select * from emp where age in(18, 20, 40);
```

查询姓名为 两个字 的员工信息
```mysql
select * from emp where name like '__'; 
# 两个下划线
```

查询身份证号最后一位是 X 的员工信息
```mysql
select * from emp where idcard like '%X';
```