基于多任务学习的视觉理解
====================================

各位尊敬的老师，您好！我是来自电子信息工程的吴振宇同学。这次毕业设计答辩的主
题为基于多任务学习的视觉理解。

研究背景
------------

深度学习和数据挖掘已经称为目前学术前沿的研究热点问题之一，在视觉理解领域，从
上世纪末基于深度学习的方法在性能上超越了传统方法之后，就引来了一大批学者的关
注：新的应用场景在不断出现，新的研究领域在不断扩展。与此同时，人们注意到应用
于每一个场景的模型只能完成对应的任务，而对其它领域的任务束手无策。这样的现实
告诉我们：仅仅是孤立的完成单独的任务，一方面与人们对计算机视觉能模拟生物视觉
，代替人眼工作的最终目标相差甚远，另一方面也暗示了模型性能依旧存在很大的提升
空间。

多任务学习
---------------

基于这样的现实，多任务学习的概念被提出：如何让一个模型完成多个任务并取得比只
能完成单个任务的模型更好的性能呢？

负迁移
---------

如果一个能完成多个任务的模型在某一个任务上性能不如只能完成单个任务的模型，则
称该模型在该任务上出现了负迁移。

目标
------

所以多任务学习的目标就是在能让模型完成多个任务的同时避免负迁移。

常见的多任务学习网络架构
------------------------------------

常见的多任务学习网络架构如图。下面我要介绍数据集、模型和任务的选择。

PASCAL
------

数据集选择了 PASCAL 上下文数据集。

模型
------

不同与大多数模型使用的残差网络 ResNet ，模型的骨干是 2019 年被提出的高分辨率
网络 HRNet ，其优点在于可以充分利用不同分辨率的特征。

HRNet
-----

如图，模型的输入经过残差层、混合层、过渡层后会得到 4 个分辨率依次减半的输出，
分辨率下降的原因是因为采用了步距为 2 的卷积层进行降采样。在每一个混合层都会将
不同分辨率的特征混合。过渡层对混合层的输出经过一个恒等变换，并通过降采样得到
一个新的分辨率的特征。

MTI 网络
----------

在高分辨率骨干网络的基础上，将 4 个不同分辨率的特征再通过一个多尺度任务交互网
络 MTI 解码器网络来得到最终 3 个不同任务的输出。在解码器内部，不同分辨率的特
征由高到低经过混合、初始化再传播到下一个分辨率。蒸馏的目的是为了减小特征的数
量以提取有用的特征。

MTI 网络
----------

对于多任务学习，除了网络结构，任务的选择也非常重要。

任务
------

我们选择语义分割、人类部位分割、显著点检测 3 个任务。

性能指标
------------

衡量各个单任务的性能指标是 IoU 。衡量多任务学习的性能指标是各个单任务的 IoU
的加权平均。权重与前人的论文选择保持一致。最终我们首先要比较加权平均 IoU 来分
析是否提升了性能，以及比较各个单任务的 IoU 来分析是否避免了负迁移。

实验
------

下面是实验的具体过程。

语义分割
------------

如图，水平线代表目前该领域实验的最优结果。

人体解析
------------

实验与最优结果平均差距不足 1 个百分点。

显著点检测
---------------

另外训练集上的结果远远优于测试集，说明模型的泛化性能不如预期的好。

实验结果
------------

下面让我们看一下多任务学习是否真的有效。表格的第二排都超过了第一排说明在各项
任务上多任务都比单任务的性能取得了提升，没有出现负迁移的现象。
但我们也要注意到一件事，在某些任务例如人体解析上，第二排甚至比第三排还低了不
到 0.05 个百分点，这说明多任务学习在某些任务上没有超过最好的单任务学习。

误差分析
------------

对差距的一些分析表明实验依旧存在改进的空间。

改进策略
------------

在模型的改进方案中，改进骨干网、某些超参数的调整能取得性能提升效果最为显著。

致谢
------

谢谢您的聆听！
