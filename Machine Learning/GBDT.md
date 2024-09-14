# 机器学习 | GBDT
## 提升树 Boosting Tree
### 提升树算法
1. 初始化 $f_0(x)=0$
2. 对 m = 1,2,...,M
	(a) 计算残差 $r_{mi}=y_i-f_{m-1}(x_i)$
	(b) 拟合残差 $r_{mi}$ 学习一个回归树 $T(x;\Theta_m)$
	(c) 更新 $f_m(x)=f_{m-1}(x)+T(x;\Theta_m)$
3. 得到提升树
	$f_M(x)=\sum_{m=1}^MT(x;\Theta_m)$



