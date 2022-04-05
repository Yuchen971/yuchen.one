alias:: 岭回归

- Definition
	- 在 [[linear regression]] 中, 通过最小化如下函数对所有 $\beta$ 进行估计
		- $$
		  \mathrm{RSS}=\sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}
		  $$
		- 等价于
		  $$
		  \underset{\beta}{\operatorname{minimize}}\left\{\sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}\right\} \quad \text { subject to } \quad \sum_{j=1}^{p} \beta_{j}^{2} \leq s
		  $$
			- 和 [[lasso regression]] 一样, 对每一个 $\lambda$ 的值都有一些 $s$ 使得上两式得到相同的系数估计, 也就是在不超过 $s$ 的条件下, 尽可能寻找 [[RSS]] 最小的系数
	- ridge regression 通过最小化下式得到 $\hat{\beta}^R$
		- $$
		  \sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}+\lambda \sum_{j=1}^{p} \beta_{j}^{2}=\mathrm{RSS}+\lambda \sum_{j=1}^{p} \beta_{j}^{2} = R S S+\lambda\|\beta\|^{2}
		  $$
			- 其中 $\lambda$ >= 0 是一个调节参数, 其中 $\lambda \sum_{j=1}^{p} \beta_{j}^{2}$ 是惩罚项 (shrinkage penalty), 把接近0 的 $\beta_1,...,\beta_p$ 压缩到0, 当 $\lambda = 0$, 结果和 [[OLS]] 一致, 当 $\lambda$ -> inf, 岭回归的估计值越来越接近0, $\lambda\|\beta\|^{2}$ 为 [[范数/L2范数]]
- Properties
	- 由于岭回归中系数平方和的存在, 所以岭回归需要对数据进行 [[标准化]]
	- 岭回归的最终模型包含全部p个变量, [[范数/L2范数]] 可以将系数往0的方向缩减但是不会压缩至0, 所以当p很大的时候, 不便于模型解释. 所以是有 [[lasso regression]]