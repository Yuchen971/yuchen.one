alias:: 方差

- Definition
	- 方差是用来度量单个随机变量的离散程度
- Formula
	- id:: 61ff7250-466f-4906-a517-51029dea4ef8
	  $$
	  \sigma_{x}^{2}=\frac{1}{n-1} \sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)^{2}
	  $$
		- $n$表示样本量，$\bar{x}$表示观测样本的均值
	- $$
	  \operatorname{Var}[X]=E\left[(X-E[X])^{2}\right]=E\left[X^{2}\right]-E[X]^{2}
	  $$
	- $$
	  \operatorname{Var}[f(x)]=E\left[(f(x)-E[f(x)])^{2}\right]
	  $$