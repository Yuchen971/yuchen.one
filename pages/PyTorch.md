language:: Python
type:: package

- {{renderer :tocgen, [[]],2}}
- Basic
	- 数据操作
	  collapsed:: true
		- reshape
		  collapsed:: true
			- ```python
			  x = torch.arange(12) # 创建一个行向量x
			  # tensor([0, 1, 2, 3, 4, 5, 6, 7, 8, 9,10,11])
			  X = x.reshape(3,4) # (12,)行向量 -> (3,4)矩阵
			  #tensor([[ 0, 1, 2, 3], 
			  #        [4, 5, 6, 7],
			  #        [ 8,  9, 10, 11]])
			  
			  # 或者使其自动计算
			  x.reshape(-1, 4) #4列, x.reshape(3, -1): 三行
			  ```
		- zeros (创建全0, 全1的tensor)
		  collapsed:: true
			- ```python
			  torch.zeros((2,3,4))
			  torch.ones((2,3,4))
			  
			  # 通过从某个特定的概率分布中随机采样来得到张量中每个元素的值
			  # 以下代码创建一个形状为(3,4)的张量
			  # 其中的每个元素都从均值为0, 标准差为1 的标准高斯分布(正态分布)中随机采样
			  torch.randn(3,4)
			  ```
		- concatenate tensor
		  collapsed:: true
			- ```python
			  X = torch.arange(12, dtype=torch.float32).reshape((3,4))
			  Y = torch.tensor([[2.0, 1, 4, 3], [1, 2, 3, 4], [4, 3, 2, 1]])
			  torch.cat((X, Y), dim=0) # shape: 3,4
			  #tensor([[ 0.,  1.,  2.,  3.],
			  #         [ 4.,  5.,  6.,  7.],
			  #         [ 8.,  9., 10., 11.],
			  #         [ 2.,  1.,  4.,  3.],
			  #         [ 1.,  2.,  3.,  4.],
			  #         [ 4.,  3.,  2.,  1.]]),
			  torch.cat((X, Y), dim=1) # shape: 3,4
			  #tensor([[ 0.,  1.,  2.,  3.,  2.,  1.,  4.,  3.],
			  #         [ 4.,  5.,  6.,  7.,  1.,  2.,  3.,  4.],
			  #         [ 8.,  9., 10., 11.,  4.,  3.,  2.,  1.]]))
			  
			  # 可以看到, 第一个输出张量轴-0⻓度的总和是3+3 = 6
			  # 第二个输出输出张量的轴-1⻓度是 4+4 = 8
			  ```
		- X==Y
		  collapsed:: true
			- ```python
			  X = torch.arange(12, dtype=torch.float32).reshape((3,4))
			  Y = torch.tensor([[2.0, 1, 4, 3], [1, 2, 3, 4], [4, 3, 2, 1]])
			  X == Y
			  #tensor([[False,  True, False,  True],
			  #        [False, False, False, False],
			  #        [False, False, False, False]])
			  ```
		- sum() 所有元素求和
		  collapsed:: true
			- 得到一个单元素tensor
		- 索引切片
		  collapsed:: true
			- ```python
			  X = torch.arange(12, dtype=torch.float32).reshape((3,4))
			  #tensor([[ 0.,  1.,  2.,  3.],
			  #         [ 4.,  5.,  6.,  7.],
			  #         [ 8.,  9., 10., 11.]])
			  X[-1] # 最后一个元素
			  # tensor([ 8.,  9., 10., 11.])
			  X[1:3] # 第二个和第三个元素
			  # tensor([[ 4.,  5.,  6.,  7.],
			  #        [ 8.,  9., 10., 11.]])
			  X[1,2] # 6.
			  ```
	- 运算
	  collapsed:: true
		- +,-,\*,/,** => 按元素计算
		  collapsed:: true
			- ```python
			  x = torch.tensor([1.0, 2, 4, 8])
			  y = torch.tensor([2, 2, 2, 2]) 
			  x+y #tensor([ 3.,  4.,  6., 10.])
			  
			  # 或者
			  torch.exp(x)
			  # tensor([2.7183e+00, 7.3891e+00, 5.4598e+01, 2.9810e+03])
			  ```
		- 求和
		  collapsed:: true
			- 默认情况下调用求和函数会沿所有的轴降低张量的维度, 使它变为一个标量
			- 为了通过求和所有行的元素来降维(轴0), 我们可以在调用函数时指定axis=0.
			  由于输入矩阵沿0轴降维以生成输出向量, 因此输入轴0的维数在输出形状中消失
			- ```python
			  A = torch.arange(20, dtype=torch.float32).reshape(5, 4)
			  #tensor([[ 0.,  1.,  2.,  3.],
			  #         [ 4.,  5.,  6.,  7.],
			  #         [ 8.,  9., 10., 11.],
			  #         [12., 13., 14., 15.],
			  #         [16., 17., 18., 19.]])
			  
			  A_sum_axis0 = A.sum(axis=0)
			  A_sum_axis0, A_sum_axis0.shape
			  # (tensor([40., 45., 50., 55.]), torch.Size([4]))
			  A_sum_axis1 = A.sum(axis=1)
			  A_sum_axis1, A_sum_axis1.shape
			  # (tensor([ 6., 22., 38., 54., 70.]), torch.Size([5]))
			  ```
		- 非降维求和 (可以广播)
		  collapsed:: true
			- ```python
			  A = torch.arange(20, dtype=torch.float32).reshape(5, 4)
			  #tensor([[ 0.,  1.,  2.,  3.],
			  #         [ 4.,  5.,  6.,  7.],
			  #         [ 8.,  9., 10., 11.],
			  #         [12., 13., 14., 15.],
			  #         [16., 17., 18., 19.]])
			  
			  sum_A = A.sum(axis=1, keepdims=True)
			  sum_A
			  #tensor([[ 6.],
			  #        [22.],
			  #        [38.],
			  #        [54.],
			  #        [70.]])
			  # 可以通过广播将A除以sum_A
			  A / sum_A
			  #tensor([[0.0000, 0.1667, 0.3333, 0.5000],
			  #        [0.1818, 0.2273, 0.2727, 0.3182],
			  #        [0.2105, 0.2368, 0.2632, 0.2895],
			  #        [0.2222, 0.2407, 0.2593, 0.2778],
			  #        [0.2286, 0.2429, 0.2571, 0.2714]])
			  ```
		- 某一axis累计总和
		  collapsed:: true
			- ```python
			  A = torch.arange(20, dtype=torch.float32).reshape(5, 4)
			  #tensor([[ 0.,  1.,  2.,  3.],
			  #         [ 4.,  5.,  6.,  7.],
			  #         [ 8.,  9., 10., 11.],
			  #         [12., 13., 14., 15.],
			  #         [16., 17., 18., 19.]])
			  
			  A.cumsum(axis=0)
			  #tensor([[ 0.,  1.,  2.,  3.],
			  #        [ 4.,  6.,  8., 10.],
			  #        [12., 15., 18., 21.],
			  #        [24., 28., 32., 36.],
			  #        [40., 45., 50., 55.]])
			  ```
		- ((62479ef9-b5e9-4db5-b9a1-9bd6d872cd33))
		  collapsed:: true
			- ```python
			  x = torch.arange(4, dtype=torch.float32)
			  x
			  # tensor([0., 1., 2., 3.])
			  y = torch.ones(4, dtype = torch.float32)
			  x, y, torch.dot(x, y)
			  # (tensor([0., 1., 2., 3.]), tensor([1., 1., 1., 1.]), tensor(6.))
			  #也可以
			  torch.sum(x * y)
			  ```
		- ((62479ef9-0cff-4d23-9ef2-89a801244bce))
		  collapsed:: true
			- 注意, $\mathbf{A}$ 的列维数(沿轴1的⻓度) 必须与$\mathbf{x}$的维数(其⻓度)相同
			- ```python
			  A = torch.arange(20, dtype=torch.float32).reshape(5, 4)
			  #tensor([[ 0.,  1.,  2.,  3.],
			  #         [ 4.,  5.,  6.,  7.],
			  #         [ 8.,  9., 10., 11.],
			  #         [12., 13., 14., 15.],
			  #         [16., 17., 18., 19.]])
			  x = torch.arange(4, dtype=torch.float32)
			  # tensor([0., 1., 2., 3.]) 列向量!!
			  
			  A.shape, x.shape, torch.mv(A, x)
			  # (torch.Size([5, 4]), torch.Size([4]), tensor([ 14.,  38.,  62.,  86., 110.]))
			  ```
		- ((62479ef9-dc1b-437b-b537-dfa297d04bbe))
		  collapsed:: true
			- 仅当第一个矩阵的列数(column, axis=1)和另一个矩阵的行数(row, axis=0)相等时才能定义
			- ```python
			  A = torch.arange(20, dtype=torch.float32).reshape(5, 4)
			  #tensor([[ 0.,  1.,  2.,  3.],
			  #         [ 4.,  5.,  6.,  7.],
			  #         [ 8.,  9., 10., 11.],
			  #         [12., 13., 14., 15.],
			  #         [16., 17., 18., 19.]])
			  B = torch.ones(4,3)
			  #tensor([[1., 1., 1.],
			  #        [1., 1., 1.],
			  #        [1., 1., 1.],
			  #        [1., 1., 1.])
			  torch.mm(A, B)
			  #tensor([[ 6.,  6.,  6.],
			  #        [22., 22., 22.],
			  #        [38., 38., 38.],
			  #        [54., 54., 54.],
			  #        [70., 70., 70.]])
			  ```
		- [[范数/L2范数]]
		  collapsed:: true
			- ```python
			  u = torch.tensor([3.0, -4.0])
			  torch.norm(u)
			  # tensor(5.)
			  ```
		- [[范数/L1范数]]
		  collapsed:: true
			- ```python
			  torch.abs(u).sum()
			  # tensor(7.)
			  ```
		- [[范数/Frobenius范数]]
		  collapsed:: true
			- ```python
			  torch.norm(torch.ones((4, 9)))
			  # tensor(6.)
			  ```
	- 广播机制
	  collapsed:: true
		- definition
		  collapsed:: true
			- 即使形状不同, 可以通过调用广播机制(broadcasting mechanism)来执行按元素操作:
			  通过适当复制元素来扩展一个或两个数组, 以便在转换之后, 两个张量具有相同的形状.其次对生成的数组执行按元素操作
			- 运算结果的shape是:A.shape和B.shape对应位置的最大值, 如果x和y的维数不等, 在维数较少的张量上添加尺寸为 1 的维度. 结果维度尺寸是x和y相应维度尺寸的较大者
				- ```python
				  A.shape=(1,9,4),B.shape=(15,1,4) # 那么A+B的shape是(15,9,4)
				  c = torch.empty(5, 1, 4, 1)
				  d = torch.empty(   3, 1, 1)
				  (c + d).size()  # torch.Size([5, 3, 4, 1])
				  ```
		- 可以broadcast的情况
		  collapsed:: true
			- 每个张量至少有一个维度
			- 迭代维度尺寸时, 从尾部的维度开始, 维度尺寸
				- 或者相等
				- 或者其中一个张量的维度尺寸为1
				- 或者其中一个张量不存在这个维度
		- example
		  collapsed:: true
			- ```python
			  # 示例1: 相同形状的张量总是可广播的, 因为总能满足以上规则.
			  x = torch.empty(5, 7, 3)
			  y = torch.empty(5, 7, 3)
			  
			  # 示例2: 不可广播, 每个张量至少有一个维度
			  a = torch.empty((0,))
			  b = torch.empty(2, 2)
			  
			  # 示例3: m 和 n 可广播
			  m = torch.empty(5, 3, 4, 1)
			  n = torch.empty(   3, 1, 1)
			  # 倒数第一个维度：两者的尺寸均为1
			  # 倒数第二个维度：n尺寸为1
			  # 倒数第三个维度：两者尺寸相同
			  # 倒数第四个维度：n该维度不存在
			  
			  # 示例4: 不可广播, 因为倒数第三个维度 2 != 3
			  p = torch.empty(5, 2, 4, 1)
			  q = torch.empty(   3, 1, 1)
			  ```
		- example2
		  collapsed:: true
			- ```python
			  a = torch.arange(3).reshape((3, 1))
			  b = torch.arange(2).reshape((1, 2))
			  a, b
			  #(tensor([[0],
			  #         [1],
			  #         [2]]),
			  # tensor([[0, 1]]))
			  ```
			- 由于a和b分别是3 × 1和1 × 2矩阵, 如果让它们相加, 它们的形状不匹配, 将两个矩阵广播为一个更大的3 × 2矩阵
			- ```python
			  # 矩阵a将复制列, 矩阵b将复制行, 然后再按元素相加
			  # a -> [[0,0],
			  #       [1,1],
			  #       [2,2]]
			  # b -> [[0,1],
			  #       [0,1],
			  #       [0,1]]
			  a + b
			  #tensor([[0, 1],
			  #        [1, 2],
			  #        [2, 3]])
			  ```
