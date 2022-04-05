alias:: K邻近, K-nearest neighbor
type:: non-parametric, ML model, regression, classification, supervised learning

- {{renderer :tocgen, [[]], 1}}
- Classification
	- For each data point (row)
		- 计算测试数据与各个训练数据之间的[[距离]]
		- 对距离从小到大进行排序
		- 选取距离最小的k个点 (rows)
		- 确定前k个点类别的出现频率
		- 出现频率最高的类别作为预测分类
	- [[hyperparameter]]
	  collapsed:: true
		- k值较小, 相当于用较小的邻域中的训练实例进行预测, 只有距离近的(相似的)起作用
			- 单个样本影响大
			- 学习的近似误差(approximation error)会减小, 但估计误差(estimation error)会增大
			- 噪声敏感
			- 整体模型变得复杂, 容易发生过拟合
		- k值较大, 这时距离远的(不相似的)也会起作用
			- 近似误差会增大，但估计误差会减小
			- 整体的模型变得简单
	- Note
		- Neighbors are ==rows== in the dataset
		- Predictors are ==columns== must be numeric
		- There is a distance between each pair of rows
		- Distance between row $p$ and row $q$ is
			- $$
			  \sqrt{\left(q_{1}-p_{1}\right)^{2}+\left(q_{2}-p_{2}\right)^{2}+\cdots+\left(q_{n}-p_{n}\right)^{2}}
			  $$
				- where $(p_1, p_2,...,p_n)$ and $(q_1, q_2,...,q_n)$ are the values in the rows $p$ and $q$
		- the object is to predict the category in column $X$
	- example (k = 1)
	  collapsed:: true
		- ![CleanShot_knn1 (page 16  44)_20220326@2x.png](../assets/CleanShot_knn1_(page_16_44)_20220326@2x_1648332985284_0.png)
		  collapsed:: true
			- sqrt((13−32)^2+(29−8)^2)
	- KNN example (balanced data) (classification) [[CheatSheet/R]]
		- question (Boston dataset)
		  collapsed:: true
			- It is of interest to predict whether a suburb has a crime rate above or below the median crime rate.
			- Create a new variable y that contains 1 if crime is a value above its median (and 0 if crime is below its median).
		- load the data
		  collapsed:: true
			- collapsed:: true
			  ```r
			  library("MASS")
			  library("class") # knn()
			  df = Boston
			  str(df)
			  ```
				- ![CleanShot_knn1 (page 27  44)_20220326@2x.png](../assets/CleanShot_knn1_(page_27_44)_20220326@2x_1648333756678_0.png)
		- data preprocessing
		  collapsed:: true
			- collapsed:: true
			  ```r
			  # create categorical var
			  medval = median(df$crim)
			  y = rep(0,n)
			  y[df$crim > medval] = 1
			  y = as.factor(y)
			  # remove column crim
			  df$crim = NULL
			  # scale the data, make the sd for each var is 1, mean is 0
			  df2 = data.frame(scale(df)) 
			  # show the categorical var
			  table(y)
			  ```
				- ```r
				  ## y
				  ##   0   1
				  ## 253 253
				  ```
		- tran test split
		  collapsed:: true
			- ```r
			  set.seed(1)
			  train = sample(1:n, 3*n/4)
			  # split predictor rows
			  xtrain = df2[train,]
			  xtest = df2[-train,]
			  # split categories (label)
			  ytrain = y[train]
			  ytest = y[-train]
			  ```
		- fit knn
		  collapsed:: true
			- collapsed:: true
			  ```r
			  yhat = knn(xtrain, xtest, ytrain, k = 3)
			  # confusion matrix
			  table(yhat, ytest) #compare predictions(yhat) with true categories
			  ```
				- ![CleanShot_knn1 (page 36  44)_20220326@2x.png](../assets/CleanShot_knn1_(page_36_44)_20220326@2x_1648336178556_0.png)
		- produce error rate (1 - accuracy rate)
		  collapsed:: true
			- ```r
			  aux = prop.table(table(yhat, ytest))
			  1-sum(diag(aux)) # => 0.0551181 is the proportion of errors
			  ```
		- Apply knn with k = 1 to 9 neighbors
		  collapsed:: true
			- collapsed:: true
			  ```r
			  # find best number neighbors k
			  erate = rep(0, 9)
			  for (i in 1:9) {
			    yhat = knn(xtrain, xtest, ytrain, k=i)
			    aux = prop.table(table(yhat, ytest))
			    erate[i] = 1-sum(diag(aux))
			  }
			  ```
				- ![CleanShot_knn1 (page 41  44)_20220326@2x.png](../assets/CleanShot_knn1_(page_41_44)_20220326@2x_1648336394758_0.png)
		- plot the error rate
		  collapsed:: true
			- collapsed:: true
			  ```r
			  xaxis = 1:9
			  plot(erate ~ xaxis, type = 'l', xlab = "N. of neighbors", ylab = "error rate")
			  ```
				- ![CleanShot_knn1 (page 43  44)_20220326@2x.png](../assets/CleanShot_knn1_(page_43_44)_20220326@2x_1648336459301_0.png)
- Regression
	-
- Note
	- KNN is distance-based model so we need to ==scaling== the data
	- Model performance is based on accuracy rate (ACC = (TP + TN)/(P + N))
- pros and cons
	- 可以用于多分类, 回归
	- 需要机选待分类样本与所有已知样本的距离, 计算量大
	- 样本容量小或样本分布不均衡时, 容易出现分类错误. 可以通过添加距离权重进行改善