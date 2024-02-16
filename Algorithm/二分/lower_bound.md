```c++
#include<algorithm>
```

## lower_bound()

函数原型

```c++
template <class ForwardIterator, class T>
ForwardIterator lower_bound (ForwardIterator first, ForwardIterator last,  const T& val);
```

$ForwardIterator$ 是一个迭代器 $vector<int> v$

在 **有序** 的前提下，返回第一个 **$\textcolor{red}{大于等于}$** $var$ 值的位置



```c++
lower_bound(a, a + n, k)
//二分搜索找出指向满足 ai >= k 的最小的指针
```



```
upper_bound(a, a + n, k)
//指向 ai > k 的最小的指针
```



长度为 $n$ 的有序数组 $a$ 中 $k$ 的个数

```c++
upper_bound(a, a + n, k) - lower_bound(a, a + n, k);
```



查找某个元素是否出现

```c++
binary_search(arr[], arr[] + size, index);
//arr[] 数组首地址
//size 数组元素的个数
//index 需要查找的词
```