- Median
	- 索引切片
		- tensor mask
	- ==自动微分== (automatic differentiation)
		- definition
			- 根据设计的模型, 系统会构建一个计算图 (computational graph), 来跟踪计算是那些数据通过哪些操作组合起来产生输出, 随后进行 [[backpropagate]], 跟踪整个计算图, 填充关于每个参数的 [[偏导数]], 求出 [[gradient]]
			- 一个==标量==调用它的`backward()`方法后, 会根据链式法则自动计算出源张量的 [[gradient]]
			- 源张量和结果张量
			  collapsed:: true
				- ```python
				  x = torch.arange(-8.0, 8.0, 0.1, requires_grad=True)
				  y = x.relu()
				  ```
				- x 为源张量, 源张量x得到的张量y为结果张量
			- 如果结果张量是一维张量
			  collapsed:: true
				- 一般通过对一维张量y进行求和来实现, 即`y.sum()`. 一个一维张量就是一个向量, 对一维张量求和等同于这个向量点乘一个等维的单位向量, 使用求和得到的标量`y.sum()`**对源张量x求导与y的每个元素对x的每个元素求导结果是一样的**, 最终对源张量x的梯度求解没有影响
				- ```python
				  y.sum().backward()
				  x.grad
				  ```
			- 如果结果张量是二维张量或高维张量
			  collapsed:: true
				- 这时可以理解为一般点乘一个等维的单位张量
				- ```python
				  y.backward(torch.ones_like(y)) # grad_tensors=torch.ones_like(y)
				  x.grad
				  ```
			- 为什么`y.backward()`, y必须是标量?
				- 如果y是矩阵, 要先把y转化为标量, 再求导. 转化为方法是`backward()`函数传入一个(权重矩阵, 一般是单位矩阵)矩阵m，计算y*m (y的各元素与m的元素对应相乘，不是矩阵相乘), 再求矩阵元素之和, 这样得到一个标量 (实际就是y中的元素加权求和), 然后才能求导
				- 反向传播必须要各个节点的权重, 因标量只有一个值, 故而无需权重, 而矩阵是一个向量, 故而需要对应的权重, 所以需要 `y.backward(torch.ones_like(y))`
			- example
				- 标量对向量求导
				  collapsed:: true
					- 对函数 $y = 2 \mathbf{x}^{\top} \mathbf{x}$ 关于列向量 $\mathbf{x}$ 求导
						- $$y = 2 \mathbf{x}^{\top} \mathbf{x} = 2 \|x\|^2$$
						  $$\frac{\partial y}{\partial \mathbf{x}} = 2 \frac{\partial \|x\|^2}{\partial \mathbf{x}}  
						  = [\frac{\sum x_i^2}{\partial x_1}, [\frac{\sum x_i^2}{\partial x_2},...,[\frac{\sum x_i^2}{\partial x_n}] 
						  = 2[2x_1, 2x_2,..., 2x_m] = 4 \mathbf{x}^{\top}
						  $$
					- 构造函数
						- ```python
						  import torch
						  x = torch.arange(4.0) # tensor([0., 1., 2., 3.])
						  # 需要一个地方来存储梯度
						  x.requires_grad_(True) # 等价于x=torch.arange(4.0,requires_grad=True) 
						  x.grad # 默认值是None
						  
						  y = 2 * torch.dot(x, x) # tensor(28., grad_fn=<MulBackward0>)
						  ```
					- 调用反向传播函数来自动计算y关于x每个分量的梯度
						- ```python
						  y.backward()
						  x.grad # tensor([ 0., 4., 8., 12.])
						  # 验证
						  x.grad == 4*x
						  # tensor([True, True, True, True])
						  ```
				- 非标量变量的反向传播 (向量对向量求导)
				  collapsed:: true
					- 向量y关于向量x的导数的最自然解释是一个矩阵. 对于高阶和高维的y和x, 求导的结果可以是一个高阶张量
					-
		- 分离计算
			- definition
				- 假设y是作为x的函数计算的, 而z则是作为y和x的函数计算的. 如果想计算z关于x的梯度, 但希望将y视为一个常数, 并且只考虑到x在y被计算后发挥的作用, 此时需要分离y来返回一个新变量u, 该变量与y具有相同的值, 但丢弃计算图中如何计算y的任何信息. 换句话说,梯度不会向后流经u到x
			- example
				- 计算 z = u*x 关于x的偏导, 同时将u作为常数处理, 而不是 z=x*x*x 关于x的偏导
				- ```python
				  x = torch.arange(4.0)
				  # 重置gradient
				  x.grad.zero_() 
				  y=x*x
				  u = y.detach() 
				  z=u*x
				  z.sum().backward()
				  x.grad == u # tensor([True, True, True, True])
				  ```
				- 由于记录了y的计算结果, 我们可以随后在y上调用反向传播, 得到y=x*x关于的x的导数, 即2*x
				- ```python
				  x.grad.zero_()
				  y.sum().backward()
				  x.grad == 2 * x
				  # tensor([True, True, True, True])
				  ```
-