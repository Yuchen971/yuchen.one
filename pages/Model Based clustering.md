alias:: mclust

- {{renderer :tocgen, [[]], 1}}
- Definition
	- These methods fit a mixture to the dataset
	- A mixture is a distribution made of several normal densities (called components)
	- The method assigns observations to the component under which they are most likely
- What is mixture
	- definition
		- A linear combination of two distribution called components
		- Density that results from combining two or more densities
	- example
		- two normal density
			- mixture on one variable x
			  collapsed:: true
				- component 1 makes up 25%, component 2 makes up 75% of the data
				- ![CleanShot_modelbased2 (page 9  60)_20220313.png](../assets/CleanShot_modelbased2_(page_9_60)_20220313_1647214951924_0.png)
			- mixture on two variables x1 and x2
			  collapsed:: true
				- ![CleanShot_modelbased2 (page 13  60)_20220313.png](../assets/CleanShot_modelbased2_(page_13_60)_20220313_1647215112236_0.png)
			- group the observations into two clusters
			  collapsed:: true
				- ![CleanShot_modelbased2 (page 14  60)_20220313.png](../assets/CleanShot_modelbased2_(page_14_60)_20220313_1647215163265_0.png)
				- ![CleanShot_modelbased2 (page 15  60)_20220313.png](../assets/CleanShot_modelbased2_(page_15_60)_20220313_1647215229096_0.png)
- Information criteria measures (ICs)
	- Measure the loss of information by fitting a model from a sample
	- All ICs measure a loss => prefer models with small IC values
	- [[AIC]]
	- [[BIC]]
- Procedure
	- Assume the data comes from a statistical distribution called a Mixture
	- Fit a mixture distribution to the data
	- Each component represents a cluster
	- Assign each observation to a cluster
	- each cluster is modeled by a [[multivariate normal]] with parameters
		- vector of means, covariance matrix
	- Each cluster is centered at the vector of means
	- The volume, shape, and orientation of each cluster is defined by the covariance matrix
	- Mixture on two variables x1 and x2 example
	  collapsed:: true
		- ![CleanShot_modelbased2 (page 36  60)_20220314.png](../assets/CleanShot_modelbased2_(page_36_60)_20220314_1647308714615_0.png)
