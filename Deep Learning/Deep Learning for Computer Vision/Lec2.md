# Image Classification
[Robustness](https://en.wikipedia.org/wiki/Robustness) 鲁棒性
## Edge images
[Edge Detection](https://en.wikipedia.org/wiki/Edge_detection)
[有关边缘检测算法](https://www.cnblogs.com/xyf327/p/14745908.html)
## Image Classification: 
input: image
output: Assign image to one of a fixed set of categories.
**Problem**: Semantic Gap(语义差距)
Object Detection:
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240406104140.png" style="zoom: 50%">
	One way to perform is via image classification of different sliding windows im the image. In a nutshell, it means classify different sub-regions of the image so we could look at s sub region over here and then classify it as background, horse, person, car or a truck...
```python
def classify_image(image):
	# Some magic here?
	return class_label
```
## Machine Learning:Data-Driven Approach
1. Collect a dataset of images and labels
2. Use Machine Learning to train a classifier
3. Evaluate the classifier on new images
```python
def train(images, labels):
	# Machine learning
	# Memorize all data and labels
	return model
```

```python
def predict(model, test_images):
	# Use model to predict labels
	# Predict the label of the most similar training image
	return test_labels
```

## Distance Metric to compare images
### 曼哈顿距离:
#### **L1(Manhattan) distance:** $d_1(I_1,I_2) = \sum_p|I_1^p-I_2^p|$
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240412191451.png" style="zoom: 50%">
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240409085507.png" style="zoom:50%">

## Nearest Neighbor Decision Boundaries
Decision Boundarie is the boundary between two classification regions.
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240409090934.png" style="zoom:50%">
Decision Boundarie can be nosiy; affected by outliers.
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240409091231.png" style="zoom: 70%">


## K-Nearest Neighbors
### Using more neighbors helps smooth out rough decision boundaries.
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240409090850.png" style="zoom:75%">
### Using more neighbors helps reduce the effect of outliers.
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240409091528.png" style="zoom:75%">
### When K > 1 there can be ties between classes. Need to break somehow!
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240409091632.png" style="zoom:75%">
白色区域均有三个最近的邻居。

### 欧几里得距离
#### **L2(Euclidean) distance** = $d_2(I_1, I_2) = \sqrt{\sum_{p}(I_1^p - I_2^p) ^ 2}$

### Setting Hyperparameters
Among the three ideas above, The best idea is **Idea #3**
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240412200840.png)
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240412201137.png" style="zoom: 50%">
当然，我们也可以将数据集划分为更多，以此更好估计我们的泛化性能。
也就是**交叉验证**
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240412201236.png)
随着训练的数量越来越多
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240412201717.png" style="zoom: 50%">
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240412201741.png" style="zoom: 50%">
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240412201753.png" style="zoom: 50%">
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240412201811.png" style="zoom: 50%">
We can see the nearest neighbor classifier performs well.
