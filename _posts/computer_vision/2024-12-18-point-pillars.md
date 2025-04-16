---
title: 快速了解一个网络：Point Pillars
date: 2024-12-18 09:00:00 +0800
categories: [Computer Vision, 3D Detection]
tags: [快速了解一个网络, computer vision, 3d detection, lidar 3d, point pillars]
---

> 以下内容偏向于记录个人学习过程及思考，非常规教学内容
{: .prompt-info }

## 背景

背景是 lidar 3d 目标检测。

1. 一些工作是将 3d lidar 点云投影到bev视角，再利用 2d cnn 网络进行检测。但由于点云的稀疏特性，这种做法效果并不好。
2. 另外一些工作推广使用 3d 卷积核进行 3d 目标检测，但显然计算效率和计算量是瓶颈。

## 核心思想

设计了一种 3d lidar 点云的 encoder，转换为了 pseudo image，再针对转换后的 image 利用成熟的 2d cnn 网络进行目标检测。

## Pipeline

![pointpillars-pipeline](assets/img/pointpillars-pipeline.png)

核心是 Pillar Feature Net 的转换过程。

## 亿些细节

### Pointcloud to Pseudo-Image

将 3d lidar 点云，在 x - y 平面上划分为 H x W = P 个 grid，每个 grid 内的点云则形成了一个 pillar。

每个 pillar 中取 N 个点为代表，若点云较稠密则采样，若点云较稀疏则补0

每个点用一个 D = 9 维的 vector 表示，分别为

- 该点自身的位置坐标 x, y, z
- 该点的反射强度 r
- 该点距离 pillar 中所有点算术平均位置的距离 x, y, z
- 该点距离 pillar x - y 平面中心点的距离 x, y

因此就得到了一个 D x P x N 的 tensor，用来表示 3d lidar 点云

对于每个点，经过 Linear layer，BatchNorm，ReLU 后转换为 C x P x N 的 tensor (D -> C)

对于每个 pillar 中的 N 个点作 max 操作，去除 N 这一维，可得到 C x P 的 tensor

将 P 个 pillar 按照之前 H x W 个 grid 的位置还原回去，即可以得到 C x H x W 的 tensor

即 pseudo image 的形式。

## 进一步了解

- PointNet
- VoxelNet
- SECOND
- Focal loss
- Deconv

## 原文和代码

<https://arxiv.org/abs/1812.05784>

<https://github.com/nutonomy/second.pytorch>

## 参考资料

[PointPillar 3D目标检测模型详解](https://blog.csdn.net/m0_37605642/article/details/128987547 "PointPillar 3D目标检测模型详解")