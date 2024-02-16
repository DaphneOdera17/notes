# **RMQ ST表**

$RMQ$ 问题 --> 区间 **最大、最小值查询** 问题。主要应用于 **倍增** 思想

## 预处理 $O(logn)$  

倍增法递推：用两个等长小区间拼凑一个大区间

$f[i][j]$ 表示以第 $i$ 个数为起点，长度为 $2^j$ 的区间中的最大值

<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231107093558083.png" alt="image-20231107093558083" style="zoom:50%; float:left" />

$f[i][j] = max(f[i][j - 1], f[i + 2^{j - 1}][j - 1])$

区间终点 $i + 2^j - 1 <= n$

```c++
for(int i = 1; i <= n; i ++)
	cin >> f[i][0];
for(int j = 1; j <= 20; j ++)
    for(int i = 1; i + (1 << j) - 1 <= n; i ++)
        f[i][j] = max(f[i][j - 1], f[i + (1 << (j - 1))][j - 1]);
```

$n = 6$

区间长度 $1,2,4,8...$

$f[i,0]:[1,1][2,2][3,3][4,4][5,5][6,6]$

$f[i,1]:[1,2][2,3][3,4][4,5][5,6]$

$f[i,2]:[1,4][2,5][3,6]$

$j=3,i + 2^j -1 = 1 + 8 - 1 > 6$

## 查询 $O(1)$

若查询区间为 $[l,r]$ 

区间长度的指数 $k = log2(r - l + 1)$

$[~]$ 代表可能的区间长度

$k = 0: [1]$

$k = 1:[2,3]$

$k = 2:[4,5,6,7]$

$k = 3:[8,9,10,11,12,13,14,15]$



即 $2^k <= r- l + 1 < 2\times 2^k$

区间可以重叠拼凑，但是不能留空

<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231107095750903.png" alt="image-20231107095750903" style="zoom:50%;" />

$max(f[l][k], f[r-2^k+1][k])$

```c++
for(int i = 1, l, r; i <= m; i ++)
{
    cin >> l >> r;
    int k = log2(r - l + 1);
    cout << max(f[l][k], f[r - (1 << k) + 1][k]);
}
```

