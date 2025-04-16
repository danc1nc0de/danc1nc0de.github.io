---
title: 快速了解一个网络：Efficient Net
date: 2025-01-18 17:30:00 +0800
categories: [Computer Vision]
tags: [快速了解一个网络, computer vision, backbone]
math: true
---

> 以下内容偏向于记录个人学习过程及思考，请审慎阅读。
{: .prompt-info }

## 背景

增大CNN网络的方法没有被很好的研究过。

为了增大一个CNN网络，通常的做法一般有3种

- 网络加深（层数变多）
- 网络变宽（通道数增大）
- 输入分辨率增大

这些改变依赖大量人工调试，且通常无法得到最佳的效果。

## 核心思想

提出一种混合的缩放方式（compound scaling method），按照以下公式同时对depth, width, resolution进行缩放。

$$
\begin{aligned}
\text{depth: } d = \alpha^{\phi} \\
\text{width: } w = \beta^{\phi} \\
\text{resolution: } r = \gamma^{\phi} \\
\text{s.t. } \alpha \cdot \beta^2 \cdot \gamma^2 \approx 2 \\
\alpha \geq 1, \ \beta \geq 1, \ \gamma \geq 1
\end{aligned}
$$

其中$\phi$是缩放比例。

本文先基于NAS的搜索方法找到一个小的baseline模型，即EfficientNet-B0

再固定$\phi=1$，基于small grid search的方式找到最佳的$\alpha$, $\beta$和$\gamma$，优化目标为Accuracy和FLOPS

最后基于这个小的baseline模型按照上面的缩放公式进行网络的扩大，得到一系列模型，即EfficientNet-B1 to B7

## Pipeline

![efficient-net-b0-pipeline](assets/img/efficient-net-b0-pipeline.png)

其中MBConv是MobileNetV2中的Convolutional Block，并且作者在其中加入了SeNet模块，即Squeeze-and-Excitation Networks

## 亿些细节

### Scaling Dimensions

- depth
  - 更深的网络可以捕捉更丰富和更复杂的features，可以帮助在新任务上进行泛化
  - 但是，更深的网络因为梯度消失问题，更加难以训练。并且当网络深度达到一定值时，网络准确度也趋于饱和。
- width
  - 更宽的网络可以帮助捕捉更精细的features也相对容易训练
  - 但是，只把模型变宽而不加深，模型很难捕捉到更高level的features
- resolution
  - 更大的分辨率可以帮助模型捕捉更精细的features
  - 但是，当分辨率达到一定值时，准确性也基本饱和。

观察1
: 增大网络的任意一个维度都可以带来准确性的提升，但是随着维度的提升准确性都会趋于饱和。

### Compound Scaling

观察2
: 为了追求更好的准确性和效率，在增大网络时需要同时平衡好各个维度。

## 进一步了解

- MobileNetV2
- SeNet, Squeeze-and-Excitation Networks

## 原文和代码

<https://arxiv.org/abs/1905.11946>

## 参考资料

无