---
title: 使用OpenCV进行人脸检测
date: 2018-02-08 17:54:15
categories: Computer Vision
tags: OpenCV
thumbnail: "/images/ComputerVision/face_detection.png"
---
![](/images/ComputerVision/face_detection.png)

## 目的
不需要高深的理论，搭建属于自己的人脸检测。

<!--more-->

## 简介
人脸检测（Face Detection）属于计算机视觉（Computer Vision）的范畴，与人脸识别（Face Recognition）不一样，人脸检测只是检测是否有人脸，不能分辨具体某个人是谁。

## 内容
需要安装以下两个环境：
+ Python 3+
+ OpenCV

OpenCV提供了2种已经训练好的分类器（Classifier）来进行人脸检测，分类器是由成百上千个人脸和非人脸图片训练出来的。
+ Haar Classifier：haarcascade_frontalface_alt.xml
+ LBP Classifier：lbpcascade_frontalface.xml

这两个分类器都是使用灰度图（gray scales）进行训练的，因为颜色对于识别人脸来说没有什么意义，这两个分类器在目录`opencv/data/`下面。

两种分类器的优缺点：
![](/images/ComputerVision/haar-vs-lbp.png)

## 代码
```python
# 加载OpenCV类库
import cv2

# 读取图片
picture = cv2.imread('data/man.jpeg')
# 将彩色图片转换为灰度图
gray_img = cv2.cvtColor(picture, cv2.COLOR_BGR2GRAY)
# 加载分类器
haar_face_cascade = cv2.CascadeClassifier('data/haarcascade_frontalface_alt.xml')
# lbp_face_cascade = cv2.CascadeClassifier('data/lbpcascade_frontalface.xml')  
# 执行人脸检测
faces = haar_face_cascade.detectMultiScale(gray_img, scaleFactor=1.1, minNeighbors=5)
print('Faces found: ', len(faces))
# 标记检测到的人脸位置
for (x, y, w, h) in faces:
    cv2.rectangle(picture, (x, y), (x + w, y + h), (0, 255, 0), 2)
# 显示图片
cv2.imshow('Test Imag', picture)
cv2.waitKey(0)
```

参考资料
[OpenCV face detection](https://www.superdatascience.com/opencv-face-detection/)
[OpenCV Tutorial](https://docs.opencv.org/master/d7/d8b/tutorial_py_face_detection.html)
