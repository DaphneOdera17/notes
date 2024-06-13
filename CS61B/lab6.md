# cs61B-sp21 | lab6
## TODO 1
在 CapersRepository.java 中
```java
static final File CAPERS_FOLDER = null; 
// TODO Hint: look at the `join`  
//      function in Utils
```
在 Utils.java 我们找到 join 函数，第一个 join 的作用是将 first 和 others 连接起来形成一个路径，并将其转换为 File 对象返回。而第二个 join 的作用是将 first 对象的路径和 others 连接起来形成一个新的对象并转换为 File 返回。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240526203021.png)
回到 CAPERS_FOLDER，实际上我们是要创建主工作目录，也就是 $(user.dir)/.capers$
```java
static final File CAPERS_FOLDER = join(CWD, ".capers");
```
## TODO 2
在 Dog.java 中
```java
public class Dog { // TODO
	...
}
```
我们需要添加 Serializable 接口
```java
public class Dog implements Serializable
```
## TODO 4
```java
static final File DOG_FOLDER = null; // TODO (hint: look at the `join`  
                                     //      function in Utils)
```
对于 DOG_FOLDER，我们要在 .capers 下创建 dogs 文件夹
```java
static final File DOG_FOLDER = join(".capers", "dogs");
```
## TODO 5
根据注释，这段代码要执行持久化的操作，也就是创建文件夹或者文件，让数据在程序关闭后仍然存在。
```java
/**  
 * Does required filesystem operations to allow for persistence. 
 * (creates any necessary folders or files) 
 * Remember: recommended structure (you do not have to follow): 
 * * .capers/ -- top level folder for all persistent data in your lab12 folder 
 *    - dogs/ -- folder containing all of the persistent data for dogs 
 *    - story -- file containing the current story 
*/
public static void setupPersistence() {  
    // TODO  
}
```
创建 .capers 文件夹，以及 .capers/dogs 文件夹。
```java
CAPERS_FOLDER.mkdir();
Dog.DOG_FOLDER.mkdir();
```
## TODO 6
```java
/**  
 * Appends the first non-command argument in args 
 * to a file called `story` in the .capers directory. 
 * @param text String of the text to be appended to the story  
 */
 public static void writeStory(String text) {  
    // TODO  
}
```
需要先在 .capers 文件夹下创建一个叫做 "story" 的文件，用 join 函数将 .capers 路径和 story 文件名连接。如果该文件存在，说明之前已经写入过字符串，那么提取原来的内容并且与新内容连接。如果该文件不存在，那么文件中内容就是 text。
```java
public static void writeStory(String text) {  
    File f = join(CAPERS_FOLDER, "story");  
    String newStory;  
    if(!f.exists()) {  
        newStory = text;  
    } else {  
        String originStory = readContentsAsString(f);  
        newStory = originStory + '\n' + text;  
    }    writeContents(f, newStory);  
    System.out.println(newStory);  
}
```
## TODO 7
在 Main.java 中的 main 函数
```java
case "dog":  
    validateNumArgs("dog", args, 4);  
    // TODO: make a dog  
    break;
```
首先，输入的参数为\dog \[name] \[breed] \[age]，name 对应 args\[1]，breed 对应 args\[2]，age 对应 args\[3]。再调用 CapersRepository 中的 makeDog 函数即可。注意 age 需要整型，所以我们要进行类型转换。
```java
case "dog":  
    validateNumArgs("dog", args, 4);  
    String name = args[1];  
    String breed = args[2];  
    int age = Integer.parseInt(args[3]);  
    CapersRepository.makeDog(name, breed, age);  
    break;
```
## TODO 8
需要创建并且保存 dog 并传入它的三个参数，并且需要打印这只狗的信息。
```java
/**  
 * Creates and persistently saves a dog using the first 
 * three non-command arguments of args (name, breed, age). 
 * Also prints out the dog's information using toString(). 
*/
public static void makeDog(String name, String breed, int age) {  
    // TODO  
}
```
观察 Dog.java
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240528231631.png" style="zoom:50%">
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240528231726.png" style="zoom:50%">
saveDog 用来将 dog 存储至文件中，toString() 返回一个包含狗的信息的字符串。
```java
public static void makeDog(String name, String breed, int age) {  
    Dog newDog = new Dog(name, breed, age);  
    newDog.saveDog();  
    System.out.println(newDog);  
}
```
## TODO 9
```java
/**  
 * Saves a dog to a file for future use. 
*/
public void saveDog() {  
    // TODO (hint: don't forget dog names are unique)  
}
```
在 Dogs 文件夹下创建这只新狗狗的文件并写入对象。
```java
public void saveDog() {  
    File newDog = join(DOG_FOLDER, name);  
    writeObject(newDog, this);  
}
```
## TODO 10
```java
case "birthday":  
    validateNumArgs("birthday", args, 2);  
    // TODO: celebrate this dog's birthday  
    break;
```
获取要庆祝生日的小狗名称，也就是 args\[1]，并且调用 CapersRepository 中的 celebrateBirthday 函数。
```java
case "birthday":  
    validateNumArgs("birthday", args, 2);  
    name = args[1];  
    CapersRepository.celebrateBirthday(name);  
    break;
```
## TODO 11
```java
/**  
 * Advances a dog's age persistently and prints out a celebratory message. 
 * Also prints out the dog's information using toString(). 
 * Chooses dog to advance based on the first non-command argument of args. 
 * @param name String name of the Dog whose birthday we're celebrating.  
 */
 public static void celebrateBirthday(String name) {  
    // TODO  
}
```
先从文件中获取 Dog，再调用 haveBirthday 函数，最终保存。
```java
public static void celebrateBirthday(String name) {  
    // TODO  
    Dog theDog = Dog.fromFile(name);  
	theDog.haveBirthday();  
	theDog.saveDog();  
}
```
## TODO 12
```java
/**  
 * Reads in and deserializes a dog from a file with name NAME in DOG_FOLDER. 
 * @param name Name of dog to load  
 * @return Dog read from file  
 */
 public static Dog fromFile(String name) {  
    // TODO (hint: look at the Utils file)  
    return null;  
}
```
先获取文件，再读取里面的对象即可。
```java
public static Dog fromFile(String name) {  
    File f = join(DOG_FOLDER, name);  
    return readObject(f, Dog.class);    
}
```

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240528234503.png)
