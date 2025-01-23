
项目中自己定义的，使用 @Component 及其衍生注解
项目中引入第三方的，使用 @Bean 注解

## bean 注册

| 注解          | 说明               | 位置            |
| ----------- | ---------------- | ------------- |
| @Component  | 声明 bean 的基础注解    | 不属于以下三类时，用此注解 |
| @Controller | @Component 的衍生注解 | 标注在控制器类上      |
| @Service    | @Component 的衍生注解 | 标注在业务类上       |
| @Repository | @Component 的衍生注解 | 标注在数据访问类上     |

yml 配置文件中：
```yml
country:  
  name: China  
  system: socialism
```

```java
@Bean  
public Country country(@Value("${country.name}") String name, @Value("${country.system}") String system) {  
    Country country = new Country();  
    country.setName(name);  
    country.setSystem(system);  
    return country;  
}
```