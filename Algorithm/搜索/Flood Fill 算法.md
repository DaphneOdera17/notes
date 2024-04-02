从一个起点开始，每次随机选择一个新加进来的格子，看看他周围能不能扩展新的格子，如果可以的话就把他扩展进来，直到不能扩展新的格子。(同样的格子只能覆盖一次)
可以在线性时间复杂度内，找到某个点所在的连通块。

## 池塘计数
[原题链接](https://www.acwing.com/problem/content/1099/)
一行一行扫描，如果碰到水，并且没有被标记过的话，就从这个点开始进行 Flood Fill 算法。只遍历周围是水的区域并且把他们全部覆盖掉，再继续遍历下个点。每次碰到一个新大陆，连通块数量就加1

```cpp
#include<bits/stdc++.h>
#define x first 
#define y second

using namespace std;

typedef pair<int, int> PII;

const int N = 1050;

int n, m;
char g[N][N];
PII q[N * N];
bool st[N][N];

void bfs(int sx, int sy)
{
    int hh = 0, tt = 0;
    
    q[0] = {sx, sy};
    st[sx][sy] = true;

    while(hh <= tt)
    {
        PII t = q[hh ++];

        for(int i = t.x - 1; i <= t.x + 1; i ++)
        {
            for(int j = t.y - 1; j <= t.y + 1; j ++)
            {
                if(i == t.x && j == t.y)
                    continue;
                if(i < 0 || i >= n || j < 0 || j >= m)
                    continue;
                if(g[i][j] == '.' || st[i][j])
                    continue;

                q[ ++ tt] = {i, j};
                st[i][j] = true;
            }
        }
    }
}

int main()
{
    cin >> n >> m;

    for(int i = 0; i < n; i ++)
        cin >> g[i];

    int cnt = 0;

    for(int i = 0; i < n; i ++)
    {
        for(int j = 0; j < m; j ++)
        {
            if(g[i][j] == 'W' && !st[i][j])
            {
                bfs(i, j);
                cnt ++;
            }
        }
    }

    cout << cnt << endl;

    return 0;
}
```

## 城堡问题
[原题链接](https://www.acwing.com/problem/content/1100/)
```cpp
#include<bits/stdc++.h>
#define x first 
#define y second

using namespace std;

const int N = 55;
typedef pair<int, int> PII;

int n, m;
int g[N][N];
PII q[N * N];
bool st[N][N];

int bfs(int sx, int sy)
{
    int dx[] = {0, -1, 0, 1};
    int dy[] = {-1, 0, 1, 0};

    int hh = 0, tt = 0;
    int area = 0;

    q[0] = {sx, sy};
    st[sx][sy] = true;

    while(hh <= tt)
    {
        PII t = q[hh ++];
        area ++;

        for(int i = 0; i < 4; i ++)
        {
            int a = t.x + dx[i];
            int b = t.y + dy[i];

            if(a < 0 || a >= n || b < 0 || b >= m)
                continue;
            if(st[a][b])
                continue;
            if(g[t.x][t.y] >> i & 1) // 这个方向有墙
                continue;

            q[ ++ tt] = {a, b};
            st[a][b] = true;
        }
    }
    return area;
}

int main()
{
    cin >> n >> m;

    for(int i = 0; i < n; i ++)
        for(int j = 0; j < m; j ++)
            cin >> g[i][j];

    int cnt = 0, area = 0;

    for(int i = 0; i < n; i ++)
        for(int j = 0; j < m; j ++) 
            if(!st[i][j])
            {
                area = max(area, bfs(i, j));
                cnt ++;
            }

    cout << cnt << endl << area << endl;

    return 0;
}
```

## 山峰和山谷
[原题链接](https://www.acwing.com/problem/content/1108/)
```cpp
#include<bits/stdc++.h>
#define x first 
#define y second

using namespace std;

typedef pair<int, int> PII;

const int N = 1010;
int n;
int h[N][N];
PII q[N * N];
bool st[N][N];

void bfs(int sx, int sy, bool& has_higher, bool& has_lower)
{
    int hh = 0, tt = 0;
    q[0] = {sx, sy};
    st[sx][sy] = true;

    while(hh <= tt)
    {
        PII t = q[hh ++];

        for(int i = t.x - 1; i <= t.x + 1; i ++)
            for(int j = t.y - 1; j <= t.y + 1; j ++)
            {
                if(i < 0 || i >= n || j < 0 || j >= n)
                    continue;
                if(h[i][j] != h[t.x][t.y])
                {
                    if(h[i][j] > h[t.x][t.y])
                        has_higher = true;
                    else
                        has_lower = true;
                }
                else if(!st[i][j])
                {
                    q[ ++ tt] = {i, j};
                    st[i][j] = true;
                }
            }
    }

}

int main()
{
    cin >> n;

    for(int i = 0; i < n; i ++)
        for(int j = 0; j < n; j ++)
            cin >> h[i][j];

    int peak = 0, valley = 0;

    for(int i = 0; i < n; i ++)
        for(int j = 0; j < n; j ++)
            if(!st[i][j])
            {
                bool has_higher, has_lower;
                has_higher = has_lower = false;
                
                bfs(i, j, has_higher, has_lower);

                if(!has_higher)
                    peak ++;
                if(!has_lower)
                    valley ++;
            }

    cout << peak << " " << valley << endl;

    return 0;
}
```