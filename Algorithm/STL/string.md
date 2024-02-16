# **string**

预处理串的时候整体可以先往右移动一个，方便下标的处理

```c++
string a = " "; //设置为一个空格
string b;
while(cin >> b)
    a += b;
```

## find

```c++
s.find(c); //在字符串 s 中查找第一个字符 c 的位置，返回下标，如果没有则返回 string::npos
```

## erase

```c++
s.erase(it); //在字符串中删除指针 it 所指向的字符
```

## **substr**

```c++
substr(num) //返回从 num 下标开始的所有字符，包括 num 下标对应的字符
```

```c++
substr(a, b) //返回从 a 下标开始的 b 个字符，[a, a + b - 1)
```

不传入参数默认截取到字符串末尾，如果 $a + b > s.size() - 1$ 则函数会自动只截取到 $s$ 的末尾



## transform

### 转换小写

```c++
transform(str.begin(), str.end(), str.begin(), ::tolower)
```

### 转换大写

```c++
transform(str.begin(), str.end(), str.begin(), ::toupper)
```



## strcmp

```c++
strcmp(a, b);
//当 a 的字典序小于 b 的字典序的时候返回一个负数，当 a 的字典序与 b 的字典序相等返回 0，当 a 的字典序大于 b 的字典序的时候返回一个正数
```

## atoi

```c++
atoi(str.c_str());
```

