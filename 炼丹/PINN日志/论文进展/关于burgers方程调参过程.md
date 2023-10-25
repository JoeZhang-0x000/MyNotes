## batch size 1024
![[Pasted image 20231022173715.png|alpha: 0.3, epochs: 20000]]
![[Pasted image 20231021141756.png|alpha:0.2, epochs:20000]]

![[Pasted image 20231021210319.png|alpha:0.1, epochs:20000]]
![[Pasted image 20231022155230.png|alpha:0.05, epochs:20000]]


## 退火学习率
![[Pasted image 20231023102559.png|T_0=500,T_mult=2]]
![[Pasted image 20231023114225.png|cosine annealing warm lr_0=1e-2, T_0=500, T_mult=2]]
由此可见，初始学习率设置为1e-3较为合适。

![[Pasted image 20231023163303.png|T_0 = 500, 1000]]
由此可见，T_0 = 500比较好