# C++ | STL
## vector
vector<类型> 名字(长度, \[初值])
### 构造
#### 一维数组
```cpp
vector<int> arr;
vector<int> arr(100);     // 构造初始长度为 100 的 int 数组
vector<int> arr(100, 1);  // 构造长度为 100 的 int 数组，初值为 1
```
#### 二维数组
```cpp
vector<vector<int>> dp(5, vector<int> (6, 1)); // 5 行 6 列初值为 1 的数组
```
#### 三维数组
```cpp
vector<vector<vector<int>>> dp2(5, vector<vector<int>> (6, vector<int> (4))); // 相当于 dp[5][6][4]
```
### 尾部操作
#### 尾部插入
输出 1 2 3 
```cpp
vector<int> a;
a.push_back(1);
a.push_back(2);
a.push_back(3);

for(auto e : a)
	cout << e << " ";
```
#### 尾部弹出
此时只输出 1。
```cpp
a.pop_back();
a.pop_back();

for(auto e : a)
	cout << e << " ";
```
### 获取长度
```cpp
cout << a.size() << endl;
```
### 清空 vector
```cpp
a.clear();
```
### 判断是否为空
如果为空，则返回 true，反之 false
```cpp
if(a.empty()) {}
```
### 改变大小
将长度为 3 的 a 数组改为长度为 5 的，最后输出 1 2 3 0 0。
```cpp
vector<int> a;
a.push_back(1);
a.push_back(2);
a.push_back(3);

a.resize(5);

for(auto e : a) 
	cout << e << " ";
```
或者如果想要设置新增加的数初值为特定数，比如设置为 1
```cpp
a.resize(5, 1);
```
### 注意事项
vector 数组存在堆空间。
能提前指定长度应当提前指定长度，而不是用 push_back 一个一个加入。
vector 的 size() 方法返回类型为 size_t。
## stack
### 构造
```cpp
stack<double> stk;
```
### 入栈
```cpp
stk.push(1.1);
stk.push(1.2);
```
### 获取栈顶元素
```cpp
cout << stk.top() << endl;
```
### 出栈
```cpp
stk.pop();
```
### 获取大小
```cpp
cout << stk.size() << endl;
```
