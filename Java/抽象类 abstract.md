
当父类的某些方法，需要声明，但是又不确定如何实现时，可以将其声明为抽象方法，那么这个类就是抽象类。
一旦类中包含了 abstract 方法，那么这个类必须声明为 abstract。
抽象类不一定要包含 abstract 方法。
抽象类不能被实例化。
abstract 只能修饰类和方法，不能修饰属性和其他的。

```java
abstract class Animal {
	String name;
	int age;
	abstract public void cry();
}
```

如果一个类继承了抽象类，那么它必须实现抽象类的所有抽象方法，除非他自己也声明为 abstract 类。

抽象方法不能使用 private、final、static 修饰。