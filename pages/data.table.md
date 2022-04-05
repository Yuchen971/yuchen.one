title:: data.table
language:: R
type:: package

- Basic
	- read csv
	  collapsed:: true
		- ```r
		  foo = fread('foo.csv')
		  ```
	- General form
	  collapsed:: true
		- ```r
		  DT[i, j, by]
		  ##   R:                 i                 j        by
		  ## SQL:  where | order by   select | update  group by
		  ```
	- Subset rows in `i`, WHERE
	  collapsed:: true
		- ```r
		  ans <- flights[origin == "JFK" & month == 6L]
		  head(ans)
		  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
		  # 1: 2014     6   1        -9        -5      AA    JFK  LAX      324     2475    8
		  # 2: 2014     6   1       -10       -13      AA    JFK  LAX      329     2475   12
		  # 3: 2014     6   1        18        -1      AA    JFK  LAX      326     2475    7
		  # 4: 2014     6   1        -6       -16      AA    JFK  LAX      320     2475   10
		  # 5: 2014     6   1        -4       -45      AA    JFK  LAX      326     2475   18
		  # 6: 2014     6   1        -6       -23      AA    JFK  LAX      329     2475   14
		  ```
	- Optimized Order
	  collapsed:: true
		- We can use “-” on a character columns within the frame of a data.table to sort in decreasing order
		- ```r
		  ans <- flights[order(origin, -dest)]
		  head(ans)
		  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
		  # 1: 2014     1   5         6        49      EV    EWR  XNA      195     1131    8
		  # 2: 2014     1   6         7        13      EV    EWR  XNA      190     1131    8
		  # 3: 2014     1   7        -6       -13      EV    EWR  XNA      179     1131    8
		  # 4: 2014     1   8        -7       -12      EV    EWR  XNA      184     1131    8
		  # 5: 2014     1   9        16         7      EV    EWR  XNA      181     1131    8
		  # 6: 2014     1  13        66        66      EV    EWR  XNA      188     1131    9
		  
		  ans <- flights[carrier == "AA", .N, by = .(origin, dest)][order(origin, -dest)]
		  head(ans, 10)
		  #     origin dest    N
		  #  1:    EWR  PHX  121
		  #  2:    EWR  MIA  848
		  #  3:    EWR  LAX   62
		  #  4:    EWR  DFW 1618
		  #  5:    JFK  STT  229
		  #  6:    JFK  SJU  690
		  #  7:    JFK  SFO 1312
		  #  8:    JFK  SEA  298
		  #  9:    JFK  SAN  299
		  # 10:    JFK  ORD  432
		  ```
	- Select columns in `j`
	  collapsed:: true
		- do not use`.()`, to return a vector
		  collapsed:: true
			- ```r
			  ans <- flights[, arr_delay]
			  head(ans)
			  # [1]  13  13   9 -26   1   0
			  ```
		- use `.()`, same as `list()`, return data.table
		  collapsed:: true
			- ```r
			  ans <- flights[, list(arr_delay)]
			  head(ans)
			  #    arr_delay
			  # 1:        13
			  # 2:        13
			  # 3:         9
			  # 4:       -26
			  # 5:         1
			  # 6:         0
			  ans <- flights[, .(arr_delay, dep_delay)]
			  head(ans)
			  #    arr_delay dep_delay
			  # 1:        13        14
			  # 2:        13        -3
			  # 3:         9         2
			  # 4:       -26        -8
			  # 5:         1         2
			  # 6:         0         4
			  ```
		- select and rename it
		  collapsed:: true
			- ```r
			  ans <- flights[, .(delay_arr = arr_delay, delay_dep = dep_delay)]
			  head(ans)
			  #    delay_arr delay_dep
			  # 1:        13        14
			  # 2:        13        -3
			  # 3:         9         2
			  # 4:       -26        -8
			  # 5:         1         2
			  # 6:         0         4
			  ```
		- using vectors variable to subset with `..`
		  collapsed:: true
			- ```r
			  select_cols = c("arr_delay", "dep_delay")
			  flights[ , ..select_cols]
			  #         arr_delay dep_delay
			  #      1:        13        14
			  #      2:        13        -3
			  #      3:         9         2
			  #      4:       -26        -8
			  #      5:         1         2
			  #     ---                    
			  # 253312:       -30         1
			  # 253313:       -14        -5
			  # 253314:        16        -8
			  # 253315:        15        -4
			  # 253316:         1        -5
			  ```
		- select columns in a variable to subset with`with = F`
		  collapsed:: true
			- ```r
			  select_cols = c("arr_delay", "dep_delay")
			  flights[ , select_cols, with = FALSE]
			  #         arr_delay dep_delay
			  #      1:        13        14
			  #      2:        13        -3
			  #      3:         9         2
			  #      4:       -26        -8
			  #      5:         1         2
			  #     ---                    
			  # 253312:       -30         1
			  # 253313:       -14        -5
			  # 253314:        16        -8
			  # 253315:        15        -4
			  # 253316:         1        -5
			  
			  DF[with(DF, x > 1), ]
			  #   x y
			  # 4 2 4
			  # 5 2 5
			  # 6 3 6
			  # 7 3 7
			  # 8 3 8
			  ```
		- select columns except `!`
		  collapsed:: true
			- ```r
			  # returns all columns except arr_delay and dep_delay
			  ans <- flights[, !c("arr_delay", "dep_delay")]
			  # or
			  ans <- flights[, -c("arr_delay", "dep_delay")]
			  # returns year,month and day
			  ans <- flights[, year:day]
			  # returns day, month and year
			  ans <- flights[, day:year]
			  # returns all columns except year, month and day
			  ans <- flights[, -(year:day)]
			  ans <- flights[, !(year:day)]
			  ```
	- Compute using `j`
	  collapsed:: true
		- ```r
		  # How many trips have had total delay < 0?
		  ans <- flights[, sum( (arr_delay + dep_delay) < 0 )]
		  ans
		  # [1] 141814
		  ```
	- Subset in `j` and do in `j`
	  collapsed:: true
		- ```r
		  ans <- flights[origin == "JFK" & month == 6L,
		                 .(m_arr = mean(arr_delay), m_dep = mean(dep_delay))]
		  #       m_arr    m_dep
		  # 1: 5.839349 9.807884
		  
		  # How many trips have been made in 2014 from “JFK” airport in the month of June?
		  ans <- flights[origin == "JFK" & month == 6L, length(dest)]
		  # [1] 8422
		  ```
		- ```r
		  # How can we concatenate columns a and b for each group in ID?
		  DT
		  #    ID a  b  c
		  # 1:  b 1  7 13
		  # 2:  b 2  8 14
		  # 3:  b 3  9 15
		  # 4:  a 4 10 16
		  # 5:  a 5 11 17
		  # 6:  c 6 12 18
		  DT[, .(val = c(a,b)), by = ID]
		  #     ID val
		  #  1:  b   1
		  #  2:  b   2
		  #  3:  b   3
		  #  4:  b   7
		  #  5:  b   8
		  #  6:  b   9
		  #  7:  a   4
		  #  8:  a   5
		  #  9:  a  10
		  # 10:  a  11
		  # 11:  c   6
		  # 12:  c  12
		  DT[, .(val = list(c(a,b))), by = ID]
		  # use list, So for each group, 
		  # we return a list of all concatenated values.
		  #    ID         val
		  # 1:  b 1,2,3,7,8,9
		  # 2:  a  4, 5,10,11
		  # 3:  c        6,12
		  
		  ## (1) look at the difference between
		  DT[, print(c(a,b)), by = ID]
		  # [1] 1 2 3 7 8 9
		  # [1]  4  5 10 11
		  # [1]  6 12
		  # Empty data.table (0 rows and 1 cols): ID
		  
		  ## (2) and
		  DT[, print(list(c(a,b))), by = ID]
		  # [[1]]
		  # [1] 1 2 3 7 8 9
		  # 
		  # [[1]]
		  # [1]  4  5 10 11
		  # 
		  # [[1]]
		  # [1]  6 12
		  # Empty data.table (0 rows and 1 cols): ID
		  
		  # in (1), for each group, a vector is returned, 
		  # with length = 6,4,2 here. 
		  # (2) returns a list of length 1 for each group, 
		  # with its first element holding vectors of length 6,4,2.
		  # Therefore (1) results in a length of 6+4+2 = 12, 
		  # whereas (2) returns 1+1+1=3.
		  ```
	- Special symbol `.N`
	  collapsed:: true
		- holds the number of rows in the **current group**
		- Note that we did not wrap .N with list() or .(). Therefore a vector is returned.
		- ```r
		  ans <- flights[origin == "JFK" & month == 6L, .N]
		  ans
		  # [1] 8422
		  ```
	- Grouping using `by`
	  collapsed:: true
		- ```r
		  # the number of trips corresponding to each origin airport?
		  ans <- flights[, .(.N), by = .(origin)]
		  ans
		  #    origin     N
		  # 1:    JFK 81483
		  # 2:    LGA 84433
		  # 3:    EWR 87400
		  
		  ## or equivalently using a character vector in 'by'
		  ans <- flights[, .(.N), by = "origin"]
		  
		  ans <- flights[carrier == "AA", .N, by = .(origin, dest)]
		  head(ans)
		  #    origin dest    N
		  # 1:    JFK  LAX 3387
		  # 2:    LGA  PBI  245
		  # 3:    EWR  LAX   62
		  # 4:    JFK  MIA 1876
		  # 5:    JFK  SEA  298
		  # 6:    EWR  MIA  848
		  
		  ## or equivalently using a character vector in 'by'
		  ans <- flights[carrier == "AA", .N, by = c("origin", "dest")]
		  ```
	- Sorted `by: keyby`
	  collapsed:: true
		- ```r
		  
		  ans <- flights[carrier == "AA",
		          .(mean(arr_delay), mean(dep_delay)),
		          keyby = .(origin, dest, month)]
		  ans
		  #      origin dest month         V1         V2
		  #   1:    EWR  DFW     1   6.427673 10.0125786
		  #   2:    EWR  DFW     2  10.536765 11.3455882
		  #   3:    EWR  DFW     3  12.865031  8.0797546
		  #   4:    EWR  DFW     4  17.792683 12.9207317
		  #   5:    EWR  DFW     5  18.487805 18.6829268
		  #  ---                                        
		  # 196:    LGA  PBI     1  -7.758621  0.3103448
		  # 197:    LGA  PBI     2  -7.865385  2.4038462
		  # 198:    LGA  PBI     3  -5.754098  3.0327869
		  # 199:    LGA  PBI     4 -13.966667 -4.7333333
		  # 200:    LGA  PBI     5 -10.357143 -6.8571429
		  ```
	- Expressions in `by`
	  collapsed:: true
		- ```r
		  ans <- flights[, .N, .(dep_delay>0, arr_delay>0)]
		  ans
		  #    dep_delay arr_delay      N
		  # 1:      TRUE      TRUE  72836
		  # 2:     FALSE      TRUE  34583
		  # 3:     FALSE     FALSE 119304
		  # 4:      TRUE     FALSE  26593
		  
		  # provide other columns along with expressions
		  DT[, .N, by = .(a, b>0)].
		  ```
	- Multiple columns in j - `.SD`
	  collapsed:: true
		- It stands for Subset of Data. It by itself is a data.table that **holds the data for the current group defined using by**.
		  collapsed:: true
			- ```r
			  DT
			  #    ID a  b  c
			  # 1:  b 1  7 13
			  # 2:  b 2  8 14
			  # 3:  b 3  9 15
			  # 4:  a 4 10 16
			  # 5:  a 5 11 17
			  # 6:  c 6 12 18
			  
			  DT[, print(.SD), by = ID]
			  #    a b  c
			  # 1: 1 7 13
			  # 2: 2 8 14
			  # 3: 3 9 15
			  #    a  b  c
			  # 1: 4 10 16
			  # 2: 5 11 17
			  #    a  b  c
			  # 1: 6 12 18
			  # Empty data.table (0 rows and 1 cols): ID
			  ```
		- `.SD` with `lapply`
		  collapsed:: true
			- ```r
			  DT[, lapply(.SD, mean), by = ID]
			  #    ID   a    b    c
			  # 1:  b 2.0  8.0 14.0
			  # 2:  a 4.5 10.5 16.5
			  # 3:  c 6.0 12.0 18.0
			  ```
		- `.SDcols`accepts either column names or column indices, ensures that .SD contains only these variables for each group
		  collapsed:: true
			- ```r
			  flights[carrier == "AA",                       ## Only on trips with carrier "AA"
			          lapply(.SD, mean),                     ## compute the mean
			          by = .(origin, dest, month),           ## for every 'origin,dest,month'
			          .SDcols = c("arr_delay", "dep_delay")] ## for just those specified in .SDcols
			  #      origin dest month  arr_delay  dep_delay
			  #   1:    JFK  LAX     1   6.590361 14.2289157
			  #   2:    LGA  PBI     1  -7.758621  0.3103448
			  #   3:    EWR  LAX     1   1.366667  7.5000000
			  #   4:    JFK  MIA     1  15.720670 18.7430168
			  #   5:    JFK  SEA     1  14.357143 30.7500000
			  #  ---                                        
			  # 196:    LGA  MIA    10  -6.251799 -1.4208633
			  # 197:    JFK  MIA    10  -1.880184  6.6774194
			  # 198:    EWR  PHX    10  -3.032258 -4.2903226
			  # 199:    JFK  MCO    10 -10.048387 -1.6129032
			  # 200:    JFK  DCA    10  16.483871 15.5161290
			  ```
		- Subset `.SD` for each group
		  collapsed:: true
			- ```r
			  ans <- flights[, head(.SD, 2), by = month]
			  head(ans)
			  #    month year day dep_delay arr_delay carrier origin dest air_time distance hour
			  # 1:     1 2014   1        14        13      AA    JFK  LAX      359     2475    9
			  # 2:     1 2014   1        -3        13      AA    JFK  LAX      363     2475   11
			  # 3:     2 2014   1        -1         1      AA    JFK  LAX      358     2475    8
			  # 4:     2 2014   1        -5         3      AA    JFK  LAX      358     2475   11
			  # 5:     3 2014   1       -11        36      AA    JFK  LAX      375     2475    8
			  # 6:     3 2014   1        -3        14      AA    JFK  LAX      368     2475   11
			  ```
