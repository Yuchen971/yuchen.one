alias:: 线性判别分析, LDA, gaussian maximum likelihood classification, LDA分类器
type:: supervised, classification
related:: [[PCA]], [[quadratic discriminant analysis]]

- What is the difference between [[logistic regression]] and LDA?
  collapsed:: true
	- In [[logistic regression]] , we model $P(Y= class_k|X = data_x)$ (the probability of each class, given a data point), 也就是给定预测变量X下, 建立响应变量Y的条件分布模型
	- In LDA, we model $P(X = data_x| Y = class_k)$ . 也就是分别对每种响应分类 (给定的Y) 建立预测变量X的分布模型, 然后运用 [[bayes theorem]] 反过来估计 
	  $P(Y= class_k|X = data_x)$
- **Why use LDA rather than [[logistic regression]]?**
  collapsed:: true
	- 类别区分度高的时候, [[logistic regression]] 的参数估计不够稳定, 这点在 [[LDA]] 中不存在
	- 如果样本量n比较小, 而且在每一类响应分类中预测变量 X 近似服从正态分布, 那么LDA比logistic regression模型更稳定
	- 响应分类Y多于两类的时候, LDA更普遍
- How to use [[bayes theorem]] in LDA to get the $P(class|X)$? (bayes theorem for classification)
  collapsed:: true
	- $$
	  P(\text {class}=k \mid \mathbf{x})=\frac{P(\mathbf{x} \mid \text {class}=k) P(\text {class}=k) }{\sum_{i} P(\mathbf{x} \mid \text {class}=i) P(\text {class}=i)} = \frac{\pi_kf_k(x)}{\sum^k_{l=1} \pi_l f_l(x)}
	  $$
		- where bottom is the normalization factor, sums over all possible classes
	- denominator is not important if we want to choose the class, because there are always the same, so we ignore the denominator and give following equation
	- id:: 621dc4f6-7ca7-48fc-9f21-593ac515217a
	  $$
	  P(Y=k \mid \mathbf{x} = x) = \frac{f_{k}(\mathbf{x}) \pi_{k}}{\sum_{l=1}^k \pi_l f_l(x)}
	  $$
	- $$
	  P(\text {class}=k \mid \mathbf{x}) \sim f_{k}(\mathbf{x}) \pi_{k}
	  $$
		- $\pi_k$: [[先验概率]] (上式中的$P(class=k)$), $f_k(x)$ is the [[Probability Distribution Function]], (上式中的$P(x|class=k)$), $f_k(x)$的估计要复杂一些, 除非假设他们的[[密度函数]] 形式
		- Note that $f_k$ 对每个class k 都不一样
