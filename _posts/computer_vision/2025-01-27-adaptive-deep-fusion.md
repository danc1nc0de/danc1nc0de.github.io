---
title: 快速了解一个网络：Seeing Through Fog Without Seeing Fog, Deep Multimodal Sensor Fusion in Unseen Adverse Weather
date: 2025-01-27 18:30:00 +0800
categories: [Computer Vision]
tags: [快速了解一个网络, computer vision, 2d detection, radar-camera fusion, adaptive deep fusion]
---

> 以下内容偏向于记录个人学习过程及思考，请审慎阅读。
{: .prompt-info }

## 背景

camera的图像质量在极端天气或低光黑暗场景极为受限。

但现在并没有包含多传感器的、极端天气下的驾驶数据。

于是采了一波数据并公开，并基于“measurement entropy”提出一种多传感器融合方案

## 核心思想

将所有传感器输出全部反投到camera image上。

并基于measurement entropy加权进行自适应的concatenation融合

检测头采用SSD

## Pipeline

![adaptive-deep-fusion-pipeline](assets/img/adaptive-deep-fusion-pipeline.png)

## 亿些细节

- lidar反投到camera image上，使用深度、高度、反射强度信息
- radar反投到camera image上，因为没有高度信息，因此反投成整条线段的形式（见上图pipeline）
- 为了将融合结果自适应地导向最优的sensor，作者引入了额外的entropy信息
  - 对于每个sensor，熵越大的地方，信息量越丰富，对应位置的权重越大，就达到了自适应的效果
- measurement entropy计算如下

![adaptive-deep-fusion-entropy](assets/img/adaptive-deep-fusion-entropy.png)

其中i范围为[0, 255]，所有sensor反投到图像后都归一化到这一范围。

对于每个(m, n)像素位置，计算其右下MxN的一个patch相关的熵作为本像素位置的熵。所有位置像素熵求和为全图的熵。

- 训练过程中仅包含正常天气数据，但时间有从早到晚

## 进一步了解

- [SSD](https://yinghao.info/posts/ssd/)

## 原文和代码

<https://arxiv.org/abs/1902.08913>

## 参考资料

无