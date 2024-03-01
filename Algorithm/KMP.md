# **KMP**

$S$ 为字符串（长串) $P$ 为模式串，所有字符串中只包含大小写英文字母以及阿拉伯数字，模式串 $P$ 在字符串 $S$ 中多次作为子串出现

## **朴素做法**

```c++
for (int i = 1; i <= n; i ++ )
{
    bool flag = true;
    for (int j = 1; j <= m; j ++ )
    {
        if (s[i + j - 1] != p[j])
        {
            flag=false;
            break;
        }
    }
}
```

![image-20231010151749963](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231010151749963.png)

假设前面都是相等的，到了圈起来的点不相等了。暴力做法是进行 $break$ 然后将整个模式串往后移动一位再进行匹配。

我们想找的是

![image-20231010152042618](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231010152042618.png)

最下面的模式串**最少**要向右移动多少位才能让黑色区域的与 $S$ 的那一段匹配

又因为 $① = ② = ③$ 即是求最长的绿色区段，也就是说求与开头相等的最大值是多少，先将这个预处理出来

<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231010152414414.png" alt="image-20231010152414414" style="zoom:50%;float:left" />



所以，对于原来的字符串，对于每一个点应该预处理出以某个点为终点的后缀和前缀相等的最大长度也就是 $next[i]$ 数组。

他表示以 $i$ 为终点的后缀和从 $1$ 开始的前缀相等，且长度最长

![image-20231010152830856](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231010152830856.png)

![image-20231010152847480](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231010152847480.png)

$next[i] = j$

<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231010153212070.png" alt="image-20231010153212070" style="zoom:67%;float:left" />

则表示

$p[1, j] = p[i - j + 1, i]$

```c++
#include<bits/stdc++.h>

using namespace std;

const int N = 100010, M = 1000010;

int n, m;
char p[N], s[M];
int ne[N]; // 表示 P[1~i] 中最长的与前缀相等的后缀

int main()
{
    cin >> n >> p + 1 >> m >> s + 1;

    // ne[1] = 0; 匹配失败往后退，退到零
    for(int i = 2, j = 0; i <= n; i ++)
    {
        while(j && p[i] != p[j + 1])
        {
            j = ne[j];
        }

        if(p[i] == p[j + 1])
            j ++;
        
        ne[i] = j;
    }

    for(int i = 1, j = 0; i <= m; i ++)
    {
        while(j && s[i] != p[j + 1])
            j = ne[j];
        if(s[i] == p[j + 1])
            j ++;
        if(j == n)
        {
            cout << i - n << " ";
            j = ne[j];
        }
    }
}
```

