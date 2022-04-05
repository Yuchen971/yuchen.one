alias:: 梯度

- Definition
	- 梯度为x方向的[偏导数]([[partial derivatives]])和y方向的[偏导数]([[partial derivatives]]), 用向量表示, 并且相加. 
	  梯度为该函数在该位置处上升或下降最快的方向
	- 设函数$f:\mathbb{R}^n \to \mathbb{R}$的输入是一个 $n$ 维向量 $\mathbf{x} = [x_1,x_2,...,x_n]^{\top}$
	- $$\nabla_x f(x) = \nabla f(x)=\left[\frac{\partial f}{\partial x_{1}}, \frac{\partial f}{\partial x_{2}}, \ldots, \frac{\partial f}{\partial x_{i}}\right]^{\top} = \left[\begin{array}{c}
	  \frac{\partial f}{\partial x_{1}} \\
	  \frac{\partial f}{\partial x_{2}} \\
	  \vdots \\
	  \frac{\partial f}{\partial x_{n}}
	  \end{array}\right]$$
- Properties
	- 假设 $\mathbf{x}$ 是n维向量, 在微分多元函数的时候经常使用以下规则
	- 对于所有 $\mathbf{A} \in \mathbb{R}^{m \times n}$ 都有 $\nabla_x \mathbf{A} \mathbf{x} = \mathbf{A}^{\top}$
	- 对于所有 $\mathbf{A} \in \mathbb{R}^{n \times m}$ 都有 $\nabla_x \mathbf{x}^{\top} \mathbf{x} = \mathbf{A}$
	- 对于所有 $\mathbf{A} \in \mathbb{R}^{n \times n}$ 都有 $\nabla_x \mathbf{x}^{\top} \mathbf{A} \mathbf{x} = (\mathbf{A} + \mathbf{A}^{\top})\mathbf{x}$
	- $\nabla_{\mathbf{x}}\|\mathbf{x}\|^{2}=\nabla_{\mathbf{x}} \mathbf{x}^{\top} \mathbf{x}=2 \mathbf{x}$