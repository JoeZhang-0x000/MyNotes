---
aliases:
  - "Multi-stage Neural Networks: Function Approximator of Machine Precision"
---

## 概括
文中指出PINN的残差难以降低到$10^{-5}$,针对这一状况，作者提出了一种多阶段训练策略，
	``To address this issue, we developed the multi-stage neural networks that divides the training process into different stages, with each stage using a new network that is optimized to fit the residue from the previous stage.``
每一个阶段由一个新的NN在原来训练的基础上进行更精细的训练，最终将残差降低到了$10^{-16}$，接近机器浮点表示的精度极限。
	``We demonstrate that the prediction error from the multi-stage training for both regression problems and physics-informed neural networks can nearly reach the machine-precision O(10−16) of double-floating point within a finite number of iterations.``
此外，文章中提到了该算法可以进一步和gPINN以及RAR进行结合，进而提高精度。
## 结论

## 细节
### 高频难以训练的解释
![[Pasted image 20231002190828.png]]
作者认为，应对高频成分时，激活函数的频率太低了，需要从O(1)->O(2$\pi f_d$)，这导致了训练失败。因此提出的解决措施是，引入一个scale factor 用以提高激活函数的频率，从而增加对高频细节的捕获能力。
### 效果
![[Pasted image 20231002165710.png]]
### 多阶段训练
第k阶段的网络:
$$
u_{k}^{c} = u_{k-1}+\epsilon_{k}u_{k}(x,K_k)
$$
where, $K_k$ : scale factor; $\epsilon_k$ magnitude prefactor;
最终的预测值由所有的网络叠加：
$$
u(x) = u_{0}+ \sum_{k=1}^{n-1}\epsilon_{k}u_{k}(x,K_k)
$$
