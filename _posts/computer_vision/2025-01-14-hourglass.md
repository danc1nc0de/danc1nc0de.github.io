---
title: 快速了解一个网络：Hourglass Network
date: 2025-01-14 15:45:00 +0800
categories: [Computer Vision]
tags: [快速了解一个网络, computer vision, backbone, hourglass]
---

> 以下内容偏向于记录个人学习过程及思考，请审慎阅读。
{: .prompt-info }

## 背景

本文提出的背景是检测人体姿态。

对于这个任务

- 既需要局部精细的空间features来精准地检测人体关节位置
- 又需要全局的features来预测人体整体的朝向、姿态等。

## 核心思想

本文的核心目标/动机是将卷积过程中不同scale的信息全部提取并融合起来，既有深层的语义信息，也有浅层的空间细节信息。

## Pipeline

1. 卷积过程中不同层的输出结果，都会经过维度对齐后在上采样过程中累加起来，补充空间细节信息。
2. 每一个hourglass模块都输出一个中间的heatmap用真值作监督，再堆叠多个hourglass模块，得到最终的heatmap。

![hourglass-pipeline](assets/img/hourglass-pipeline.png)

![hourglass-block](assets/img/hourglass-block.png)

## 亿些细节

- 上采样部份结构，作者使用近邻上采样和跳连结构实现，融合方式是通过使用1x1卷积将维度对齐后进行对应元素相加融合。
- 作者将传统的卷积结构替换为ResNet的残差结构和Inception的融合结构，性能有比较大的提升。
- 作者使用了test time augmentation，在测试时，对图像进行翻转操作，将heatmap求平均以获得更加robust的结果。

## 进一步了解

无

## 原文和代码

<https://arxiv.org/abs/1603.06937>

## 参考资料

无