- Linear discriminant analysis when $p = 1$, 只有一个预测变量
  collapsed:: true
	- 首先获取 $f_k(x)$ 密度函数, 从而估计 $p_k(x)$, 根据 $p_k(x)$, 将观测点分到值最大的一类中
	- 假设 $f_k(x)$ 是normal distribution, 密度函数为
		- $$
		  f(x)=\frac{1}{\sigma_k \sqrt{2 \pi}} e^{-\frac{1}{2}\left(\frac{x-\mu_k}{\sigma_k}\right)^{2}}
		  $$
			- 其中 $\mu_k$, $\sigma_k$是第$k$ 类的平均值和方差, 再假设 $\sigma_1^2 = ... = \sigma_k^2$, 即所有$K$ 个类的方差是相同
		- 带入
		  $$
		  P_k(x) = P(Y=k \mid \mathbf{x} = x) = \frac{f_{k}(\mathbf{x}) \pi_{k}}{\sum_{l=1}^k \pi_l f_l(x)}
		  $$
		- 取对数得到判别函数 (discriminant function) [[decision boundary]] for LDA
		  $$
		  \delta_{k}(x)=x \cdot \frac{\mu_{k}}{\sigma^{2}}-\frac{\mu_{k}^{2}}{2 \sigma^{2}}+\log \pi_{k}
		  $$
		  叫线性判别函数是因为该函数为x的线性函数
		- [[bayes decision boundary]] in this case is
			- $$
			  x=\frac{\mu_{1}^{2}-\mu_{2}^{2}}{2\left(\mu_{1}-\mu_{2}\right)}=\frac{\mu_{1}+\mu_{2}}{2}
			  $$
		- ==Procedure==
			- calculate $\delta_k$ for each k
			- Find the largest $\delta_k$ and assign observation to that group
	- example
		- 该例中实现知道每一类$X$ 都符合高斯分布, 且分布中参数都已知, 因此能直接计算贝叶斯分类器, 但是实际情况中不能, 就算确定每一类$X$都服从正态分布, 仍然需要估计参数 $\mu$ $\pi$ $\sigma^2$
			- 估计参数用$\hat{\mu}$估计$\mu$, 用$\hat{\sigma}$估计$\sigma$ (plug-in estimate), 放入判别函数中
			- $$
			  \begin{aligned}
			  \hat{\mu}_{k} &=\frac{1}{n_{k}} \sum_{i: y_{i}=k} x_{i} \\
			  \hat{\sigma}^{2} &=\frac{1}{n-K} \sum_{k=1}^{K} \sum_{i: y_{i}=k}\left(x_{i}-\hat{\mu}_{k}\right)^{2} \\
			  \hat{\pi}_{k} &= n_k / n
			  \end{aligned}
			  $$
			- 得到
			  $$
			  \hat{\delta}_{k}(x)=x \cdot \frac{\hat{\mu}_{k}}{\hat{\sigma}^{2}}-\frac{\hat{\mu}_{k}^{2}}{2 \hat{\sigma}^{2}}+\log \left(\hat{\pi}_{k}\right)
			  $$
		- 左图:k = 2, $\pi_1 = \pi_2 = 0.5$, 右图: k = 2, $\pi_1 = 0.3$ , $\pi_2 = 0.7$
		- ![Screen Shot 2022-03-01 at 4.15.50 PM.png](../assets/Screen_Shot_2022-03-01_at_4.15.50_PM_1646180162354_0.png)
			- 绿色的线和红色的线都是 [[probability density function]] , 中间
			  中间的虚线是 [[decision boundary]], x轴为 $x$
			  如果 class1 $\pi_1$ 的 [[先验概率]] 和 class2 $\pi_2$ 都为0.5, 那么决策边界就在中间, 决策边界左边的classify as blue, 右边的classify as purple
		- ![Screen Shot 2022-03-01 at 6.08.43 PM.png](../assets/Screen_Shot_2022-03-01_at_6.08.43_PM_1646186932046_0.png)
			- 左: 两个一维的正态密度函数, 坚直的虚钱代表贝叶斯决策边界. 
			  右: 分别来自两类 20 个观测的直方图
			  竖直的虚线为贝叶斯决策边界 [[decision boundary]] 
			  竖直的实线为且训练数据得到的 LDA决策估计边界, 说明分类效果相当不错
- [[assumption]] of Linear discriminant analysis
  collapsed:: true
	- 每一类的观测都来自于一个均值不同, [[Covariance Matrix]] 相同 ($\Sigma$)的正态分布假设上的, 将这些参数带入 [[贝叶斯分类器]]中得到 LDA分类器,
	- By making these strong assumptions, replace challenging problem of estimating $K$ dimensional [[probability density function]], [[QDA]] 也是一样
	- [[QDA]] 需要 assume $K(p*p)$ dimensional [[Covariance Matrix]]
	  [[LDA]] 需要 assume $(p*p)$ dimensional [[Covariance Matrix]]
- Linear discriminant analysis when $p>1$ 多个预测变量
  collapsed:: true
	- 假设 Density function $f_k(x)$ 为多元正态分布
		- $$
		  f(x)=\frac{1}{(2 \pi)^{p / 2}|\boldsymbol{\Sigma}| 1 / 2} e^{-\frac{1}{2}(x-\mu)^{T} \boldsymbol{\Sigma}^{-1}(x-\mu)}
		  $$
	- 使用 [[贝叶斯定理]] 取对数得到判别函数 (discriminant function) (也是linear function)
		- $$
		  \delta_{k}(x)=x^{T} \boldsymbol{\Sigma}^{-1} \mu_{k}-\frac{1}{2} \mu_{k}^{T} \boldsymbol{\Sigma}^{-1} \mu_{k}+\log \pi_{k}
		  $$
	- example
		- The dashed lines is the [[bayes decision boundary]], which would yield the ==fewest== misclassification errors among all possible classifiers
		- ![Screen Shot 2022-03-01 at 6.45.19 PM.png](../assets/Screen_Shot_2022-03-01_at_6.45.19_PM_1646189132518_0.png)
			- p = 2, K = 3, $\pi_1 = \pi_2 = \pi_3 = 1/3$, 每一类的观测服从一个均值不同, [[协方差矩阵]] 相同的多元高斯分布
			  左图: Ellipses that contain 95 % of the probability for each of the three classes are shown, 虚线是 [[bayes decision boundary]]
			  右图: 黑色实线表示LDA决策边界, 错误率很低, 说明LDA 准确率很高
	-
