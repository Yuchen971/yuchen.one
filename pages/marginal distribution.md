alias:: 边缘分布

- Definition
	- the distribution of each predictor on its own
	- 假设有一个和两个变量相关的概率分布
	  $$P(x, y)$$
	  关于其中一个特定变量的边缘分布则为给定其他变量的 [[条件概率]]分布
	  $$
	  P(x)=\sum_{y} P(x, y)=\sum_{y} P(x \mid y) P(y)
	  $$
	  这也称为边际化 (marginalization)
	- 我们得到只关于一个变量的概率分布, 而不再考虑另一变量的影响, 实际上进行了降维操作
	- 例如 [[neural network]] 的神经元互相关联, 在计算它们各自的参数的时候, 就会使用边缘分布计算得到某一特定神经元(变量)的值
-