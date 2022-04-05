alias:: mlr, 多元线性回归, 多元回归
type:: regression

- Definition
	- 代数表达
		- 基本格式
			- $$
			  y=\beta_{0}+\beta_{1} x_{1}+\beta_{2} x_{2}+\cdots+\beta_{p} x_{p}+\varepsilon \quad \varepsilon \sim N\left(0, \sigma^{2}\right)
			  $$
		- 样本表达
			- $$
			  \begin{gathered}
			  y_{i}=\beta_{0}+\beta_{1} x_{i 1}+\beta_{2} x_{i 2}+\cdots+\beta_{p} x_{i p}+\varepsilon_{i} \\
			  \varepsilon_{1}, \varepsilon_{2}, \cdots, \varepsilon_{n} i . i . d . N\left(0, \sigma^{2}\right)
			  \end{gathered}
			  $$
	- 矩阵表达
		- $$\hat{y} = w_1x_1 + ... + w_dx_d + b$$
			- b is the bias, or offset, or intercept
		- 将所有特征放入向量 $\mathbf{x} \in \mathbb{R}^d$ 中, 权重放入 向量 $\mathbf{w} \in \mathbb{R}^d$ 中
		- $$\hat{y} = \mathbf{w}^{\top} \mathbf{x} + b$$
		- 对于集合 $\mathbf{X}$ 预测值 $\hat{\mathbf{y}} \in \mathbb{R}^n$ 可以通过矩阵向量乘法表示
		- $$\hat{\mathbf{y}} = \mathbf{Xw}+b$$
	- [[loss function]] for [[mlr]]
		- $$
		  l^{(i)}(\mathbf{w}, b)=\frac{1}{2}\left(\hat{y}^{(i)}-y^{(i)}\right)^{2}
		  $$
			- 1/2 不会带来本质区别, 只是好求导
		- 由于二次方项, 估计值和观测值较大的差异会导致更大的损失, 为了度量模型在整个数据集的质量, 需要计算出在训练集n个样本上的损失均值(也等价于求和)
			- $$
			  L(\mathbf{w}, b)=\frac{1}{n} \sum_{i=1}^{n} l^{(i)}(\mathbf{w}, b)=\frac{1}{n} \sum_{i=1}^{n} \frac{1}{2}\left(\mathbf{w}^{\top} \mathbf{x}^{(i)}+b-y^{(i)}\right)^{2}
			  $$
		- 训练模型时, 希望找到一组参数 $(\mathbf{w^*}, b^*)$, 最小化所有训练样本上的总loss
			- $$
			  \mathbf{w}^{*}, b^{*}=\underset{\mathbf{w}, b}{\operatorname{argmin}}  L(\mathbf{w}, b) .
			  $$
		- 在噪声是 [[normal distribution]] 的假设下, [[RSS]] ([[OLS]])等价于对线性模型的 [[极大似然估计]]
- [[假设性检验]] (确定回归是否显著)
  collapsed:: true
	- $$
	  H_{0}: \beta_{1}=\beta_{2}=\cdots=\beta_{p}=0\\
	  H_{a} \text { : at least one } \beta_{j} \text { is non-zero. }
	  $$
	- [[hypothesis test]] is performed by computing the [[F-statistic]] (越大越好)
		- $$
		  F=\frac{(\mathrm{TSS}-\mathrm{RSS}) / p}{\mathrm{RSS} /(n-p-1)}
		  $$
			- $p$ is the number of variables (penalty)
			  where ((620076fd-f6bc-4ce1-b2f5-e2021b6da3e9)) (variability in y), 
			  and ((62048e84-073b-4035-99fc-a8a7667c36a4))
		- if the linear model assumptions are correct, show that
			- $$
			  E\{\mathrm{RSS} /(n-p-1)\}=\sigma^{2}
			  $$
		- if $H_0$ is true, 也就是x,y之间没有联系
			- $$
			  E\{(\mathrm{TSS}-\mathrm{RSS}) / p\}=\sigma^{2}
			  $$
		- 如果 $H_\alpha$ 是 True, 那么 $F$ expected to be greater than 1
		- 如果$F$很大
			- The large F-statistic suggests that at least one of y must be related to x.
		- 如果$F$ close to 1
			- the answer depends on the values of n and p. When n is large, an F-statistic that is just a little larger than 1 might still provide evidence against $H_0$
		- 当n很小的时候, F-statistic需要很大来reject $H_0$
- 逐步回归 (确定预测变量是否针对结果变量起到了预测作用)
  collapsed:: true
	- 以 [[AIC]] 为准则, 选择最小的 [[AIC]] 信息统计量来达到删除或者增加变量的目的
	- **Forward selection**
		- 1. Select a significance level to enter the model (e.g. SL = 0.05)
		  2. Fit all simple regression models $y \sim x_n$ Select the one with the lowest p-value
		  3. Keep this variable and fit all possible models with one extra predictor added to the one(s) you already have
		  4. Consider the predictor with the _lowest_ p-value, if p < SL, go to step 3, otherwise finish.
	- **Backward selection**
		- 1. Select a significance level to stay in the model (e.g. SL = 0.05)
		  2. Fit the full model with all possible predictors
		  3. Consider the predictor with the highest p-value, if p > SL, go to step 4, otherwise finish
		  4. Remove the predictor
		  5. Fit the model without this variable, and jump to step 3
	- **Mixed selection (Stepwise selection)**
		- 1. Select a significance level to enter and to stay in the model (e.g. SL-enter = 0.05, SL-stay = 0.05)
		  2. Perform the next step of forward selection (new variables must have p < SL-enter to enter)
		  3. Perform all steps of backward selection (old variables must have p < SL-stay to stay), and go to step 2.
		  4. No new variable can enter and no old variables can exit, finish
- Note
  collapsed:: true
	- [[RSS]] for multiple linear regression
	- 根据 [[RSE]] 公式, 伴随自变量n个数增加影响超过RSS减少的影响, RSE会增大