# 宽度优先搜索

每次取出队头元素，将扩展出的所有元素放到队尾

层序遍历

<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20240218155259842.png" alt="image-20240218155259842" style="zoom: 80%;" />
$$
queue:\\最开始队列中[1]~~~~~~~~~~~~~~~~~~~~~~~~~~\\ 取出1并加入3,4
-->[2, 3, 4]~ \\
~~~取出2并加入5,6-->[3, 4, 5, 6] \\
~~~~~~~取出3并加入7,8-->[4, 5, 6, 7, 8] \\
取出4-->[5, 6, 7, 8] ~~~~~~~~~~~~~\\
取出5-->[6,7,8] ~~~~~~~~~~~~~~~~\\
取出6-->[7, 8]~~~~~~~~~~~~~~~~~~~~\\
~~~取出7并加入9,10-->[8, 9, 10]\\
取出8-->[9, 10]~~~~~~~~~~~~~~~~~~\\
取出9-->[10]~~~~~~~~~~~~~~~~~~~~~\\
取出10-->[]~~~~~~~~~~~~~~~~~~~~~~~
$$


判重数组 st\[] 入队时判重

初始状态入队

当队列不空的时候，每次取出队头元素，扩展队头元素，将新节点插入到队尾（没有出现过的话）

## 迷宫问题
[原题链接](https://www.acwing.com/problem/content/1078/)
```cpp
#include<bits/stdc++.h>
#define x first 
#define y second

using namespace std;

const int N = 1050;

typedef pair<int, int> PII;

int n;
int g[N][N];
PII q[N * N];
PII pre[N][N];

int dx[] = {-1, 0, 1, 0};
int dy[] = {0, 1, 0, -1};

void bfs(int sx, int sy)
{
    int hh = 0, tt = 0;
    q[0] = {sx, sy};

    memset(pre, -1, sizeof pre);

    pre[sx][sy] = {0, 0};
    while(hh <= tt)
    {
        PII t = q[hh ++];

        for(int i = 0; i < 4; i ++)
        {
            int a = t.x + dx[i];
            int b = t.y + dy[i];

            if(a < 0 || a >= n || b < 0 || b >= n)
                continue;
            if(g[a][b])
                continue;
            if(pre[a][b].x != -1)
                continue;
            
            q[++ tt] = {a, b};
            pre[a][b] = t;
            
        }
    }
}

int main()
{   
    cin >> n;

    for(int i = 0; i < n; i ++)
        for(int j = 0; j < n; j ++)
            cin >> g[i][j];
    
    bfs(n - 1, n - 1);

    PII end(0, 0);

    while(1)
    {
        cout << end.x << " " << end.y << endl;
        if(end.x == n - 1 && end.y == n - 1)
            break;
        end = pre[end.x][end.y]; 
    }

    return 0;
}
```

## 武士风度的牛
[原题链接](https://www.acwing.com/problem/content/190/)
```cpp
#include<bits/stdc++.h>
#define x first 
#define y second

using namespace std;

typedef pair<int, int> PII;
const int N = 155;

int n, m;
char g[N][N];
PII q[N * N];
int dist[N][N];
int dx[] = {-2, -1, 1, 2, 2, 1, -1, -2};
int dy[] = {1, 2, 2, 1, -1, -2, -2, -1};

int bfs()
{
    int sx, sy;
    for(int i = 0; i < n; i ++)
        for(int j = 0; j < m; j ++)
            if(g[i][j] == 'K')
            {
                sx = i;
                sy = j;
                break;
            }
    
    int hh = 0, tt = 0;
    q[0] = {sx, sy};

    memset(dist, -1, sizeof dist);
    dist[sx][sy] = 0;

    while(hh <= tt)
    {
        auto t = q[hh ++];

        for(int i = 0; i < 8; i ++)
        {
            int a = t.x + dx[i];
            int b = t.y + dy[i];
            if(a < 0 || a >= n || b < 0 || b >= m)
                continue;
            if(g[a][b ] == '*')
                continue;
            if(dist[a][b] != -1)
                continue;
            if(g[a][b] == 'H')
                return dist[t.x][t.y] + 1;

            dist[a][b] = dist[t.x][t.y] + 1;
            q[++ tt] = {a, b};
        }
    }

    return -1;
}

int main()
{
    cin >> m >> n;

    for(int i = 0; i < n; i ++)
        cin >> g[i];

    cout << bfs() << endl;

    return 0;
}
```

## 抓住那头牛
[原题链接](https://www.acwing.com/problem/content/1102/)
```cpp
#include<bits/stdc++.h>

using namespace std;

const int N = 2e5 + 10;

int n, k;
int q[N];
bool st[N];
int dist[N];

int bfs()
{
    memset(dist, -1, sizeof dist);
    dist[n] = 0;
    q[0] = n;

    int hh = 0, tt = 0;
    while(hh <= tt)
    {
        int t = q[hh ++];

        if(t == k)
            return dist[k];
        
        if(t + 1 < N && dist[t + 1] == -1)
        {
            dist[t + 1] = dist[t] + 1;
            q[++ tt] = t + 1;
        }
        if(t - 1 >= 0 && dist[t - 1] == -1)
        {
            dist[t - 1] = dist[t] + 1;
            q[++ tt] = t - 1;
        }
        if(t * 2 < N && dist[t * 2] == -1)
        {
            dist[t * 2] = dist[t] + 1;
            q[++ tt] = t * 2;
        }
    }
    return -1;
}

int main()
{
    cin >> n >> k;
    
    cout << bfs() << endl;
    
    return 0;
}
```

# 多源 BFS
## 矩阵距离
[原题链接](https://www.acwing.com/problem/content/175/)
```cpp
#include<bits/stdc++.h>
#define x first 
#define y second

using namespace std;

typedef pair<int, int> PII;

const int N = 1010;
PII q[N * N];
char g[N][N];
int dist[N][N];
int n, m;

int dx[] = {-1, 0, 1, 0};
int dy[] = {0, 1, 0, -1};

void bfs()
{
    memset(dist, -1, sizeof dist);
    int hh = 0, tt = -1;

    for(int i = 0; i < n; i ++)
        for(int j = 0; j < m; j ++)
            if(g[i][j] == '1')
            {
                dist[i][j] = 0;
                q[++ tt] = {i, j};
            }

    while(hh <= tt)
    {
        auto t = q[hh ++];
        for(int i = 0; i < 4; i ++)
        {
            int a = t.x + dx[i];
            int b = t.y + dy[i];

            if(a < 0 || a >= n || b < 0 || b >= m)
                continue;
            if(dist[a][b] != -1)
                continue;
            
            dist[a][b] = dist[t.x][t.y] + 1;
            q[++ tt] = {a, b};
        }
    }
}

int main()
{
    cin >> n >> m;

    for(int i = 0; i < n; i ++)
        cin >> g[i];
    
    bfs();

    for(int i = 0; i < n; i ++)
    {
        for(int j = 0; j < m; j ++)
            cout << dist[i][j] << " ";
        puts("");
    }

    return 0;
}
```

# 最小步数模型
## 魔板
[原题链接](https://www.acwing.com/problem/content/1109/)
12345678 -> A 变化 -> 87654321
		  -> B 变化 -> 41236785
		  -> C 变化 -> 17245368
可以用哈希表存储状态

扩展的时候按照 ABC 的顺序扩展，就一定能得到字典序最小的操作

```cpp
#include<cstring>
#include<iostream>
#include<algorithm>
#include<unordered_map>
#include<queue>

using namespace std;

char g[2][4];

unordered_map<string, int> dist;
// 存它从哪个字符串转移过来，以及他的操作
unordered_map<string, pair<char, string>> pre;
queue<string> q;

void set_(string state)
{
    for(int i = 0; i < 4; i ++)
        g[0][i] = state[i];
    for(int i = 3, j = 4; i >= 0; i --, j ++)
        g[1][i] = state[j];
}

string get()
{
    string res;
    for(int i = 0; i < 4; i ++)
        res += g[0][i];
    for(int i = 3; i >= 0; i --)
        res += g[1][i];
    return res;
}

string move0(string state)
{
    set_(state);

    for(int i = 0; i < 4; i ++)
        swap(g[0][i], g[1][i]);

    return get();
}

string move1(string state)
{
    set_(state);

    char v0 = g[0][3], v1 = g[1][3];
    for(int i = 3; i > 0; i --)
        for(int j = 0; j < 2; j ++)
            g[j][i] = g[j][i - 1];
    g[0][0] = v0;
    g[1][0] = v1;

    return get();
}

string move2(string state)
{
    set_(state);

    char v = g[0][1];
    g[0][1] = g[1][1];
    g[1][1] = g[1][2];
    g[1][2] = g[0][2];
    g[0][2] = v;

    return get();
}

void bfs(string start, string end)
{
    if(start == end)
        return ;

    q.push(start);
    dist[start] = 0;

    while(q.size())
    {
        auto t = q.front();
        q.pop();

        string m[3];
        m[0] = move0(t);
        m[1] = move1(t);
        m[2] = move2(t);

        for(int i = 0; i < 3; i ++)
        {
            string str = m[i];
            if(dist.count(str) == 0)
            {
                dist[str] = dist[t] + 1;
                pre[str] = {char(i + 'A'), t};
                if(str == end)
                    break ;
                q.push(str);
            }
        }
    }
}

int main()
{
    int x;
    string start, end;
    for(int i = 0; i < 8; i ++)
    {
        cin >> x;
        end += char(x + '0');
    }

    for(int i = 0; i < 8; i ++)
        start += char(i + '1');

    bfs(start, end);

    cout << dist[end] << endl;

    string res;
    while(end != start)
    {
        res += pre[end].first;
        end = pre[end].second;
    }

    reverse(res.begin(), res.end());

    if(res.size())
        cout << res << endl;

    return 0;
}
```

# 双端队列广搜
只包含 0 和 1 的 bfs 问题

从队头扩展出来的边权如果是 0，插到队头。如果是 1，插到队尾。

[原题链接](https://www.acwing.com/problem/content/description/177/)
因为起点是 (0, 0)，那么经过的点 x + y 一定是偶数。
所以如果终点横纵坐标之和不是偶数，那么无解。

```cpp
#include<bits/stdc++.h>
#define x first 
#define y second

using namespace std;

const int N = 510;
typedef pair<int, int> PII;

int n, m;
char g[N][N];
PII q[N * N];
int dist[N][N];
bool st[N][N];

int bfs()
{
    deque<PII> q;

    memset(st, 0, sizeof st);
    memset(dist, 0x3f, sizeof dist);
    dist[0][0] = 0;
    
    char cs[5] = "\\/\\/";
    int dx[] = {-1, -1, 1, 1};
    int dy[] = {-1, 1, 1, -1};
    int ix[] = {-1, -1, 0, 0};
    int iy[] = {-1, 0, 0, -1};

    q.push_back({0, 0});

    while(q.size())
    {
        auto t = q.front();
        q.pop_front();

        int x = t.x;
        int y = t.y;

        if(x == n && y == m)
            return dist[x][y];
        
        if(st[x][y])
            continue ;
        st[x][y] = true;

        for(int i = 0; i < 4; i ++)
        {
            int a = x + dx[i];
            int b = y + dy[i];
            if(a < 0 || a > n || b < 0 || b > m)
                continue;
            
            int ga = x + ix[i];
            int gb = y + iy[i];
            int w = (g[ga][gb] != cs[i]);
            int d = dist[x][y] + w;
            if(d <= dist[a][b])
            {
                dist[a][b] = d;
                if(!w)
                    q.push_front({a, b});
                else
                    q.push_back({a, b});
            }
        }
    }

    return -1;
}

int main()
{
    int T;
    cin >> T;
    while(T --)
    {
        cin >> n >> m;

        for(int i = 0; i < n; i ++)
            cin >> g[i];

        if(n + m & 1)
            puts("NO SOLUTION");
        else
            cout << bfs() << endl;
    }

    return 0;
}
```

# 双向广搜
