---
aliases:
  - "When and why PINNs fail to train: A neural tangent kernel perspective"
---
## 概括
1. 作者分析了PINN的NTK，发现PINN的NTK的特征值衰减的很迅速。
2. NTK的特征值大小与训练该分量的误差下降速度成正比，特征值越大的越先收敛。
3. 不同频率分量的NTK特征值衰减速度一致，说明PINN几乎同时学习所有的频段，与LuLu的观察一致。
4. $K_{rr}$ 和特征值大于$K_{uu}$的特征值，意味着PDE residual比PDE boundary收敛的快。作者认为这种收敛速度的不协调可能导致了PINN的训练失败。
5. 提出动态权重算法

![[Pasted image 20231003104301.png]]
## 收获
1. Introduction部分引用了许多PINN在各行各业的应用，可以参考。
2. Recent researches of fully-connected neural networks demonstrated that it suffers from **spectral bias** and incapable of learning functions with high frequencies, both in theory and practice.
3. The convergence rate of the total training error can be evaluated by the spectrum of its NTK at initialization.

