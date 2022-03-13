alias:: Hessian Matrix, 黑塞矩阵, 海森矩阵

- # Definition
	- 如果已知n元函数的二阶导数存在, 那么Hessian matrix为:
	- 黑塞矩阵为二阶的偏导矩阵 (梯度再导), 接
	  $$\nabla f(x)=\left[\frac{\partial f}{\partial x_{1}}, \frac{\partial f}{\partial x_{2}}, \ldots, \frac{\partial f}{\partial x_{i}}\right]^{T} = \left[\begin{array}{c}
	  \frac{\partial f}{\partial x_{1}} \\
	  \frac{\partial f}{\partial x_{2}} \\
	  \vdots \\
	  \frac{\partial f}{\partial x_{n}}
	  \end{array}\right]$$
	  
	  再次偏导
	- $$\nabla\left(\frac{\partial f}{\partial x_{i}}\right)=\left[\begin{array}{lllll}
	  \frac{\partial}{\partial x_{1}} \frac{\partial f}{\partial x_{i}} & \frac{\partial}{\partial x_{2}} \frac{\partial f}{\partial x_{i}} & \cdots & \frac{\partial}{\partial x_{n}} \frac{\partial f}{\partial x_{i}}
	  \end{array}\right]^{\top}$$
	- $$=\nabla^{2} f(\boldsymbol{x})=\left[\begin{array}{cccccc}
	  \frac{\partial}{\partial x_{1}} \frac{\partial f}{\partial x_{1}} & \frac{\partial}{\partial x_{2}} \frac{\partial f}{\partial x_{1}} & \cdots & \frac{\partial}{\partial x_{n}} \frac{\partial f}{\partial x_{1}} \\
	  \frac{\partial}{\partial x_{1}} \frac{\partial f}{\partial x_{2}} & \frac{\partial}{\partial x_{2}} \frac{\partial f}{\partial x_{2}} & \cdots & \frac{\partial}{\partial x_{n}} \frac{\partial f}{\partial x_{2}} \\
	  \vdots & \vdots & \ddots & \vdots \\
	  \frac{\partial}{\partial x_{1}} \frac{\partial f}{\partial x_{n}} & \frac{\partial}{\partial x_{2}} \frac{\partial f}{\partial x_{n}} & \cdots & \frac{\partial}{\partial x_{n}} \frac{\partial f}{\partial x_{n}}
	  \end{array}\right]$$
- # Properties
	- 方形矩阵, 对称, (i为行, j为列), 所以:
	- $$\boldsymbol{H}_{i j}=\frac{\partial}{\partial x_{j}} \frac{\partial f}{\partial x_{i}}=\frac{\partial}{\partial x_{i}} \frac{\partial f}{\partial x_{j}}=\boldsymbol{H}_{j i}$$
	- **Example**
		- $$\begin{aligned}
		  &f(x, y)=5 x+8 y+x y-x^{2}-2 y^{2} \\
		  &\nabla f(x, y)=\left[\begin{array}{l}
		  \frac{\partial f}{\partial x} \\
		  \frac{\partial f}{\partial y}
		  \end{array}\right]=\left[\begin{array}{l}
		  5-2 x+y \\
		  8+x-4 y
		  \end{array}\right]
		  \end{aligned}$$
		- 对其中的 $$5-2x+y$$, $$8+x-4y$$, 分别对x,y再求一次偏导
		  $$\begin{aligned}
		  &\frac{\partial^{2} f}{\partial x^{2}}=\frac{\partial(5-2 x+y)}{\partial x}=-2 \\
		  &\frac{\partial}{\partial y} \frac{\partial f}{\partial x}=\frac{\partial(5-2 x+y)}{\partial y}=1 \\
		  &\frac{\partial}{\partial x} \frac{\partial f}{\partial y}=\frac{\partial(8+x-4 y)}{\partial x}=1 \\
		  &\frac{\partial^{2} f}{\partial y^{2}}=\frac{\partial(8+x-4 y)}{\partial y}=-4
		  \end{aligned}$$
		- 可以得到 
		  $$\boldsymbol{H}(\boldsymbol{x})=\left[\begin{array}{cc}
		  -2 & 1 \\
		  1 & -4
		  \end{array}\right]$$ 也就是
		  $$\left[\begin{array}{l}
		  5-2 x+y \\
		  8+x-4 y
		  \end{array}\right]$$ 
		  的系数
- **Summary**
	- 对于二次矩阵, [黑塞矩阵]([[hessian matrix]])为常数矩阵, 于x无关, 但是一般而言, 黑塞矩阵是可以为x的函数
	- [黑塞矩阵]([[hessian matrix]])储存了函数的二阶导数信息