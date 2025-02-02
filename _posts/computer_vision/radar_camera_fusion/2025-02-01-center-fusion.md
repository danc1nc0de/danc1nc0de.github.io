---
title: 快速了解一个网络：CenterFusion, Center-based Radar and Camera Fusion for 3D Object Detection
date: 2025-02-01 11:00:00 +0800
categories: [Computer Vision, Radar-Camera Fusion]
tags: [快速了解一个网络, computer vision, 3d detection, radar-camera fusion, center fusion]
math: true
---

> 以下内容偏向于记录个人学习过程及思考，非常规教学内容
{: .prompt-info }

## 背景

多传感器融合可以提高系统的鲁棒性和准确性，但同时为系统和算法设计带来了新的挑战。

前融合的方法对于传感器间的时序/空间对齐误差比较敏感；而后融合的方法又无法完全利用多传感器的感知能力。

因此本文提出一种middle fusion的融合算法。

## 核心思想

基于camera分支获得一些初步的3d检测框，再利用这些框关联相关的radar点云并产生radar features，进而将对应的image features和radar features concat起来对初步的3d检测框进行精调，并输出3d box、速度等属性。

## Pipeline

![center-fusion-pipeline](assets/img/center-fusion-pipeline.png)

## 亿些细节

### Radar Point Cloud

将radar检测当作ego系下的3d点，包含x,y,z,vx,vy共5种属性，其中速度是用ego速度补偿后得到的绝对速度。

对于每个场景，积累约过去0.25s的radar点云，约3帧。

### Radar Frustum Association Mechanism

在middle fusion方法中，正确的关联非常关键。因此作者考虑以下关联思路：

![center-fusion-frustum-association](assets/img/center-fusion-frustum-association.png)

并且将radar点延z方向延长为具有一定高度的pillar（见pipeline）

只考虑完全落入roi frustum区域的radar pillar，如区域内有多个radar pillar，只使用距离最近的那个。

### Radar Feature Extraction

对于每个关联上image object的radar pillar，以image object的2d box中点为中心生成3个heat map，分别对应深度，vx，vy

如果2个heat map有交叠区域，则距离更近的heatmap覆盖距离较远的heatmap（类似于距离近的物体挡住距离远的物体）

产生的heat map和image features concat起来作为额外的channel (features)

### Implementation Details

使用基于Deep Layer Aggregation (DLA)的预训练CenterNet作为backbone

训练过程中使用right-left flipping和random shifting作为数据增强手段

测试过程中使用flipping作为数据增强手段

pillar设置为[0.2m, 0.2m, 1.5m]

## 进一步了解

- [CenterNet](https://yinghao.info/posts/centernet/)
- Deep Layer Aggregation

## 原文和代码

<https://arxiv.org/abs/2011.04841>

## 参考资料

无