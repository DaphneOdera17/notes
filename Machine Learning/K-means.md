# 机器学习 | K-means 聚类算法
一种无监督学习算法，把无分类的数据分为 K 类。
## 算法流程
选取 k 个初始质心，对于每个样本点，计算得到距离它最近的质心，将其标记为该质心所对应的 cluster，重新计算 k 个 cluster 对应的质心，重复上述步骤，直到质心不再发生变化。
## 距离计算
分为三种方法
### Minkowski(闵可夫斯基距离)
$d(x,y)=(\sum_{i=1}^{n}|x_i-y_i|^p)^{\frac{1}{p}}$
### Cosine Similarity(余弦相似度)
$$
\begin{aligned}
s(x,y)&=cos(\theta)\\&=\frac{x^Ty}{|x|\cdot|y|}\\
&=\frac{\sum_{i=1}^{n}x_iy_i}{\sqrt{\sum_{i=1}^{n}x_i^2}\sqrt{\sum_{i=1}^{n}y_i^2}}
\end{aligned}
$$
### Pearson coefficient(皮尔逊相关系数)
$$
\begin{aligned}
p(x,y)&=\frac{cov(x,y)}{\sigma_x\sigma_y}\\
&=
\end{aligned}
$$