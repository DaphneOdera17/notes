https://blog.csdn.net/Javascript_tsj/article/details/127163683
# static instance
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

# static methods
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

相当于 static 方法是适用于一个类的。比如:
```java
public class Dog {
	public int weightInPounds;
	
	public static void makeNoise() {
		System.out.println("Bark!");
	}
}
```
可以用如下代码来激发：
```java
Dog.makeNoise();
```
但是，在 makeNoise() 函数中不能直接用 weightInPounds。
而对于 non-static 方法，可以使用 weightInPounds
```java
public static void makeNoise() {
	if(weightInPounds < 10) {
		System.out.println("yipyipyip!");
	} 
}
```
但是，使用 makeNoise 需要先创建一个实例
```java
Dog maya = new Dog(100);
maya.makeNoise();
```



```java
public class Dog {
	public int weightInPounds;

	public Dog(int startingWeight) {
		weightInPounds = startingWeight;
	}

	// static
	public static Dog maxDog(Dog d1, Dog d2) {
		if(d1.weightInPounds > d2.weightInPounds) {
			return d1;
		} else {
			return d2;
		}
	}

	// non-static
	public Dog maxDog(Dog d2) {
		if(weightInPounds > d2.weghtInPounds) {
			return this;
		} else {
			return d2;
		}
	}

	public static void makeNoise() {
		if(weightInPounds < 10) {
			System.out.println("yipyipyip!");
		} 
	}
}

```

```java
public class DogLauncher {
	public static void main(String[] args) {
		Dog chester = new Dog(17);
		Dog yusuf = new Dog(150);

		Dog larger1 = chester.maxDog(yusuf);
		Dog larger2 = Dog.maxDog(chester, yusuf);
		larger1.makeNoise();
		larger2.makeNoise();
	}
}
```