- What is [[sensitivity]] and [[specificity]] (class-specific preformance)
  collapsed:: true
	- Confusion matrix
		- ![Screen Shot 2022-03-01 at 8.05.21 PM.png](../assets/Screen_Shot_2022-03-01_at_8.05.21_PM_1646193923624_0.png)
		- LDA预测了104个人会发生违约, 但是事实上只有81人违约, 23人并没有违约, 信用卡公司的目标是辨别出高风险人群, 但是违约人群 252/333 = 75.7% 的错误率太高了
		- sensitivity = 81/(81+252) = 24.3%, specificity = 9644/(9644+23) = 99.8%
	- 为什么 LDA的[[sensitivity]] 那么低?
		- 因为LDA和所有分类器中错误率最低的贝叶斯分类器 (前提是高斯分布假设) 很相似, 也就是说贝叶斯分类是在不考虑错误来源时, 产生的被错误分类的观测数是最少的.
		- 如何改进?
		  collapsed:: true
			- [[贝叶斯分类器]] 的原理是将观测分入后验概率 $p_k(x)$ 最大的一类中, 在两类情况中, 如果 $Pr(default = Yes | X = x)>0.5$ 那么就将观测分入违约的一组, 这里采用的是 50% 作为后验违规概率的阈值, 
			  如果现在关心的是错误的将违约者判为未违约的概率, 可以考虑降低阈值, 比如可以将后验违约概率在 20%以上的人纳入违约的一组, 也就是说 
			  $Pr(default = Yes | X = x)>0.2$
			- 改进之后的 confusion matrix
				- ![Screen Shot 2022-03-01 at 8.24.20 PM.png](../assets/Screen_Shot_2022-03-01_at_8.24.20_PM_1646195062509_0.png)
				- 此时sensitivity = 195/(138+195) = 58.6%, specificity = 9432/(9432+235) = 97.6%
				- sensitivity 有所增长, 但是代价是 235个人错误分类, 总的错误率增涨了3.73%
		- Threshold VS Error Rate
		  collapsed:: true
			- ![Screen Shot 2022-03-01 at 8.28.49 PM.png](../assets/Screen_Shot_2022-03-01_at_8.28.49_PM_1646195331228_0.png)
			- 黑色实线: 总的错误率, 蓝色虚线: 违约者被错误分类的比例, 橙色的点: 没有违约者被错误分类的比例
			- 因为 [[贝叶斯分类器]]所用的阈值为0.5, 所以错误率最低, 但是阈值为0.5时, 违约者的错误率是最高的
- What is [[ROC]] ?
- What is the difference between [[PCA]] and Linear discriminant analyais
  collapsed:: true
	- LDA是一种监督学习的降维技术, PCA focuses with the variance, The LDA is like PCA, but focuses on maximizing the seperatibility among known categories
	- Both rank the new axes in order of importance
		- PC1 (the first new axis that PCA creates) accounts for the most variation ==in the data==.
		  collapsed:: true
			- PC2 (the second new axis) does the second best job...
		- LD1 (the first new axis that LDA creates) accounts for the most variation ==between the categories==.
			- LD2 (the second new axis) does the second best job...
			- ![Screen Shot 2022-02-28 at 10.01.21 PM.png](../assets/Screen_Shot_2022-02-28_at_10.01.21_PM_1646114483648_0.png)
