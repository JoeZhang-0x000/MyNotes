## 实验介绍
We will solve the Kovasznay flow equation on : $\Omega = [0, 1]^2$

$$u\frac{\partial u}{\partial x} + v\frac{\partial u}{\partial y}= -\frac{\partial p}{\partial x} + \frac{1}{Re}(\frac{\partial^2u}{\partial x^2} + \frac{\partial^2u}{\partial y^2}) $$

$$ u\frac{\partial v}{\partial x} + v\frac{\partial v}{\partial y}= -\frac{\partial p}{\partial y} + \frac{1}{Re}(\frac{\partial^2v}{\partial x^2} + \frac{\partial^2v}{\partial y^2}) $$

with the Dirichlet boundary conditions

$$ u(x,y)=0, \qquad (x,y)\in \partial \Omega$$

The reference solution is $$u = 1 - e^{\lambda x} \cos(2\pi y)$$ $$v = \frac{\lambda}{2\pi}e^{\lambda x} \sin(2\pi x)$$ $$p =\frac{1}{2}(1 - e^{2\lambda x})$$where $$\lambda = \frac{1}{2\nu}-\sqrt{\frac{1}{4\nu^2}+4\pi^2}.$$
## MIC值表格
采用与LuLu实验中相同的参数，$Re=20$，则有如下的MIC值表格。
### x方向
| $uu_{x}$ | $vu_y$ | $p_{x}$ | $\nabla\cdot\nabla u$ |
| -------- | ------ | ------- | --------------------- |
| 1        | 0.12    | 0.48    | 1                     | 
### y方向
| $vv_{x}$ | $vv_y$ | $p_{y}$ | $\nabla\cdot\nabla v$ |
| -------- | ------ | ------- | --------------------- |
| 1        | 0.21    | 0    | 1                     | 
这说明：
	1. x方向NS eq可以忽略$vu_{y}$；
	2. y方向的NS eq可以忽略$vv_{y}$与$p_{y}$；
综合而言，我们选择忽略含有$u_{y}$分量的项。
