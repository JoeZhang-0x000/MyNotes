# 粗细采样
## [[log-2023-06-09]]
后台阶流的粗细采样相关实验
## [[log-2023-06-10]]
考虑到N-S方程可能过于复杂，不利于训练。考虑使用简单的方程观测。因此泊松方程的粗细采样实验。
## [[log-2023-06-11]]
Helmholtz eq需要5w步训练方可捕捉到波形。考虑将其他两组实验也跑5w步。
## [[log-2023-06-13]]
## [[log-2023-06-15]]
Helmholtz eq训练10w步，结果过拟合了。
## [[log-2023-06-23]]
# 同伦延拓
## [[log-2023-06-17]]
## [[log-2023-06-20]]
## [[log-2023-06-21]]
## [[log-2023-06-24]]
A simple experiment with lid driven cavity.
## [[log-2023-06-25]]
An extension for the last experiment.
## [[log-2023-06-26]]
Include an experiment about the potential influence of the test point density on R2 scores.
## [[log-2023-06-30]]
## 数据同伦的探究
This study investigating the impact of different distribution of the smoothing factor $t$ on the performance of the NN, providing insights into the relationship between *auxiliary data*, *training duration*, and *curve smoothness*. For more details, refer to [[log-2023-07-01]]
### [[log-2023-07-01]] 
This experiment focuses exclusively on the impact of *auxiliary data*, specifically comparing the differences between Re=50 and Re=10.
### [[log-2023-07-02]]
This experiment aims to explore the specific impact of _segments_ and compare the differences among different segment values. The segments being investigated are set to $[5, 10, 20, 40]$.
### [[log-2023-07-03]]
This experiment aims to explore the specific impact of *total iterations* and compare the difference among different training steps. The training steps being investigated are set to $[10k,20k,40k,100k]$, and segments are $[10,10,10,10]$.
### [[log-2023-07-04]]
This experiment is an exclusion of the previous study, which fixes the *segment iterations* while increasing the *total iterations*. The total iterations being investigated are set to $[10k,20k,40k,100k]$, and segments are set to $[10,20,40,100]$.
## 方程同伦的探究
This study aims to investigate the impact of adding a smoothing factor to N-S equations on the training accuracy.
### [[log-2023-07-05]]
The study comprises a series of experiments investigating the impact of incorporating a smoothing factor. The experiments explore the variations in performance from different alpha values, ranging form 0.2 to 0.8.
### [[log-2023-07-06]]
Same as the previous study, except for the range of smoothing factor is between 2 to 1.
### [[log-2023-07-09]]
Adding a smoothing factor to the convection term inside the diffusion term, ranging from 0 to 1, and testing different alpha values ranging from 0.2 to 0.8
### [[log-2023-07-11]]
This study is the same as the pervious one, but the smoothing factor t ranges between 2 and 1.
### [[log-2023-07-12]]
Both adding a smoothing factor to the convection term and the diffusion term, which named $t_{c}$ and $t_{d}$, ranges form 0 to 1 and 2 to 1.

## [[暑期小论文1]]
后续实验内容总结于此。
# 两次训练
# 初始化手段
先采用粗粒度的解，构造衰减权重。
# 高斯积分