- Example of reducing 2-d graph to 1-d graph with LDA
  collapsed:: true
	- projects the data onto this new axis in a way to maximize the separation of the two categories
	  collapsed:: true
		- ![Screen Shot 2022-02-28 at 9.30.31 PM.png](../assets/Screen_Shot_2022-02-28_at_9.30.31_PM_1646112633584_0.png)
		- ![Screen Shot 2022-02-28 at 9.37.24 PM.png](../assets/Screen_Shot_2022-02-28_at_9.37.24_PM_1646113048550_0.png){:height 411, :width 621}
		-
	- collapsed:: true
	  1. ==maximize the distance between means==. 2. ==Minimize the variation== (LDA calls 'scatter' and is represented by $s^2$) within each category
	  collapsed:: true
		- $$
		  \frac{(\mu-\mu)^{2}}{s^{2}+s^{2}}
		  $$
		- ![Screen Shot 2022-02-28 at 9.45.00 PM.png](../assets/Screen_Shot_2022-02-28_at_9.45.00_PM_1646113502833_0.png)
		- ![Screen Shot 2022-02-28 at 9.55.49 PM.png](../assets/Screen_Shot_2022-02-28_at_9.55.49_PM_1646114157068_0.png)
- What is [[quadratic discriminant analysis]] ?
  collapsed:: true
	- [[assumption]]
		- QDA 也是假设每一类观测都服从一个高斯分布, 但是每一类观测都有自己的 [[协方差矩阵]] 和mean $\mu_k$
		  也即是说它假设来自第K类的观测形如
		  $$
		  X \sim N\left(\mu_{k}, \boldsymbol{\Sigma}_{k}\right)
		  $$
		  where the $\boldsymbol{\Sigma}_{k}$ is the covariance matrix for the $k_{th}$ class
		- estimate p-dimensional [[density function]] is challenging, because it must consider not only the [[marginal distribution]] of each predictor, but also the [[joint distribution]]
		  id:: 6222b6df-c624-4af6-9f51-311744997893
	- QDA 判别函数 (discriminant function) (关于x的二次函数)
	  collapsed:: true
		- $$
		  \begin{aligned}
		  \delta_{k}(x) &=-\frac{1}{2}\left(x-\mu_{k}\right)^{T} \boldsymbol{\Sigma}_{k}^{-1}\left(x-\mu_{k}\right)-\frac{1}{2} \log \left|\boldsymbol{\Sigma}_{k}\right|+\log \pi_{k} \\
		  &=-\frac{1}{2} x^{T} \boldsymbol{\Sigma}_{k}^{-1} x+x^{T} \boldsymbol{\Sigma}_{k}^{-1} \mu_{k}-\frac{1}{2} \mu_{k}^{T} \boldsymbol{\Sigma}_{k}^{-1} \mu_{k}-\frac{1}{2} \log \left|\boldsymbol{\Sigma}_{k}\right|+\log \pi_{k}
		  \end{aligned}
		  $$
	- QDA分类器把 $\Sigma_{k}, \mu_{k}, \pi_k$ 的估计 (hat) 带入 上式, 然后将观测 $X = x$ 分入使上式最大的一类里.
	- 对比 LDA 和 QDA
	  collapsed:: true
		- 左图中, 两个类 $X_1, X_2$ 有相同的相关系数 0.7, 并服从高斯分布, 因此 [[bayes decision boundary]] 是线性的, 并且被LDA的决策边界逼近, 而QDA次之, 因为其方差较大而偏差没有得到相应的减小
		- 右图中, 橙色部分是变量之间相关系数为0.7的类, 蓝色部分是变量之间的相关系数为-0.7的类, 此时的 [[bayes decision boundary]] 是二次的, QDA更接近
		- ![Screen Shot 2022-03-01 at 9.09.11 PM.png](../assets/Screen_Shot_2022-03-01_at_9.09.11_PM_1646197757081_0.png){:height 311, :width 627}
			- 左: $\Sigma_1 = \Sigma_2$ 时两类分类问题的贝叶斯 (紫色虚线) LDA (黑色点线), QDA (绿色实线) 的决策边界
			  右: $\Sigma_1 \neq \Sigma_2$
- When we use [[LDA]], when we use [[QDA]]?
  collapsed:: true
	- This is a [[bias-variance tradeoff]] problem
		- 当有p个预测变量的时候, [[Covariance Matrix]] 需要 $p(p+1)/2$个参数, 
		  QDA需要对每一类分别估计协方差, 需要 $Kp(p+1)/2$ 个参数 (K为class个数)
		  LDA 有 $Kp$ 个线性系数需要估计
		- LDA 没有 QDA 分类器光滑, 有更低的方差
		- 训练集大用QDA, 观测数据方差大用QDA
- What is [[naive bayes classifier]]