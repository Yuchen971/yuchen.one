alias:: 损失函数, cost function, 代价函数

- {{renderer :tocgen}}
- Definition
	- 损失函数(Loss function)
		- 定义在单个训练样本上的, 也就是就==单个样本的误差==, 比如想要分类, 就是预测的类别和实际类别的区别, 是一个样本的, 用L表示
	- 代价函数(Cost function)
		- 是定义在整个训练集上面的, 也就是==所有样本的误差的总和的平均==, 也就是损失函数的总和的平均, 有没有这个平均其实不会影响最后的参数的求解结果, 用 J 表示
		- 表示多样本同时输入模型的时候总体的误差—每个样本误差的和然后取平均值
- 类别
	- 平方损失函数 (square loss) [[OLS]]
		- formula
			- $$L(Y, f(x))=(Y-f(X))^2$$
				- 其中 $Y-f(x)$ 是残差, 整个式子是 [[残差平方和]]
				- 实际运用中使用 [[MSE]]
- reference
	- [机器学习常用损失函数](https://cloud.tencent.com/developer/article/1165263)