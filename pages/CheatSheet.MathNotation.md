title:: CheatSheet/MathNotation

- # Linear Algebra
	- $\mathbf{x}$ 向量 (默认为列向量), $x_n$ 为标量 $\mathbf{x} \in \mathbb{R}^{n}$. 
	  collapsed:: true
		- $$
		  \mathbf{x}=\left[\begin{array}{c}
		  x_{1} \\
		  x_{2} \\
		  \vdots \\
		  x_{n}
		  \end{array}\right]
		  $$
		- 若该矩阵属于$\mathbf{M}(n,1)$，即列向量，则用粗体小写字母表示，如$\mathbf{a, x, y}$等, 不做特别说明的话, 向量默认为列向量
	- $\mathbf{A}$: Matrix $\mathbf{A} \in \mathbb{R}^{m \times n}$
	  collapsed:: true
		- 每个元素 $a_{ij}$ 为第i行, 第j列
		- $$
		  \mathbf{A}=\left[\begin{array}{cccc}
		  a_{11} & a_{12} & \cdots & a_{1 n} \\
		  a_{21} & a_{22} & \cdots & a_{2 n} \\
		  \vdots & \vdots & \ddots & \vdots \\
		  a_{m 1} & a_{m 2} & \cdots & a_{m n}
		  \end{array}\right]
		  $$
		- 矩阵 $\mathbf{A}$ 中元素的和为 $\sum_{i=1}^{m} \sum_{j=1}^{n} a_{i j}$
	- $\mathbf{A}^{\top}$ Matrix Transpose
	  collapsed:: true
		- 如果 $\mathbf{B} = \mathbf{A}^{\top}$, 那么对于任意i和j, 都有$b{ij} = a{ij}$
		- $$
		  \mathbf{A}^{\top}=\left[\begin{array}{cccc}
		  a_{11} & a_{21} & \ldots & a_{m 1} \\
		  a_{12} & a_{22} & \ldots & a_{m 2} \\
		  \vdots & \vdots & \ddots & \vdots \\
		  a_{1 n} & a_{2 n} & \ldots & a_{m n}
		  \end{array}\right]
		  $$
	- $\mathbf{A}^{-1}$: Matrix Inverse
	- $\prod_{k=1}^{n} a_{k}$: 表示 $a_{1} a_{2} \dots a_{n}$, 连乘
	- $I$: 单位矩阵 (identify matrix)
	- $argmax$: 最大值
	  collapsed:: true
		- 函数 $y = f(x)$, $x_0 = argmax(f(x))$ 的意思就是参数 $x_0$ 满足 $f(x_0)$ 为 $f(x)$的最大值
	- $\odot$ : 按元素相乘 ((623f8997-940d-4bd0-98c9-fb784f526f4b))
	- $\nabla$: 梯度算子nabla, 空间各个方向上的全积分
	- $a^{\top}a = \|a\|^2$ 矩阵的 [[范数]] (是标量)
	  collapsed:: true
		- $$
		  a^{T} a=\left[\begin{array}{llll}
		  a_{1} & a_{2} & \cdots & a_{n}
		  \end{array}\right]\left[\begin{array}{c}
		  a_{1} \\
		  a_{2} \\
		  \vdots \\
		  a_{n}
		  \end{array}\right]=\left[a_{1}^{2}+a_{2}^{2}+\cdots+a_{n}^{2}\right]=\|a\|^{2}
		  $$
	- $\operatorname{tr}(\mathbf{X})$, $\operatorname{Sp}(\mathbf{X})$: 矩阵 $\mathbf{X}$ 的[[迹]]
	- $det(\mathbf{X})$, $|X|$ 矩阵的 [[行列式]]
	- 标量a,b,c,d,e为常量, 标量u,v为x, $\mathbf{x}$ 或 $\mathbf{X}$ 的函数
	- 向量 $\mathbf{a,b,c,d,e}$ 为常向量，向量 $\mathbf{u,v}$ 为 x, $\mathbf{x}$或$\mathbf{X}$ 的函数
	- 矩阵 $\mathbf{A, B, C, D}$ 为常矩阵, 矩阵 $\mathbf{U,V}$ 为x, $\mathbf{x}$或$\mathbf{X}$ 的函数
- # Set
	- $a \in A:$ a is the element of set A
	- $A \subseteq B:$ A is a subset of (or equal to) B
	- $A \cup B:$ The union of A and B
	- $A \cap B:$ The intersection of A and B
	- $\left\{x \mid x^{2}=1\right\}:$ The set of all x with $$x^2=1$$
	- $\mathbb{R}^{n}$ : n 维的实数向量集合
	- $\mathbb{R}^{x \times y}$ : x 行 y 列的实数矩阵集合
	- $\exists$: 存在一个, 至少一个, exists
	- $\forall$ : 任意的, for all
	- $\Leftrightarrow$ : preferred for equivalence
- # Abbreviations
	- iff: if and only if
	- $st.$ subject to (such that), 使得...满足..., 受约束的意思
- # Statistics
	- $iid$: Independent and identically distributed
	- $\pi_k$ prior, [[先验概率]]
- # [[calculus]]