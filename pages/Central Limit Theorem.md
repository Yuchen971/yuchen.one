alias:: 中心极限定理, Central Limit Theorem, CLT

- # Definition
	- 给定一个任意分布的总体, 我每次从这些总体中随机抽取n个抽样, 一共抽m次, 然后把这m组抽样分别求出平均值, 这些平均值的分布接近正态分布
	- The sum of many random variables ($$X_1...X_n$$) is approximately a normal random variable
	- if $$(X_1, X_2, ... , X_n)$$ are independent from ^^any^^ distribution with mean $$\mu$$ and variance $$\sigma^2$$ and n is large
		- $$
		  \begin{aligned}
		  \sum_{i=1}^{n} X &=X_{1}+X_{2}+\ldots X_{n} \sim N\left[n \mu, n \sigma^{2}\right] \\
		  \bar{X} &=\frac{1}{n}\left[X_{1}+X_{2}+\ldots X_{n}\right] \sim N\left[\mu, \frac{\sigma^{2}}{n}\right]
		  \end{aligned}
		  $$
	- [[Z-score]]
	  id:: 61f6183e-5d7b-4951-a6f7-7e42fbd1af87
	- Example
		- 调查体重, 调查1000组, 每组50人, 求出每组体重的平均值, 呈正态分布
- # Properties
	- **总体本身的分布不要求正态分布**. 比如投色子(平均分布), 每组的平均值也会是正态分布
	- **样本每组要足够大**, 大于等于30个