- model based clustering methods [[CheatSheet/R]]
	- preparation
	  collapsed:: true
		- library `mclust`, function `Mclust()`
		- no need to define n. of clusters k
		- for each k, 14 models are compared based on BIC
		- Each one denoted by three letters
		- example
		  collapsed:: true
			- ![CleanShot_modelbased2 (page 37  60)_20220314.png](../assets/CleanShot_modelbased2_(page_37_60)_20220314_1647308853612_0.png){:height 469, :width 476}
		- meanings
			- Volume component
				- E-Gaussians with equal volume
				- V-Gaussians with different volumes
			- Shape component:
				- E-Gaussians with equal aspect ratios
				- V-Gaussians with different aspect ratios
				- I-Clusters that are perfectly spherical
			- Orientation component:
				- E-Gaussians with the same orientation
				- V-Gaussians with different orientations
				- I-Clusters that are orthogonal to the axes
	- Example 1 geyser dataset (from MASS)
		- description
		  collapsed:: true
			- time between eruptions from the old faithful geyser in yellowstone
			- variables are the time between eruptions (waiting) and the eruption duration
			- time in minutes
			- identify cluster of eruptions
			- 2 variables, 299 observations
		- libraries
		  collapsed:: true
			- ```r
			  library(mclust) # Mclust() diabetes dataset
			  library(factoextra) # fviz_mcluster()
			  library(ggpubr) # ggscatter()
			  library(RColorBrewer) #brewer.pal()
			  library (MASS) # dataset geyser, murnorm()
			  ```
		- show the scatter plot and show clusters
		  collapsed:: true
			- if the variable >= 2, use [[PCA]] and get PC1 and PC2 and following code to see the clusters
			- ```r
			  ggscatter(geyser, y = "duration", x = "waiting")
			  ggscatter(geyser, y = 'duration', x = 'waiting') +
			  	geom_density2d()
			  ```
		- model1 (set to 3 clusters)
		  collapsed:: true
			- ```r
			  model1 = Mclust(geyser, G = 3) #choose 3 clsuters
			  summary(model1)
			  ```
				- output
				  collapsed:: true
					- ![CleanShot_modelbased2 (page 44  60)_20220314.png](../assets/CleanShot_modelbased2_(page_44_60)_20220314_1647309716941_0.png)
			- ```r
			  fviz cluster(model1, stand=F,
			  	geom="point",pointsize=1.8,ellipse=FALSE,palette="jco",
			  	ggtheme=theme_bw())+
			  scale_shape_manual(values=c(19,19,19))
			  ```
				- output
				  collapsed:: true
					- ![CleanShot_modelbased2 (page 45  60)_20220314.png](../assets/CleanShot_modelbased2_(page_45_60)_20220314_1647309865233_0.png)
		- model2 (default clusters) (auto choose better [[BIC]] )
		  collapsed:: true
			- ```r
			  model2 = Mclust(geyser) 
			  summary(model1)
			  ```
				- output
				  collapsed:: true
					- ![CleanShot_modelbased2 (page 46  60)_20220314.png](../assets/CleanShot_modelbased2_(page_46_60)_20220314_1647309949908_0.png)
			- ```r
			  fviz_cluster(model2, stand=F,
			  	geom="point",pointsize=1.8,ellipse=FALSE,palette="jco",
			  	ggtheme=theme_bw())+
			  scale_shape_manual(values=c(19,19,19))
			  ```
				- output
				  collapsed:: true
					- ![CleanShot_modelbased2 (page 47  60)_20220314.png](../assets/CleanShot_modelbased2_(page_47_60)_20220314_1647310002146_0.png)
	- Example 2 diabetes dataset
		- description
		  collapsed:: true
			- data set on 145 patients classified into 3 groups, with variables class, glucose, insulin, sspg
		- plot the dataset (use `ggpair` because more than 2 variables)
		  collapsed:: true
			- ```r
			  ggpairs(diabetes,mapping=aes(col class))+theme_bw()
			  ```
				- output
				  collapsed:: true
					- ![CleanShot_modelbased2 (page 51  60)_20220314.png](../assets/CleanShot_modelbased2_(page_51_60)_20220314_1647310125522_0.png)
		- model
		  collapsed:: true
			- ```r
			  # remove the first column (class)
			  df = diabetes[,-1]
			  # build model
			  model1 = Mclust(df)
			  summary(model1)
			  ```
				- output
				  collapsed:: true
					- ![CleanShot_modelbased2 (page 54  60)_20220314.png](../assets/CleanShot_modelbased2_(page_54_60)_20220314_1647310200645_0.png)
		- check the model
		  collapsed:: true
			- ```r
			  model1$modelName # => VVV
			  # optimal number of clusters
			  model1$G # => 3
			  # row probab of belonging to a given cluster
			  head(model1$z)
			  # cluster assignments
			  model1$classification
			  # cluster sizes
			  table(model1$classification)
			  # coordinates of estimated means
			  model1$parameters$mean
			  # estimated covariance matrices
			  model1$parameters$variance$sigma
			  ```
		- Plot the model
		  collapsed:: true
			- BIC values
			  collapsed:: true
				- ```r
				  # BIC values used for choosing the best number of clusters
				  fviz_mclust(model1,"BIC",palette ="jco")
				  ```
					- output
					  collapsed:: true
						- ![CleanShot_modelbased2 (page 57  60)_20220314.png](../assets/CleanShot_modelbased2_(page_57_60)_20220314_1647310357367_0.png)
			- classification
			  collapsed:: true
				- ```r
				  fviz_mclust(model1,"classification",
				  	geom="point",palette="jco")+theme_bw()
				  ```
					- output
					  collapsed:: true
						- ![CleanShot_modelbased2 (page 58  60)_20220314.png](../assets/CleanShot_modelbased2_(page_58_60)_20220314_1647310413399_0.png)
			- Uncertainty (size of the dot is the uncertainty)
			  collapsed:: true
				- ```r
				  fviz_mclust(model1,"uncertainty",palette="jco")+theme_bw()
				  ```
					- output
					  collapsed:: true
						- ![CleanShot_modelbased2 (page 59  60)_20220314.png](../assets/CleanShot_modelbased2_(page_59_60)_20220314_1647310485111_0.png)
			- plot with class name
			  collapsed:: true
				- ```r
				  fviz_cluster(model1,data=df,show.clust.cent=FALSE,
				  	geom NULL,cluster=clusters, ellipse.type "norm")
				  ```
					- output
					  collapsed:: true
						- ![CleanShot_modelbased2 (page 60  60)_20220314.png](../assets/CleanShot_modelbased2_(page_60_60)_20220314_1647310549795_0.png)