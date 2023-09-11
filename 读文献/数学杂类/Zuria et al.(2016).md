date:2023-06-13
title: Newton Homotopy Continuation Method for Solving Nonlinear Equations using Mathematica
url:https://www.researchgate.net/publication/301776880_Newton_Homotopy_Continuation_Method_for_Solving_Nonlinear_Equations_using_Mathematica
source:
## 概括
提出了一种HCM辅助牛顿迭代法，用于求解非线性方程。比Newton method要更容易收敛，且不容易会受到不合理**initial value**的选择而导致**divergence**。
## 结论
![[Pasted image 20230613141803.png|500]]

## 细节
### 评价
我认为该文章内容较水，概念含糊不清，算法指向不明，但是思想可以借鉴。文中的评价指标并不严谨。
Newton method 的方法已经很好用了，但是当$f^{'}(x)\approx 0$时，$\frac{f(x)}{f^{'}(x)}\to\infty$，这样就导致了Newton迭代难以收敛或继续进行。
采用HCM可以通过一步一步求解与$f(x)$相似的一组方程$g(x)=tf(x)+(1-t)h(x)=0$的解，最终当$t=1$时即$g(x)=f(x)$，来逐渐的逼近$f(x)=0$的解。从$x_{0}=x_0$开始，以此类推，每一个$t_n$的初值都是$h(x,t_{n-1})=0$的根，最终到了$h(x,1)=f(x)=0$。这样有效降低了初值选择对迭代法敛散性的影响。
### codes
与网络资料结合，给出以下HCM代码。
```python
import numpy as np

# 定义原始方程 f(x)

def f(x):

    return x**2+8*x-9

  

# 定义辅助方程 g(x, t)

def g(x, t):

    return t*f(x) + (1-t)*(x)

  

# 定义辅助方程 g(x, t) 的导数

def g_prime(x, t):

    return t*(2*x+8)+(1-t)

  

# 同伦牛顿法迭代函数

itr = 0

def homotopy_newton_method(x0, t, threshold):

    global itr

    itr += 1

    x = x0  # 初始解的近似值

    delta = threshold + 1  # 初始变化量

    while delta > threshold:

        gx = g(x, t)  # 计算辅助方程的值

        gx_prime = g_prime(x, t)  # 计算辅助方程的导数

        x_new = x - gx / gx_prime  # 使用牛顿迭代更新解的近似值

        delta = abs(x_new - x)  # 计算解的近似值的变化量

        x = x_new  # 更新解的近似值

    return x

  

# 主程序

x0 = 0.0  # 初始解的近似值

t = 0.0  # 参数 t 的初始值

t_increment = 0.1  # t 的增量

threshold = 1e-6  # 收敛阈值

  

roots = []  # 存储方程的近似根

  

while t <= 1.0:

    root = homotopy_newton_method(x0, t, threshold)

    roots.append(root)

    x0 = root

    t += t_increment

print('迭代总次数',itr)

# 打印方程的近似根

for i, root in enumerate(roots):

    print("t = {:.1f}, 方程的近似根: {:.6f}".format(i * t_increment, root))

print(f'方程的解是{roots[-1]}, 此时f(x)={f(roots[-1])}')
```
```
迭代总次数 11 t = 0.0,
方程的近似根: 0.000000 t = 0.1,
方程的近似根: 0.513878 t = 0.2,
方程的近似根: 0.708204 t = 0.3,
方程的近似根: 0.807816 t = 0.4,
方程的近似根: 0.868051 t = 0.5,
方程的近似根: 0.908327 t = 0.6,
方程的近似根: 0.937129 t = 0.7,
方程的近似根: 0.958741 t = 0.8,
方程的近似根: 0.975551 t = 0.9,
方程的近似根: 0.988999 t = 1.0,
方程的近似根: 1.000000 方程的解是1.0, 此时f(x)=0.0
```