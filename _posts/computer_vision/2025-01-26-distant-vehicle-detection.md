---
title: 快速了解一个网络：Distant Vehicle Detection Using Radar and Vision
date: 2025-01-26 19:00:00 +0800
categories: [Computer Vision, Radar-Camera Fusion]
tags: [快速了解一个网络, computer vision, 2d detection, radar-camera fusion]
---

> 以下内容偏向于记录个人学习过程及思考，非常规教学内容
{: .prompt-info }

## 背景

基于camera的cnn系列目标检测网络对于小目标的检测效果较差（即对于远距离的目标检测效果较差）。

本文考虑通过radar的信息（尤其是动态目标的多普勒信息）来辅助远距离目标的检测。

## 核心思想

将radar的点云根据相机内外参反投到图像上，通过concatenation的方式融合，相当于给图像features增加2个channel

2个channel分别对应radar的位置信息和radar的多普勒频移信息。

![distant-vehicle-detection-train-data](assets/img/distant-vehicle-detection-train-data.png)

远距离目标真值方面，通过对一个长焦镜头的图像用yolo网络进行目标检测来生成（2d detection）。

## Pipeline

![distant-vehicle-detection-pipeline](assets/img/distant-vehicle-detection-pipeline.png)

## 亿些细节

- 作者也使用的私有数据集，因为特殊的需求
  - 1个长焦（辅助远距离真值生成），2个短焦（构成stereo camera模拟实际车辆传感器构型，也通过stereo visual odometry用作ego motion的估计），1个radar
  - 其中长焦和其中1个短焦镜头尽可能的靠近以近似满足共用相机中心的假设，在不需要知道目标真实距离的情况下将长焦图像检测的uv近似反投到短焦图像uv，简化真值获取过程。
- 通过基于kitti数据集训练的yolo网络，在采集的数据集上产生伪标注结果当作真值
- 产生伪标注过程中，对于短焦图像的检测结果，如果和长焦检测结果iou大于0.5则弃用短焦镜头检测结果
- 在将radar点云反投图像时，反投结果采用了一个临近的圆形区域而非单个pixel，这样可以一定程度上增加radar点对训练结果的影响，也可以在一定程度上反应radar位置的不确定性。
- 因为camera采样频率（30hz）和radar采样频率（20hz）都很高，相邻帧几乎没有差别，所以作者做了进一步的下采样，采用camera和radar间delay尽可能小的帧 + 进一步下采样结果进行训练。
- 因为自采数据vehicle占了大部份，因此后文只focus vehicle部份的结果（估计是其他类别效果不佳）
- 检测框架使用SSD
  - 因为SSD对于更小目标的检测效果较差，这里作者借鉴了Detecting traffic lights by single shot detection的思路，通过重复default boxes的方式来提升小目标检测效果。
- 作者提出了2个进一步的研究方向
  1. 本文还是简单的将radar点云反投图像，作为图像来处理，没有很好的利用radar点云的稀疏特性。
  2. 本文没有利用时序信息，作者认为时序信息对于目标检测有很好的作用，尤其是可以过滤radar的一些噪声等。

## 进一步了解

- [SSD](https://yinghao.info/posts/ssd/)
- Detecting traffic lights by single shot detection

## 原文和代码

<https://arxiv.org/abs/1901.10951>

## 参考资料

无