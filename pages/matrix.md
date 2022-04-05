alias:: Matrix, 矩阵
title:: matrix

- {{renderer :tocgen}}
- 向量, 矩阵运算, i:行(row), j:列(column)
	- **加减法**
	  collapsed:: true
		- $$
		  (\mathbf{A} \pm \mathbf{B})_{i, j}=\mathbf{A}_{i, j} \pm \mathbf{B}_{i, j}
		  $$ where $$1 \leq i \leq m, 1 \leq j \leq n$$
	- **数乘**
	  collapsed:: true
		- $$
		  (c \mathbf{A})_{i, j}=c \cdot \mathbf{A}_{i, j}
		  $$
	- 矩阵-向量积 (matrix-vector product)
	  collapsed:: true
	  id:: 62479ef9-0cff-4d23-9ef2-89a801244bce
		- 用法
			- 向量被看成是一行或一列的矩阵, **行向量左乘矩阵，结果是行向量。列向量右乘矩阵，结果是列向量。另外两种组合是不允许的。**
			-
		- example
			- 定义矩阵 $\mathbf{A} \in \mathbb{R}^{m \times n}$ 和向量 $\mathbf{x} \in \mathbb{R}^n$
			- 矩阵 $\mathbf{A}$ 用他的行向量表示
				- $$
				  \mathbf{A}=\left[\begin{array}{c}
				  \mathbf{a}_{1}^{\top} \\
				  \mathbf{a}_{2}^{\top} \\
				  \vdots \\
				  \mathbf{a}_{m}^{\top}
				  \end{array}\right]
				  $$
				- 其中每个 $\mathbf{a}_i^{\top} \in \mathbb{R}^n$ 都是==行向量==, 表示矩阵的第i行.
			- 矩阵的向量积 $\mathbf{Ax}$ 是一个长度为 m 的==列向量==, 第 i 个元素是点积 $\mathbf{a}_i^{\top} \mathbf{x}$
				- $$
				  \mathbf{A x}=\left[\begin{array}{c}
				  \mathbf{a}_{1}^{\top} \\
				  \mathbf{a}_{2}^{\top} \\
				  \vdots \\
				  \mathbf{a}_{m}^{\top}
				  \end{array}\right] \mathbf{x}=\left[\begin{array}{c}
				  \mathbf{a}_{1}^{\top} \mathbf{x} \\
				  \mathbf{a}_{2}^{\top} \mathbf{x} \\
				  \vdots \\
				  \mathbf{a}_{m}^{\top} \mathbf{x}
				  \end{array}\right]
				  $$
		- 合法表达
			- $$
			  \begin{aligned}
			  &{\left[\begin{array}{lll}
			  x & y & z
			  \end{array}\right]\left[\begin{array}{lll}
			  m_{11} & m_{12} & m_{13} \\
			  m_{21} & m_{22} & m_{23} \\
			  m_{31} & m_{32} & m_{33} 
			  \end{array}\right]= 
			  \left[\begin{array}{ll}
			  x m_{11}+y m_{21}+z m_{31} & x m_{12}+y m_{22}+z m_{32} & x m_{13}+y m_{23}+z m_{33}
			  
			  \end{array}\right]} \\
			  &{\left[\begin{array}{lll}
			  m_{11} & m_{12} & m_{13} \\
			  m_{21} & m_{22} & m_{23} \\
			  m_{31} & m_{32} & m_{33}
			  \end{array}\right]\left[\begin{array}{l}
			  x \\
			  y \\
			  z
			  \end{array}\right]=\left[\begin{array}{lll}
			  x m_{11} + y m_{12} + z m_{13} \\
			  x m_{21} + y m_{22} + z m_{23} \\
			  x m_{31} + y m_{32} + z m_{33}
			  \end{array}\right]} \\
			  &{\left[\begin{array}{lll}
			  m_{11} & m_{12} & m_{13} \\
			  m_{21} & m_{22} & m_{23} \\
			  m_{31} & m_{32} & m_{33}
			  \end{array}\right]\left[\begin{array}{lll}
			  x & y & z
			  \end{array}\right]=(\text { 无定义 })} \\
			  &{\left[\begin{array}{l}
			  x \\
			  y \\
			  z
			  \end{array}\right]\left[\begin{array}{lll}
			  m_{11} & m_{12} & m_{13} \\
			  m_{21} & m_{22} & m_{23} \\
			  m_{31} & m_{32} & m_{33}
			  \end{array}\right]=(\text { 无定义 })}
			  \end{aligned}
			  $$
	- **转置**
	  collapsed:: true
		- $$
		  \left(\mathbf{A}^{\mathrm{T}}\right)_{i, j}=\mathbf{A}_{j, i}
		  $$
			- $$
			  \left[\begin{array}{ccc}
			  1 & 2 & 3 \\
			  0 & -6 & 7
			  \end{array}\right]^{T}=\left[\begin{array}{cc}
			  1 & 0 \\
			  2 & -6 \\
			  3 & 7
			  \end{array}\right]
			  $$
	- **matrix product (矩阵乘法)**
	  collapsed:: true
	  id:: 62479ef9-dc1b-437b-b537-dfa297d04bbe
		- 假设有两个矩阵 $\mathbf{A} \in \mathbb{R}^{n \times k}$ 和 $\mathbf{B} \in \mathbb{R}^{k \times m}$
			- $$
			  \mathbf{A}=\left[\begin{array}{cccc}
			  a_{11} & a_{12} & \cdots & a_{1 k} \\
			  a_{21} & a_{22} & \cdots & a_{2 k} \\
			  \vdots & \vdots & \ddots & \vdots \\
			  a_{n 1} & a_{n 2} & \cdots & a_{n k}
			  \end{array}\right], \quad \mathbf{B}=\left[\begin{array}{cccc}
			  b_{11} & b_{12} & \cdots & b_{1 m} \\
			  b_{21} & b_{22} & \cdots & b_{2 m} \\
			  \vdots & \vdots & \ddots & \vdots \\
			  b_{k 1} & b_{k 2} & \cdots & b_{k m}
			  \end{array}\right]
			  $$
			- 用行向量 $\mathbf{a}_i^{\top} \in \mathbb{R}^k$ 表示矩阵 $\mathbf{A}$ 的第i行,  让列向量 $\mathbf{b}_j \in \mathbb{R}^k$ 作为矩阵 $\mathbf{B}$ 的第j列
		- 要生成矩阵积 $\mathbf{C} = \mathbf{AB}$, 矩阵-矩阵乘法AB看作是简单地执行m次矩阵-向量积, 并将结果拼接在一起, 形成一个n × m矩 阵
			- $$
			  \mathbf{A}=\left[\begin{array}{c}
			  \mathbf{a}_{1}^{\top} \\
			  \mathbf{a}_{2}^{\top} \\
			  \vdots \\
			  \mathbf{a}_{n}^{\top}
			  \end{array}\right], \quad \mathbf{B}=\left[\begin{array}{llll}
			  \mathbf{b}_{1} & \mathbf{b}_{2} & \cdots & \mathbf{b}_{m}
			  \end{array}\right]
			  $$
			- $$
			  \mathbf{C}=\mathbf{A B}=\left[\begin{array}{c}
			  \mathbf{a}_{1}^{\top} \\
			  \mathbf{a}_{2}^{\top} \\
			  \vdots \\
			  \mathbf{a}_{n}^{\top}
			  \end{array}\right]\left[\begin{array}{llll}
			  \mathbf{b}_{1} & \mathbf{b}_{2} & \cdots & \mathbf{b}_{m}
			  \end{array}\right]=\left[\begin{array}{cccc}
			  \mathbf{a}_{1}^{\top} \mathbf{b}_{1} & \mathbf{a}_{1}^{\top} \mathbf{b}_{2} & \cdots & \mathbf{a}_{1}^{\top} \mathbf{b}_{m} \\
			  \mathbf{a}_{2}^{\top} \mathbf{b}_{1} & \mathbf{a}_{2}^{\top} \mathbf{b}_{2} & \cdots & \mathbf{a}_{2}^{\top} \mathbf{b}_{m} \\
			  \vdots & \vdots & \ddots & \vdots \\
			  \mathbf{a}_{n}^{\top} \mathbf{b}_{1} & \mathbf{a}_{n}^{\top} \mathbf{b}_{2} & \cdots & \mathbf{a}_{n}^{\top} \mathbf{b}_{m}
			  \end{array}\right]
			  $$
		- 仅当第一个矩阵的列数(column)和另一个矩阵的行数(row)相等时才能定义
		- $$
		  \left[\begin{array}{ll}
		  a & b \\
		  c & d
		  \end{array}\right]\left[\begin{array}{ll}
		  e & f \\
		  g & h
		  \end{array}\right]=\left[\begin{array}{ll}
		  a e+b g & a f+b h \\
		  c e+d g & c f+d h
		  \end{array}\right]
		  $$
		- $$
		  (\mathbf{A B})^{\mathrm{T}}=\mathbf{B}^{\mathrm{T}} \mathbf{A}^{\mathrm{T}}
		  $$
	- Cross Product (矩阵叉积)
	  collapsed:: true
		- $$
		  \|\mathbf{a} \times \mathbf{b}\|=\|\mathbf{a}\|\|\mathbf{b}\| \sin \theta 
		  $$
	- Hadamard Product (矩阵哈达玛积)
	  id:: 623f8997-940d-4bd0-98c9-fb784f526f4b
	  collapsed:: true
		- $$
		  \left[\begin{array}{ll}
		  a_{11} & a_{12} \\
		  a_{21} & a_{22}
		  \end{array}\right] \odot\left[\begin{array}{ll}
		  b_{11} & b_{12} \\
		  b_{21} & b_{22}
		  \end{array}\right]=\left[\begin{array}{ll}
		  a_{11} b_{11} & a_{12} b_{12} \\
		  a_{21} b_{21} & a_{22} b_{22}
		  \end{array}\right]
		  $$
	- kronecker Product (矩阵克罗内克积)
	  collapsed:: true
		- $$
		  \left[\begin{array}{ll}
		  a_{11} & a_{12} \\
		  a_{21} & a_{22}
		  \end{array}\right] \otimes\left[\begin{array}{ll}
		  b_{11} & b_{12} \\
		  b_{21} & b_{22}
		  \end{array}\right]=\left[\begin{array}{llll}
		  a_{11} b_{11} & a_{11} b_{12} & a_{12} b_{11} & a_{12} b_{12} \\
		  a_{11} b_{21} & a_{11} b_{22} & a_{12} b_{21} & a_{12} b_{22} \\
		  a_{21} b_{11} & a_{21} b_{12} & a_{22} b_{11} & a_{22} b_{12} \\
		  a_{21} b_{21} & a_{21} b_{22} & a_{22} b_{21} & a_{22} b_{22}
		  \end{array}\right]
		  $$
	- Dot Product (向量点乘)
	  id:: 62479ef9-b5e9-4db5-b9a1-9bd6d872cd33
	  collapsed:: true
		- 用法
			- 给定一组由向量 $\mathbf{x} \in \mathbb{R}^{d}$ 表示的值, 和一组由 $\mathbf{w} \in \mathbb{R}^{d}$ 表示的权重, $\mathbf{x}$ 中的值根据权重 $\mathbf{w}$ 的加权和, 可以表示为点积 $\mathbf{x}^T \mathbf{w}$
			- 给定两个变量 $$\mathbf{x}, \mathbf{y} \in \mathbb{R}^{d}$$, 他们的点积 $\mathbf{x}^T \mathbf{y}$ 是相同位置按元素乘积的和 $\mathbf{x}^T \mathbf{y} = \sum_{i=1}^d x_i y_i$ (顺序不影响)
		- example
			- $$
			  \vec{a} \cdot \vec{b}=|\vec{a}||\vec{b}| \cos \theta
			  $$
			- $$
			  \vec{a} \cdot \vec{b}=\sum_{i=1}^{n} a_{i} b_{i}=a_{1} b_{1}+a_{2} b_{2}+\cdots+a_{n} b_{n}
			  $$
			- $$
			  \vec{a} \cdot \vec{b}=\vec{a} \vec{b}^{T}
			  $$
				- $$
				  \left[\begin{array}{lll}
				  1 & 3 & -5
				  \end{array}\right]\left[\begin{array}{c}
				  4 \\
				  -2 \\
				  -1
				  \end{array}\right]=[3]=3
				  $$
	- 向量内积 (Inner product)
		- $$
		  \begin{gathered}
		  a=\left(a_{1}, a_{2}, \cdots, a_{n}\right) \\
		  b=\left(b_{1}, b_{2}, \cdots, b_{n}\right) \\
		  a \cdot b=a_{1} b_{1}+a_{2} b_{2}+\cdots+a_{n} b_{n}
		  \end{gathered}
		  $$
	- 向量外积 (outer product)
	  collapsed:: true
		- $$
		  \begin{gathered}
		  u=\left(u_{1}, u_{2}, \cdots, u_{m}\right) \\
		  u \otimes v=\left(v_{1}, v_{2}, \cdots, v_{n}\right) \\
		  u=\left[\begin{array}{cccc}
		  u_{1} v_{1} & u_{1} v_{2} & \cdots & u_{1} v_{n} \\
		  u_{2} v_{1} & u_{2} v_{2} & \cdots & u_{2} v_{n} \\
		  \vdots & \vdots & \ddots & \vdots \\
		  u_{m} v_{1} & u_{m} v_{2} & \cdots & u_{m} v_{n}
		  \end{array}\right]
		  \end{gathered}
		  $$
	- 向量叉积 (Cross Production)
	  collapsed:: true
		- $$
		  \begin{gathered}
		  a=\left(x_{1}, y_{1}, z_{1}\right) \\
		  b=\left(x_{2}, y_{2}, z_{2}\right) \\
		  a \times b=\left|\begin{array}{ccc}
		  i & j & k \\
		  x_{1} & y_{1} & z_{1} \\
		  x_{2} & y_{2} & z_{2}
		  \end{array}\right|=\left(y_{1} z_{2}-y_{2} z_{1}\right) i+\left(z_{1} x_{2}-z_{2} x_{1}\right) j+\left(x_{1} y_{2}-x_{2} y_{1}\right) k \\
		  i=[1,0,0], j=[0,1,0], k=[0,0,1]
		  \end{gathered}
		  $$
		- 结果为两个向量的法向量
	- [[Determinant]] (行列式$$det()$$)
	  id:: 61f23283-b64f-491a-9bc9-3d22073155ed
	- Inverse Matrix (逆矩阵)
	  collapsed:: true
		- $det(A) \neq 0 \Rightarrow A^T exists$, 也就是$rank\neq 0$的时候
