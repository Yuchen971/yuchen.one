topic:: mse, bias variance trade off, bayes classifier

- # Notes
	- **What is [[mean squared error]] (MSE)?**
	- **What is [[bias variance tradeoff]] ?**
	- **分类问题准确度标准?**
	  collapsed:: true
		- $$
		  \frac{1}{n} \sum_{i=1}^{n} I\left(y_{i} \neq \hat{y}_{i}\right)
		  $$
		- $\hat{y_i}$ is the predicted class label for the ith observation using $\hat{f}$
		- $I\left(y_{i} \neq \hat{y}_{i}\right)$ is an indicator variable that equals **1 (错误)** if $$y_{i} \neq \hat{y}_{i}$$ and **Zero(正确)** if $$y_{i} = \hat{y}_{i}$$
	- **贝叶斯分类器** [[bayes classifier]]
	  collapsed:: true
		- assigns each observation to the most likely class
		- 有时候有X无法确定Y的条件分布, 所以估测概率的预测方法叫[[KNN]]
- # Summary
	- 通过训练数据均方差估测测试数据的均方差的方法: [[cross validation]]