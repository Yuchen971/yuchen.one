alias:: 协方差, cov

- Definition
	- 两个变量的过程中是同方向还是反方向变化, 程度如何
	- 如果有X,Y两个变量，每个时刻的“X值与其均值之差”乘以“Y值与其均值之差”得到一个乘积，再对这每时刻的乘积求和并求出均值 (期望)
- Formula
	- formula 1
		- $$
		  \operatorname{Cov}(X, Y)=E\left[\left(X-\mu_{x}\right)\left(Y-\mu_{y}\right)\right] = \sigma_{x y}
		  $$
		- $$
		  -\infty<\sigma_{x y}<\infty
		  $$
	- formula 2
		- id:: 61ff739f-eba9-4dcc-ab66-f2ed2f76fed7
		  $$
		  \sigma(x, y)=\frac{1}{n-1} \sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)\left(y_{i}-\bar{y}\right)
		  $$
- Note
	- 方差是用来度量单个变量 '自身变异' 大小的总体参数, 方差越大表明该变量的变异越大
	- 协方差是用来度量两个变量之间 "协同变异" 大小的总体参数, 即二个变量相互影响大小的参数, 协方差的绝对值越大, 则二个变量相互影响越大
	- 协方差矩阵能处理多维问题
	- 协方差矩阵是一个对称的矩阵, 而且对角线是各个维度上的方差.
	- 协方差矩阵计算的是不同维度之间的协方差, 而不是不同样本之间的.
	- 样本矩阵中若每行是一个样本, 则每列为一个维度, 所以计算协方差时要按列计算均值.