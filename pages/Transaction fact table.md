alias:: 事务事实表, transaction fact, transaction facts

- **Definition**
	- Events (transactions), 保存的是最原子的数据, 也称"原子事实表".
- **Dimension**
	- typically include date/time, geography/branch, product, customer, supplier
- **Grain**
	- specific event/transaction
	- specified in one of two basic way
		- Transaction id/order line item
		- Dimensional terms "orders by day, customer, product, and salesperson
	- May be individual transaction or aggregated transactions one or more dimension
- **Properties**
	- Transaction fact tables are sparse
		- Rows are recorded only for activities that take place
		- Many combinations of dimension values are never used
	- Transaction fact tables contain [[additive facts]]
	- 一旦事务被提交, 事实表数据被插入, 数据就不再进行更改, 增量更新.
	- A business process that represents ==a series of steps or statuses== may be tracked using a transaction fact table. This model is useful for studying and quantifying the various activities but is notoriously difficult to use when studying the elapsed time spent at one or more stages.
- example
	- 比如, 地产行业里面的排卡, 订购, 签约, 回款这些都是一个特定的业务动作.
	  包含有具体业务的发生时间, 以及业务发生时的相关渠道, 组织, 人力, 产品以及客户.
	  这个形成了一个典型的star模型. 中间的事实表就是一个交易事实表也称为事务事实记录表.