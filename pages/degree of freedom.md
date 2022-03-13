alias:: 自由度, d.f., degrees of freedom

- Definition
	- number of free moving observation
- Explanation
	- Assume we have (u is the error term)
	  $$y_i = b_0 + b_1 x_i + u_i$$
		- for $y_i$ we have $i = 1,2,3,4,...,n$
		- for $x_i$ we have $i = 1,2,3,4,...,n$
	- For each observation we have $(x_1, y_1), (x_2, y_2), (x_3, y_3),(x_4, y_4) ..., (x_n, y_n)$, make the scatter plot
	- so we can use OLS to draw a regression line $\hat{y} = b_0 + b_1 x_i$, where the intercept is $b_0$, and the slope is $b_1$
	- Let's say we want to estimate $b_0$ and $b_1$, how many observations do you need to get the value to get them?
	- ==minimum observation to get them is 2==
	- if we have only 1 point, we can draw any line go through that point, if we have 2 points, we can get a line, we can get the $\hat{y}$
	- ==if we have 2 observations, this model's d.f. is 0==, because there is only one specific line R2 is 1
	- ==if we have 3 observations, this model's d.f. is 1==, the model gains a degree of freedom to pass through the points R2 变小
	- ==if we have 4 observations, this model's d.f. is 2== R2变小
	- ==if we have n observations, this model's d.f. is n-2==
	- So the degree of freedom is
	  $$d.f. = n-(k+1)$$
		- Where $k$ is the number of regressor $x_i$
	- 所以 [[r2]] 十分misleading是因为如果取得一个大的值, 可能只是 [[degree of freedom]] 太小了