# **vector**
变长数组 基本思想：**倍增**

系统为某一程序分配空间时，所需时间基本上与空间大小无关，与申请次数有关。

每一次数组长度不够的时候，就把数组长度乘以 2，再把之前的元素复制过来

申请空间的次数为 log n

额外复制为 O（1）

```c++
size() //返回元素个数
empty()  //返回是否为空
clear() //清空
front() //返回第一个数
back() //返回最后一个数
push_back() //在最后插入一个数
pop_back() //把最后一个数删掉
begin() //第 0 个数
end() //最后一个数的后面一个数
```

遍历方式

```c++
vector<int> a;

for(int i = 0; i < 10; i++) a.push_back(i);

//数组下标遍历
for(int i = 0; i < a.size(); i++) cout << a[i] << ' ';
cout << endl;

//用迭代器遍历
for(vector<int>::iterator i = a.begin(); i != a.end(); i ++)
	cout << *i << " ";
//for(auto i = a.begin(); i != a.end(); i ++)
cout << endl;
//a.begin() 为 a[0]   a.end() 为 a[a.size()] 

//范围遍历
for(auto x : a)
    cout << x << ' ';
cout << endl;

return 0;
```



```c++
vector<int> a(4, 3), b(3, 4);

//字典序比较
if(a < b) puts("a < b");
```



# **pair<int, int>**

存储一个二元组

```c++
pair<int, string> p;
//里面类型可以自定义
```

一些基本操作

```c++
first() //第一个元素
second() //第二个元素

//支持比较运算，按照字典序，以 first 为第一关键字，second 为第二关键字
p = make_pair(10, "abc");
p = {20, "abc"};
```

需要两种不同属性，按一定顺序排序的时候用

还可以存储三种属性

```c++
pair<int, pair<int, int>> p;
//用来存储 3 个不同的东西
```

# **string**

字符串

```c++
substr( ) //可以返回某一个子串
c_str( ) //可以返回 string 字符数组的头指针 
size() //返回字母个数
empty() //判断是否为空
clear() //清空字符串
length() //返回字符串长度 
```

```c++
string a = "zxy";
a += "abc";
a += "123";
```

substr()

```c++
a.substr(1, 2);
//从下标 1 开始，返回 2 个字母
//当第二个数字很大，超过字符串长度时，就会输出到字符串末尾为止
//若省略第二个参数，就是返回从下标为第一个参数开始到末尾的字符串

printf("%s\n", a.c_str());
//a.c_str() 返回 string a 存储字符串的起始地址
```

# **queue**

```c++
push( ) //往队尾插入
front( ) //返回队头元素
back() //返回队尾元素
pop( ) //把队头弹出
```

没有 clear() 函数，但是如果想清空一个队列

```c++
queue<int> q;

//清空队列
q = queue<int>();
```

# **priority_queue**

优先队列 ---> **堆**

```c++
push( ) //插入一个元素
top( ) //返回堆顶元素
pop( ) //弹出堆顶元素
```

默认是 大根堆

如果想定义一个小根堆

向堆中插入一个数的时候，直接插入负数，- x 按照从大到小的顺序排列，实际上就是 x 按照从小到大的顺序进行排列

```c++
priority_queue<int> heap;

heap.push(-x);
```

直接定义小根堆

```c++
#include<queue>
#include<vector>

......
//定义一个小根堆
priority_queue<int, vector<int>, greater<int>> heap;
```

# **stack**

栈

```c++
push( ) //像栈顶插入一个元素
top( ) //返回栈顶元素
pop( ) //弹出栈顶元素
size( )
empty( )
```

# **deque**

双端队列

```c++
size()
clear()
empty()
front() //返回第一个元素
back() //返回最后一个元素
push_back() //向最后插入一个元素
pop_back() //弹出最后一个元素
push_front() //向队首插入一个元素
pop_front() //从队首弹出来一个元素 
begin()
end()
[]
```

缺点：速度比较慢

# **set, map, multiset, multimap**

基于平衡二叉树（红黑树），动态维护有序序列

```c++
size()
empty()
clear()
begin() //支持 ++ -- 操作，返回前驱和后继 O (logn) 
end() //支持 ++ -- 操作，返回前驱和后继 O (logn)
```



```c++
#include<set>
...

set<int> S; //不支持有重复元素
multiset<int> S;
	insert() //插入一个数
	find() //查找一个数
	count() //返回某个数的个数
    erase()
        (1) //输入是一个数 x，删除所有 x  O(k + logn)  k 为 x 的个数
        (2) //输入是一个迭代器，删除这个迭代器
    lower_bound(x) //返回大于等于 x 的最小的迭代器
    upper_bound(x) //返回大于 x 的最小的迭代器
        //不存在范围 end()
        
map/multimap
        insert() //插入的数是一个pair
        erase() //输入的参数时 pair 或者迭代器
        find()
        [] //时间复杂度是 O (logn)
        lower_bound(x)
        upper_bound(x)
```

```c++
map<string, int> a;

a["abc"] = 1;

cout << a["abc"] << endl;
// 1
//完全可以像个数组来用它
```



# **unordered_set, unordered_map, unordered_multiset, unordered_multimap**

**哈希表**

和上面类似，增删查改的时间复杂度是 O（1）

不支持 lower_bound(x)  / upper_bound(x)

也不支持迭代器的 ++ ， --

# **bitset**

**压位**

```c++
bitset<10000>
~, &, |, ^
>>, <<
==, !=
[]

count() //返回有多少个 1
any() //判断是否至少有一个 1
none() //判断是否全为 0 
set() //把所有位置成 1
set(k, v) //将第 k 位变成 v
reset() //把所有位变成 0 
flip() //等价于 ~
flip(k) //把第 k 位取反
```

