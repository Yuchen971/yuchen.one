topic:: K-means, clustering

- # Notes
	- What is clustering?
	  collapsed:: true
		- Methods for finding groups, or clusters, from a population
		- A good clustering is one where the observations within a group are similar but observations between groups are different
	- What is the difference between Classification VS Clustering?
	  collapsed:: true
		- Classification (supervised)
			- categories are known
			- predict the category of new observations
		- Clustering (unsupervised)
			- categories are unknown
			- Want to discover categories of a new categorical variable called cluster
	- **Types of clustering methods** #recall
	  collapsed:: true
		- [[Hierarchical clustering]]
			- Clusters may have subclusters (nested)
			- Nested clusters that may be displayed as a **tree**
			- methods
			  id:: 620ac899-c18f-4859-9ff7-2b76fa540b06
				- Agglomerative methods
					- Begin with _n_ clusters then merge similar clusters until a single cluster is obtained
				- Divisive methods
					- Begin with _1_ cluster then split dissimilar clusters until _n_ clusters are obtained
		- [[Non-Hierarchical clustering]]
			- Center-based (distance based method)
				- Each data point (row) is closer to the center of its cluster than to the center of any other cluster
				- [[k-mean]]
			- Density-based
				- Clusters are high density regions of data points separated by low density regions
				- [[DBSCAN]]
		-
	- **What is [[k-mean]] ?** #recall
	  collapsed:: true
		- 算法原理
		- 常用的中心距离度量有哪些
		- 轮廓系数 Silhouette Coefficient
		- 起始点的选择是否对最终结果有影响
			- 不同的初始值结果不一样(选不好可能得到局部最优)
		- 空聚类的处理
			- 选择一个距离当前任何质心最远的点. 这将消除当前对总平方误差影响最大的点
			- 从具有最大SSE的簇中选择一个替补的质心, 这将分裂簇并降低聚类的总SSE. 如果有多个空簇, 则该过程重复多次
		- 是否会一直陷入选择质心循环不停下
			- 不会, kmeans一定会收敛. 因为[[SSE]] 误差平方和(每个点到自身归属的质心距离的平方和)是凸函数, 所以迭代可以达到局部最优解
		- 数据量较大如何快速收敛
		- 优缺点
			- 原理简单, 解释性强
			- k值难确定, 局部最优, 对噪声敏感, 需样本存在均值, 聚类效果依赖于初始化, 对非凸数据集或类别规模差距大的数据效果不好
	- **Kmeans and [[KNN]] difference?** #recall
	  collapsed:: true
		- [[KNN]] 是分类算法, K-means是聚类算法
		- [[KNN]] 是监督学习, K-means 是非监督学习
		-