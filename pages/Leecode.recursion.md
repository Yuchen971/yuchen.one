title:: Leecode/recursion

- Add Digits
  difficulty:: easy
  technique:: recursion
  number:: 258
  collapsed:: true
	- Given an integer num, repeatedly add all its digits until the result has only one digit, and return it.
	- example
	  collapsed:: true
		- Input: num = 38
		  Output: 2
		  Explanation: The process is
		  38 --> 3 + 8 --> 11
		  11 --> 1 + 1 --> 2 
		  Since 2 has only one digit, return it.
		- Input: num = 0
		  Output: 0
	- constrains
	  collapsed:: true
		- 0 <= num <= 2^31 - 1
	- Solution 1
	  collapsed:: true
		- 思路
			- 233 // 10 = 23
			  233 % 10 = 3 -> 得到个位数
			- 23 // 10 = 2 
			  23 % 10 = 3 -> 得到个位数
			- 2 // 10 = 0
			  2 % 10 = 2 -> 得到个位数
		- Answer
			- ```python
			  def addDigits(num):
			      if num == 0:
			          return num
			      return num%10 + addDigits(num//10)
			  
			  addDigits(12345) # 15
			  ```
-