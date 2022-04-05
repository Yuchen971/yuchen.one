language:: R
type:: package

- [Tibbles Tutorial](https://r4ds.had.co.nz/tibbles.html)
- Basic
	- Creating tibbles
	  collapsed:: true
		- Normal way
		  collapsed:: true
			- ```r
			  as_tibble(iris)
			  
			  # or
			  tibble(
			    x = 1:5, 
			    y = 1, 
			    z = x ^ 2 + y
			  )
			  #> # A tibble: 5 x 3
			  #>       x     y     z
			  #>   <int> <dbl> <dbl>
			  #> 1     1     1     2
			  #> 2     2     1     5
			  #> 3     3     1    10
			  #> 4     4     1    17
			  #> 5     5     1    26
			  ```
		- column name with special symbol
		  collapsed:: true
			- ```r
			  # or
			  tb <- tibble(
			    `:)` = "smile", 
			    ` ` = "space",
			    `2000` = "number"
			  )
			  #> # A tibble: 1 x 3
			  #>   `:)`  ` `   `2000`
			  #>   <chr> <chr> <chr> 
			  #> 1 smile space number
			  ```
		- Use tribble
		  collapsed:: true
			- ```r
			  # or tribble() Transposed tibble
			  # column headings are defined by formulas 
			  # (i.e. they start with ~), 
			  # and entries are separated by commas
			  tribble(
			    ~x, ~y, ~z,
			    #--|--|----
			    "a", 2, 3.6,
			    "b", 1, 8.5
			  )
			  #> # A tibble: 2 x 3
			  #>   x         y     z
			  #>   <chr> <dbl> <dbl>
			  #> 1 a         2   3.6
			  #> 2 b         1   8.5
			  ```
		- create nested table
		  collapsed:: true
			- ```r
			  tibble(x = 1:3, y = list(1:5, 1:10, 1:20))
			  #> # A tibble: 3 × 2
			  #>       x y         
			  #>   <int> <list>    
			  #> 1     1 <int [5]> 
			  #> 2     2 <int [10]>
			  #> 3     3 <int [20]>
			  ```
	- Print tibbles
	  collapsed:: true
		- the data frame and control the number of `rows (n)` and the width of the display. `width = Inf` will display all columns
		- ```r
		  nycflights13::flights %>% 
		    print(n = 10, width = Inf)
		  ```
	- Subsetting
	  collapsed:: true
		- ```r
		  df <- tibble(
		    x = runif(5),
		    y = rnorm(5)
		  )
		  
		  # Extract by name
		  df$x
		  #> [1] 0.73296674 0.23436542 0.66035540 0.03285612 0.46049161
		  df[["x"]]
		  #> [1] 0.73296674 0.23436542 0.66035540 0.03285612 0.46049161
		  
		  # Extract by position
		  df[[1]]
		  #> [1] 0.73296674 0.23436542 0.66035540 0.03285612 0.46049161
		  
		  df %>% .$x
		  #> [1] 0.73296674 0.23436542 0.66035540 0.03285612 0.46049161
		  df %>% .[["x"]]
		  #> [1] 0.73296674 0.23436542 0.66035540 0.03285612 0.46049161
		  ```
	- Add column
	  collapsed:: true
		- `add_column()`
			- ```r
			  # add_column ---------------------------------
			  df <- tibble(x = 1:3, y = 3:1)
			  
			  df %>% add_column(z = -1:1, w = 0)
			  #> # A tibble: 3 × 4
			  #>       x     y     z     w
			  #>   <int> <int> <int> <dbl>
			  #> 1     1     3    -1     0
			  #> 2     2     2     0     0
			  #> 3     3     1     1     0
			  df %>% add_column(z = -1:1, .before = "y")
			  #> # A tibble: 3 × 3
			  #>       x     z     y
			  #>   <int> <int> <int>
			  #> 1     1    -1     3
			  #> 2     2     0     2
			  #> 3     3     1     1
			  
			  # You can't overwrite existing columns
			  try(df %>% add_column(x = 4:6))
			  #> Error : Column name `x` must not be duplicated.
			  #> Use .name_repair to specify repair.
			  
			  # You can't create new observations
			  try(df %>% add_column(z = 1:5))
			  #> Error : New columns must be compatible with `.data`.
			  #> ✖ New column has 5 rows.
			  #> ℹ `.data` has 3 rows.
			  ```