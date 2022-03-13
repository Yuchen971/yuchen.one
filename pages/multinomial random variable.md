alias:: 多项式随机变量, multinomial random vector, Multinomial Random Variable, Multinomial Random Vector
title:: multinomial random variable

- # Definition
	- multinomial random variable is the generalization of [[binomial random variable]], **it applies when the trials can result in k outcomes**
	- [[probability distribution function]] of multinomial random variable
		- consider independent trials that can result in one of __k__ possible outcomes with probabilities $$p_1, p_2,...,p_k$$, Let
		  $X_1$: number of observed outcomes type 1
		  $X_k$: number of observed outcomes type k
		- $$
		  \begin{aligned}
		  P\left[X_{1}=x_{1}, \ldots, X_{k}
		  =x_{k}\right] &=\frac{n !}{x_{1} ! \ldots x_{k} !} p_{1}^{x_{1}} \ldots p_{k}^{x_{k}} \quad x_{i}=0, \ldots, n \\
		  E\left[X_{i}\right] &=n p_{i} \\
		  \operatorname{Var}\left[X_{i}\right] &=n p_{i}\left(1-p_{i}\right) \quad i=1, \ldots, k
		  \end{aligned}
		  $$
- # Example
	- the probability of a light bulb last less than 500 hours is 0.5 and the probability the same type of light bulb lasts more than 800 hours is 0.2. In a random selection of ten light bulbs, what is the probability of obtaining four bulbs that last less than 500 hours and two that more than 800 hours? (**Infer: The probability that it lasts between 500 and 800 hours is 0.3.**)
		- X1: n. of light bulbs that last less than 500 hours ($$p_1$$ = 0.5) 
		  X2: n. of light bulbs that last between 500 and 800 hours 
		  X3: n. of light bulbs that last more than 800 hours ($$p_3$$= 0.2) 
		  For n=10, find
		- $$
		  \begin{aligned}
		  \mathbb{P}\left(X_{1}=4, X_{2}=4, X_{3}=2\right) &=\frac{10 !}{4 ! 4 ! 2 !}(0.5)^{4}(0.3)^{4}(0.2)^{2} \\
		  &=0.0638
		  \end{aligned}
		  $$
		- ```r
		  # 其中p, x均为向量，分别代表各试验结果的概率和发生次数，
		  # 即p=c(p1, p2, ..., pk), x=c(x1, x2, ..., xk)
		  multi <- function(p, x) {
		    n <- sum(x)   ##试验次数
		    f1 <- prod(p^x)
		    f2 <- prod(factorial(x))
		    factorial(n)*f1/f2      ##返回值
		  }
		  p <- c(0.5, 0.2, 0.3)
		  x <- c(4, 2, 4)
		  multi(p, x)
		  > 0.0637875
		  
		  # 或者
		  x = c(4,4,2)
		  p = c(0.5,0.3,0.2)
		  n = 10
		  dmultinom(x,n,p)
		  > 0.0637875
		  ```