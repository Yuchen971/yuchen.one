title:: CheatSheet/dplyr

- {{renderer :tocgen}}
- Column
	- New column (factor) based on current column
	  collapsed:: true
		- ```r
		  d6 = mutate (df, DECADE= ifelse (YEAR %in% 1980:1989, "1980-1989",
		  			ifelse (YEAR %in% 1990:1999, "1990-1999"
		  			ifelse (YEAR %in% 2000:2009, "2000-2009",
		  			ifelse (YEAR %in% 2010:2016, "2010-2016" , "-99")))))
		  
		  
		  ```
		- ![Screen Shot 2022-02-25 at 9.20.38 PM.png](../assets/Screen_Shot_2022-02-25_at_9.20.38_PM_1645852841582_0.png)
- Other
	- Shuffle the tibble
	  collapsed:: true
		- ```r
		  df = crabs %>%
		  	sample_n(nrow(.))
		  ```