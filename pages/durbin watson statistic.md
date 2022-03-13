alias:: durbin-watson statistic, 杜宾 瓦特森统计量, 杜宾-瓦特森统计量

- # Definition
	- 用于检验[自相关性]([[Autocorrelation]])
	- dubin watson statistic formula
		- $$
		  D W=\frac{\sum_{t=2}^{T}\left(e_{t}-e_{t-1}\right)^{2}}{\sum_{t=1}^{T} e_{t}^{2}}
		  $$
	- 该统计量的值落在$(0,4)$内, $DW=2$ 意味着没有自相关性, 
	  $0<DW<2$ 表明残差间有正的相关性, 
	  $2<DW<4$ 表明残差间有负的相关性.
	- 经验上, 如果$DW<1$或$DW>3$, 则自相关性已经达到了需要示警的水平. 
	  如果事先给定了检验的方向(正/负相关性)和置信度$α$, 也可以根据假设检验的思路进行对应计算.
-