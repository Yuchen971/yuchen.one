alias:: bias-variance tradeoff
- Definition
	- 当算法从数据集学习真实信号的灵活性有限时, 就会出现偏差, ( 想的太过简单，欠拟合), 所以模型整体产生偏差 **Bias**
	- 高方差模型非常关注训练数据, 而对以前没有见过的数据不进行泛化. 因此, 这样的模型在训练数据上表现得很好, 但在测试数据上却有很高的错误率 **Variance**
		- 概率论中方差用来度量随机变量和其数学期望(即均值)之间的偏离程度. 方差越大, 数据离均值波动越大(分布越散), 
		  统计中的方差(样本方差)是每个样本值与全体样本值的平均数之差的平方值的平均数
	- ^^variance^^: the amount by which $$\hat f$$ would change if we estimated it using a training set, 也就是预测值的变化范围, 离散程度. 当我们使用不同的训练数据组去建立模型时就会产生方差
	- ^^bias^^: 估计值的期望与真实值之前的差距, 越灵活(复杂)的模型带来越低的偏差
	- ^^expected test MSE can never below^^ $$Var(\epsilon)$$ which is the irreducible error
	- ==Bias Variance 公式==
		- {{embed ((7966e105-61bc-4a47-b1a0-68b84c86e5e1))}}
- **graph of bias-variance decomposition and why**
	- ![image.png](../assets/image_1646369061357_0.png)
		- i. (squared) bias - ==decreases== monotonically because ==increases== in ==flexibility==, yield a closer fit
		- ii. variance - ==increases== monotonically because ==increases== in ==flexibility==,  yield overfit
		- iii. training error - ==decreases== monotonically because ==increases== in ==flexibility== yield a closer fit
		- iv. test error - ==concave up curve== because ==increase in flexibility== yields a closer fit ==before it overfits==
		- v. Bayes (irreducible) error - defines the lower limit, the test error is bounded below by the irreducible error due to variance in the error (epsilon) in the output values (0 <= value). When the training error is lower than the irreducible error, overfitting has taken place.
		  The [[bayes error rate]] is defined for classification problems and is determined by the ratio of data points which lie at the 'wrong' side of the [[decision boundary]] , (0 <= value < 1).
	-
-