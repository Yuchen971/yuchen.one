topic:: optimization
type:: #lecturenote

- # Notes
	- What is the big picture of the optimization? #recall
	  collapsed:: true
		- $$\boldsymbol{x}^{*}=\arg \min _{\boldsymbol{x} \in X} f(\boldsymbol{x})$$
			- $f$ is the [[objective function]], $$X$$ is the domain, $${x}^{*}$$ is the minimize
			- if $$f$$ is strictly [[convex]] function on $$X$$ , then the minimizer is unique
	- What is the hierarchy of optimization problems? #recall
	  collapsed:: true
		- LP: [[linear programming]] $\subseteq$ QP: [[quadratic programming]]
		  $\subseteq$ SOCP: [[second-order cone programming]] $\subseteq$ SDP: [[semi-definite programming]] $\subseteq$ CP: [[conic programming]]
		- solution for more general problem class also solve the subsumed problem classes
	- [[Math Notation]]
	- [[matrix]]
	- What is the derivation in One Dimension? #recall
	  collapsed:: true
		- Let $$X$$ be an open subset of $$\mathbb{R}$$ and let $$f: X \rightarrow \mathbb{R}$$. Then $$f$$ is differentiable at $$x \in X$$ with derivative $$\frac{d}{d x} f(x)$$ if the following limit exists:
		  $$
		  \frac{d}{d x} f(x)=\lim _{h \rightarrow 0} \frac{1}{h}(f(x+h)-f(x))
		  $$
		- 也就是导数
	- What is [[gradient]] and [[partial derivatives]]? #recall
	- What is [[hessian matrix]]? #recall
	- What is [[taylor expansion]]? #recall
	- What is [[convex]] (Convexity)?
	-