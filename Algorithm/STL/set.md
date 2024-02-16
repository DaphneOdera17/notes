# **set**

set 是一个内部自动有序且不含重复元素的容器

```c++
#include<set>
```

set 内的元素自动递增排序，且自动去除了重复元素。

```c++
size() //返回 set 中元素的个数 O(1)
clear() //清空 set O(n)
begin() //返回指向 set 开头的迭代器 O(1)
end() //返回指向 set 末尾的迭代器	O(1)
insert(key) //向 set 中插入元素 key O(logn)
erase(key) //删除含有 key 的元素 O(logn)
find(key) //搜索与 key 一致的元素，并返回指向该元素的迭代器，没有与 key 一致的元素则返回末尾 end() O(logn)
```

set 由二叉搜索树实现，并且对树进行了平衡处理

