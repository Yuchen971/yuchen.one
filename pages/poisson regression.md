alias:: 泊松回归
type:: regression

- what is [[poisson distribution]]
- properties
	- typically used to model counts
	- 平稳性: 发生频率的大小只和单位大小有关系(比如1w为单位, 或者100w为单位时患癌症人数不同)
	- 独立性: 发生频率的大小, 各个数之间没有影响关系, 即频数数值彼此独立, 比如前一小时闯红灯的人多, 后一小时人数不会受影响
	- 普通性: 发生频率足够小, 即低概率性
- Procedure
	- 设定事件在单位时间发生 $k$ 次的概率为
		- $$
		  \operatorname{Pr}(Y=k)=\frac{e^{-\lambda} \lambda^{k}}{k !} \text { for } k=0,1,2, \ldots
		  $$
		- 其中 $\lambda = E(k)$ ==表示单位时间内事件发生次数的期望== (k为非负整数, 但是期望 $\lambda$ 可以为小数), 因为 $\lambda$ 是连续的, 所以可以直接考虑自变量和 $\lambda$ 之间的关系, 因为 $\lambda$ 是非负整数, 并且我们希望 mean number of users $\lambda = E(k)$ to vary as a function of the hour of the day, the month of the year..., so rather than modeling the number of users, Y as a poisson distribution with a fixed mean value, we would like to allow the mean to vary as a function of the covariates => $\lambda(X_1, ..., X_p)$
		- $$
		  \log \left(\lambda\left(X_{1}, \ldots, X_{p}\right)\right)=\beta_{0}+\beta_{1} X_{1}+\cdots+\beta_{p} X_{p}
		  $$
	- [[似然函数]]
		- $$
		  \ell\left(\beta_{0}, \beta_{1}, \ldots, \beta_{p}\right)=\prod_{i=1}^{n} \frac{e^{-\lambda\left(x_{i}\right)} \lambda\left(x_{i}\right)^{y_{i}}}{y_{i} !}
		  $$
			- where $\lambda\left(x_{i}\right)=e^{\beta_{0}+\beta_{1} x_{i 1}+\cdots+\beta_{p} x_{i p}}$
		- 求极值可以得到参数估计值
		  id:: 62391f83-0b06-4eb8-bffa-b247c1a6607f
- difference between [[linear regression]] and poisson regression (ISLRv2,P160)
	- in poisson regression
		- we implicitly assume that mean bike usage in a given hour equals the variance of bike usage during that hour
	- in linear regression
		- the variance of bike usage always takes on a constant value