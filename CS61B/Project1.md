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