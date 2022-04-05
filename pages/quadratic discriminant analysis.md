alias:: 二次判别分析, QDA
type:: supervised, classification

- Quadratic discriminant analysis when $p>1$ (多个预测变量)
	- ==Procedure==
		- dataset
		  collapsed:: true
			- $$
			  f_{1}(x)=N_{p}\left(\underline{\mu_{1}}, \Sigma_{1}\right)
			  $$
			  $$
			  f_{2}(x)=N_{p}\left(\underline{\mu_{2}}, \Sigma_{2}\right)
			  $$
			  $$
			  f_{3}(x)=N_{p}\left(\underline{\mu_{3}}, \Sigma_{3}\right)
			  $$
			- ![CleanShot_da (page 70  102)_20220403@2x.png](../assets/CleanShot_da_(page_70_102)_20220403@2x_1649039498873_0.png)
			- ![CleanShot_da (page 72  102)_20220403@2x.png](../assets/CleanShot_da_(page_72_102)_20220403@2x_1649039530040_0.png)
		- ((624a35fb-6413-4819-b374-1953165cece4))
		- according to ((6247a8cf-17cd-47c0-b3cb-58bca404aefa))
		  collapsed:: true
			- 下划线是 vector 是 dataset 里面的 row
			- $$
			  p_{k}(\underline{x})=\frac{f_{k}(\underline{x}) \pi_{k}}{\sum_{i=1}^{i=3} f_{i}(\underline{x}) \pi_{i}} =
			  \frac{\frac{1}{(\sqrt{2 \pi})^{p}\left|\Sigma_{k}\right|^{1 / 2}} e^{-\frac{1}{2}\left(\underline{x}-\underline{\mu}_{k}\right)^{T} \Sigma_{k}^{-1}\left(\underline{x}-\underline{\mu}_{k}\right)} \pi_{k}}{\sum_{i=1}^{i=3} \frac{1}{(\sqrt{2 \pi})^{p}\left|\Sigma_{i}\right|^{1 / 2}} e^{-\frac{1}{2}\left(\underline{x}-\underline{\mu}_{i}\right)^{T} \Sigma_{i}^{-1}\left(\underline{x}-\underline{\mu}_{i}\right)} \pi_{i}}
			  $$
			- cancel common factor
			- $$
			  \begin{aligned}
			  p_{k}(\underline{x}) &=\frac{f_{k}(\underline{x}) \pi_{k}}{\sum_{i=3}^{i=3} f_{i}(\underline{x}) \pi_{i}} \\
			  n_{k}(\underline{x}) &=\frac{1}{\left|\Sigma_{k}\right|^{1 / 2}} e^{-\frac{1}{2}\left(\underline{x}-\underline{\mu}_{k}\right)^{T} \Sigma_{k}^{-1}\left(\underline{x}-\underline{\mu}_{k}\right)} \pi_{k}
			  \end{aligned}
			  $$
			- normalize $n_{k}(\underline{x})$ to get $p_k(x)$
			  choose the class with largest $n_k(\underline{x})$
- [[CheatSheet/R]] QDA example 1 (with `qda()`)
	- build model with qda()
	  collapsed:: true
		- ![CleanShot_da (page 79  102)_20220403@2x.png](../assets/CleanShot_da_(page_79_102)_20220403@2x_1649040022319_0.png)
	- confusion matrix and error rate
	  collapsed:: true
		- ![CleanShot_da (page 81  102)_20220403@2x.png](../assets/CleanShot_da_(page_81_102)_20220403@2x_1649040236749_0.png)
-