- Git workflow
	- Fetch and merge changes from the remote
	  collapsed:: true
		- ```shell
		  git fetch
		  git merge origin/master
		  ```
	- Create a branch to work on a new project feature
	- Develop the feature on your branch and commit your work
	- Fetch and merge from the remote again (in case new commits were made while you were working)
	- Push your branch up to the remote for review
	  collapsed:: true
		- ```shell
		  git push origin <branch_name>
		  ```
- 下载
	- linux 命令行下载github release 资源
	  collapsed:: true
		- ```shell
		  wget --no-check-certificate --content-disposition <address>
		  ```
- Trick
	- `git log` 其他用法 (图形显示和搜索)
	  collapsed:: true
		- ```shell
		  git log --oneline #shows th list o fcommits in one line format
		  git log -S "keyword" #displays a list of commits that contain the keyword in the message
		  git log --oneline --graph # visual显示
		  ```
	- 用 `aliases` 来缩写command
	  collapsed:: true
		- ```shell
		  git config --global alias.co "checkout"
		  git config --global alias.br "branch"
		  git config --global alias.glop "log --pretty=format:"%h %s" --graph"
		  ```
- Others
	- Show the `HEAD` (first) commit
	  collapsed:: true
		- ```shell
		  git show HEAD
		  ```