alias:: Mean Value Theorem, 微分中值定理, 中值定理
title:: mean value theorem

- lagrange mean value theorem 拉格朗日中值定理
	- Definition
		- 如果函数$$f(x)$$满足: 在闭区间[a,b]上连续, 在开区间(a,b)上可微分, 那么至少有一点 $$\xi$$, $$a<\xi<b$$ 使下面等式成立
		  $$f(b)-f(a)=f^{\prime}(\xi)(b-a)$$
- Cauchy mean value theorem 柯西中值定理
  id:: 4c6027e5-a529-4feb-b8f5-f3c40ab8eb8e
	- 如果函数$$f(x)$$满足: 在闭区间[a,b]上连续, 在开区间(a,b)上可微分, 对任意$$x \in(a, b), g^{\prime}(x) \neq 0$$
	  那么在$$(a,b)$$ 内至少有一点$$\xi \in(a, b)$$, 使得 $$\frac{f(b)-f(a)}{g(b)-g(a)}=\frac{f^{\prime}(\xi)}{g^{\prime}(\xi)}$$ 成立