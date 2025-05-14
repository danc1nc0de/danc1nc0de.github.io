---
title: 快速了解一个网络：Deformable Convolutional Networks
date: 2025-05-14 09:30:00 +0800
categories: [Computer Vision]
tags: [快速了解一个网络, computer vision, ops]
---

> 以下内容偏向于记录个人学习过程及思考，请审慎阅读。
{: .prompt-info }

## 背景

传统卷积核和pooling的感受野形状是固定的，缺乏处理几何变换的机制。

## 核心思想

提出一种可变形卷积和pooling算法，引入offset增强卷积核空间采样的能力，对应offset根据不同任务是可学习、自适应的。

![deformable-conv-receptive-field](assets/img/deformable-conv-receptive-field.png)

## Pipeline

![deformable-conv-pipeline](assets/img/deformable-conv-pipeline.png)

offset field也是通过input feature map通过卷积得到的，空间大小也相同，channel数为2N，表示N个2D offset，其中N为卷积核所有卷积位置数量（如对于3x3卷积核，N=9）

![deformable-pooling-pipeline](assets/img/deformable-pooling-pipeline.png)

对于pooled的feature maps，通过一个fc产生归一化后的offsets，再通过feature maps的宽、高+系数恢复真实的offsets。最后再利用这些offsets重新做pooling。

## 亿些细节

- 由于offset可能是小数，则此时对应位置feature由原feature map通过bilinear interpolation得到。
- 在训练过程中，对于offset learning新增加的conv和fc，初始化权重均设置为0，即初始offsets均为0
- 从空间采样点可视化结果可见，训练后的offset对于image内容是高度自适应的

## 进一步了解

暂无

## 原文和代码

<https://arxiv.org/abs/1703.06211>

## 参考资料

暂无