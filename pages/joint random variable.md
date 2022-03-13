alias:: 联合分布随机变量, 多维分布随机变量, random vector, joint distribution

- Definition
	- the association between the different predictors
	- Variables defined on the same sample space, if $$X$$ and $$Y$$ are continuous random variables, then $$f(x,y)$$ is the joint probability density function for $$X$$ and $$Y$$
	- example
		- Verbal and quantitative GRE scores
		- Profit of a portfolio made of two stocks
	- **joint discrete random variables** (example)
		- [[Multinomial Random Variable]]
			- $$P[X_1 = x_1, X_2 = x_2]$$
			  $$
			  P\left[X_{1}=x_{1}, \ldots, X_{n}=x_{n}\right]
			  $$
	- **joint continuous random variables** (example)
		- [[multivariable normal]] random variable
			- $$
			  f\left(x_{1}, x_{2}\right) \quad f\left(x_{1}, \ldots, x_{n}\right)
			  $$
			- the association between the different predictors is summarized by the ==off-diagonal== elements of the [[Covariance Matrix]]
- Properties
	- $X$ and $Y$ are **independent random variables** if $$f(x,y)=f(x)*f(y)$$ for all possible values of x and y