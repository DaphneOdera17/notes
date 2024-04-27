# 监督学习与无监督学习
## 监督学习 Supervised Learning
有回归 Regression 和 分类 Classification 两种类型
### Regression Model
#### Linear regression model
线性回归模型
下图是一个房价预测图，通过一条直线来拟合数据。当 size 为 1250，对应直线，我们可以估计房价会是 220k。
Infinitely many possible outputs.
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240423144723.png" style="zoom:50%">
训练模型：
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240423150343.png" style="zoom:50%">
How to represent $f$:
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240423150602.png" styld="zoom:50%">
对于一个输入变量的线性模型的另一个名称是 单因素线性回归 Univariate linear regression.
#### Cost function:Squared error cost function
$J(w, b) = \frac{1}{2m}\sum_{i = 1}^m(\hat{y}^{(i)} - y^{(i)})^2,~ ~(m~ ~is~ ~the~ ~number~ ~of~ ~training~ ~examples)$
$\hat{y}^{(i)} = f_{w, b}(x^{(i)})$
$f_{w, b}(x^{(i)}) = wx^{(i)} + b$
$w~and~b~are~the~parameters~of~the~model$
### Gradient descent 梯度下降
$Simultaneously~update~w~and~b$ (同时更新)
$w = w - \alpha \frac{\partial}{\partial w}J(w, b),~~ \alpha~ ~also~ ~displays~ ~the~ ~Learning~ ~rate$
$b = b - \alpha~~\frac{\partial}{\partial b}J(w, b)$
#### "Batch" gradient descent 批量梯度下降
"Batch": Each step of gradient descent uses all the training examples.
### Classification Model
Predicts categories. Only small number of possible outputs.
## 无监督学习 Unsupervised Learning
有 聚类 Clustering 这种类型