- Median
	- `:=` operator
	  collapsed:: true
		- `:=` operator updates data.table columns in-place (by reference).
		- it can be used in `j` in two ways
		- ```r
		  # The LHS := RHS form
		  DT[, c("colA", "colB", ...) := list(valA, valB, ...)]
		  
		  # when you have only one column to assign to you
		  # can drop the quotes and list(), for convenience
		  DT[, colA := valA]
		  
		  # The functional form
		  DT[, `:=`(colA = valA, # valA is assigned to colA
		            colB = valB, # valB is assigned to colB
		            ...
		  )]
		  ```
	- **Add/Update/Delete** columns by reference
	  collapsed:: true
		- Add columns by reference
			- ```r
			  flights[, `:=`(speed = distance / (air_time/60), # speed in mph (mi/h)
			                 delay = arr_delay + dep_delay)]   # delay in minutes
			  head(flights)
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour    speed delay
			  # 1: 2014     1   1        14        13      AA    JFK  LAX      359     2475    9 413.6490    27
			  # 2: 2014     1   1        -3        13      AA    JFK  LAX      363     2475   11 409.0909    10
			  # 3: 2014     1   1         2         9      AA    JFK  LAX      351     2475   19 423.0769    11
			  # 4: 2014     1   1        -8       -26      AA    LGA  PBI      157     1035    7 395.5414   -34
			  # 5: 2014     1   1         2         1      AA    JFK  LAX      350     2475   13 424.2857     3
			  # 6: 2014     1   1         4         0      AA    EWR  LAX      339     2454   18 434.3363     4
			  
			  ## alternatively, using the 'LHS := RHS' form
			  flights[, c("speed", "delay") := list(distance/(air_time/60), arr_delay + dep_delay)]
			  ```
		- Replace/Update some rows of columns by reference - sub-assign by reference
			- ```r
			  # get all 'hours' in flights
			  flights[, sort(unique(hour))]
			  #  [1]  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
			  
			  # Replace those rows where hour == 24 with the value 0
			  # subassign by reference
			  flights[hour == 24L, hour := 0L]
			  ```
		- Delete column by reference
		  collapsed:: true
			- ```r
			  flights[, c("delay") := NULL]
			  head(flights)
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour    speed
			  # 1: 2014     1   1        14        13      AA    JFK  LAX      359     2475    9 413.6490
			  # 2: 2014     1   1        -3        13      AA    JFK  LAX      363     2475   11 409.0909
			  # 3: 2014     1   1         2         9      AA    JFK  LAX      351     2475   19 423.0769
			  # 4: 2014     1   1        -8       -26      AA    LGA  PBI      157     1035    7 395.5414
			  # 5: 2014     1   1         2         1      AA    JFK  LAX      350     2475   13 424.2857
			  # 6: 2014     1   1         4         0      AA    EWR  LAX      339     2454   18 434.3363
			  
			  ## or using the functional form
			  flights[, `:=`(delay = NULL)]
			  ```
		- `:=` along with grouping using `by`
		  collapsed:: true
			- ```r
			  flights[, max_speed := max(speed), by = .(origin, dest)]
			  head(flights)
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour    speed max_speed
			  # 1: 2014     1   1        14        13      AA    JFK  LAX      359     2475    9 413.6490  526.5957
			  # 2: 2014     1   1        -3        13      AA    JFK  LAX      363     2475   11 409.0909  526.5957
			  # 3: 2014     1   1         2         9      AA    JFK  LAX      351     2475   19 423.0769  526.5957
			  # 4: 2014     1   1        -8       -26      AA    LGA  PBI      157     1035    7 395.5414  517.5000
			  # 5: 2014     1   1         2         1      AA    JFK  LAX      350     2475   13 424.2857  526.5957
			  # 6: 2014     1   1         4         0      AA    EWR  LAX      339     2454   18 434.3363  518.4507
			  ```
		- Multiple columns and `:=`
		  collapsed:: true
			- ```r
			  #How can we add two more columns 
			  # computing max() of dep_delay and arr_delay 
			  # for each month, using .SD?
			  in_cols  = c("dep_delay", "arr_delay")
			  out_cols = c("max_dep_delay", "max_arr_delay")
			  flights[, c(out_cols) := lapply(.SD, max), by = month, .SDcols = in_cols]
			  head(flights)
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour    speed max_speed
			  # 1: 2014     1   1        14        13      AA    JFK  LAX      359     2475    9 413.6490  526.5957
			  # 2: 2014     1   1        -3        13      AA    JFK  LAX      363     2475   11 409.0909  526.5957
			  # 3: 2014     1   1         2         9      AA    JFK  LAX      351     2475   19 423.0769  526.5957
			  # 4: 2014     1   1        -8       -26      AA    LGA  PBI      157     1035    7 395.5414  517.5000
			  # 5: 2014     1   1         2         1      AA    JFK  LAX      350     2475   13 424.2857  526.5957
			  # 6: 2014     1   1         4         0      AA    EWR  LAX      339     2454   18 434.3363  518.4507
			  #    max_dep_delay max_arr_delay
			  # 1:           973           996
			  # 2:           973           996
			  # 3:           973           996
			  # 4:           973           996
			  # 5:           973           996
			  # 6:           973           996
			  
			  # RHS gets automatically recycled to length of LHS
			  flights[, c("speed", "max_speed", "max_dep_delay", "max_arr_delay") := NULL]
			  head(flights)
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
			  # 1: 2014     1   1        14        13      AA    JFK  LAX      359     2475    9
			  # 2: 2014     1   1        -3        13      AA    JFK  LAX      363     2475   11
			  # 3: 2014     1   1         2         9      AA    JFK  LAX      351     2475   19
			  # 4: 2014     1   1        -8       -26      AA    LGA  PBI      157     1035    7
			  # 5: 2014     1   1         2         1      AA    JFK  LAX      350     2475   13
			  # 6: 2014     1   1         4         0      AA    EWR  LAX      339     2454   18
			  ```
