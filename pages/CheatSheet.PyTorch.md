title:: CheatSheet/PyTorch

- {{renderer :tocgen,[[]],2}}
- Trick
	- 节省内存
		- 变量赋值原地更新
			- example
			  collapsed:: true
				- ```python
				  before = id(Y) 
				  Y=Y+X 
				  id(Y) == before # False
				  
				  ```
			- solution (使用切片)
			  collapsed:: true
				- ```python
				  Y = torch.tensor([[2.0, 1, 4, 3], [1, 2, 3, 4], [4, 3, 2, 1]])
				  X = torch.arange(12, dtype=torch.float32).reshape((3,4))
				  
				  Z = torch.zeros_like(Y)
				  print('id(Z):', id(Z)) # 139675260544480
				  Z[:] = X + Y
				  print('id(Z):', id(Z)) # 139675260544480
				  
				  #如果在后续计算中没有重复使用X, 使用:
				  X[:] = X + Y
				  X += Y
				  ```