title:: CheatSheet/ggplot2

- {{renderer :tocgen}}
- Related Links
	- [R Graphics Cookbook](https://r-graphics.org/recipe-quick-scatter)
	- [ggplot2 Tutorial for Beautiful Plotting in R](https://www.cedricscherer.com/2019/08/05/a-ggplot2-tutorial-for-beautiful-plotting-in-r/)
- Quickly Exploring Data
  collapsed:: true
	- quick scatter plot
	  collapsed:: true
		- ```r
		  ggplot(mtcars, aes(x = wt, y = mpg)) + geom_point()
		  ```
	- quick line plot
	  collapsed:: true
		- ```r
		  ggplot(pressure, aes(x = temperature, y = pressure)) + geom_line()
		  ```
	- quick box plot
	  collapsed:: true
		- ```r
		  ggplot(ToothGrowth, aes(x = supp, y = len)) + geom_boxplot()
		  ```
	- quick plot function curve
	  collapsed:: true
		- ```r
		  # This sets the x range from 0 to 20
		  myfun <- function(xvar) {
		    1 / (1 + exp(-xvar + 10))
		  }
		  ggplot(data.frame(x = c(0, 20)), aes(x = x)) + stat_function(fun = myfun, geom = "line")
		  ```
- Bar Graph
	- Basic Bar Graph
		- use `ggolot()` with `geom_col()` and specify variables
			- ```r
			  library(gcookbook)  # Load gcookbook for the pg_mean data set
			  ggplot(pg_mean, aes(x = group, y = weight)) +
			    geom_col()
			  ```
		-
-
-
-
-
-
-