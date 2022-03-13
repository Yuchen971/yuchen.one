alias:: 协方差矩阵

- Definition
	- [[variance]] $\sigma_x^2$ 可以视作[[random variable]] $x$ 关于自身的 [[covariance]] $\sigma(x, y)$
		- variance 公式: ((61ff7250-466f-4906-a517-51029dea4ef8))
		- covariance 公式: ((61ff739f-eba9-4dcc-ab66-f2ed2f76fed7))
	- 根据方差的定义, 给定$d$ 个随机变量 $x_k, \text{where k} = 1,2,3,..,d$, 则这些随机变量的方差为
		- $$
		  \sigma\left(x_{k}, x_{k}\right)=\frac{1}{n-1} \sum_{i=1}^{n}\left(x_{k i}-\bar{x}_{k}\right)^{2}, k=1,2, \ldots, d
		  $$
	- 根据协方差的定义, 求出两两之间的协方差
		- $$
		  \sigma\left(x_{m}, x_{k}\right)=\frac{1}{n-1} \sum_{i=1}^{n}\left(x_{m i}-\bar{x}_{m}\right)\left(x_{k i}-\bar{x}_{k}\right)
		  $$
	- 因此, 协方差矩阵, covariance matrix 等于
		- $$
		  \Sigma=\left[\begin{array}{ccc}
		  \sigma\left(x_{1}, x_{1}\right) & \cdots & \sigma\left(x_{1}, x_{d}\right) \\
		  \vdots & \ddots & \vdots \\
		  \sigma\left(x_{d}, x_{1}\right) & \cdots & \sigma\left(x_{d}, x_{d}\right)
		  \end{array}\right] \in \mathbb{R}^{d \times d}
		  $$
		- 其中对角线上的元素为各个随机变量的方差, 非对角线上的元素为各个随机变量之间的协方差, 并且矩阵$\sum$为正方形的对称矩阵 (symmetric matrix) 大小为$d \times d$, 所以可以计算 [[Eigenvalue]]
- Note
	- **协方差矩阵的最大特征值对应的特征向量, 总是指向方差最大的方向. (PC1)**
	- **第二大特征值对应的特征向量, 正交于最大特征值对应的特征向量, 并指向第二大方差指向的方向 (PC2)**