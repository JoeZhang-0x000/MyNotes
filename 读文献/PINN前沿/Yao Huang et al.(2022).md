date:2023-06-13
title: HomPINNs:Homotopy physics-informed neural networks for learning multiple solutions of nonlinear elliptic differential equations
url: https://www.sciencedirect.com/science/article/pii/S0898122122002851?via%3Dihub
source: Computers & Mathematics with Applications
## 概括
提出HomPINNs，使用同伦算法求解出偏微分方程的多解。先使用一个starting NN进行初始化，再通过同伦算法求出一些列解。
### 主要算法
![[Pasted image 20230613152056.png|500]]
### 网络模型
![[Pasted image 20230613152440.png|500]]
## 结论
主要涉及具有不止一个解的偏微分方程系统，借助同伦延拓可以求出一系列解。
### 展望
作者认为可以研究自适应激活函数以及starting network的构造。
## 细节