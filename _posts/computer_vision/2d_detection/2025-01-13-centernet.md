---
title: 快速了解一个网络：CenterNet (Objects as Points)
date: 2025-01-13 13:00:00 +0800
categories: [Computer Vision, 2D Detection]
tags: [快速了解一个网络, computer vision, 2d detection, centernet]
---

> 以下内容偏向于记录个人学习过程及思考，非常规教学内容
{: .prompt-info }

## 背景

一阶段目标检测网络通常是按照一定规则在图像/feature map上滑动选取一系列anchors进行检测

二阶段目标检测网络通常是基于proposals的方式进行检测

以上两种方案都需要增加后处理NMS来去除大量的重复框，但后处理过程很难求导和训练。

## 核心思想

将目标用其中心点表示，然后利用回归网络预测其其它属性，如尺寸、朝向等。

文章基于CNN预测heatmap，heatmap的峰值即为目标的中心点。使用峰值位置部份的img features来回归预测目标属性。

峰值点的提取过程则等价地取代了NMS计算部份。

## Pipeline

backbone仍使用hourglass network / up-convolutional residual networks (ResNet) / deep layer aggregation (DLA)等

只是输出建模为了heatmap形式

## 亿些细节

目标是基于CNN预测一个H/R x W/R x C的heatmap，其中H，W为图像的原始长宽，R为下采样倍率，C为类别数。预测值为1表示center point，预测值为0表示背景。

真值生成过程使用Gaussian kernel。均值使用目标真值的中心点位置下采样R，方差则根据目标尺寸和下采样倍率计算。

如果同一个类别有两个Gaussian分布重叠，则重叠部份取max

为了减少下采样R的离散过程带来的位置误差，额外预测一个local offset去调整位置，所有的class共享相同的offset预测

同样，为了减小计算量，所有类别也是共用一个size预测

因此，对于每个位置，网络会预测C+4个输出，其中C为对应类别的中心点概率，4分别为size和offset的预测

在预测阶段，从heatmap中提取峰值即可（对应位置的值大于周围8个临近点的值）

## 进一步了解

- hourglass network
- up-convolutional residual networks (ResNet)
- deep layer aggregation (DLA)

## 原文和代码

<https://arxiv.org/abs/1904.07850>

## 参考资料

无