# DFS 深度优先搜索

### 迷宫
[AcWing 1114](https://www.acwing.com/problem/content/1114/)
```cpp
#include<bits/stdc++.h>

using namespace std;

const int N = 110;

int n;
char g[N][N];
bool st[N][N];
int xa, xb, ya, yb;

int dx[] = {-1, 0, 1, 0};
int dy[] = {0, 1, 0, -1};

bool dfs(int xx, int yy)
{
    if(g[xx][yy] == '#')
        return false;

    if(xx == xb && yy == yb)
        return true;
    
    st[xx][yy] = true;
    
    for(int i = 0; i < 4; i ++)
    {
        int a = xx + dx[i];
        int b = yy + dy[i];
        if(a < 0 || a >= n || b < 0 || b >= n)
            continue;
        if(st[a][b])
            continue;
        
        if(dfs(a, b))
            return true;
    }

    return false;
}

int main()
{       
    int T;
    cin >> T;

    while(T --)
    {
        cin >> n;
        for(int i = 0; i < n; i ++)
            cin >> g[i];
        memset(st, 0, sizeof st);

        cin >> xa >> ya >> xb >> yb;

        if(dfs(xa, ya))
            puts("YES");
        else
            puts("NO");
    }

    return 0;
}
```
### 红与黑
[AcWing 1115](https://www.acwing.com/problem/content/1115/)
```cpp
#include<bits/stdc++.h>

using namespace std;

const int N = 25;

int n, m;
char g[N][N];
bool st[N][N];

int dx[] = {-1, 0, 1, 0};
int dy[] = {0, 1, 0, -1};

int dfs(int x, int y)
{
    int cnt = 1;
    
    st[x][y] = true;
    for(int i = 0; i < 4; i ++)
    {
        int a = x + dx[i];
        int b = y + dy[i];
        if(a < 0 || a >= n || b < 0 || b >= m)
            continue;
        if(st[a][b])
            continue;
        if(g[a][b] != '.')
            continue;
        
        cnt += dfs(a, b);
    }

    return cnt;
}

int main()
{       
    while(cin >> m >> n, n || m)
    {
        for(int i = 0; i < n; i ++)
            cin >> g[i];
        
        int x, y;
        for(int i = 0; i < n; i ++)
            for(int j = 0; j < m; j ++)
                if(g[i][j] == '@')
                {
                    x = i;
                    y = j;
                }
        memset(st, 0, sizeof st);
        cout << dfs(x, y) << endl;
    }
    
    return 0;
}
```
### 马走日
[AcWing 1118](https://www.acwing.com/problem/content/1118/)
需要回溯。
```cpp
#include<bits/stdc++.h>

using namespace std;

const int N = 10;

int n, m;
bool st[N][N];
int ans;

int dx[] = {2, 1, -1, -2, 2, 1, -1, -2};
int dy[] = {-1, -2, -2, -1, 1, 2, 2, 1};

void dfs(int x, int y, int cnt) // cnt 表示在搜第几个点
{
    if(cnt == n * m)
    {
        ans ++;
        return ;
    }

    st[x][y] = true;

    for(int i = 0; i < 8; i ++)
    {
        int a = x + dx[i];
        int b = y + dy[i];

        if(a < 0 || a >= n || b < 0 || b >= m)
            continue;
        if(st[a][b])
            continue;
        
        dfs(a, b, cnt + 1);
    }

    st[x][y] = false;
}

int main()
{       
    int T;
    cin >> T;

    while(T --)
    {
        int x, y;
        cin >> n >> m >> x >> y;

        memset(st, 0, sizeof st);

        ans = 0;
        dfs(x, y, 1);

        cout << ans << endl;
    }

    return 0;
}
```
### 单词接龙
[洛谷 P1019](https://www.luogu.com.cn/problem/P1019)
```cpp
#include<bits/stdc++.h>

using namespace std;

const int N = 25;

int n;
string word[N];
int g[N][N]; // 两个单词重合最小的长度
int used[N];
char start; // 起始单词
int ans;

void dfs(string s, int last)
{
    ans = max((int)s.size(), ans);
    used[last] ++;

    for(int i = 0; i < n; i ++)
        if(g[last][i] && used[i] < 2)
        {
            dfs(s + word[i].substr(g[last][i]), i);
        }

    used[last] --;
}

int main()
{
    // 先预处理判断 B 能不能放到 A 的后面
    // 预处理之后暴搜

    // 先枚举以给定字母开头的单词
    // 再以这些单词递归向下搜索
    // 每次枚举可以接在后面的单词
    // 直到搜到不能搜为之。更新最大值
    // 回溯

    cin >> n;

    for(int i = 0; i < n; i ++)
        cin >> word[i];
    
    cin >> start;

    // 初始化
    for(int i = 0; i < n; i ++)
        for(int j = 0; j < n; j ++)
        {
            string a = word[i];
            string b = word[j];
            for(int k = 1; k < min(a.size(), b.size()); k ++)
            {
                // 判断 a 的后 k 个字母和 b 的前 k 个字母是否相同
                if(a.substr(a.size() - k, k) == b.substr(0, k))
                {
                    g[i][j] = k;
                    break;
                }
            }
        }

    for(int i = 0; i < n; i ++)
    {
        if(word[i][0] == start)
        {
            dfs(word[i], i);
        }
    }

    cout << ans << endl;

    return 0;
}
```
### 分成互质组
