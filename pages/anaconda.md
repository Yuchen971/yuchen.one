alias:: Anaconda

- Debug
	- conda command not find
		- anaconda的路径，一般是/usr/local/anaconda3/bin/conda, 然后/usr/local/anaconda3/conda init zsh，再重启终端
	- conda package not found
		- conda config --append channels conda-forge
- 环境管理
	- ```shell
	  conda create --name myenv # 创建新环境
	  conda create -n myenv python=3.6 # 指定版本
	  conda env list # 查看所有environment
	  conda create --name myclone --clone myenv # 环境克隆
	  ```