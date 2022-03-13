- # Basic model
	- Given a sample of n individuals, we observe data 
	  $$
	  \left(y_{1}, x_{1}\right),\left(y_{2}, x_{2}\right), \cdots,\left(y_{n}, x_{n}\right)
	  $$
	- Variables y and x are assumed to be related through
	  $$
	  \mathrm{E}\left(y_{i} \mid x_{i}\right)=\mu_{y \mid x}=\beta_{0}+\beta_{1} x_{i}
	  $$
	- or
	  $$
	  y_{i}=\beta_{0}+\beta_{1} x_{i}+\epsilon_{i}
	  $$
	- where the error $\epsilon_{i} \sim N\left(0, \sigma^{2}\right)$ and $\beta_0$=intercept, $\beta_1$=slope 所以可以推出 $y_i \sim N(\beta_0+\beta_1x_i, \sigma^2)$
		- 假设$\epsilon$为均值为0, 方差为$\sigma^2$的正态分布
	- 线性关系不是指y和x的关系, 而是$\beta_0$, $\beta_1$是一次的, 因为x可以通过变换得到