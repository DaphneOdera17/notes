## 覆盖类型

$n \times m$ 的地需要用 $a \times a$ 的地板覆盖(铺的范围可以更大)

则需要 $ceil(n / a) \times ceil(m / a)$ 的数量

或者 $((n + a - 1) / a) \times ((m + a - 1) / a)$

## 判断连续子串

若存在连续的数量大于等于 $7$ 的子串，则输出 $YES$

可以利用 $string$ 的 $find$

```c++
if(a.find("1111111") != string::npos || a.find("0000000") != string::npos)
   puts("YES");
else
    puts("NO");
```

若在一个字符串中按顺序出现 $hello$ 就输出 $YES$

#### 方法一

按顺序依次比较是否匹配

```c++
#include<bits/stdc++.h>

using namespace std;

char ans[6] = {"hello"}; 
string s;

int main()
{
    cin >> s;
    int k = 0;
    for(int i = 0; i < s.size(); i ++)
    {
        if(s[i] == ans[k])
            k ++;
    }
    if(k >= 5)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

#### 方法二 正则表达式

```c++
#include<regex>
#include<string>
#include<iostream>

using namespace std;

int main()
{
    string s;
    cin >> s;
    regex pat(".*h.*e.*l.*l.*o.*");
    if(regex_search(s, pat))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

#### 方法三 队列

```c++
queue<int> q;
string a = "hello";
string s;
for(int i = 0; i < a.size(); i ++)
    q.push(a[i]);
cin >> s;
for(int i = 0; i < s.size(); i ++)
{
    if(s[i] == q.front())
        q.pop();
}
if(q.empty())
    cout << "YES" << endl;
else
    cout << "NO" << endl;
```



