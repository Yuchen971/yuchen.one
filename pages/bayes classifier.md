alias:: 朴素贝叶斯分类器, naive bayes classifier

- 原理
	- 对于给出的待分类项, 求解在此项出现的条件下各个类别出现的概率, 哪个最大, 就认为此待分类项属于哪个类别.
- [[assumption]]
	- ==conditional independence==
	  collapsed:: true
		- independence and conditional independence
		  collapsed:: true
			- the features are independent if
				- $$
				  \begin{gathered}
				  P\left[X_{1}=x_{1}, X_{2}=x_{2}, X_{3}=x_{3}\right]=
				  P\left[X_{1}=x_{1}\right] P\left[X_{2}=x_{2}\right] P\left[X_{3}=x_{3}\right]
				  \end{gathered}
				  $$
			- the features are conditionally independent given Y if
				- $$
				  \begin{gathered}
				  P\left[X_{1}=x_{1}, X_{2}=x_{2}, X_{3}=x_{3} \mid Y\right]= 
				  P\left[X_{1}=x_{1} \mid Y\right] P\left[X_{2}=x_{2} \mid Y\right] P\left[X_{3}=x_{3} \mid Y\right]
				  \end{gathered}
				  $$
	- Within the $k_{th}$ class, the $p$ predictors are indipendent
	- id:: e0caca76-390f-4a0f-b74b-ae0963b3d11c
	  $$
	  f_{k}(x)=f_{k 1}\left(x_{1}\right) \times f_{k 2}\left(x_{2}\right) \times \cdots \times f_{k p}\left(x_{p}\right)
	  $$
		- $f_{kj}$ is the [[probability density function]] of the $j_{th}$ predictor among observations in $k_{th}$ class
	- 这个假设可以 eliminate the need to worry about the association between the p-predictors, given that: 
	  ((6222b6df-c624-4af6-9f51-311744997893))
	- 并且这个假设虽然 ==increase== bias, but ==reduce== variance, ([[bias-variance tradeoff]])
	- 通俗解释: 每个属性都是相互独立的, 概率就是两个事件的概率相乘
	  collapsed:: true
		- ![image.png](../assets/image_1646369745156_0.png){:height 308, :width 480}
- Formula
  collapsed:: true
	- Plug
	  $$
	  f_{k}(x)=f_{k 1}\left(x_{1}\right) \times f_{k 2}\left(x_{2}\right) \times \cdots \times f_{k p}\left(x_{p}\right)
	  $$
	  into 
	  $$
	  \operatorname{Pr}(Y=k \mid X=x)=\frac{\pi_{k} f_{k}(x)}{\sum_{l=1}^{K} \pi_{l} f_{l}(x)}
	  $$
	  get
	  $$
	  \operatorname{Pr}(Y=k \mid X=x)=\frac{\pi_{k} \times f_{k 1}\left(x_{1}\right) \times f_{k 2}\left(x_{2}\right) \times \cdots \times f_{k p}\left(x_{p}\right)}{\sum_{l=1}^{K} \pi_{l} \times f_{l 1}\left(x_{1}\right) \times f_{l 2}\left(x_{2}\right) \times \cdots \times f_{l p}\left(x_{p}\right)}
	  $$
	- to estimate the one-dimensional density function $f_{kj}$, using training data $x_{1j}...x_{nj}$
		- if $X_j$ is quantitative (定量)
			- [[assumption]]
				- $$
				  X_{j} \mid Y=k \sim N\left(\mu_{j k}, \sigma_{j k}^{2}\right)
				  $$
				- In other words, assume within each class, the $j_{th}$ predictor is drawn from a normal distribution, the difference with [[QDA]] is that here we assume that the predictors are independent, which means that the non-diagonal $\Sigma$ is 0
		- if $X_j$ is quantitative (定量)
			- use a non-parametric estimate for $f_{kj}$, [[kernel density estimator]]
		- if $X_j$ is qualitative (定性)
			- ISLRv2 p156
