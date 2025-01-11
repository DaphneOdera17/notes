
```java
String s = "birdy";
```
先从常量池查看是否有 "birdy" 数据空间，如果有的话直接指向；如果没有则重新创建，然后指向。s 最终指向的是常量池的空间地址。

```java
String s2 = new String("birdy");
```
现在堆中创建空间，里面维护了 value 属性，指向常量池的 birdy 空间。如果常量池没有 "birdy", 则重新创建。如果有的话直接通过 value 指向。最终指向的是堆中的空间地址。


String 是一个 final 类，代表不可变的字符序列。
字符串是不可变的。一个字符串对象一旦被分配，其内容是不可变的。

```java
String a = "hello";
String b = "abc";
String c = a + b;
```
在底层，实际上是：
```java
StringBuilder sb = new StringBuilder();
sb.append(a);
sb.append(b);
String c = sb.toString();
```