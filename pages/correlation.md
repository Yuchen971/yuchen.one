alias:: cor, 相关系数

- Definition
	- $$
	  \rho=\frac{\operatorname{Cov}(X, Y)}{\sigma_{X} \sigma_{Y}}
	  $$
	- $$-1<p<+1$$
	- correlation 公式
		- $$
		  \operatorname{Cor}(X, Y)=\frac{\sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)\left(y_{i}-\bar{y}\right)}{\sqrt{\sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)^{2}} \sqrt{\sum_{i=1}^{n}\left(y_{i}-\bar{y}\right)^{2}}},
		  $$
	- X,Y的[协方差]([[covariance]])除以X和Y的标准差, 相关系数也可以看成协方差：一种剔除了两个变量量纲影响、标准化后的特殊协方差
	- 它消除了两个变量变化幅度的影响，而只是单纯反应两个变量每单位变化时的相似程度
	- [如何通俗易懂地解释「协方差」与「相关系数」的概念？ - 知乎](https://www.zhihu.com/question/20852004)