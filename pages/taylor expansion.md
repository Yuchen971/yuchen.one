alias:: taylor expansion, 泰勒展开式

- [Taylor Expansion](https://www.youtube.com/watch?v=3d6DsjIBzJ4)
- # Definition
	- 设 n 是一个正整数如果定义在一个包含 $$x_{0}$$ 的区间上的函数 f 在 $$x_{0}$$ 点处 n+1 次可导，那么对于这个区间上的任意 x，都有：
	- $$f(x)=f(x_{0})+\frac{f^{\prime}(x_{0})}{1 !}(x-x_{0})+\frac{f^{(2)}(x_{0})}{2 !}(x-x_{0})^{2}+\cdots+\frac{f^{(n)}(x_{0})}{n !}(x-x_{0})^{n}+R(x)$$
		- 其中的多项式称为函数在 $$x_{0}$$ 处的 **泰勒展开式**，剩余的!$$R(x)$$是泰勒公式的余项
		- $n!$ = factorial of n
		  $x_{0}$ = real or complex number
		  $f^{(n)}(x_{0})=$ = nth derivative of f evaluated at the point a
		  $R(x)$ 为余项(误差项): 
		  $\frac{f^{(n+1)}(x_{0})}{(n+1) !}\left(x-x_{0}\right)^{n+1}+\cdots \frac{f^{(\infty)}(x_{0})}{\infty !}\left(x-x_{0}\right)^{\infty}$$
		  拉格朗日余项: $R(x) = \frac{f^{n+1}(\xi)}{(n+1) !}\left(x-x_{0}\right)^{n+1}$
		  $\xi$处于$x$和$x_{0}$之间
- # 拉格朗日余项推导
	- $$R(x) = \frac{f^{(n+1)}(x_{0})}{(n+1) !}\left(x-x_{0}\right)^{n+1}+\cdots \frac{f^{(\infty)}(x_{0})}{\infty !}\left(x-x_{0}\right)^{\infty}$$ 
	  显然 $$R(x_{0}) = 0$$
	- 设 $$T(x)=\left(x-x_{0}\right)^{n+1}$$
	  显然 $$T(x_{0}) = 0$$
	- $R(x)$ 两边同除$$\left(x-x_{0}\right)^{n+1}$$
	  $$\frac{R(x)}{T(x)}=\frac{R(x)-0}{T(x)-0}=\frac{R(x)-R\left(x_{0}\right)}{T(x)-T\left(x_{0}\right)}$$
	- 根据[中值定理](((4c6027e5-a529-4feb-b8f5-f3c40ab8eb8e))) 有
	  background-color:: #793e3e
	  $$\frac{R(x)-R\left(x_{0}\right)}{T(x)-T\left(x_{0}\right)}=\frac{R^{\prime}\left(\xi_{1}\right)}{T^{\prime}\left(\xi_{1}\right)}$$
	  $$=\frac{R^{\prime}\left(\xi_{1}\right)}{(n+1)\left(\xi_{1}-x_{0}\right)^{n}}$$
		- 先看分子$$R^{\prime}\left(\xi_{1}\right)$$
			- 根据误差项$$R(x)$$可以求出求出$$R'(x)$$
			  $$R^{\prime}\left(\xi_{1}\right)=
			  (n+1) \frac{f^{(n+1)}\left(x_{0}\right)}{(n+1) !}\left(\xi_{1}-x_{0}\right)^{n}$$
			  $$+(n+2) \frac{f^{(n+2)}\left(x_{0}\right)}{(n+2) !}\left(\xi_{1}-x_{0}\right)^{n+1}+\cdots$$
			- 设 $$R^{\prime}\left(\xi_{1}\right)=\mathrm{P}\left(\xi_{1}\right)$$
			  显然 $$P(x_{0})=0$$
		- 再看分母 $${(n+1)\left(\xi_{1}-x_{0}\right)^{n}}$$
			- 设 $$Q\left(\xi_{1}\right)=(n+1)\left(\xi_{1}-x_{0}\right)^{n}$$
			  显然$$Q(x_{0})=0$$
		- 再次根据中值定理
		  $$\frac{R^{\prime}\left(\xi_{1}\right)}{(n+1)\left(\xi_{1}-a\right)^{n}}=\frac{P\left(\xi_{1}\right)}{Q\left(\xi_{1}\right)}=\frac{P\left(\xi_{1}\right)-0}{Q\left(\xi_{1}\right)-0}=\frac{P\left(\xi_{1}\right)-P\left(a\right)}{Q\left(\xi_{1}\right)-Q\left(a\right)}=\frac{P^{\prime}\left(\xi_{2}\right)}{Q^{\prime}\left(\xi_{2}\right)}$$
	- **一直求解下去, 最终误差项为**
	  $$R(x) = \frac{f^{n+1}(\xi)}{(n+1) !}\left(x-x_{0}\right)^{n+1}$$
- **多元函数泰勒展开**
	- 一元函数在点 $$x_k$$ 处的泰勒展开式为
		- $$f(x)=f\left(x_{k}\right)+\left(x-x_{k}\right) f^{\prime}\left(x_{k}\right)+\frac{1}{2 !}\left(x-x_{k}\right)^{2} f^{\prime \prime}\left(x_{k}\right)+o^{n}$$
	- 二元函数在点 $$x_{k}$$ 处的泰勒展开式为
		- $$
		  \begin{gathered}
		  f(x, y)=f\left(x_{k}, y_{k}\right)+\left(x-x_{k}\right) f_{x}^{\prime}\left(x_{k}, y_{k}\right)+\left(y-y_{k}\right) f_{y}^{\prime}\left(x_{k}, y_{k}\right) \\
		  +\frac{1}{2 !}\left(x-x_{k}\right)^{2} f_{x x}^{\prime \prime}\left(x_{k}, y_{k}\right)+\frac{1}{2 !}\left(x-x_{k}\right)\left(y-y_{k}\right) f_{x y}^{\prime \prime}\left(x_{k}, y_{k}\right) \\
		  +\frac{1}{2 !}\left(x-x_{k}\right)\left(y-y_{k}\right) f_{y x}^{\prime \prime}\left(x_{k}, y_{k}\right)+\frac{1}{2 !}\left(y-y_{k}\right)^{2} f_{y y}^{\prime \prime}\left(x_{k}, y_{k}\right) \\
		  +o^{n}
		  \end{gathered}
		  $$
	- 多元函数(n个元)在点 $$x_k$$ 处的泰勒展开式为
		- $$
		  \begin{gathered}
		  f\left(x^{1}, x^{2}, \ldots, x^{n}\right)=f\left(x_{k}^{1}, x_{k}^{2}, \ldots, x_{k}^{n}\right)+\sum_{i=1}^{n}\left(x^{i}-x_{k}^{i}\right) f_{x^{i}}^{\prime}\left(x_{k}^{1}, x_{k}^{2}, \ldots, x_{k}^{n}\right) \\
		  +\frac{1}{2 !} \sum_{i, j=1}^{n}\left(x^{i}-x_{k}^{i}\right)\left(x^{j}-x_{k}^{j}\right) f_{i j}^{\prime \prime}\left(x_{k}^{1}, x_{k}^{2}, \ldots, x_{k}^{n}\right) \\
		  +o^{n}
		  \end{gathered}
		  $$
	- **多元函数的泰勒展开式的矩阵形式出现了**[黑塞矩阵]([[hessian matrix]]) 
	  这里注意 $$\nabla$$ 符号的定义, 也就是[[gradient]]
		- $$
		  \begin{gathered}
		  f(\mathbf{x})=f\left(\mathbf{x}_{k}\right)+\left[\nabla f\left(\mathbf{x}_{k}\right)\right]^{T}\left(\mathbf{x}-\mathbf{x}_{k}\right)+\frac{1}{2 !}\left[\mathbf{x}-\mathbf{x}_{k}\right]^{T} H\left(\mathbf{x}_{k}\right)\left[\mathbf{x}-\mathbf{x}_{k}\right]+o^{n} \\
		  H\left(\mathbf{x}_{k}\right)=\left[\begin{array}{cccc}
		  \frac{\partial^{2} f\left(x_{k}\right)}{\partial x_{1}^{2}} & \frac{\partial^{2} f\left(x_{k}\right)}{\partial x_{1} \partial x_{2}} & \cdots & \frac{\partial^{2} f\left(x_{k}\right)}{\partial x_{1} \partial x_{n}} \\
		  \frac{\partial^{2} f\left(x_{k}\right)}{\partial x_{2} \partial x_{1}} & \frac{\partial^{2} f\left(x_{k}\right)}{\partial x_{2}^{2}} & \cdots & \frac{\partial^{2} f\left(x_{k}\right)}{\partial x_{2} \partial x_{n}} \\
		  \vdots & \vdots & \ddots & \vdots \\
		  \frac{\partial^{2} f\left(x_{k}\right)}{\partial x_{n} \partial x_{1}} & \frac{\partial^{2} f\left(x_{k}\right)}{\partial x_{n} \partial x_{2}} & \cdots & \frac{\partial^{2} f\left(x_{k}\right)}{\partial x_{n}^{2}}
		  \end{array}\right]
		  \end{gathered}
		  $$
- # Summary
	- taking information about the higher order derivatives of a function **at a single point** and translating it into information about the **value of that function near that point**.
	- 也就是用函数某一点的各阶导数值做系数构建一个多项式来近似表达这个函数
	- 展开第一项叫一阶, 展开第二项叫二阶