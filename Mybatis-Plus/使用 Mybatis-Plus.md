## 导入依赖
```xml
<dependency>  
    <groupId>com.baomidou</groupId>  
    <artifactId>mybatis-plus-boot-starter</artifactId>  
    <version>3.5.3.1</version>  
</dependency>
```

## 定义接口
定义 Mapper 接口并且继承 BaseMapper，同时要指定实体类的泛型，MyBatisPlus 通过扫描实体类，基于反射获取实体类信息作为数据库表信息。
```java
public interface UserMapper extends BaseMapper<User> {
}
```

## 约定
1. 类名驼峰转下划线作为表名。
2. 名为 id 的字段会作为主键。
3. 变量名驼峰转下划线作为表的字段名。

![|375](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250131112044.png)

会转为：
![|575](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250131112112.png)

如果符合约定，则不需要自己去配置。但是不符合约定的话，就需要自己配置。

| 注解          | 作用            |
| ----------- | ------------- |
| @TableName  | 用来指定表名        |
| @TableId    | 用来指定表中的主键字段信息 |
| @TableField | 用来指定表中的普通字段信息 |

使用 @TableField 常用场景：
1. 成员变量名与数据库字段名不一致
2. 成员变量名以 is 开头，且是布尔类型 (is 开头的经过反射处理会把 is 去掉作为变量名)
3. 成员变量名与数据库关键字冲突
4. 成员变量不是数据库字段

如果要生成这样一张表
![|450](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250131114637.png)

```java
@TableName("tb_user")
public class User {
	@TableId(value="id", type=IdType.AUTO)
	private Long id;
	
	@TableField("username")
	private String name;
	
	@TableField("is_married")
	private Boolean isMarried;
	
	@TableField("`order`")
	private Integer order; // 数据库关键字有 order by
	
	@TableField(exist = false)
	private String address; // 数据库中没有 address 字段
}
```