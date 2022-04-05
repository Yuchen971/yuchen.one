alias:: bootstrapping, 自助法
type:: non-parametric

- Definition
	- 是一类非参数的 [[Monte Carlo method]], 实质是对观测消息再抽样, 进而对总体的分布特性进行统计推断. (也就是从 unknownable world 进行从新抽样). 通过bootstrap, 可以得到模型参数的统计范围比如标准差, 标准差越小, 说明越接近真实值.
- Example
	- Qustion
		- 假设有两个金融资产X和Y, 现在想合理配置这两个资产, 使得其资产组合的风险最小, 也就是找到一个 $\alpha$ 使得 $Var(\alpha X + (1-\alpha)Y)$ 最小
		- 最优的$\alpha$表达式如下 (马尔可维茨, 投资组合理论)
			- $$
			  \alpha=\frac{\sigma_{Y}^{2}-\sigma_{X Y}}{\sigma_{X}^{2}+\sigma_{Y}^{2}-2 \sigma_{X Y}},
			  $$
				- where $\sigma_{X}^{2} = Var(X), \sigma_{Y}^{2} = Var(Y), \sigma_{XY} = Cov(X,Y)$
		- 现实生活中不知道 $\sigma_X^2$, $\sigma_Y^2$, $\sigma_{XY}$ 的值, 所以只能通过X和Y的一系列样本进行估计, 使用 plugin method
			- $$
			  \hat{\alpha}=\frac{\hat{\sigma}_{Y}^{2}-\hat{\sigma}_{X Y}}{\hat{\sigma}_{X}^{2}+\hat{\sigma}_{Y}^{2}-2 \hat{\sigma}_{X Y}}
			  $$
		- 现在的任务就是合理估计$\hat{\sigma}_{Y}^{2}$, $\hat{\sigma}_{X}^{2}$ and $\hat{\sigma}_{X Y}$, 传统方法考虑直接使用样本方差去估计真实值, 但是使用Bootstrap, 可以更好地去估计总体的分布特性, 不仅可以估计 $\sigma$, 也可以估计 $\sigma$ 的方差, 中位数等
	- Procedure
		- 在原有样本中通过重抽样(re-sample 有放回的抽取, 一个数据可以被重复抽取)抽取一定数量的新样本(比如100个)
			- 生成100个收益X和Y, 计算$\alpha$
		- 基于产生的新样本, 计算需要估计的统计量
			- 在这个例子中, 需要估计的统计量是 $\alpha$, 所以需要基于新样本计算样本方差, 协方差的值作为 $\hat{\sigma}_{Y}^{2}$, $\hat{\sigma}_{X}^{2}$ 和 $\hat{\sigma}_{X Y}$, 然后通过上面的公式计算 $\hat{\alpha}$
		- 重复上述步骤n次 (一般n>1000)
			- 这个例子, 可以得到1000个$\alpha_i$, 也就是 $\alpha_1,\alpha_2,...,\alpha_{1000}$
		- 最后计算被估计量的均值和方差, 也可以计算中位数等其他统计量
			- $$
			  \begin{gathered}
			  mean: \bar{\alpha}=\frac{1}{1,000} \sum_{r=1}^{1,000} \hat{\alpha}_{r}=0.5996 \\
			  variance: \sqrt{\frac{1}{1,000-1} \sum_{r=1}^{1,000}\left(\hat{\alpha}_{r}-\bar{\alpha}\right)^{2}}=0.083
			  \end{gathered}
			  $$
		- 图示
			- ![image.png](../assets/image_1648092557436_0.png){:height 357, :width 450}
				- 每个数据集得到一个estimate $\hat{\alpha}$, 也就是point estimate, 所有bootstrap得到的数据集可以的得到一个 vector point estimate 可以得到 $Var(\hat{\alpha})$, 之后可以做 hypothesis test 之类的