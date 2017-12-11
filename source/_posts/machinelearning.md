---
title: 什么是机器学习
date: 2017-12-09 22:41:12
categories: Machine Learning
thumbnail: "/images/ml/ml.jpg"
---
![](/images/ml/ml.jpg)

## 目的
简述机器学习相关的概念和常用的工具使用。

<!--more-->

## 什么是机器学习
机器学习简单的讲就是从数据中提取知识。生活中有很多应用的场景，比如应用中的电影、商品、音乐推荐等可利用机器学习提取用户历史行为信息来推测用户潜在的需求，进而进行个性化推荐服务和商品。

机器学习是一门交叉学科，入门机器学习除了计算机编程基础外，还需要有一定的数学基础如高等数学，线性代数和概率论统计。

## 机器学习基本概念
机器学习分为监督学习（supervised Learning）和非监督学习（unsupervised Learning）。

#### 监督学习
监督学习有两种：分类（classification）和回归（regression），这类算法必须知道预测什么。
区别是分类还是回归，主要看结果是连续的还是离散的。比如真与假、动物分类集合{爬行类，哺乳类，鱼类，两栖类，鱼类}等一个有限的集合或者离散值，那么就是分类。如果结果是从无限的数值集合中取值如工资6383.34、2345.12、7569.321等连续值，就是回归。

我们准备做一个专家系统，这个系统是识别鸟类的系统。
现在我们手中有不同的鸟类的数据，这些数据按照属性(attribute)可以归类为体重，翼展长度，是否有脚蹼和后背颜色等，这些属性也叫做特征(feature)。现在我们使用机器学习的分类来实现这个专家系统。我们需要准备两组数据，这些数据我们称为样本（sample），一组是训练数据（training data or training set)，另一组是测试数据（test data or test set）。训练数据是为了构建机器学习模型，测试数据是为了校验训练出来的模型工作的如何。

#### 无监督学习
无监督学习有两种：聚类（clustering），密度评估(density estimation)，这类算法不知道要预测什么。
将数据集合分成由类似的对象组成的多个类的过程被称为聚类。将寻找描述数据统计值的过程称之为密度估计。

## 机器学习开发工具
+ Python：推荐使用Python3进行机器学习开发。
+ Jupyter Notebook：网页版开发编辑器。
+ NumPy：提供强大的N维数组对象。
+ SciPy：进行科学计算的基础工具包。
+ Matplotlib：提供了很多图表控件，方便进行数据可视化。
+ Pandas：提供了高性能的，简单易用的数据结构和数据分析工具。
+ Scikit-learn：机器学习算法的实现。

可以使用[Anaconda](https://www.anaconda.com/)一站式安装配置。
或者安装好Python3后，使用pip进行安装。在安装之前，可以使用[Python 虚拟环境](http://www.garfieldwiki.com/2017/12/03/pythonVirtualEnv/)，创建一个独立干净的开发环境。
```shell
$ pip install jupyter numpy scipy matplotlib pandas scikit-learn
```
安装好后，使用命令启动编辑器，启动成功后将会自动打开浏览器。
```shell
$ jupyter notebook
```
在jupyter notebook使用`matplotlib`，需在网页编辑器执行下面命令。
```shell
%matplotlib inline
```

参考资料
[Scipy getting started](https://scipy.org/getting-started.html)
[Scipy Lecture Notes](http://www.scipy-lectures.org/index.html)
[Anaconda](https://www.anaconda.com/)
[Installing Jupyter](https://jupyter.org/install.html)
[Indalling Matplotlib](http://matplotlib.org/users/installing.html)
[Pandas](http://pandas.pydata.org/)
[Installing scikit-learn](http://scikit-learn.org/stable/install.html)
