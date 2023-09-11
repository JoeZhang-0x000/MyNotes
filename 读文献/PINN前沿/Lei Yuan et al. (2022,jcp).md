date:2023-07-23
title: A-PINN: Auxiliary physics informed neural networks for forward and inverse problems of nonlinear integro-differential equations
url:[https://doi.org/10.1016/j.jcp.2022.111260](https://doi.org/10.1016/j.jcp.2022.111260 "Persistent link using digital object identifier")
source: Journal of Computational Physics

## 概括
针对积分问题，提出使用NN直接对积分中间态进行预测的方法，称为A-PINN。
## 结论

## 细节
对于积分问题：
![[Pasted image 20230724000427.png]]
可以写作：
![[Pasted image 20230724000459.png]]
若为传统PINN则利用牛顿莱布尼茨公式，将积分转化为离散积分。
本文**创新点**在于，利用NN预测中间变量$v(x)$.从而省去离散积分的误差。
![[Pasted image 20230724000356.png#C|]]
以及相应损失函数：
![[Pasted image 20230724000655.png]]