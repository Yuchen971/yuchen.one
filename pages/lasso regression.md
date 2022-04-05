alias:: lasso 回归

- Definition
	- 求解下式 (在 [[OLS]] 的基础上添加 [[范数/L1范数]] )
	- $$
	  \sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}+\lambda \sum_{j=1}^{p}\left|\beta_{j}\right|=\operatorname{RSS}+\lambda \sum_{j=1}^{p}\left|\beta_{j}\right|
	  $$
		- 等价于
		  $$
		  \underset{\beta}{\operatorname{minimize}}\left\{\sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}\right\} \quad \text { subject to } \sum_{j=1}^{p}\left|\beta_{j}\right| \leq s
		  $$
			- 和 [[ridge regression]] 一样, 对每一个 $\lambda$ 的值都有一些 $s$ 使得上两式得到相同的系数估计, 也就是在不超过 $s$ 的条件下, 尽可能寻找 [[RSS]] 最小的系数
		- 调节参数足够大的时候可以将其中的某些系数的估计值强制设定为0的, 所以lasso也完成了 [[变量选择]], 模型跟易于解释.
- Properties
	- lasso模型会得到 [[稀疏模型]]
	  id:: 62465726-628a-4849-bb4d-da4fcec4c9b4
	- why lasso regression can make coefficient exactly equal to 0?
		- [[OLS]] 估计的系数记为 $\hat{\beta}$, 菱形和圆形分别代表lasso 和 ridge regression的限制条件区域, 如果 $s$ 足够大, 那么限制条件区域将包含 $\hat{\beta}$ (也就是$\lambda = 0$), lasso 和 ridge regression的系数估计会和 [[OLS]]一样
			- ![CleanShot_ISLRv2_website (page 252  612)_20220331@2x.png](../assets/CleanShot_ISLRv2_website_(page_252_612)_20220331@2x_1648778284418_0.png)
			- 以$\hat{\beta}$为中心的椭圆代表了一个RSS的数值, 给定一个椭圆边界上, 每个点代表的RSS是相等的, 随着椭圆与 $\hat{\beta}$ 越来越远, RSS逐渐增大. lasso 和 ridge regression的系数是估计是其条件区域和椭圆第一次相交点所决定的 因为 ridge regression的条件区域是圆形, 所以, ridge的回归系数估计不为0.