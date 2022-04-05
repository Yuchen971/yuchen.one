alias:: 逻辑回归
type:: classification

- Definition of logistic regression
	- 解决二分类问题的机器学习方法, 用于估计某种事物的可能性, 比如某广告被用户点击的可能性. 这里的可能性不是数学上的概率, 不可以用作概率值. 和 [[linear regression]] 一样都是广义的线性模型.
- Algorithm
	- 使用 [[logistic function]], 使对任意$X$值, 该函数的输出结果都在0,1之间, 如果使用线性回归没有意义, 所以构造如下函数, 得到S形的曲线
	  collapsed:: true
		- $$
		  p(X)=\frac{e^{\beta_{0}+\beta_{1} X}}{1+e^{\beta_{0}+\beta_{r} X}}
		  $$
	- 整理得到
	  collapsed:: true
		- $$
		  \frac{p(X)}{1-p(X)}=e^{\beta_{0}+\beta_{1} X}
		  $$
		- 其中, $p(X) /[1-p(X)]$ 为发生比 (odd), 取值范围为0 到正无穷
	- 两边取对数得到
	  collapsed:: true
		- $$
		  \log \left(\frac{p(X)}{1-p(X)}\right)=\beta_{0}+\beta_{1} X
		  $$
		- 左边称为对数发生比 (log odd) 或者分对数 (logit), 所以==logistic regression model has a logit that is linear in X==
	- 使用 [[极大似然估计]] 估计回归系数
	  collapsed:: true
		- [[似然函数]]形式如下
			- $$
			  \ell\left(\beta_{0}, \beta_{1}\right)=\prod_{i: y_{i}=1} p\left(x_{i}\right) \prod_{i^{\prime}: y_{i^{\prime}}=0}\left(1-p\left(x_{i^{\prime}}\right)\right)
			  $$
		- 寻找 $\beta_{0}, \beta_{1}$的一个估计, 使得 $\hat{p}(x_i)$ 最大可能的与观测结果接近, 换句话说, 求出的 $\hat{\beta_0}$, $\hat{\beta_1}$ 带入上式中, 使所有违约的人的值接近1, 为违约的人的值接近0
- Multiple logistic regression
  collapsed:: true
	- $$
	  \log \left(\frac{p(X)}{1-p(X)}\right)=\beta_{0}+\beta_{1} X_{1}+\cdots+\beta_{p} X_{p}
	  $$
	  整理得
	  $$
	  p(X)=\frac{e^{\beta_{0}+\beta_{1} X_{1}+\cdots+\beta_p X_{p}}}{1+\mathrm{e}^{\beta_{0}+\beta_{1} X_{2}+\cdots+\beta_p X_{p}}}
	  $$
- [[assumption]] of logistic regression
	- 线性相关假设: 对数概率比 ($Logit(p)$)和自变量之间存在线性关系
	- 随机抽样假设: 自变量 $X$ 的观测过程是随机的, 观测值之间互相独立
	- 共线性假设, 自变量 $X$ 之间无严格线性关系
	- 误差项期望值为0
	- 因变量y服从 [[bernoulli distribution]]
	- 对比 [[linear regression]]
		- $\hat{Y}$ 不服从正态分布, 服从 logistic  分布
		- Logistic回归模型对于稳健标准误不作要求，即不考虑模型误差项异方差问题
-