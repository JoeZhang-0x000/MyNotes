date:2023-07-12
title: Spatiotemporal parallel physics-informed neural networks: A framework to solve inverse problems in fluid mechanics
url: https://doi.org/10.1063/5.0155087
source: Physics of Fluids 35, 065141 (2023)

## 概括
针对流场重构，提出**重叠型区域分解**PINN来进行。对比了使用N-S方程和使用**RANS**两种方法二维圆柱绕流的预测结果。
对比了strong scaling 和 weak scaling 两种问题下的并行效率。
此外，使用了**带热重启的余弦退火学习率**，认为退火学习率有利于加速收敛。
## 结论
相同条件下，使用RANS能提高重构精度。
![[Pasted image 20230712122850.png#C|Relative $L_{2}$ norm]]

For strong scaling, STPINNs yielded satisfactory speedup. For weak scaling, STPINNs presented parallel efficiency of over 90% when the number of devices was less than 40 and exhibited relatively stable and reasonable prediction accuracy
## 细节
### 重叠型区域分解
所谓重叠型区域分解，与前人所属类似，在交界面处保持连续性。
![[Pasted image 20230712122114.png#C|Schematic diagram of overlapping domain decomposition.]]
![[Pasted image 20230712122148.png#C|Domain decomposition along x, y, and t directions.]]
### 模拟退火
![[Pasted image 20230712122554.png#C|Cosine annealing learning rate schedule, with warm restart.]]
### 局限性
因为二维非定常问题加上时间维就是三维的，因此目前该框架只能做2d unsteady flows, 要处理3d unsteady flows 需要用4d区域分解，这是本文的局限。
