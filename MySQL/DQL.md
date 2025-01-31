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

## 聚合函数
作用于某一列数据。

| 函数    | 功能   |
| ----- | ---- |
| count | 统计数量 |
| max   | 最大值  |
| min   | 最小值  |
| avg   | 平均值  |
| sum   | 求和   |

null 值不参与所有聚合函数运算。
```mysql
SELECT 聚合函数(字段列表) FROM 表名;
```

查询 emp 表中年龄最小值。
```mysql
select min(age) from emp;
```

## 分组查询 GROUP BY
```mysql
SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名 [HAVING 分组后过滤条件]; 
```

where 和 having 区别
- 执行时机不同：where 是分组之前进行过滤，不满足 where 条件不参与分组。而 having 是分组之后对结果进行过滤。
- 判断时机不同：where 不能对聚合函数进行判断，但是 having 可以。

### Ex
根据性别分组，统计男性员工和女性员工的数量
```mysql
select gender, count(*) from emp group by gender;
```

根据性别分组，统计男性员工和女性员工的平均年龄
```mysql
select gender, avg(age) from emp group by gender;
```

查询年龄小于 45 的员工，并根据工作地址分组，获取员工数量大于等于 3 的工作地址。
```mysql
select workaddress, count(*) address_count from emp where age < 45 group by workaddress having address_count >= 3;
```

## 排序查询 ORDER BY
```mysql
SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1, 字段2 排序方式2;
```

ASC 表示升序 (默认)
DESC 表示降序。

多字段排序，当第一个字段相同时，才会根据第二个字段进行排序。

### Ex
根据年龄对公司的员工进行升序排序
```mysql
select * from emp order by age asc;
```
或者直接省略 asc，因为默认就是
```mysql
select * from emp order by age;
```

根据年龄对公司的员工进行降序排序
```mysql
select * from emp order by age desc;
```

根据年龄对公司的员工进行升序排序，年龄相同时，再按照入职时间进行降序排序。
```mysql
select * from emp order by age, entrydate desc;
```

## 分页查询 LIMIT
```mysql
SELECT 字段列表 FROM 表名 LIMIT 起始索引, 查询记录数;
```

起始索引从 0 开始，为 (查询页码 - 1) * 每页显示记录数。
如果查询的是第一页数据，起始索引可以省略，直接简写为 limit 10。

## DQL 执行顺序

![|550](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250123202834.png)

