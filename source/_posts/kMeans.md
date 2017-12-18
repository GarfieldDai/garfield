---
title: K-means聚类算法
date: 2017-12-18 18:18:35
categories: Machine Learning
thumbnail: "/images/ml/ml_map.png"
---
![](/images/ml/ml_map.png)

## 目的
简述如何使用`scikit-learn`K-均值（K-means）聚类算法。

<!--more-->

## 简介
K-均值聚类算法属于无监督学习，K指的是用户指定要创建的聚类（Cluster）的数目。

这里使用`mglearn`进行数据展示，该模块是基于`matplotlib`进行封装的，可以使用`pip`进行安装。
```shell
$ pip install mglearn
```

## 内容
```python
from sklearn.datasets import make_blobs
from sklearn.cluster import KMeans
import mglearn as mglearn
# 准备数据
X, y = make_blobs(random_state=1)
# 构建聚类模型，设置k值为3
kmeans = KMeans(n_clusters=3)
# 将数据放入模型中
kmeans.fit(X)
# 输出分类后的标记结果
print("标记分类结果:\n{}".format(kmeans.labels_))

# 使用散点图展示数据结果
mglearn.discrete_scatter(X[:, 0], X[:, 1], kmeans.labels_, markers='o')

# 显示聚类结果中心点
mglearn.discrete_scatter(
    kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], [0, 1, 2],
    markers='^', markeredgewidth=2)

# 根据当前模型来预测未知测试数据
# print(kmeans.predict(X_test))

```


参考资料
[K-means](http://scikit-learn.org/stable/modules/clustering.html#k-means)
[mglearn homepage](https://github.com/amueller/introduction_to_ml_with_python)
