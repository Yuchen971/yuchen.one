alias:: 简单线性回归, LR
type:: regression

- # Definition
	- It assumes that there is approximately a linear relationship between X and Y
	- also called regressing $Y$ on $X$
	- $$
	  Y \approx \beta_{0}+\beta_{1} X
	  $$
- ## Estimating the Coefficients
	- residual $$e$$ 
	  background-color:: #793e3e
	  id:: 61f23283-68fc-40a3-8eb3-164243a4e48f
		- the difference between the ith observed response value and the ith response value that is predicted.
	- [[residual sum of square]] (RSS)
	  background-color:: #793e3e
		- {{embed ((61f23283-4ccc-4166-b211-3e429f6f0db9))}}
- ## Accessing the Accuracy of the Coefficient Estimates
	- how accurate is the sample mean $$\hat{\mu}$$ as a estimate of $$\mu$$ ? (当数据集很多的时候, $$\hat{\mu}$$ 会无线趋近$$\mu$$, 也就是真实的$$\mu$$) (样本的mean和population mean(数据真实平均数)
	- **standard error of** $${\mu}$$
	  background-color:: #793e3e
		- $$
		  \operatorname{Var}(\hat{\mu})=\operatorname{SE}(\hat{\mu})^{2}=\frac{\sigma^{2}}{n}
		  $$
			- where $$\sigma$$ is the standard deviation of each of the realization $$y_i$$ of $$Y^2$$ (This formula holds provided that the n observations are **uncorrelated**.)
			- the standard error tells us the average amount that this estimate $$\hat{\mu}$$ differs from the actual value of $${\mu}$$ 偏差的均值
	- **standard error of** $$\hat{\beta}_0$$ and $$\hat{\beta}_{1}$$
	  background-color:: #793e3e
		- $$
		  \mathrm{SE}\left(\hat{\beta}_{0}\right)^{2}=\sigma^{2}\left[\frac{1}{n}+\frac{\bar{x}^{2}}{\sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)^{2}}\right]
		  $$
		- $$
		  \operatorname{SE}\left(\hat{\beta}_{1}\right)^{2}=\frac{\sigma^{2}}{\sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)^{2}},
		  $$
		- where $$\sigma^{2}=\operatorname{Var}(\epsilon)$$, assume that the errors $$\epsilon_i$$ for each observation have common variance $$\sigma^{2}$$ and are **uncorrelated**
	- **residual standard error [[RSE]]**
	  background-color:: #793e3e
		- {{embed ((620076fe-6edf-42aa-beb2-5cc7dcc13f00))}}
	- standard errors can compute [[confidence interval]]
	  background-color:: #793e3e
		- a 95% [[confidence interval]] for $$\hat{\beta}_{1}$$ approximately takes the form
			- $$
			  \left[\hat{\beta}_{1}-2 \cdot \operatorname{SE}\left(\hat{\beta}_{1}\right), \hat{\beta}_{1}+2 \cdot \operatorname{SE}\left(\hat{\beta}_{1}\right)\right]
			  $$
	- standard errors 可以做[假设性检验]([[hypothesis testing]])
	  background-color:: #793e3e
		- $H_0$: there is no relationship between $X$ and $Y$
		- $H_A$: there is some relationship between $$X$$ and $$Y$$
		- 等于 
		  $$\begin{aligned}
		  &H_{0}: \beta_{1}=0 \\
		  &H_{A}: \beta_{1} \neq 0
		  \end{aligned}$$
		- 如果 $$\beta_{1}=0$$ 那么X, Y之间没有相关性, 为了测试the null hypothesis, 需要确认对 $$\beta_{1}$$ 的估计 $$\hat{\beta_{1}}$$是否离0足够远. But how far is far enough? 取决于 $$\hat{\beta_{1}}$$ 的精度, 也就是依赖于$$SE(\hat{\beta_{1}})$$, 如果其足够小, 那么$$\hat{\beta_{1}}$$ 相对于 $$SE(\hat{\beta_{1}})$$ 足够大, 那么既是相对较小的$$\hat{\beta_{1}}$$ 也能证明 $$\beta_1 \neq 0$$. t-statistic 公式如下
		- $$
		  t=\frac{\hat{\beta}_{1}-0}{S E\left(\hat{\beta}_{1}\right)}
		  $$
		- 若有一个较小的 [[p-value]] ，则我们可以推断predictor和response之间有一定的相关性，即拒绝原假设。p值越小，其相关性越显著。
- ## Accessing the Accuracy of the Model
	- [[residual standard error]] (RSE) 很少用, 和 [[coefficient of determination]]差不多
	- [[coefficient of determination]] ($$R^2$$)
-