- Advanced
	- Keys and fast binary search (speeeeed uppppp!)
	  collapsed:: true
		- use keys to index row
		  collapsed:: true
			- ```r
			  setkey(flights, origin)
			  head(flights)
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
			  # 1: 2014     1   1         4         0      AA    EWR  LAX      339     2454   18
			  # 2: 2014     1   1        -5       -17      AA    EWR  MIA      161     1085   16
			  # 3: 2014     1   1       191       185      AA    EWR  DFW      214     1372   16
			  # 4: 2014     1   1        -1        -2      AA    EWR  DFW      214     1372   14
			  # 5: 2014     1   1        -3       -10      AA    EWR  MIA      154     1085    6
			  # 6: 2014     1   1         4       -17      AA    EWR  DFW      215     1372    9
			  
			  ## alternatively we can provide character vectors to the function 'setkeyv()'
			  setkeyv(flights, "origin") # useful to program with
			  
			  flights[.("JFK")]
			  #        year month day dep_delay arr_delay carrier origin dest air_time distance hour
			  #     1: 2014     1   1        14        13      AA    JFK  LAX      359     2475    9
			  #     2: 2014     1   1        -3        13      AA    JFK  LAX      363     2475   11
			  #     3: 2014     1   1         2         9      AA    JFK  LAX      351     2475   19
			  #     4: 2014     1   1         2         1      AA    JFK  LAX      350     2475   13
			  #     5: 2014     1   1        -2       -18      AA    JFK  LAX      338     2475   21
			  #    ---                                                                              
			  # 81479: 2014    10  31        -4       -21      UA    JFK  SFO      337     2586   17
			  # 81480: 2014    10  31        -2       -37      UA    JFK  SFO      344     2586   18
			  # 81481: 2014    10  31         0       -33      UA    JFK  LAX      320     2475   17
			  # 81482: 2014    10  31        -6       -38      UA    JFK  SFO      343     2586    9
			  # 81483: 2014    10  31        -6       -38      UA    JFK  LAX      323     2475   11
			  
			  ## alternatively
			  flights[J("JFK")] 
			  #(or) 
			  flights[list("JFK")]
			  
			  key(flights)
			  # [1] "origin"
			  ```
		- set keys for multiple columns
		  collapsed:: true
			- ```r
			  setkey(flights, origin, dest)
			  head(flights)
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
			  # 1: 2014     1   2        -2       -25      EV    EWR  ALB       30      143    7
			  # 2: 2014     1   3        88        79      EV    EWR  ALB       29      143   23
			  # 3: 2014     1   4       220       211      EV    EWR  ALB       32      143   15
			  # 4: 2014     1   4        35        19      EV    EWR  ALB       32      143    7
			  # 5: 2014     1   5        47        42      EV    EWR  ALB       26      143    8
			  # 6: 2014     1   5        66        62      EV    EWR  ALB       31      143   23
			  
			  ## or alternatively
			  # setkeyv(flights, c("origin", "dest")) # provide a character vector of column names
			  
			  key(flights)
			  # [1] "origin" "dest"
			  ```
		- combining keys with `j` and `i`
		  collapsed:: true
			- Return `arr_delay` column as a data.table corresponding to `origin = "LGA"` and `dest = "TPA"`
			- ```r
			  key(flights)
			  # [1] "origin" "dest"
			  flights[.("LGA", "TPA"), .(arr_delay)]
			  #       arr_delay
			  #    1:         1
			  #    2:        14
			  #    3:       -17
			  #    4:        -4
			  #    5:       -12
			  #   ---          
			  # 1848:        39
			  # 1849:       -24
			  # 1850:       -12
			  # 1851:        21
			  # 1852:       -11
			  ```
		- first or last match `mult`
		  collapsed:: true
			- ```r
			  # Subset only the first matching row from all rows 
			  # where origin matches “JFK” and dest matches “MIA”
			  flights[.("JFK", "MIA"), mult = "first"]
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
			  # 1: 2014     1   1         6         3      AA    JFK  MIA      157     1089    5
			  
			  
			  # Subset only the last matching row of all the rows 
			  # where origin matches “LGA”, “JFK”, “EWR” and dest matches “XNA”
			  flights[.(c("LGA", "JFK", "EWR"), "XNA"), mult = "last"]
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
			  # 1: 2014     5  23       163       148      MQ    LGA  XNA      158     1147   18
			  # 2:   NA    NA  NA        NA        NA    <NA>    JFK  XNA       NA       NA   NA
			  # 3: 2014     2   3       231       268      EV    EWR  XNA      184     1131   12
			  ```
		- make do not match return NA
		  collapsed:: true
			- ```r
			  lights[.(c("LGA", "JFK", "EWR"), "XNA"), mult = "last"]
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
			  # 1: 2014     5  23       163       148      MQ    LGA  XNA      158     1147   18
			  # 2:   NA    NA  NA        NA        NA    <NA>    JFK  XNA       NA       NA   NA
			  # 3: 2014     2   3       231       268      EV    EWR  XNA      184     1131   12
			  
			  # From the previous example, Subset all rows only if there’s a match
			  flights[.(c("LGA", "JFK", "EWR"), "XNA"), mult = "last", nomatch = NULL]
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
			  # 1: 2014     5  23       163       148      MQ    LGA  XNA      158     1147   18
			  # 2: 2014     2   3       231       268      EV    EWR  XNA      184     1131   12
			  
			  ```
		-
	- Secondary indices (fast subset)
	  collapsed:: true
		- Why have secondary indices?
		  collapsed:: true
			- setkey() requires: computing the order vector for the column(s) provided, here, origin, and
			- reordering the entire data.table, by reference, based on the order vector computed.
			- Secondary indices are similar to `keys`, but
				- It doesn’t physically reorder the entire data.table in RAM. Instead, it only computes the order for the set of columns provided and stores that order vector in an additional attribute called index.
				- There can be more than one secondary index for a data.table
		- Set and get and remove secondary indices
		  collapsed:: true
			- ```r
			  setindex(flights, origin)
			  head(flights)
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
			  # 1: 2014     1   1        14        13      AA    JFK  LAX      359     2475    9
			  # 2: 2014     1   1        -3        13      AA    JFK  LAX      363     2475   11
			  # 3: 2014     1   1         2         9      AA    JFK  LAX      351     2475   19
			  # 4: 2014     1   1        -8       -26      AA    LGA  PBI      157     1035    7
			  # 5: 2014     1   1         2         1      AA    JFK  LAX      350     2475   13
			  # 6: 2014     1   1         4         0      AA    EWR  LAX      339     2454   18
			  
			  ## alternatively we can provide character vectors to the function 'setindexv()'
			  # setindexv(flights, "origin") # useful to program with
			  
			  # 'index' attribute added
			  names(attributes(flights))
			  # [1] "names"             "row.names"         "class"             ".internal.selfref"
			  # [5] "index"
			  
			  # remove all secondary indices.
			  setindex(flights, NULL)
			  
			  indices(flights)
			  # [1] "origin"
			  
			  setindex(flights, origin, dest)
			  indices(flights)
			  # [1] "origin"       "origin__dest"
			  # Note that by creating another index on the columns 
			  # origin, dest, we do not lose the first index created on the column origin, 
			  # i.e., we can have multiple secondary indices.
			  ```
		- Fast subsetting using `on` and secondary indices
		  collapsed:: true
			- ```r
			  # subset all rows when the origin airport matches "JFK"
			  flights["JFK", on = "origin"]
			  # This statement performs a fast binary search based subset as well, 
			  # by computing the index on the fly. 
			  # However, note that it doesn’t save the index as an attribute automatically. 
			  # This may change in the future.
			  
			  
			  # If we had already created a secondary index, using setindex(), 
			  # then on would reuse it instead of (re)computing it. 
			  # We can see that by using verbose = TRUE:
			  setindex(flights, origin)
			  flights["JFK", on = "origin", verbose = TRUE][1:5]
			  # i.V1 has same type (character) as x.origin. No coercion needed.
			  # on= matches existing index, using index
			  # Starting bmerge ...
			  # forder.c received 1 rows and 1 columns
			  # bmerge done in 0.000s elapsed (0.001s cpu) 
			  # Constructing irows for '!byjoin || nqbyjoin' ... 0.000s elapsed (0.000s cpu)
			  #    year month day dep_delay arr_delay carrier origin dest air_time distance hour
			  # 1: 2014     1   1        14        13      AA    JFK  LAX      359     2475    9
			  # 2: 2014     1   1        -3        13      AA    JFK  LAX      363     2475   11
			  # 3: 2014     1   1         2         9      AA    JFK  LAX      351     2475   19
			  # 4: 2014     1   1         2         1      AA    JFK  LAX      350     2475   13
			  # 5: 2014     1   1        -2       -18      AA    JFK  LAX      338     2475   21
			  
			  
			  ```
		- Using `on` and `j` with indexing
		  collapsed:: true
			- ```r
			  flights[.("LGA", "TPA"), .(arr_delay), on = c("origin", "dest")]
			  #       arr_delay
			  #    1:         1
			  #    2:        14
			  #    3:       -17
			  #    4:        -4
			  #    5:       -12
			  #   ---          
			  # 1848:        39
			  # 1849:       -24
			  # 1850:       -12
			  # 1851:        21
			  # 1852:       -11
			  
			  # Find the maximum arrival delay corresponding to 
			  # origin = "LGA" and dest = "TPA".
			  flights[.("LGA", "TPA"), max(arr_delay), on = c("origin", "dest")]
			  # [1] 486
			  ```
		- sub-assign by reference using `:=` in `j`
		  collapsed:: true
			- ((6212e128-6e1e-40b6-a7c6-0bc25805464e))
			- ```r
			  # get all 'hours' in flights
			  flights[, sort(unique(hour))]
			  #  [1]  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
			  
			  # replace 24 with 0
			  flights[.(24L), hour := 0L, on = "hour"]
			  ```
		- Aggregation using `by`
		  collapsed:: true
			- ```r
			  # Get the maximum departure delay for each month corresponding 
			  # to origin = "JFK". Order the result by month
			  ans <- flights["JFK", max(dep_delay), keyby = month, on = "origin"]
			  head(ans)
			  #    month   V1
			  # 1:     1  881
			  # 2:     2 1014
			  # 3:     3  920
			  # 4:     4 1241
			  # 5:     5  853
			  # 6:     6  798
			  ```
	- Auto indexing
	  collapsed:: true
		- when using `==` or `%in%`, a secondary index created automatically
		  collapsed:: true
			- ```r
			  ## have a look at all the attribute names
			  names(attributes(dt))
			  # [1] "names"             "row.names"         "class"             ".internal.selfref"
			  
			  ## run thefirst time
			  (t1 <- system.time(ans <- dt[x == 989L]))
			  #    user  system elapsed 
			  #   0.538   0.015   0.097
			  head(ans)
			  #      x         y
			  # 1: 989 0.7757157
			  # 2: 989 0.6813302
			  # 3: 989 0.2815894
			  # 4: 989 0.4954259
			  # 5: 989 0.7885886
			  # 6: 989 0.5547504
			  
			  ## secondary index is created
			  names(attributes(dt))
			  # [1] "names"             "row.names"         "class"             ".internal.selfref"
			  # [5] "index"
			  
			  indices(dt)
			  # [1] "x"
			  
			  ## successive subsets
			  (t2 <- system.time(dt[x == 989L]))
			  #    user  system elapsed 
			  #   0.001   0.001   0.001
			  system.time(dt[x %in% 1989:2012])
			  #    user  system elapsed 
			  #   0.001   0.000   0.001
			  ```
	- Efficient reshaping
	  collapsed:: true
		- `melt` data.tables (wide to long)
		  collapsed:: true
			- ```r
			  DT <- fread(s1)
			  DT
			  #    family_id age_mother dob_child1 dob_child2 dob_child3
			  # 1:         1         30 1998-11-26 2000-01-29       <NA>
			  # 2:         2         27 1996-06-22       <NA>       <NA>
			  # 3:         3         26 2002-07-11 2004-04-05 2007-09-02
			  # 4:         4         32 2004-10-10 2009-08-27 2012-07-21
			  # 5:         5         29 2000-12-05 2005-02-28       <NA>
			  ## dob stands for date of birth.
			  ```
			- ```r
			  DT.m1 = melt(DT, id.vars = c("family_id", "age_mother"),
			                  measure.vars = c("dob_child1", "dob_child2", "dob_child3"))
			  DT.m1
			  #     family_id age_mother   variable      value
			  #  1:         1         30 dob_child1 1998-11-26
			  #  2:         2         27 dob_child1 1996-06-22
			  #  3:         3         26 dob_child1 2002-07-11
			  #  4:         4         32 dob_child1 2004-10-10
			  #  5:         5         29 dob_child1 2000-12-05
			  #  6:         1         30 dob_child2 2000-01-29
			  #  7:         2         27 dob_child2       <NA>
			  #  8:         3         26 dob_child2 2004-04-05
			  #  9:         4         32 dob_child2 2009-08-27
			  # 10:         5         29 dob_child2 2005-02-28
			  # 11:         1         30 dob_child3       <NA>
			  # 12:         2         27 dob_child3       <NA>
			  # 13:         3         26 dob_child3 2007-09-02
			  # 14:         4         32 dob_child3 2012-07-21
			  # 15:         5         29 dob_child3       <NA>
			  str(DT.m1)
			  # Classes 'data.table' and 'data.frame':    15 obs. of  4 variables:
			  #  $ family_id : int  1 2 3 4 5 1 2 3 4 5 ...
			  #  $ age_mother: int  30 27 26 32 29 30 27 26 32 29 ...
			  #  $ variable  : Factor w/ 3 levels "dob_child1","dob_child2",..: 1 1 1 1 1 2 2 2 2 2 ...
			  #  $ value     : IDate, format: "1998-11-26" "1996-06-22" "2002-07-11" ...
			  #  - attr(*, ".internal.selfref")=<externalptr>
			  
			  # if you want to change the variable name
			  DT.m1 = melt(DT, measure.vars = c("dob_child1", "dob_child2", "dob_child3"),
			                 variable.name = "child", value.name = "dob")
			  DT.m1
			  #     family_id age_mother      child        dob
			  #  1:         1         30 dob_child1 1998-11-26
			  #  2:         2         27 dob_child1 1996-06-22
			  #  3:         3         26 dob_child1 2002-07-11
			  #  4:         4         32 dob_child1 2004-10-10
			  #  5:         5         29 dob_child1 2000-12-05
			  #  6:         1         30 dob_child2 2000-01-29
			  #  7:         2         27 dob_child2       <NA>
			  #  8:         3         26 dob_child2 2004-04-05
			  #  9:         4         32 dob_child2 2009-08-27
			  # 10:         5         29 dob_child2 2005-02-28
			  # 11:         1         30 dob_child3       <NA>
			  # 12:         2         27 dob_child3       <NA>
			  # 13:         3         26 dob_child3 2007-09-02
			  # 14:         4         32 dob_child3 2012-07-21
			  # 15:         5         29 dob_child3       <NA>
			  ```
		- `dcast` data.table (long to wide)
		  collapsed:: true
			- ```r
			  dcast(DT.m1, family_id + age_mother ~ child, value.var = "dob")
			  #    family_id age_mother dob_child1 dob_child2 dob_child3
			  # 1:         1         30 1998-11-26 2000-01-29       <NA>
			  # 2:         2         27 1996-06-22       <NA>       <NA>
			  # 3:         3         26 2002-07-11 2004-04-05 2007-09-02
			  # 4:         4         32 2004-10-10 2009-08-27 2012-07-21
			  # 5:         5         29 2000-12-05 2005-02-28       <NA>
			  
			  # Starting from DT.m, 
			  # how can we get the number of children in each family?
			  dcast(DT.m1, family_id ~ ., fun.agg = function(x) sum(!is.na(x)), value.var = "dob")
			  #    family_id .
			  # 1:         1 2
			  # 2:         2 1
			  # 3:         3 3
			  # 4:         4 3
			  # 5:         5 2
			  ```
		- enhanced `melt` for multiple columns simultaneously
		  collapsed:: true
			- ```r
			  colA = paste("dob_child", 1:3, sep = "")
			  colB = paste("gender_child", 1:3, sep = "")
			  DT.m2 = melt(DT, measure = list(colA, colB), value.name = c("dob", "gender"))
			  DT.m2
			  #     family_id age_mother variable        dob gender
			  #  1:         1         30        1 1998-11-26      1
			  #  2:         2         27        1 1996-06-22      2
			  #  3:         3         26        1 2002-07-11      2
			  #  4:         4         32        1 2004-10-10      1
			  #  5:         5         29        1 2000-12-05      2
			  #  6:         1         30        2 2000-01-29      2
			  #  7:         2         27        2       <NA>     NA
			  #  8:         3         26        2 2004-04-05      2
			  #  9:         4         32        2 2009-08-27      1
			  # 10:         5         29        2 2005-02-28      1
			  # 11:         1         30        3       <NA>     NA
			  # 12:         2         27        3       <NA>     NA
			  # 13:         3         26        3 2007-09-02      1
			  # 14:         4         32        3 2012-07-21      1
			  # 15:         5         29        3       <NA>     NA
			  
			  str(DT.m2) ## col type is preserved
			  # Classes 'data.table' and 'data.frame':    15 obs. of  5 variables:
			  #  $ family_id : int  1 2 3 4 5 1 2 3 4 5 ...
			  #  $ age_mother: int  30 27 26 32 29 30 27 26 32 29 ...
			  #  $ variable  : Factor w/ 3 levels "1","2","3": 1 1 1 1 1 2 2 2 2 2 ...
			  #  $ dob       : IDate, format: "1998-11-26" "1996-06-22" "2002-07-11" ...
			  #  $ gender    : int  1 2 2 1 2 2 NA 2 1 1 ...
			  #  - attr(*, ".internal.selfref")=<externalptr>
			  ```
			-
		- using `patterns()` in enhanced `melt`
		  collapsed:: true
			- ```r
			  DT.m2 = melt(DT, measure = patterns("^dob", "^gender"), value.name = c("dob", "gender"))
			  DT.m2
			  #     family_id age_mother variable        dob gender
			  #  1:         1         30        1 1998-11-26      1
			  #  2:         2         27        1 1996-06-22      2
			  #  3:         3         26        1 2002-07-11      2
			  #  4:         4         32        1 2004-10-10      1
			  #  5:         5         29        1 2000-12-05      2
			  #  6:         1         30        2 2000-01-29      2
			  #  7:         2         27        2       <NA>     NA
			  #  8:         3         26        2 2004-04-05      2
			  #  9:         4         32        2 2009-08-27      1
			  # 10:         5         29        2 2005-02-28      1
			  # 11:         1         30        3       <NA>     NA
			  # 12:         2         27        3       <NA>     NA
			  # 13:         3         26        3 2007-09-02      1
			  # 14:         4         32        3 2012-07-21      1
			  # 15:         5         29        3       <NA>     NA
			  ```
		- enhanced `dcast` casting multiple `value.var` simultaneously
		  collapsed:: true
			- ```r
			  ## new 'cast' functionality - multiple value.vars
			  DT.c2 = dcast(DT.m2, family_id + age_mother ~ variable, value.var = c("dob", "gender"))
			  DT.c2
			  #    family_id age_mother      dob_1      dob_2      dob_3 gender_1 gender_2 gender_3
			  # 1:         1         30 1998-11-26 2000-01-29       <NA>        1        2       NA
			  # 2:         2         27 1996-06-22       <NA>       <NA>        2       NA       NA
			  # 3:         3         26 2002-07-11 2004-04-05 2007-09-02        2        2        1
			  # 4:         4         32 2004-10-10 2009-08-27 2012-07-21        1        1        1
			  # 5:         5         29 2000-12-05 2005-02-28       <NA>        2        1       NA
			  ```
