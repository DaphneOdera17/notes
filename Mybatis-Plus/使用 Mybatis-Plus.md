
导入依赖
```xml
<dependency>  
    <groupId>com.baomidou</groupId>  
    <artifactId>mybatis-plus-boot-starter</artifactId>  
    <version>3.5.3.1</version>  
</dependency>
```

定义 Mapper 接口并且继承 BaseMapper
```java
public interface UserMapper extends BaseMapper<User> {
}
```

