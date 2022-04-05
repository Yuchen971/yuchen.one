alias:: Akaike information criterion, 赤池信息量准则

- Definition
	- 评估统计模型的复杂度和衡量统计模型拟合优度的指标之一
- Formula
	- 一般情况
	- $$
	  A I C=2 p-2 \ln (L)
	  $$
		- L 为 [[似然函数]]
	- 假设模型的误差服从正态分布, n为观察数, [[SSE]] 为误差平方和
	- $$
	  A I C=n \log \left(\frac{S S E}{n}\right)+2 p
	  $$
		- p 是参数的数量