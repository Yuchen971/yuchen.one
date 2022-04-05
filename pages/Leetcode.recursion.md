title:: Leetcode/recursion

- Add Digits #card 
  difficulty:: easy
  technique:: recursion
  number:: 258
  collapsed:: true
	- question
	  collapsed:: true
		- Given an integer num, repeatedly add all its digits until the result has only one digit, and return it.
	- examples
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
			    	assert n >= 0 and int(n) == n,
			      if num == 0:
			          return num
			      return num%10 + addDigits(num//10)
			  
			  addDigits(12345) # 15
			  ```
- Pow(x,n) #card 
  difficulty:: medium
  technique:: recursion
  number:: 50
  collapsed:: true
	- question
	  collapsed:: true
		- Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e., $x^n$).
	- examples
	  collapsed:: true
		- Input: x = 2.00000, n = 10
		  Output: 1024.00000
		- Input: x = 2.10000, n = 3
		  Output: 9.26100
		- Input: x = 2.00000, n = -2
		  Output: 0.25000
		  Explanation: $2^{-2} = \frac{1}{2}^2 = \frac{1}{4} = 0.25$
	- constraints
	  collapsed:: true
		- -100.0 < x < 100.0
		- -2^31 <= n <= 2^31-1
		- -10^4 <= x^n <= 10^4
	- First attempt
	  collapsed:: true
		- $x^n = x * x^{n-1}$
		- ```python
		  def pow(x, n):
		      if n == 0:
		          return 1
		      if n == 1:
		          return x
		      if n != 1 and n > 0:
		          return x * pow(x, n-1)
		  
		  pow(2,2)
		  ```
		- what if n is negative?
	- Solution 1 普通递归 (超时)
	  collapsed:: true
		- 思路
			- 如果想求 x^4, 可以求 (x^2)^2. 如果是奇数, x^5 = x * (x^2)^2
			- 将n地板除2, 设结果为a, 那么 pow(x,n) = pow(x, a) * pow(x, n-a)
			  $$
			  \begin{align*}
			  x^4 = (x^2)^2 = x^2 * x^2\\
			  x^5 = x*(x^2)^2 = x^3 * x^2\\
			  x^6 = (x^2)^3 = x^3 * x^3\\
			  x^7 = x*(x^2)^3 = x^3 * x^4\\
			  x^8 = ((x^2)^2)^2 = x^4 * x^4
			  \end{align*}
			  $$
			-
		- Answer
			- ```python
			  def pow(x,n):
			      if n == 0:
			          return 1
			      if n == 1:
			          return x
			      if n < 0:
			          return 1/pow(x, -n)
			      return pow(x, n//2) * pow(x, n-n//2)
			  ```
	- Solution 2 优化递归
	  collapsed:: true
		- 思路
			- 上面的解法每次直接pow()都会调用自己两次, 考虑只调用一次
			- 如果n是偶数, n折半, 底数变为 x^2
			- 如果n是奇数, n-1, 底数不变, 得到的结果再乘底数x
		- Answer
			- ```python
			  class Solution:
			      def myPow(self, x: float, n: int) -> float:
			          def quick_pow(N):
			              if N == 0:
			                  return 1.0
			              y = quick_pow(N // 2)
			              return y * y if N % 2 == 0 else y * y * x
			  
			          return quick_pow(n) if n >= 0 else 1.0 / quick_pow(-n)
			  ```
- Find GCD #card 
  difficulty:: easy
  technique:: recursion
  number:: 1979
  collapsed:: true
	- question
		- Given an integer array nums, return the greatest common divisor of the smallest number and largest number in nums.
		- The greatest common divisor of two numbers is the largest positive integer that evenly divides both numbers.
	- examples
		- Input: nums = [2,5,6,9,10]
		  Output: 2
		  Explanation:
		  The smallest number in nums is 2.
		  The largest number in nums is 10.
		  The greatest common divisor of 2 and 10 is 2.
		- Input: nums = [7,5,6,8,3]
		  Output: 1
		  The smallest number in nums is 3.
		  The largest number in nums is 8.
		  The greatest common divisor of 3 and 8 is 1.
	- constraints
		- 2 <= nums.length <= 1000
		- 1 <= nums[i] <= 1000
	- First attempt
		- 思路
			- use [[GCD]]
		- Answer
			- ```python
			  def Findgcd(nums):
			      def gcd(mx, mn):
			          if mn == 0:
			              return mx
			          else:
			              return gcd(mn, mx%mn)
			      mx, mn = max(nums), min(nums)
			      return gcd(mx, mn)
			  
			  Findgcd([2,5,6,9,10])
			  ```
- Complement of Base 10 Integer #card 
  difficulty:: easy
  technique:: recursion
  number:: 1009
  collapsed:: true
	- question
		- The complement of an integer is the integer you get when you flip all the 0's to 1's and all the 1's to 0's in its binary representation.
	- examples
		- Input: n = 5
		  Output: 2
		  Explanation: 5 is "101" in binary, with complement "010" in binary, which is 2 in base-10.
		- Input: n = 7
		  Output: 0
		  Explanation: 7 is "111" in binary, with complement "000" in binary, which is 0 in base-10.
		- Input: n = 10
		  Output: 5
		  Explanation: 10 is "1010" in binary, with complement "0101" in binary, which is 5 in base-10.
	- Constrains
		- 0 <= n < 10^9
	- First attempt
	  collapsed:: true
		- 思路
		  collapsed:: true
			- [[二进制]]
		- Answer
		  collapsed:: true
			- 和答案倒过来了
			- ```python
			  def toBinary(num):
			      if num == 0:
			          return None
			      print(num%2)
			      return toBinary(num//2)
			  
			  toBinary(13)
			  #1
			  #0
			  #1
			  #1
			  ```
	- Second attempt
	  collapsed:: true
		- ```python
		  def toBinary(num):
		      if num == 0:
		          return 0
		      return num%2 + 10*toBinary(num//2)
		  
		  toBinary(13) # => 1101
		  
		  def toBase10(num):
		      l = len(num)-1
		      if l == 0 and int(num) == 1:
		          return 1
		      if l == 0 and int(num) == 0:
		          return 0
		      return int(num[0])*pow(2,l) + toBase10(num[1:])
		  toBase10('1101') # => 13
		  ```
	- Solution 1
		- Answer
			- ```python
			  class Solution:
			      def bitwiseComplement(self, n: int) -> int:
			          list_two_num = list(bin(n).replace('0b',''))
			          for i in range(len(list_two_num)):
			              if list_two_num[i] == '0':
			                  list_two_num[i] = '1'
			              else:
			                  list_two_num[i] = '0'
			          res = ''.join(list_two_num)
			          return(int(res,2))
			  
			  ```
-