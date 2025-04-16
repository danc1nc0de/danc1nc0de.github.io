---
title: Normalization Layer
date: 2024-11-04 09:00:00 +0800
categories: [Algorithms]
tags: [algorithm, normalization layer]
---

> 以下内容偏向于记录个人学习过程及思考，请审慎阅读。
{: .prompt-info }

## Batch Normalization (BN) Layer

Batch Normalization（BN）是深度学习中广泛使用的一种正则化技术，主要用于加速神经网络的训练过程，减小网络对初始化权重的依赖，并在一定程度上缓解梯度消失或爆炸的问题。

BN 的核心思想是对神经网络的**每一层的输出进行标准化**，即对每个小批次中的激活值（激活输出）做均值和方差归一化，从而消除输入数据的分布偏移（Internal Covariate Shift）。

在CNN网络中，一般将每个Channel的输出看作是图像的一种特征。所以2D-BN通常是对神经网络中的**每个Channel进行标准化**。

注意，BN 引入了两个可学习的参数  &gamma;  和  &beta; ，用于恢复网络的表达能力，使得网络在标准化的基础上可以学习到合适的分布。

- 在训练阶段，BN 使用 mini-batch 的均值和方差进行标准化。
- 在测试阶段，BN 使用训练期间的滑动平均值来估计全局的均值和方差，从而保证模型输出的稳定性。

BN的局限性在于

- 依赖 mini-batch 大小：BN 的效果对 mini-batch 大小敏感，当 mini-batch 过小时，计算得到的均值和方差不够稳定，从而影响标准化效果。
- 不适合小型数据集：在小数据集上训练时，BN 可能会导致模型性能下降，因为每个 mini-batch 可能无法很好地代表整体数据分布。

## Layer Normalization (LN) Layer

Layer Normalization（LN）是一种常用的正则化方法，主要用于深度学习中，尤其是循环神经网络（RNN）和 Transformer 中。Layer Normalization 的作用和 Batch Normalization（BN）类似，但它适合于不同的应用场景。与 BN 不同，Layer Normalization 不依赖 mini-batch 的大小，而是在每个样本的特征维度上进行标准化，特别适合用于序列数据和小型 mini-batch 的场景。

Layer Normalization 的核心思想是对**每个样本的所有特征在特征维度上进行归一化**，使得每一层的输出具有相对稳定的均值和方差。这一过程不依赖于 batch size，因此在小 batch size 或单个样本输入的情况下仍然表现良好。

在 2D 卷积网络中，Layer Normalization 对**每个样本的所有通道的特征进行标准化**，目的是减少特征间的统计偏差，改善模型的收敛速度和泛化能力。

同样，LN 也引入了两个可学习的参数  &gamma;  和  &beta; ，用于恢复网络的表达能力，使得网络在标准化的基础上可以学习到合适的分布。

Layer Normalization 的优点
- 不依赖 batch size：LN 在特征维度上进行标准化，因此不依赖于 batch size，特别适用于小 batch 或单样本训练的场景。
- 适合序列数据：在 RNN 和 Transformer 等处理序列数据的模型中，LN 在时间步之间共享均值和方差，因此标准化的效果对序列数据更稳定。
- 不受 mini-batch 分布变化的影响：由于 LN 在样本内标准化，不受 mini-batch 中不同样本分布差异的影响，适合不稳定数据。

在 Transformer 中，Layer Normalization 用于标准化每一层的输入和输出，以提高训练稳定性。由于 Transformer 是基于注意力机制的序列模型，LN 可以在不依赖于 batch size 的情况下为每个样本进行标准化，因此 Transformer 各层之间的输入分布更加稳定。

Layer Normalization 的局限性
- 不适用于 CNN：由于 CNN 中各通道的局部性特征，LN 对 CNN 的标准化效果不如 BN。
- 未必适合所有数据类型：对于某些数据分布相对稳定的场景（如大 batch size 的 CNN 任务），BN 仍然可能比 LN 更有效。

