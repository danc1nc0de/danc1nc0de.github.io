---
title: 每天学网络：Faster RCNN
date: 2024-09-07 15:30:00 +0800
categories: [Computer Vision, 2D Detection]
tags: [每天学网络, computer vision, 2d detection, faster rcnn]
---

> 以下内容偏向于记录个人学习过程及思考，非常规教学内容
{: .prompt-info }

## 背景

不管是RCNN还是Fast RCNN，其中Region Proposals这个计算过程，仍然非常耗时，成为计算瓶颈。

## 核心思想

使用CNN网络产生Region Proposals！即RPN，Region Proposals Network

CNN部分，可以与后续的分类与回归网络共用，实现更快速的推理

## Pipeline

![faster-rcnn-pipeline](assets/img/faster-rcnn-pipeline.png)

通过在feature maps上滑窗，再进入一个小网络，得到各种region proposals。具体执行过程如下

![region-proposals-network-pipeline](assets/img/region-proposals-network-pipeline.png)

这里设定了k个anchor boxs，每个anchor box负责预测与它形状类似的region proposals

## 亿些细节

### anchor boxs的尺寸与比例

本文使用3种scale和3种比例，共9种anchor boxs

对于coco数据集，由于小目标比较多，多设置了一种scale

若anchor跨越了图像边界，本文的做法是直接忽略掉了

### loss function

一个GT box可能被分配给多个anchor box（只要iou大于一定阈值），用作分类损失训练

### RPN training

4步交替训练法

1. 训练RPN网络（使用ImageNet预训练模型初始化）
2. 用第一步训练的RPN网络单独训练一个Fast RCNN网络
3. 使用训练第2步训练的Fast RCNN网络初始化RPN网络，固定共享的卷积层，只微调RPN自己的层
4. 固定共享的卷积层，使用以上微调后的RPN网络，微调Fast RCNN自己的层

### Region Proposals的筛选

由于网络会产生大量region proposals。本文作者使用NMS算法，基于cls的score排序，保留约2000个region proposals

## 进一步了解

NMS（TODO）

## 原文和代码

<https://arxiv.org/abs/1506.01497>

## 参考资料

{% include embed/bilibili.html id='BV1GB4y1r7rM' %}