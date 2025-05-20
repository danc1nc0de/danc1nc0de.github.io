---
title: 快速了解一个网络：Focal Loss for Dense Object Detection
date: 2025-05-19 09:30:00 +0800
categories: [Computer Vision]
tags: [快速了解一个网络, computer vision, 2d detection, loss]
math: true
---

> 以下内容偏向于记录个人学习过程及思考，请审慎阅读。
{: .prompt-info }

## 背景

作者认为一阶段目标检测器的精度达不到二阶段目标检测器的原因是：

前景和背景类别数量极不均衡，训练过程中大量“背景”的出现影响了训练效果。

在二阶段目标检测器中，通过region proposals和正负样本按比例采样，改善了正负样本数量不均衡的问题。

## 核心思想

设置一种自适应loss

- 对于检测概率极高/极低的类别，即容易的样例，减小其对应的loss
- 对于检测概率接近0.5的类别，即困难的样例，增大其对应的loss

以达到类似于“难例挖掘”的目的。

## Pipeline

```python
def sigmoid_focal_loss(
    inputs: torch.Tensor,
    targets: torch.Tensor,
    alpha: float = -1,
    gamma: float = 2,
    reduction: str = "none",
) -> torch.Tensor:
    """
    Loss used in RetinaNet for dense detection: https://arxiv.org/abs/1708.02002.
    Args:
        inputs: A float tensor of arbitrary shape.
                The predictions for each example.
        targets: A float tensor with the same shape as inputs. Stores the binary
                 classification label for each element in inputs
                (0 for the negative class and 1 for the positive class).
        alpha: (optional) Weighting factor in range (0,1) to balance
                positive vs negative examples. Default = -1 (no weighting).
        gamma: Exponent of the modulating factor (1 - p_t) to
               balance easy vs hard examples.
        reduction: 'none' | 'mean' | 'sum'
                 'none': No reduction will be applied to the output.
                 'mean': The output will be averaged.
                 'sum': The output will be summed.
    Returns:
        Loss tensor with the reduction option applied.
    """
    inputs = inputs.float()
    targets = targets.float()
    p = torch.sigmoid(inputs)
    ce_loss = F.binary_cross_entropy_with_logits(inputs, targets, reduction="none")
    p_t = p * targets + (1 - p) * (1 - targets)
    loss = ce_loss * ((1 - p_t) ** gamma)

    if alpha >= 0:
        alpha_t = alpha * targets + (1 - alpha) * (1 - targets)
        loss = alpha_t * loss

    if reduction == "mean":
        loss = loss.mean()
    elif reduction == "sum":
        loss = loss.sum()

    return loss
```

## 亿些细节

### Class Imbalance

类别不均衡会造成

- 在大部分图片位置训练是不充分的，因为背景的占据贡献了大量无用信息
- 比较easy的负样本会占据training过程，让网络忽视难例

### Robust Estimation

像Huber loss等是通过降低outliers的权重来减小对结果的影响

而Focal loss则是通过降低inliers（大量easy samples）的权重来减小其对结果的影响

### Focal Loss

- 在本文中，实验发现$\gamma=2$的效果最好
- 在实际中会进一步定义一个${\alpha}_t$用于loss平衡（相比于不用会有轻微提升，见上述代码）
- 在本文中，实验发现$\alpha=0.25$的效果最好
  
### Class Imbalance and Model Initialization

对于二分类检测器，由于训练初期，网络对于正负样本的估计概率都大致相同，使用focal loss训练初期，大量背景anchor的loss会非常大，使得训练变得极不稳定。

因此作者考虑在网络初始化过程中，增加一个初始的先验概率，即初始时每个框都是一个概率很小的目标。

具体地，是通过分类网络最后一层添加一个bias（sigmoid之前）

```python
# Use prior in model initialization to improve stability
# prior_prob = 0.01 for default
bias_value = -(math.log((1 - prior_prob) / prior_prob)) # inverse sigmoid
torch.nn.init.constant_(self.cls_score.bias, bias_value)
```

## 进一步了解

- [Huber loss](https://en.wikipedia.org/wiki/Huber_loss)

## 原文和代码

<https://arxiv.org/abs/1708.02002>

<https://github.com/facebookresearch/detectron2>

## 参考资料

无