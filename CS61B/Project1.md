# Project1
## LinkedListDeque
实现一个双端队列，每个节点有前驱和后继。
```java
private class Node {  
    private T item;  
    private Node front; /* 前驱节点 */    
    private Node next; /* 后继节点 */    
    private Node(T i, Node n) {  
        item = i;  
        next = n;  
    }
}
```

## ArrayDeque

## GuitarString
笔者选择使用 ArrayDeque。
### TODO 1:
```java
// TODO: uncomment the following import once you're ready to start this portion  
 import deque.ArrayDeque;  
 import deque.Deque;  
// TODO: maybe more imports
```
### TODO 2：
需要创建一个容量为 $\frac{SR}{frequency}$ 的 buffer。提示我们需要用到 Math.round() 以增强精确度，还需要转换为 int 类型，并且初始化 buffer 数组内所有值为 0。
```java
/* Create a guitar string of the given frequency.  */
public GuitarString(double frequency) {  
    // TODO: Create a buffer with capacity = SR / frequency. You'll need to  
    //       cast the result of this division operation into an int. For  
    //       better accuracy, use the Math.round() function before casting.  
    //       Your should initially fill your buffer array with zeros.  
}
```
考虑到 buffer 数组是双精度的，我们初始化的时候用 0.0 填充。
```java
public GuitarString(double frequency) {  
    int capacity = (int)(Math.round(SR / frequency));  
    buffer = new ArrayDeque<>() ;  
    for(int i = 0; i < capacity; i ++)  
        buffer.addLast(0.0);  
}
```
### TODO 3:
用 -0.5 到 0.5 之间的随机值填充 buffer 数组，我们要用到 Math.random() 函数生成 \[0, 1) 之间的实数。
```java
/* Pluck the guitar string by replacing the buffer with white noise. */  
public void pluck() {  
    // TODO: Dequeue everything in buffer, and replace with random numbers  
    //       between -0.5 and 0.5. You can get such a number by using:  
    //       double r = Math.random() - 0.5;  
    //  
    //       Make sure that your random numbers are different from each    
    //       other. This does not mean that you need to check that the numbers    
    //       are different from each other. It means you should repeatedly call    
    //       Math.random() - 0.5 to generate new random numbers for each array index.    
}
```
先把 buffer 首个元素取出来，生成在 \[-0.5, 0.5) 之间的实数值 r，并将它添加到 buffer 中。我们将它添加到最后。
```java
public void pluck() {  
	for(int i = 0; i < buffer.size(); i ++) {  
        buffer.removeFirst();  
        double r = Math.random() - 0.5;  
        buffer.addLast(r);  
    }
}
```
### TODO 4：
提示我们需要先取出 buffer 中第一个元素值并删除，再取出下一个首元素，两者之和乘以 DECAY 并求平均值。
```java
/* Advance the simulation one time step by performing one iteration of  
 * the Karplus-Strong algorithm. */
public void tic() {  
    // TODO: Dequeue the front sample and enqueue a new sample that is  
    //       the average of the two multiplied by the DECAY factor.  
    //       **Do not call StdAudio.play().**  
}
```
注意产生的值类型为 double。
```java
public void tic() {  
    double tmp1 = buffer.removeFirst();  
    double tmp2 = buffer.get(0);;  
    double res = (tmp1 + tmp2) * DECAY * 0.5;  
    buffer.addLast(res);  
}
```
### TODO 5:
```java
/* Return the double at the front of the buffer. */  
public double sample() {  
    // TODO: Return the correct thing.  
}
```
根据题意，也就是取出 buffer 首元素。
```java
public double sample() {  
    return buffer.get(0);  
}
```