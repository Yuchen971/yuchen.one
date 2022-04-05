language:: R
type:: package

- [21 Iteration | R for Data Science](https://r4ds.had.co.nz/iteration.html#iteration)
- Basic
	- properties
	  collapsed:: true
		- each function takes a vector as input, applies a function to each piece, returns a vector that's the same list
	- `map(.x, .f)` make a list, `.x` vector 数据, `.f` 方程
	  collapsed:: true
		- `.` refers to the current list element (same with `i` in for loop)
		- fit a linear model to each group in a dataset
			- ```r
			  models <- mtcars %>% 
			    split(.$cyl) %>% 
			    map(function(df) lm(mpg ~ wt, data = df))
			        
			  # or
			  models <- mtcars %>% 
			    split(.$cyl) %>% 
			    map(~lm(mpg ~ wt, data = .))
			  ```
	- `map()` 提取嵌套数据
	  collapsed:: true
		- ```r
		  pk = list(
		  	ob1 = list (
		  		name = "R",
		  		id = 1L,
		  		feature = list(first = "library++", second = "performance-")
		  	),
		  	ob2 = list(
		  		name = "Julia",
		  		id = 2L,
		  		feature = list (first = "library-", second = "performance++")
		        )
		    )
		  
		  # 按名称提取
		  pk %>% map("name")
		  #$ob1
		  #[1] "R"
		  #$ob2
		  #[1] "Julia"
		  
		  pk %>% map("id")
		  #$ob1
		  #[1] 1
		  #$ob2
		  #[1] 2
		  
		  # 根据特性选择相应函数
		  pk %>% map_chr("name")
		  #ob1     ob2 
		  #"R" "Julia" 
		  
		  # 使用dataframe
		  df = data.table(
		    name = map_chr(pk,"name"),
		    id = map_int(pk, "id"),
		    feature1 = map_chr(pk,c("feature","first")),
		    feature2 = map_chr(pk,c("feature","second"))
		  )
		  ```
	- `map2()` function has 2 input
	  collapsed:: true
		- ```r
		  n = list(3,4,5) 
		  mean = list(0,1,2)
		  map2(n,mean,rnorm) #rnorm 传入两个参数, n和mean, 返回三个list
		  map2_dbl(n,mean,rnorm) #返回一个list
		  ```
	- `pmap()` function has 2 input
	  collapsed:: true
		- ```r
		  n = list(3,4,5)
		  mean = list(0,1,2)
		  sd = list(1,2,3)
		  lists = list(n, mean, sd)
		  pmap(lists, rnorm)
		  ```
	- `map_lgl()` make a logical vector
	- `map_int()` make a integer vector
	- `map_dbl()` returns a numeric (double) vector
	  collapsed:: true
		- ```r
		  numbers <- list(11, 12, 13, 14)
		  map(numbers, sqrt)
		  #[[1]]
		  #[1] 3.316625
		  #
		  #[[2]]
		  #[1] 3.464102
		  #
		  #[[3]]
		  #[1] 3.605551
		  #
		  #[[4]]
		  #[1] 3.741657
		  
		  map_dbl(numbers, sqrt)
		  # [1] 3.316625 3.464102 3.605551 3.741657
		  
		  ```
	- `map_if()` 判断
	  collapsed:: true
		- ```r
		  #创造一个辅助函数，如果为偶数则返回TRUE
		  is_even <- function(x){
		    !as.logical(x %% 2)
		  }
		  map_if(numbers, is_even, sqrt)
		  ```
	- `map_at()` 对某一些行进行map
	  collapsed:: true
		- ```r
		  numbers <- list(11, 12, 13, 14)
		  map_at(numbers, c(1,3), sqrt)
		  ## [[1]]
		  ## [1] 3.316625
		  ## 
		  ## [[2]]
		  ## [1] 12
		  ## 
		  ## [[3]]
		  ## [1] 3.605551
		  ## 
		  ## [[4]]
		  ## [1] 14
		  ```
	- `modify()` 修改变量值
	  collapsed:: true
		- ```r
		  mtcars %>%
		  	modify(function(x) x*2)     
		  # or
		  mtcars %>%
		  	modify(~.*2)   
		  ```
	- `modify_at()` 针对行修改变量
	  collapsed:: true
		- ```r
		  # 修改gear, carb
		  mtcars %>%
		  	modify_at(c(10,11), function(x) x*2)
		  # or
		  mtcars %>%
		      modify_at(c("gear","carb"),function(x) x*2)
		  ```
	-