title:: CheatSheet/SQL/SQlite

- Date and time
	- `strftime`
	  collapsed:: true
		- `strftime(format_string, time_string [, modifier, ...])`
		- |Format|Description|
		  |--|--|
		  |%d|day of the month: 01-31|
		  |%f|fractional seconds: SS.SSS|
		  |%H|hour: 00-24|
		  |%j|day of the year: 001-366|
		  |%J|Julian day number|
		  |%m|month: 01-12|
		  |%M|minute: 00-59|
		  |%s|seconds since 1970-01-01|
		  |%S|seconds: 00-59|
		  |%w|day of week 0-6 with Sunday == 0|
		  |%W|week of the year: 00-53|
		  |%Y|year: 0000-9999|
		  |%%|%|
		- |Function|Equivalent `strftime()`|
		  |--|--|
		  |`date(...)`|`strftime("%Y-%m-%d", ...)`|
		  |`time(...)`|`strftime("%Y-%m-%d", ...)`|
		  |`datetime(...)`|`strftime("%Y-%m-%d", ...)`|
		  |`julianday(...)`|`strftime("%Y-%m-%d", ...)`|
- python读取sqlite
	- 链接
		- ```python
		  import sqlite3
		  con = sqlite3.connect('xxx.db')
		  cur = con.cursor()
		  ```
	- 获取
		- ```python
		  data_table = cur.execute('''
		  	select *
		      from datamart
		  ''').fetchall()
		  datamart = pd.DataFrame(data_table)
		  ```
- [[Bugs]]
	- Description
		- build data mart 的时候用 sqlite insert into 命令: foreign key constraint failed
	- How to fix
		- 在fact table中的一个FK有问题, 再LEFT JOIN一个表, 用那个表去insert