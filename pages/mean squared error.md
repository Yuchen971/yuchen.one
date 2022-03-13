alias:: MSE, 均方差

- # Definition
  id:: 61f0b3dd-13c9-4419-a4b6-dd5dbd2d3d4f
	- [[ESS]] (误差平方和) 也就是拟合数据和原始数据对应点的误差的平方和
		- ESS公式
			- $$
			  S S E=\sum_{i=1}^{n} w_{i}\left(y_{i}-\hat{y_{i}}\right)^{2}
			  $$
	- MSE 就是 SSE 除以n算出average
	- $$
	  \begin{aligned}
	  M S E_{T r} &=A v e_{i \in T r}\left[y_{i}-\hat{f}\left(x_{i}\right)\right]^{2} \\
	  M S E_{T e} &=A v e_{i \in T e}\left[y_{i}-\hat{f}\left(x_{i}\right)\right]^{2}
	  \end{aligned}
	  $$
	  $$
	  \operatorname{MSE}(\hat{\theta})=\operatorname{Var}(\hat{\theta})+(\operatorname{Bias}(\hat{\theta}, \theta))^{2}
	  $$
	- Where $$\hat{f}(x_i)$$ is the prediction that $$\hat{f}$$ gives for the ith observation
	- training MSE and testing MSE