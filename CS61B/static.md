https://blog.csdn.net/Javascript_tsj/article/details/127163683

# $static~instance$
```java
class Book {
	public String title;
	public static Book last = null;
}
```
title 是 instance(实例变量), is specific to each **instance** of the class.
	也就是每次创建一个 Book，它的 title 是独一无二特属于它的。
last is static variable.
	static variable is specific to the **class**.
static 意味着一个类中的所有实例都共享相同的静态变量。
在这里 last will be shared with all instances of the book class.

# $static~methods$
```java
public static String lastBookTitle() {
	return last.title;
}

public String getTitle() {
	return title;
}
```
lastBookTitle is a static method.
可以把静态方法看作是属于类的方法。
getTitle is an instance method.
实例方法属于实例

类的实例可以访问实例方法和变量以及静态方法和变量。
类名**只能**访问静态变量和方法。
It's **wrong** to access title by "Book.title"

如果一个方法并不是真正特定于一个实例，it's rather specific to the whole class. 可以把它设为静态的方法。

我们可以访问实例方法中的静态变量，因为类的实例可以访问静态变量。
但是我们不允许在静态方法中访问实例变量。实例变量特定于实例。

```java
class Book {
	public Book last = null;
	public Book(String name) {
		last = this;
	}
}
```
在构造函数中访问实例变量和静态变量是完全可以的。