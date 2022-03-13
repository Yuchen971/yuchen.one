alias:: RSE, 残差的标准误差, 残差标准差

- # Definition
	- RSE is an estimate of the standard deviation of $\epsilon$
	- For [[simple linear regression]]
		- id:: 620076fe-6edf-42aa-beb2-5cc7dcc13f00
		  $$
		  \mathrm{RSE}=\sqrt{\frac{1}{n-2} \mathrm{RSS}}=\sqrt{\frac{1}{n-2} \sum_{i=1}^{n}\left(y_{i}-\hat{y}_{i}\right)^{2}} .
		  $$
			- Where
			  $$
			  \mathrm{RSS}=\sum_{i=1}^{n}\left(y_{i}-\hat{y}_{i}\right)^{2}
			  $$
		- 如果$RSE=3.26$, 说明actual sales in each market平均偏离预测3260个单位
	- For [[multiple linear regression]]
		- $$RSE = \frac{RSS}{n-p-1}$$
		-