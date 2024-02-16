

利用 $typedef$ 为 $struct~Node$ 起了别名 $node$

```c
typedef struct Node{
	int x;
}node;

node stud;
```

而以下代码是错误的

```c
struct Node{
	int x;
}node;

node stud;
```