Layer Normalization 是在特征维度上进行标准化的正则化技术，特别适用于序列数据、RNN、Transformer 以及小 batch size 场景。它可以有效地提高模型的稳定性和泛化能力，不依赖于 mini-batch 大小，与 BN 互为补充。

## Instance Normalization (IN) Layer

Instance Normalization 的主要思路是在**每个样本和每个通道上计算均值和方差**，以独立地进行标准化，从而去除样本间的统计干扰。IN 的目标是让模型的输出仅依赖于样本内部的统计信息，这对保持样本特有的风格特征尤为重要，适用于图像生成等任务。例如在生成对抗网络（GAN）中，尤其是图像生成和风格迁移任务中，IN 有助于生成高质量的图像，能够更好地适应风格变化。

Instance Normalization 的优点

- 保留样本风格特征：IN 能够去除样本间的统计干扰，对保持样本内部的风格特征非常有效。例如在风格迁移任务中，IN 有助于将内容与风格分离。
- 不依赖 batch size：IN 只在样本的通道维度上进行标准化，不依赖于 batch size，因此在小 batch size 或单样本任务中仍然有效。

Instance Normalization 的局限性
- 降低模型泛化能力：由于 IN 仅依赖于单个样本的统计信息，因此会导致模型在不同样本间无法很好地捕捉到整体分布特征。这在某些任务中可能降低泛化能力。
- 对分类任务的效果有限：IN 去除样本间的统计差异，这对于分类任务（尤其是有类别间区分的特征差异）可能不利。BN 在分类任务中通常效果更好。

## Group Normalization (GN) Layer

Group Normalization（GN）是一种常用的正则化方法，特别适用于小批次（small batch）或单样本的深度学习场景。与 Batch Normalization（BN）不同，Group Normalization 主要是通过将通道划分为多个组来进行标准化，而不是在 batch 维度上进行操作。**对于每个样本，它会把特征通道分成若干组，然后在每一组内部独立计算均值和方差**，对组内的值进行标准化。这种方式在一定程度上可以保留输入的统计特征，同时不受 mini-batch 大小的影响。

Group Normalization 的标准化计算发生在每个样本的每组通道上，而不是所有通道上或所有样本上。

Group Normalization 的优点

- 不依赖 batch size：GN 不依赖 mini-batch 大小，适合在小 batch 或单样本场景中使用。
- 平衡样本和特征的统计信息：GN 结合了 Instance Normalization 和 Batch Normalization 的优点，通过在组内进行标准化，既能捕捉样本内部的特征差异，也能捕捉部分样本间的统计信息。
- 适合不同任务：GN 在计算机视觉任务中非常常用，特别是在物体检测、分割等需要保持较高特征稳定性的场景中有良好效果。

选择合适的G值对 GN 的性能有重要影响

- 如果G=1，则 GN 退化为 Layer Normalization。
- 如果G=C，即每个通道单独一组，则 GN 退化为 Instance Normalization。

在实际应用中，GN 特别适合以下场景：
- 小 batch size 训练：例如在小批次样本训练时，BN 可能会失效，而 GN 可以更稳定地捕捉样本特征。
- 图像分割和检测任务：GN 的组内标准化有助于保持特征的一致性，这对需要细致定位的任务非常有效。
- 生成对抗网络（GAN）：在一些图像生成任务中，GN 的稳定性可以帮助生成更平滑的图像。

Group Normalization 是一种在每个样本的组内通道上进行标准化的方法，既保留了 BN 的效果又不依赖于 batch size，特别适合小 batch size 或单样本训练的场景。通过对通道分组计算均值和方差，GN 结合了 Instance Normalization 和 Layer Normalization 的优势，是一种高效且稳定的正则化技术。

参考 [Group Normalization](https://arxiv.org/abs/1803.08494 "Group Normalization") 的插图
![alt text](assets/img/normalization-layer.png)