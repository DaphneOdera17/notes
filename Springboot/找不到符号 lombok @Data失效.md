![44a7a3152911f6fd1fcc3ae93bbab3f.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/44a7a3152911f6fd1fcc3ae93bbab3f.png)

pom.xml 里面把这个自动导入的插件给删掉。

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250111193902.png)

还要手动添加版本号
```xml
<dependency>  
    <groupId>org.projectlombok</groupId>  
    <artifactId>lombok</artifactId>  
    <optional>true</optional>  
    <version>1.18.28</version>  
</dependency>
```
好像直接添加版本号就行了？ 实测不能这样.