date:2023-09-23
title: Dynamics-informed deconvolutional neural networks for super-resolution identification of regime changes in epidemiological time series
url: https://www.science.org/doi/10.1126/sciadv.adf0673
source: 

## 概括
提出了一个基于反卷积神经网络(dynamics-informed deconvolutional neural network， DIDNN)的新方法,可以仅从死亡记录中反推出流行病学动力学中的体制变化,实现每日级别的识别精度。
## 结论
1. 研究者开发了一种基于卷积神经网络的反向方法,称为DIDNN,可以从平滑的死亡曲线中提取出不连续的发病率曲线。
2. 利用了流行病学动力学方程作为正则化,使得该方法可以准确识别各种非药物干预措施的实施时间,精度达到每日级别。
3. 在新冠肺炎大流行初期的欧洲多个国家进行了验证,结果表明该方法可以以0.22天的误差识别重大封锁措施的启动和取消时间。
4. 这表明重大干预措施对传染病传播的影响是瞬时的,而不是之前认为的会有延迟的。
5. 该方法为评估和决策非药物干预措施的影响提供了一个重要工具。
6. 也可以通过反向应用该方法来推断疾病的临床和传播特征。
7. 总体来说,这项研究开创了卷积神经网络在流行病学反问题研究中的新方向,使我们可以更准确地理解流行病学动态。

## 细节
![[Pasted image 20230923213118.png]]