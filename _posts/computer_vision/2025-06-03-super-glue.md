---
title: 快速了解一个网络：Super Glue, Learning Feature Matching with Graph Neural Networks
date: 2025-06-03 10:30:00 +0800
categories: [Computer Vision]
tags: [快速了解一个网络, computer vision, gnn, feature matching]
math: true
---

> 以下内容偏向于记录个人学习过程及思考，请审慎阅读。
{: .prompt-info }

## 背景

对于两张图像的特征匹配：较大的视点和光照变化、遮挡、模糊和缺乏纹理是使 2D 到 2D 数据关联具有较大的挑战性。

## 核心思想

Super Glue 从特征点匹配角度（而非特征点提取角度）出发，通过Graph Neural Networks (GNN)建模特征点间的匹配关系。

## Pipeline

![super-glue-pipeline](assets/img/super-glue-pipeline.png)

## 亿些细节

### Multiplex Graph Neural Network

对于第l层、图A中的第i个特征点，通过GNN结构将其与图A中的其它特征点及图B中的特征点做交互，最终得到汇聚的特征与当前层输入特征进行concat，经过MLP后再与当前层输入特征相加。

### Attentional Aggregation

每层汇聚的特征是通过attention机制得到的。

- 对于奇数层，汇聚的是本图中特征点交互的特征；
- 对于偶数层，汇聚的是它图中特征点交互的特征；

![super-glue-attention](assets/img/super-glue-attention.png)

### Score Prediction

在最优匹配过程中，特征间的相似度是通过特征向量的内积得到的。

### Occlusion and Visibility

对于各图中没有匹配上的点，会将这些点都指定其匹配到一个dustbin（垃圾桶）上，以使网络抑制某些特征点。

### Sinkhorn Algorithm

最优匹配算法采用Sinkhorn Algorithm，是一种可微的Hungarian Algorithm

### Loss

分配方案的负对数似然，并且包含未匹配上的点。

## 进一步了解

- [Sinkhorn Algorithm](https://blog.csdn.net/zsfcg/article/details/112510577)
- [Hungarian Algorithm](https://en.wikipedia.org/wiki/Hungarian_algorithm)

## 原文和代码

<http://arxiv.org/abs/1911.11763>

## 参考资料

[论文阅读《Super Glue, Learning Feature Matching with Graph Neural Networks》](https://blog.csdn.net/weixin_40957452/article/details/123611466 "论文阅读《Super Glue, Learning Feature Matching with Graph Neural Networks》")