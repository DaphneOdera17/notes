# **map**

### **头文件**

包含头文件

```c++
#include <map>
```

创建一个 map

### **创建**

```c++
std::map<KeyType, ValueType> myMap;
```

KeyType 是 键 的类型

ValueType 是 值 的类型

### **插入**

向 map 中插入键值对，可以使用 insert 也可以使用 下标操作符 [ ]

```c++
myMap[key] = value;
```

### **访问**

可以通过键来访问 map 中的值

```c++
ValueType value = myMap[key];
```

### **删除**

可以用 erase 函数删除指定的键值对

```c++
myMap.erase(key); 
```

### **检查键是否存在**

```c++
if (myMap.count(key) > 0) 
{
    // 键存在
} else 
{
    // 键不存在
}
```

### **遍历**

```c++
for (auto it = myMap.begin(); it != myMap.end(); ++ it) 
{
    KeyType key = it->first;
    ValueType value = it->second;
    // 使用 key 和 value 进行操作
}

```

也可以

```c++
for (const auto& pair : myMap) 
{
    KeyType key = pair.first;
    ValueType value = pair.second;
    // 使用 key 和 value 进行操作
}
```

