alias:: VIF, 方差膨胀系数

- # Definition
	- 用于检验[多重共线性]([[Multicollinearity]])
	- variance inflation factor formula
	- 假设回归模型为
		- $$
		  Y=\beta_{0}+\beta_{1} X_{1}+\beta_{2} X_{2}+\cdots+\beta_{k} X_{k}+\varepsilon
		  $$
	- 对于变量 $X_j$ 可以证得其估计系数 $\beta_j$的方差为
		- $$
		  \operatorname{\hat{var}}\left(\hat{\beta}_{j}\right)=\frac{s^{2}}{(n-1) \operatorname{var}\left(X_{j}\right)} \cdot \frac{1}{1-R_{j}^{2}}
		  $$
	- 其中唯一与其它自变量有关的值是$R^2_j$，$R^2_j$是$X_j$关于其它自变量回归的残差
		- $$
		  X_{j}=\beta_{0}+\beta_{1} X_{1}+\beta_{2} X_{2}+\cdots+\beta_{j-1} X_{j-1}+\beta_{j+1} X_{j+1}+\cdots+\beta_{k} X_{k}+\varepsilon
		  $$
	- $\frac{1}{1-R_{j}^{2}}$ 被称为$VIF$也就是方差膨胀系数, 如果$VIF<3$说明该变量基本不存在多重共线性问题, 如果$VIF>10$ 说明多重共线性问题严重