alias:: 事实表, fact tables

- Definition
	- 数据聚合后根据某个维度生成的结果表, 是具体的统计表
	- 事实表为数据聚合后根据某个维度生成的结果表
- Example
	- 销售事实表: Prod_id(引用产品维度表), TimeKey(引用时间维度表), SalesAmount(销售总量, 以货币计), Unit(销售量)
- Granularity (粒度)
	- level of detail in the fact table
	- example
		- each row represents one order
		- each row represents total orders for a specific month
	- Generally, we select the lowest level grain possible
- Type
	- [[Additive fact table]]
	- [[Semi-Additive fact table]]
	- [[Non-Additive fact table]]
	- [[Factless Fact table]]
	- Quantity example of [[Additive fact table]] and [[Non-Additive fact table]]
	  collapsed:: true
		- ![Screen Shot 2022-03-01 at 9.46.52 PM.png](../assets/Screen_Shot_2022-03-01_at_9.46.52_PM_1646200019058_0.png){:height 434, :width 215}
		- Sample additive queries (有意义的)
			- For a given day, what is our total number of products on hand?
			- For a given day and a given store, what is our total number of products on hand?
			- For a given day and a given product, what is our total number of products on hand?
		- Sample non-additive queries (无意义)
			- For a given store, what is our total number of products on hand? (聚合每一个store的所有product类型的手头数量是没意义的, 因为每天的都不一样, 加起来也没意义)
			- For a given product, what is our total number of products on hand? (同上)
			- For a given store and a given product, what is our total number of products on hand? (同上)
	- [[Transaction fact table]]
	- [[Periodic snapshot table]]
	- [[Accumulating snapshot tables]]
	- Banking example of [[Transaction fact table]] VS [[Periodic snapshot table]]
	  collapsed:: true
		- ![Screen Shot 2022-03-02 at 12.31.04 AM.png](../assets/Screen_Shot_2022-03-02_at_12.31.04_AM_1646209867153_0.png)
		- [[Transaction fact table]]
			- ![Screen Shot 2022-03-02 at 12.32.09 AM.png](../assets/Screen_Shot_2022-03-02_at_12.32.09_AM_1646209931772_0.png)
		- [[Periodic snapshot table]]
			- ![Screen Shot 2022-03-02 at 12.32.53 AM.png](../assets/Screen_Shot_2022-03-02_at_12.32.53_AM_1646209977224_0.png)
	- [[aggregate fact table]]