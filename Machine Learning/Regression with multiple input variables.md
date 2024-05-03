## 多元线性回归
$f_{\vec {w}, b}(\vec {x})=w_1x_1+w_2x_2+...+w_nx_n+b$
$\vec{w}=[w_1~~w_2~~w_3~~...~~w_n]$
$\vec {x} = [x_1~~x_2~~x_3~~...~~x_n]$
$f_{\vec {w}, b}(\vec {x})=\vec{w} \cdot \vec{x}+b$
## 矢量化
对于 n = 3, $\vec{w}=[w_1~~w_2~~w_3]$，$\vec {x} = [x_1~~x_2~~x_3]$
```python
import numpy as np
w = np.array([1.0, 2.5, -3.3])
b = 4
x = np.array([10, 20, 30])
```
如果没有矢量化，那么
```python
f = w[0] * x[0] + w[1] * x[1] + w[2] * x[2] + b

'''also'''
f = 0
for j in range(n):
	f = f + w[j] * x[j]
f = f + b
```
如果运用矢量化，只需要简短的一行代码，并且比前面的代码运行快的多。
```python
f = np.dot(w, x) + b
```
np.dot 函数使用并行硬件来加快运行速度。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240430225843.png)
## 多元线性回归的梯度下降
引入矢量化之后，Cost function: $J(\vec {w}, b)$
Gradient descent 
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503002801.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240503002919.png)

