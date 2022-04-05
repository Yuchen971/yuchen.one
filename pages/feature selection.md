alias:: variable selection, 变量选择, 特征选择

- definition
	- 标准线性回归模型为
		- $$
		  Y=\beta_{0}+\beta_{1} X_{1}+\cdots+\beta_{p} X_{p}+\varepsilon
		  $$
	- 除了 [[OLS]], 还有几种拟合方法, 具有更好地预测准确率和模型解释力
- method
	- Subset selection
		- definition
			- 从p个预测变量中挑选出于响应变量相关的变量形成子集, 在对缩减的变量使用 [[OLS]]
		- example
			- stepwise selection (forward, backward, both)
	- Shrinkage
		- definition
			- 基于全部p个预测变量进行模型的拟合, 与 [[OLS]] 不同的是, 这个方法可以将估计系数往零的方向进行压缩, 通过系数缩减([[regularization]]) 减少方差. 通过选择不同的系数缩减方法, 某些回归系数可以缩减至0, 可以用于变量选择.
		- example
			- [[ridge regression]]
			- [[lasso regression]]
	- Dimension reduction
		- definition
			- 将p维预测变量投影至M维子空间中
		- example
			- [[PCA]]