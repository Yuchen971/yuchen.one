alias:: generalized linear models, 广义线性模型, GLM
type:: statistical linear models

- Definition
  id:: 623913d1-b088-4365-b56f-7ba0b3e3ac5b
	- Each approach uses predictors $X_1, ..., X_p$ to predict response $Y$.
	  Each approach models the mean of $Y$ as a function of the predictors.
		- for [[linear regression]], assume $Y$ follows Gaussian distribution
			- $$
			  \mathrm{E}\left(Y \mid X_{1}, \ldots, X_{p}\right)=\beta_{0}+\beta_{1} X_{1}+\cdots+\beta_{p} X_{p}
			  $$
		- for [[logistic regression]], assume $Y$ follows Bernoulli distribution
			- $$
			  \begin{aligned}
			  \mathrm{E}\left(Y \mid X_{1}, \ldots, X_{p}\right) &=\operatorname{Pr}\left(Y=1 \mid X_{1}, \ldots, X_{p}\right) \\
			  &=\frac{e^{\beta_{0}+\beta_{1} X_{1}+\cdots+\beta_{p} X_{p}}}{1+e^{\beta_{0}+\beta_{1} X_{1}+\cdots+\beta_{p} X_{p}}}
			  \end{aligned}
			  $$
		- for [[poisson regression]], assume $Y$ follows Poisson distribution
			- $$
			  \mathrm{E}\left(Y \mid X_{1}, \ldots, X_{p}\right)=\lambda\left(X_{1}, \ldots, X_{p}\right)=e^{\beta_{0}+\beta_{1} X_{1}+\cdots+\beta_{p} X_{p}}
			  $$
	- all of them above can be expressed using a ==link function== $\eta$, which applies a transformation to $\mathrm{E}\left(Y \mid X_{1}, \ldots, X_{p}\right)$, that is
		- $$
		  \eta\left(\mathrm{E}\left(Y \mid X_{1}, \ldots, X_{p}\right)\right)=\beta_{0}+\beta_{1} X_{1}+\cdots+\beta_{p} X_{p}
		  $$
	- the ==link function== for linear regression is $\eta(\mu) = \mu$
	- the ==link function== for logistic regression is $\eta(\mu) = log(\mu/(1-\mu))$
	- the ==link function== for poisson regression is $\eta(\mu) = log(\mu)$
- Other GLM models
	- [[Binomial regression]]
	- [[Negative binomial regression]]
	- [[Multinomial regression]]