- Summary
	- Using `j`
	  collapsed:: true
		- As long as `j` returns a list, **each element of the list will become a column** in the resulting data.table
		- Select columns the data.table way: `DT[, .(colA, colB)]`.
		- Select columns the data.frame way: `DT[, c("colA", "colB")]`.
		- Compute on columns: `DT[, .(sum(colA), mean(colB))]`.
		- Provide names if necessary: `DT[, .(sA =sum(colA), mB = mean(colB))]`.
		- Combine with `i`: `DT[colA > value, sum(colB)]`.
	- Using`by`
	  collapsed:: true
		- `DT[, lapply(.SD, fun), by = ..., .SDcols = ...]` - applies `fun` to all columns specified in `.SDcols` while grouping by the columns specified in `by`.
		- `DT[, head(.SD, 2), by = ...]` - return the first two rows for each group.
		- `DT[col > val, head(.SD, 1), by = ...]` - combine `i` along with `j` and `by`.
	- `:=` operator
	  collapsed:: true
		- It is used to **add/update/delete** columns by reference.
		- We have also seen how to use `:=` along with `i` and `by` the same way as we have seen in the Introduction to data.table vignette. We can in the same way use `keyby`, chain operations together, and pass expressions to `by` as well all in the same way. The syntax is consistent.
		- We can use `:=` for its side effect or use `copy()` to not modify the original object while updating by reference.
	- Keys
	  collapsed:: true
		- subset using keys which fetches row indices in `i`, but **much faster.**
		- combine key based subsets with `j` and `by`. Note that the j and by operations are exactly the same as before.
		- Key based subsets are incredibly fast and are particularly useful when the task involves **repeated subsetting**. But it may not be always desirable to set key and physically reorder the data.table.