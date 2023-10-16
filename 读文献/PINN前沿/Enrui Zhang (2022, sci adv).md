## 题目
Analyses of internal structures and defects in materials using physics-informed neural networks
## 概括
本文的主要贡献：
>“we present a general framework based on physics-informed neural networks for identifying unknown geometric and material parameters.” (Zhang 等, 2022, p. 1)

求解反问题，预测材料内部缺陷或夹杂物的形状，位置，大小等信息。

## 原理
在一个含有缺陷或夹杂物的试样中选取几个观测点，然后测量几个位置的应变。
![[Pasted image 20231016214404.png]]

## 结果
根据作者的实验，PINN预测的缺陷位置以及形状与ABAQUS预测值高度近似，可以认为其具备正确性。
![[Pasted image 20231016214657.png]]
## 结论
作者认为他们提出的这种方法，可以广泛应用于工程实践和科学研究之中。这种基于PINN的缺陷预测方法的优势在于：
1. 相比于有限元：
	1. 不需要额外的设置参数的更新规则，不需要每次迭代完之后都重新划分网格；
	2. 实现起来门槛较低，相关的深度学习库比较完善，省去了设计反问题算法的开销；
2. 相比于传统数据驱动算法：
	1. 数据依赖性小，更加具备物理可解释性；

## 小细节
>“Inspired by the transfer learning technique, we propose to maintain all the estimated unknown parameters fixed (not trainable) and only update the trainable parameters of the NN  for the first few iterations. During this pretraining process, the PINN essentially solves a forward problem, seeking to roughly capture the qualitative pattern of the displacement field and the stress field.” (Zhang 等, 2022, p. 11)

作者提出，在训练反问题时候，预训练是很有必要的。即，在开始训练的一小段时间内，只训练正问题。如果没有这样的一小段预训练，则反演的参数值会偏离参考值越来越远。