title:: CheatSheet/data.table

- {{renderer :tocgen, [[]], 2}}
- Column
	- change column types
	  collapsed:: true
		- ```r
		  # for a single column
		  dtnew = dt[, Quarter:=as.character(Quarter)]
		  
		  # for multiple column
		  dtnew = dt[,lapply(.SD, as.factor)]
		  ```
	- do calculation on specific column
	  collapsed:: true
		- ```r
		  dt[,CRS_DEP_TIME := round(CRS_DEP_TIME/100)]
		  ```
	- rename column with space
	  collapsed:: true
		- ```r
		  setnames(df, "Flight Status", "Flight_Status")
		  ```
- ML
	- train and test split
	  collapsed:: true
		- ```r
		  inTrain <- MyDT[,sample(.N, floor(.N*.75))]
		  Train <- foo.dt[inTrain]
		  Test <- foo.dt[-inTrain]
		  ```