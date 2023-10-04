---
aliases:
  - Adapting PINN Models of Physical Entities to Dynamical Data
---
## 概括
1. 本文解决的问题是==动态系统==。
2. 本文比较了PINN和PPINN(parametric PINN)的优劣性，得出结论：
	1. 在观测点较多，参数变化不大时用PINN效果好；
	2. 观测点较少，参数变化剧烈时用PPINN效果好；
## 收获

### 内容引用
1. 作者在Introudction部分提到，PINN的主干发展过程。作者在05年已经开始研究相关内容，但是当时的用的术语不同，可cite此内容。
### 文章结构
1. 本文的文章结构可以借鉴，在Results部分，作者先介绍了所有的Benchmark Problems，再分别每一个其Computional Experiments and Results。这样写条理更加清晰，但是如果读者对于问题待解决的问题不太熟悉，可能需要来回上下翻页，阅读体验不佳。
	Benchmark Problems:
		1. benchmark 1
		2. benchmark 2
		3. ...
	Results:
		1. results 1
		2. results 2
		3. ...