alias:: 特征值, eigenvalues

- Definition
	- 矩阵$A$是一个变换, 当$A$作用在特征向量$u$的时候, $u$ 只发生缩放变换, 方向没有改变, 也没有旋转
- Formula
	- $$
	  A \overrightarrow{\mathbf{v}}=\lambda \overrightarrow{\mathbf{v}}
	  $$
	- 解线性方程组
	  $$
	  \begin{gathered}
	  (A-\lambda I) \vec{x}=\overrightarrow{0}
	  \end{gathered}
	  $$
		- 通过$$\operatorname{det}(A-\lambda I)=0$$, 解出 $$\lambda$$. 该方程也叫特征方程 ([[characteristic equation]])
- Note
	- 一个矩阵可能可以拉长(缩短)多个向量, 因此它就可能有 _多个_ 特征值, **也就是多个不变的轴**
	- n 阶方阵有 n 个特征向量, 每一个特征向量表征一个维度上的线性变换方向
	- 对于 [[实对称矩阵]] 来说, 不同特征值对应的特征向量必定正交
	- 一个变换矩阵的所有特征向量组成了这个变换矩阵的一组 _基_
	- 求特征向量就是把矩阵A所代表的空间进行正交分解, 使得A的向量集合可以表示为每个向量a在各个特征向量上的投影长度. 通常求特征值和特征向量即为求出这个矩阵能使哪些向量只发生拉伸, 而方向不发生变化, 观察其发生拉伸的程度.这样做的意义在于, **看清一个矩阵在哪些方面能产生最大的分散度, 减少重叠, 意味着更多的信息被保留下来**
- Additional reading
	- [如何理解特征值和特征向量](https://www.matongxue.com/madocs/228/)