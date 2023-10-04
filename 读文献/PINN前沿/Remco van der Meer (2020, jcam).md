---
aliases:
  - Optimally weighted loss functions for solving PDEs with Neural Networks
---
## 概括
1. 文章证明了For any linear PDEs,  the loss function is convex; however, it is still not clear about nonlinear PDEs.
2. 文章试图提出一种更具一般性的loss function，增加了一个幅度归一化，作者描述该方法可以应对导数较大的问题。
>![[Pasted image 20231004162438.png]]![[Pasted image 20231004162344.png]]![[Pasted image 20231004162909.png]]
3. 此外作者还提出一种==自适应采样==方法，用于平衡边界和PDE residual，核心思想就是，如果BC residual >p* PDE residual，这就说明其中有一项训练的不好，那么就需要增加其采样点数量。
	1. #idea 这与我们的逐渐增加采样点的思路不谋而合。
## 收获
### 写作✍
1. 深度神经网络已经出现了60多年了，但是直到最近才可以在通用设备上进行训练。参考自Deep learning in neural networks: An overview (2014)。于是==This lead to exceptional achievements== in wide rage of problems, including ... ==Aside from these empirical achievements==, the ==theorical understanding== of such methods is also advancing rapidly. ==This has sparked interest== in ....
2. 
### PINN的理解
原文提到:
>so far, it is only clear that minimizing the loss functional exactly yields a solution of the PDE. However, when one minimizes the Monte-Carlo approximation instead, it is ==highly unlikely== that this exact minimum is attained.

1. 作者与我的想法不谋而合，使用Monte Claro 积分只能保证在有限个点上处于最优，因为采样点的影响十分关键，倘若不用Monte Claro积分则可以规避采样点的选取造成的影响。
	1. #idea 那么我是否就可以采取一种替代手段去更精确的表示积分，比如我之前想到的三角形高斯积分？或许能提升精度？🤔