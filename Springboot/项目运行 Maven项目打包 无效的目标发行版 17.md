
https://blog.csdn.net/Yusian_/article/details/127763882


![|550](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250118125705.png)

![|550](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250118125813.png)

![|550](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250118125837.png)

![|550](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250118125851.png)

![|550](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250118125918.png)


pom. xml

```xml
<properties>  
    <java.version>17</java.version>  
    <maven.compiler.source>17</maven.compiler.source>  
    <maven.compiler.target>17</maven.compiler.target>  
    <maven.compiler.release>17</maven.compiler.release>  
</properties>
```

插件
```xml
<plugin>  
    <groupId>org.apache.maven.plugins</groupId>  
    <artifactId>maven-compiler-plugin</artifactId>  
    <version>3.10.1</version>  
    <configuration>        <source>17</source>  
        <target>17</target>  
    </configuration>
</plugin>
```

Maven 
![|550](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250118125733.png)

D:\apache-maven-3.9.8\conf\settings. xml

```xml
<profile>
          <id>jdk-version-17</id>
          <activation>
              <activeByDefault>true</activeByDefault> 
          </activation>
          <properties>         	<maven.compiler.source>17</maven.compiler.source>         <maven.compiler.target>17</maven.compiler.target>  
	  </properties>
  </profile>
```

```xml
<activeProfiles>
        <activeProfile>jdk-version-17</activeProfile>  
</activeProfiles>
```

