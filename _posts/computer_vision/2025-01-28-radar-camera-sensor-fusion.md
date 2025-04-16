---
title: 快速了解一个网络：Radar-Camera Sensor Fusion for Joint Object Detection and Distance Estimation in Autonomous Vehicles
date: 2025-01-28 22:00:00 +0800
categories: [Computer Vision]
tags: [快速了解一个网络, computer vision, 2d detection]
---

> 以下内容偏向于记录个人学习过程及思考，请审慎阅读。
{: .prompt-info }

## 背景

多传感器信息可以很好的互相补足劣势，但是设计好的融合算法却比较难。

融合radar相比于融合lidar有两个优势

1. radar点比较稀疏，一个到几个radar点就对应一个目标，相比于lidar更有效
2. radar点包含的信息也比较直接，包括目标距离、目标速度

本文提出一种新的radar-camera fusion算法

## 核心思想

设计二阶段目标检测网络，首先基于radar点云和类别先验尺寸给出带深度的3d object proposals，再反投camera上得到2d proposals，并用2d image features进行refine，最后与image的2d object proposals作nms后一起送到后续网络进行目标检测。

## Pipeline

![radar-camera-sensor-fusion-pipeline](assets/img/radar-camera-sensor-fusion-pipeline.png)

## 亿些细节

### Radar Proposal Network

作者直接将radar点云作为直接的检测来生成proposals，而不使用相关feature提取。

anchor的size根据相关类别的先验尺寸设置

anchor朝向仅设置两个角度，即0°和90°

anchor的位置中心直接使用radar点在vehicle系的坐标（个人疑问：radar一般是目标车的最近点？

所有3d anchors再通过内外参反投到camera image上得到带深度信息的2d anchors

并且由于有深度信息 + 类别的先验尺寸，生成的2d anchors可以比较好的反馈相关类别在2d图像上的真实尺寸

因为radar点通常只存在于路平面上的目标，因此自然地忽略掉了很多不必要处理的背景区域

接着作者通过一个Radar Proposal Refinement (RPR)模块，结合proposals内的image features来调整anchors的位置和尺寸，同时也会回归一个有无目标的概率。

因为radar proposals拥有不同的size，这里作者采用了roi pooling进行维度对齐。

### Image Proposal Network

对于某些类别的目标（如行人等），radar点云有可能覆盖不到，因此给不出有效的proposals

但radar可以给出一些远距离小目标的proposals

因此作者保留了image proposals，与radar proposals结合后可以获得比较全的结果

为了对每个proposal都估计深度，作者针对image proposals单独增加了一部份网络结构用于深度估计

### Distance Refinement

因为image proposals的深度估计必然存在较大的误差，因此作者在nms前，先将image proposals和radar proposals通过iou关联，进而将image proposals的深度用radar深度覆盖。

### Dataset and Implementation Details

作者使用nuScenes作为数据集，FPN with ResNet-50作为backbone，预训练权重基于ImageNet数据集。

同其它文章做法，作者将nuScenes中的3d标注通过内外参反投到图像上得到2d标注

作者表明并没有使用任何data augmentation因为每个类别的数据量已相对足够。

## 进一步了解

- [Faster RCNN](https://yinghao.info/posts/faster-rcnn/)
- [FPN](https://yinghao.info/posts/fpn/)

## 原文和代码

<https://arxiv.org/abs/2009.08428>

## 参考资料

无