- Concepts
	- Column Space (列空间) $$Col(A)$$
	  collapsed:: true
		- 变换后基向量张成的空间就是所有可能的变换结果, 也就是矩阵的列所张成的空间
		- 零向量一定在列空间中
	- Rank (秩)
	  collapsed:: true
		- Rank: number of dimensions in the output (变换后空间的维数)
			- Rank = 1 if output of a transformation is a line (矩阵变换后为1维空间, 线)
			- Rank = 2 if out put of a transformation is a plane (矩阵变换后为一个平面)
		- 满秩矩阵 (a.k.a. 可逆矩阵)
			- 设A是n阶矩阵, 若 $$rank(A) = n$$, 则为满秩矩阵
			- 非满秩矩阵就是变换后的dimention减少了, 比如三维变成平面, 平面变成点
		- 想象二元一次方程组，两个方程系数如果线性相关，那么俩方程能代表的只有一个有效线索，方程组的解也不是唯一的。
		  如果两个方程线性无关，它俩有两个有效线索，方程组的解是唯一的。n行m列矩阵可以看成n个方程m个未知数组成的齐次方程组。
		  满秩，就是n个方程系数都线性无关，不能被其他方程代替以后消除。
	- [[Eigenvalue]], [[Eigenvector]] (特征值, 特征向量)
	- [[对称矩阵]]
	- Null Space (零空间) (核, Kernel) $$Null(A), Ker(A)$$
	  collapsed:: true
		- 非满秩矩阵变换后一些向量落在零向量上, 也就是被压缩到了原点 (如果三维, 那么有一个面压缩到原点, 如果二位那么有一条线压缩到原点), 零空间正是这些向量所构成的空间
			- [Inverse matrices, column space and null space | Chapter 7, Essence of linear algebra - YouTube](https://www.youtube.com/watch?v=uQhTuRlWMxw&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab&index=7)
	- Definite Matrix (定值矩阵)
	  collapsed:: true
		- Positive Definite Matrix (正定矩阵)
			- 例子和意义
				- $$
				  \begin{aligned}
				  f(x) &=\left(x_{1}-x_{2}\right)^{2}+2 x_{1}+x_{2}+3 \\
				  &
				  =\left[\begin{array}{ll}
				  x_{1} & x_{2}
				  \end{array}\right]\left[\begin{array}{cc}
				  1 & -1 \\
				  -1 & 1
				  \end{array}\right]\left[\begin{array}{l}
				  x_{1} \\
				  x_{2}
				  \end{array}\right]+\left[\begin{array}{ll}
				  2 & 1
				  \end{array}\right]\left[\begin{array}{l}
				  x_{1} \\
				  x_{2}
				  \end{array}\right]+3
				  \end{aligned}
				  $$
				- 一般形式:$$f(x)= x^{T} A x+b^{T} x+c$$ 
				  其中x和b都是向量
				- $$
				  \nabla f(x)=A x+b, \nabla^{2} f(x)=A
				  $$
				- 只要A是正定的, 那么二阶导数[黑塞矩阵]([[hessian matrix]])就是正定的, 所以$$f(x)$$就是凸函数, 极值就是最小值, 也是全局最小值
			- 定义
				- 1. 给定一个大小为 $$n \times n$$ 的实对称矩阵 $$A$$, 若对于任意长度为 $$n$$ 的非零向量 $$x$$, 有$$\boldsymbol{x}^{T} A \boldsymbol{x}>0$$ 恒成立, 则矩阵A是一个正定矩阵
		- Positive semi-definite matrix (半正定矩阵)
		- Negative definite matrix
		- Negative semi-definite matrix