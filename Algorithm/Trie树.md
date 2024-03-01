# $Trie$ 树

$Trie$ 树是高效地存储和查找字符串集合的数据结构



```cpp
#include<bits/stdc++.h>

using namespace std;

// 快速存储和查找字符串集合

const int N = 1e5 + 10;

int son[N][26], cnt[N], idx; // 下标是 0 的点，既是根节点，又是空节点
char str[N];

void insert(char str[])
{
    int p = 0;
    for(int i = 0; str[i]; i ++)
    {
        int u = str[i] - 'a';
        if(!son[p][u])
            son[p][u] = ++ idx;
        p = son[p][u];
    }

    // 以该点结尾的单词数量 +1
    cnt[p] ++;
}

int query(char str[])
{
    int p = 0;
    for(int i = 0; str[i]; i ++)
    {
        int u = str[i] - 'a';
        if(!son[p][u])
            return 0;
        p = son[p][u];
    }

    return cnt[p];
}

int main()
{
    int n;
    cin >> n;
    while(n --)
    {
        char op[2];
        scanf("%s%s", op, str);
        if(op[0] == 'I')
            insert(str);
        else
            cout << query(str) << endl;
    }

    return 0;
}
```



## 最大异或对



```cpp
#include<bits/stdc++.h>

using namespace std;

const int N = 100010, M = 3e6;

int n;
int son[M][2], idx;
int a[N];

void insert(int x)
{
    int p = 0;
    // i >= 0 等价于 ~i
    // 因为 -1 在二进制补码表示中全为 1，取反后为 0
    for(int i = 30; ~i; i --)
    {
        // s 是引用，s 变了的话数组里的值也会跟这边
        int &s = son[p][x >> i & 1];
        if(!s)
            s = ++ idx; // 创建新节点
        p = s;
    }
}

int query(int x)
{
    int res = 0, p = 0;
    for(int i = 30; ~i; i --)
    {
        // 看 x 的第 i 位是不是 1
        int s = x >> i & 1;
        if(son[p][!s])
        {
            res += 1 << i;
            p = son[p][!s];
        }
        else
        {
            res += 0 << i;
            p = son[p][s];
        }
    }

    return res;
}

int main()
{
    cin >> n;
    for(int i = 0; i < n; i ++)
    {
        cin >> a[i];
        insert(a[i]);
    }

    int res = 0;
    for(int i = 0; i < n; i ++)
        res = max(res, query(a[i]));

    cout << res << endl;

    return 0;
}
```