- **Algorithm**
  collapsed:: true
	- 设 $x=\left\{a_{1}, a_{2}, \ldots, a_{m}\right\}$ 为一个待分类项, 每个a为x的一个特征属性
	- 有类别集合$C=\left\{y_{1}, y_{2}, \ldots, y_{n}\right\}$
	- 根据[[bayes theorem]]计算$$P\left(y_{1} \mid x\right), P\left(y_{2} \mid x\right), \ldots, P\left(y_{n} \mid x\right)$$
		- 找到一个已知分类的待分类项集合, 这个集合叫做训练样本集
		- 统计各个类别下各个特征属性的条件概率统计
		  $$P\left(a_{1} \mid y_{1}\right), P\left(a_{2} \mid y_{1}\right), \ldots, P\left(a_{m} \mid y_{1}\right)$$
		  $$P\left(a_{1} \mid y_{2}\right), P\left(a_{2} \mid y_{2}\right), \ldots, P\left(a_{m} \mid y_{2}\right)\ldots$$
		  $$P\left(a_{1} \mid y_{n}\right), P\left(a_{2} \mid y_{n}\right), \ldots, P\left(a_{m} \mid y_{n}\right)$$
		- 如果各个特征属性是条件独立的, 根据 $P(A \mid B)=\frac{P(A) P(B \mid A)}{P(B)}$ , 因为分母对于所有类别为常数, 因此将分子最大化即可, 又因为各特征属性是条件独立的, 所以有
		- $$P\left(x \mid y_{i}\right) P\left(y_{i}\right)=P\left(a_{1} \mid y_{i}\right) P\left(a_{2} \mid y_{i}\right) \ldots P\left(a_{m} \mid y_{i}\right) P\left(y_{i}\right)$$
		  $$=P\left(y_{i}\right) \prod_{j=1}^{m} P\left(a_{j} \mid y_{i}\right)$$
		- 如果$$P\left(y_{k} \mid x\right)=\max \left\{P\left(y_{1} \mid x\right), P\left(y_{2} \mid x\right), \ldots, P\left(y_{n} \mid x\right)\right\}$$, 
		  则$$x \in y_{k}$$
- 通俗Example
  collapsed:: true
	- ![image.png](../assets/image_1646369277073_0.png)
	- ![image.png](../assets/image_1646369751289_0.png)
	- 根据假设, 可以得到是求下面式子中最高的一项
	  $$P(上述所有症状\mid Flu)*P(Flu)$$
	  $$P(上述所有症状\mid Allergy)*P(Allergy)$$
	  $$P(上述所有症状\mid Other)*P(Other)$$
	- ![image.png](../assets/image_1646369297440_0.png)
	-
- naive bayes example 1 (all features are categorical) [[CheatSheet/R]]
	- question and dataset
	  collapsed:: true
		- predict if a car (of a given color and type) will be stolen
		- ![CleanShot_nbayes2(1) (page 16  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_16_83)_20220326@2x_1648338325368_0.png){:height 308, :width 446}
		- what is the probability that a red sports car will be stolen?
			- choose the largest of the following
			  collapsed:: true
				- $$
				  P[\text { yes } \mid \operatorname{Red}, \text { Sport }]=\frac{P[\text { Red }, \text { Sport } \mid \text { yes }] \quad P[\text { yes }]}{P[\text { Red }, \text { Sport }]}
				  $$
				  $$
				  P[\text { no } \mid \operatorname{Red}, \text { Sport }]=\frac{P[\text { Red }, \text { Sport } \mid \text { no }] \quad P[\text { no }]}{P[\text { Red }, \text { Sport }]}
				  $$
			- find the prior probabilities
			  collapsed:: true
				- P[Y = yes] = 0.5, P[Y = no] = 0.5 (看Y列)
			- conditional independence (分子)
			  collapsed:: true
				- collapsed:: true
				  $$
				  P[\text { Red }, \text { Sport } \mid \text { yes }]=P[\text { Red } \mid \text { yes }] \times P[\text { Sport } \mid \text { yes }]
				  $$
					- ![CleanShot_nbayes2(1) (page 27  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_27_83)_20220326@2x_1648338944213_0.png)
			- law of total probability (分母)
			  collapsed:: true
				- $$
				  P[\text { Red }, \text { Sport }]=P[\text { Red }, \text { Sport } \mid \text { yes }] P[\text { yes }]+P[\text { Red }, \text { Sport } \mid \text { no }] P[\text { no }]
				  $$
	- build naive bayes model
	  collapsed:: true
		- ![CleanShot_nbayes2(1) (page 34  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_34_83)_20220326@2x_1648339154352_0.png)
		- ![CleanShot_nbayes2(1) (page 37  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_37_83)_20220326@2x_1648339179114_0.png)
	- predict and produce the accuracy rate
	  collapsed:: true
		- ![CleanShot_nbayes2(1) (page 38  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_38_83)_20220326@2x_1648339263656_0.png)
		- ![CleanShot_nbayes2(1) (page 43  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_43_83)_20220326@2x_1648339324379_0.png)
		- ![CleanShot_nbayes2(1) (page 46  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_46_83)_20220326@2x_1648339355534_0.png)
