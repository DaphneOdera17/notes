
Aspect Oriented Programming 面向切面编程，也就是面向特定方法编程。

引入依赖
```java
<dependency>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-aop</artifactId>  
</dependency>
```

注解
```java
@Component
@Aspect
```

连接点：JoinPoint，可以被 AOP 控制的方法 (暗含方法执行时的相关信息)
通知： Advice，指哪些重复的逻辑，也就是共性功能 (最终体现为一个方法)
切入点：PointCut，匹配连接点的条件，通知仅会在切入点方法执行时被应用。
切面：Aspect，描述通知与切入点的对应关系
目标对象：Target，通知所应用的对象

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250117142511.png)

执行流程：
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250117142616.png)

## 通知类型

|                 |                                       |
| --------------- | ------------------------------------- |
| @Around         | 环绕通知，此注解标注的通知方法在目标方法前、后都被执行           |
| @Before         | 前置通知，此注解标注的通知方法在目标前被执行                |
| @After          | 后置通知，此注解标注的通知方法在目标后被执行，无论是否异常都会执行     |
| @AfterReturning | 返回后通知，此注解标注的通知方法在目标方法后被执行，**有异常不会执行** |
| @AfterThrowing  | 异常后通知，此注解标注的通知方法发生异常后执行               |

@Around 环绕通知需要自己调用 ProceedingJoinPoint. proceed() 来让原始方法执行，其他通知不需要考虑目标方法执行。并且它的返回值必须指定为 Object，来接收原始方法的返回值。

## 通知顺序
不同切面类中，默认按照切面类的类名字母排序。
- 目标方法前的通知方法：字母排名靠前的先执行
- 目标方法后的通知方法：字幕排名靠前的后执行

可以用 `@Order(数字)` 加在切面类上来控制顺序
- 目标方法前的通知方法：数字小的先执行
- 目标方法后的通知方法：数字小的后执行

## 切入点表达式
主要用来决定项目中的哪些方法需要加入通知

- `execution(...)` 根据方法的签名来匹配
- `@annotation(...)` 根据注解匹配

```java
@Before("execution(* com.itheima.service.impl.DeptServiceImpl.*(..))")
```

```java
execution(访问修饰符? 返回值 包名.类名.?方法名(方法参数) throws 异常?)
```
? 表示可以省略的部分
- 访问修饰符：可省略，比如 public、protected
- 包名. 类名：可省略
- throws 异常：可省略（注意是方法上声明抛出的异常，不是实际抛出的异常）

```java
@Before("@annotation(com.itheima.anno.Log)")
```

通配符
![|525](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250117154504.png)


注解的方式
创建一个注解 MyLog
```java
@Retention(RetentionPolicy.RUNTIME)  
@Target(ElementType.METHOD)  
public @interface MyLog {  
  
}
```

在对应的方法上加上
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20250117155711.png)

最后
```java
@Slf4j  
@Aspect  
@Component  
public class MyAspect6 {  
    @Pointcut("@annotation(com.itheima.aop.MyLog)")  
    private void pt() {  
  
    }  
  
    @Before("pt()")  
    public void before() {  
        log.info("MyAspect6 ... before ...");  
    }  
}
```

## 连接点
对于 @Around 连接点获取只能用 ProceedingJoinPoint
对于其它四种通知，只能使用 JoinPoint，他是 ProceedingJoinPoint 的父类型
```java
@Slf4j  
@Aspect  
@Component  
public class MyAspect7 {  
    @Pointcut("execution(* com.itheima.service.DeptService.*(..))")  
  
    private void pt() {}  
  
    @Before("pt()")  
    public void before(JoinPoint joinPoint) {  
        log.info("MyAspect7 ... before ...");  
    }  
  
    @Around("pt()")  
    public Object around(ProceedingJoinPoint joinPoint) throws Throwable {  
        log.info("MyAspect7 around before ...");  
  
        // 获取目标对象的类名  
        String className = joinPoint.getTarget().getClass().getName();  
        log.info("目标对象的类名:{}", className);  
  
        // 获取目标方法的方法名  
        String methodName = joinPoint.getSignature().getName();  
        log.info("目标方法的方法名: {}",methodName);  
  
        // 获取目标方法运行时传入的参数  
        Object[] args = joinPoint.getArgs();  
        log.info("目标方法运行时传入的参数: {}", Arrays.toString(args));  
  
        // 放行 目标方法执行  
        Object result = joinPoint.proceed();  
        log.info("目标方法运行的返回值: {}",result);  
  
        // 获取 目标方法运行的返回值  
        log.info("目标方法运行的返回值: {}",result);  
  
        log.info("MyAspect7 around after ...");  
        return result;  
    }  
}
```

