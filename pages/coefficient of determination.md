alias:: R2, R^2, r2, 决定系数, r-square

- # Definition
	- $R^2$ measures the proportion of variability in $Y$ that can be explained using $X$
	- R2公式
		- $$
		  R^{2}=\frac{\mathrm{TSS}-\mathrm{RSS}}{\mathrm{TSS}}=1-\frac{\mathrm{RSS}}{\mathrm{TSS}}
		  =1-\frac{\sum_{i=1}^{n}\left(y_{i}-\hat{y}_{i}\right)^{2}}{\sum_{i=1}^{n}\left(y_{i}-\bar{y}\right)^{2}}
		  $$
			- Where [[TSS]] is the total sum of squares
	- $R^2$ **is a measure of the linear relationship between** $X$ and $Y$, just like the [[correlation]] (r), 其实在 [[simple linear regression]], $R^2 = r^2$
- #+BEGIN_NOTE
  如果线性回归中增加特征, $$R^2$$ 也会增加 (non-decreasing property of R Square)
  #+END_NOTE
	- 线性回归的方程目标为
	- $$
	  \min S S E=\min \sum_{i=1}^{n}\left(e_{i}\right)^{2}=\min _{\beta} \sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\beta_{1} x_{i, 1}-\beta_{2} x_{i, 2}-\ldots-\beta_{p} x_{i, p}\right)^{2}
	  $$
	- 增加特征时, 目标方程变为
		- $$
		  \min S S E=\min _{\beta} \sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\beta_{1} x_{i, 1}-\beta_{2} x_{i, 2}-\ldots-\beta_{p} x_{i, p}-\beta_{p+1} x_{i, p+1}\right)^{2}
		  $$
	- 如果$\beta_{p+1}$为零，则[[ESS]]和 [[决定系数]] 的值保持不变。如果 $\beta_{p+1}$ 取非零的值，则[[ESS]]减小，此时 [[决定系数]] 的值增大
- # 缺点
	- when variable are added to the model, R2 cannot decrease, 模型中不断添加新的特征, 来提高拟合度 (不会降低), 即使这些特征不是线性相关的., 所以使用R2来对比两个具有不同特征数量的模型是不准确的., 需要使用 [[adjusted R2]]
	-
-