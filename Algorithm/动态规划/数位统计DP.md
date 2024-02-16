

## **计数问题**



$count(n, x)$ 求 $1 \sim n$ 中 $x$ 出现的次数

则求 $(a, b)$ 中 $x$ 出现的次数可以类似于前缀和的做法

$count(b,x) - count(a-1,x)$