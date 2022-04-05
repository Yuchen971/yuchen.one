alias:: 偏导数

- Definition
	- 设 $y = f(x_1, x_2, ..., x_n)$ 是一个具有n个变量的函数, $y$ 关于第$i$ 个参数$x_i$ 的偏导数
	- $$
	  \frac{\partial y}{\partial x_{i}}=\lim _{h \rightarrow 0} \frac{f\left(x_{1}, \ldots, x_{i-1}, x_{i}+h, x_{i+1}, \ldots, x_{n}\right)-f\left(x_{1}, \ldots, x_{i}, \ldots, x_{n}\right)}{h}
	  $$
- 表达形式
	- $$
	  \frac{\partial y}{\partial x_{i}}=\frac{\partial f}{\partial x_{i}}=f_{x_{i}}=f_{i}=D_{i} f=D_{x_{i}} f
	  $$
- Example
  collapsed:: true
	- $$z = x^2 + 3xy + y^2$$
		- $$
		  \frac{\partial z}{\partial x}=2 x+3 y ; \frac{\partial z}{\partial y}=3 x+2 y
		  $$
	- $z = f(x, y)$(一个面)
	  偏导数为函数在每个位置处沿着自变量 (x或者y) 坐标轴方向上的导数, 也就是固定x或者y, 把曲面切开之后那一点的切线斜率.
	  note: 
	  $\frac{\partial f}{\partial x}$ **y为常数**
	  $\frac{\partial f}{\partial y}$ **x为常数**
	  [偏導數 - YouTube](https://www.youtube.com/watch?v=JQ4lSc48QCw)
	- 当函数在某点的所有偏导数为0时, 该点为函数的极值点或者鞍点
		- ![image.png](../assets/image_1643005410411_0.png)