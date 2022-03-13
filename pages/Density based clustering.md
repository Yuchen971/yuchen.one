alias:: 密度聚类, density-based clustering
topic:: clustering

- # Notes
	- **difference between [[k-mean]], [[Hierarchical clustering]] and density based clustering **
	  collapsed:: true
		- for k-means and hierarchical clustering
			- find clusters using the distance between observations (or clusters)
			- k-means 是基于距离的算法, 结果是球状的簇
		- for density-based clustering methods
			- find clusters using the density of observations (or clusters)
			- still needs to scale the data
			- 可以发现任意形状的聚类 (非球状的)
	- Common density based clustering methods
		- [[DBSCAN]]
		- [[OPTICS]]