- naive bayes example 2 (categorical and numeric features) [[CheatSheet/R]]
	- question and dataset
	  collapsed:: true
		- ![CleanShot_nbayes2(1) (page 50  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_50_83)_20220326@2x_1648339468677_0.png)
		- choose the largest of the following
		  collapsed:: true
			- $$P[\text { Default }=N o \mid \text { Home Owner }=N o, \text { Status }=\text { Married }, \text { Income }=120 K]$$
				- $$= \frac{P[H O=N o, S t=\text { Married }, \text { Inc }=120 K \mid N o] \times P[N o]}{P[H O=N o, S t=\text { Married }, \text { Inc }=120 K]}$$
			- $$P[\text { Default }=\text { Yes } \mid \text { Home Owner }=N o, \text { Status }=\text { Married }, \text { Income }=120 K]$$
				- $$
				  =\frac{P[H O=N o, S t=\text { Married }, \text { Inc }=120 K \mid Y e s] \times P[Y e s]}{P[H O=N o, S t=\text { Married }, \text { Inc }=120 K]}
				  $$
		- use naive bayes assumption (出现了原数据没有的条件概率怎么办)
		  collapsed:: true
			- $$
			  \begin{array}{l}
			  P[H O=N o, S t=\text { Married, } \operatorname{Inc}=120 K \mid N o]= \\
			  P[H O=N o \mid N o] \times P[S t=\text { Married } \mid N o] \times P[\text { Inc }=120 K \mid N o]
			  \end{array}
			  $$
			- from the data set, find
				- ![CleanShot_nbayes2(1) (page 64  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_64_83)_20220326@2x_1648340229542_0.png)
			- to find P[Inc = 120K | No], assume that
			  collapsed:: true
				- $$
				  P[\operatorname{Inc}=x \mid Y=N o]=\frac{1}{\sqrt{2 \pi} \sigma_{N o}} e^{-\frac{\left(x-\mu_{N o}\right)^{2}}{2 \sigma_{N o}^{2}}}
				  $$
					- and then estimate $\mu_{No}$ and $\sigma_{No}$
				- ![CleanShot_nbayes2(1) (page 66  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_66_83)_20220326@2x_1648340390139_0.png)
			- 假设正态分布, 得到
			  collapsed:: true
				- ![CleanShot_nbayes2(1) (page 68  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_68_83)_20220326@2x_1648340460871_0.png)
		- law of total probability (分母)
		  collapsed:: true
			- ![CleanShot_nbayes2(1) (page 72  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_72_83)_20220326@2x_1648340547463_0.png)
		- so the posterior probabilities are
		  collapsed:: true
			- ![CleanShot_nbayes2(1) (page 74  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_74_83)_20220326@2x_1648340572961_0.png)
	- build naive bayes model
	  collapsed:: true
		- ![CleanShot_nbayes2(1) (page 75  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_75_83)_20220326@2x_1648340601822_0.png)
		- ![CleanShot_nbayes2(1) (page 79  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_79_83)_20220326@2x_1648340618599_0.png)
	- predict new data point and produce the accuracy rate
	  collapsed:: true
		- ![CleanShot_nbayes2(1) (page 81  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_81_83)_20220326@2x_1648340709607_0.png)
		- ![CleanShot_nbayes2(1) (page 83  83)_20220326@2x.png](../assets/CleanShot_nbayes2(1)_(page_83_83)_20220326@2x_1648340723842_0.png)
	- work flow for Naive Bayes
	  collapsed:: true
		- create a classification problem using the Kaiser Babies datasets by partitioning the baby weight variable (e.g. underweight, normal weight)
		- ```r
		  load(url("http://www.stodden.net/StatData/KaiserBabies.rda"))
		  set.seed(1)
		  infants = infants[,-c(5,9,12,15)]
		  infants = na.omit(infants)
		  medval = median(infants$bwt)
		  
		  y = rep(0, length(infants$bwt))
		  y[infants$bwt > medval] = 1
		  infants$bwt = NULL
		  train = sample(1:length(infants[[1]]), 0.75*length(infants[[1]]))
		  
		  xtrain = infants[train,]
		  xtest = infants[-train,]
		  # labels
		  ytrain = y[train]
		  ytest = y[-train]
		  
		  nb.fit = naiveBayes(ytrain~., data = xtrain)
		  nb.pred = predict(nb.fit, xtest)
		  nb.class = nb.pred
		  aux = prop.table(table(nb.class, ytest))
		  acc = sum(diag(aux))
		  acc
		  ```