- Basic workflow
	- Diagram
	  collapsed:: true
		- ![Screen Shot 2022-02-26 at 5.31.08 PM.png](../assets/Screen_Shot_2022-02-26_at_5.31.08_PM_1645925471841_0.png)
	- Initializing
	  collapsed:: true
		- ```shell
		  git init
		  ```
		- This command only needs to be used once per project (**current folder**) to complete the initial setup
	- Check status (check changes)
	  collapsed:: true
		- ```shell
		  git status
		  ```
		- `untracked files` means that git sees the file but has not started tracking changes yet
	- Add changed file to staging area
	  collapsed:: true
		- ```shell
		  git add filename
		  ```
	- See changes (staged file and local saved file)
	  collapsed:: true
		- ```shell
		  git diff filename
		  ```
	- Git commit will stores changes from staging area inside the repository
	  collapsed:: true
		- ```shell
		  git commit -m "xxxxx"
		  ```
		- `-m` followed by a message, must use "", less than 50 characters
	- See the log
	  collapsed:: true
		- ```shell
		  git log
		  ```
		- A 40 character code called [[SHA]], uniquely identifies the commit
- Basic
	- Reset
	  collapsed:: true
		- 回滚工作区文件 `git checkout`
		  collapsed:: true
			- 这条命令会重写工作区!!
			- Rolling Back to Last Commit
				- restore the file in the working directory to look exactly as it did when you last made a commit
				- ```shell
				  # restore the file
				  git checkout HEAD <filename>
				  # or shortcut:
				  git checkout -- <filename>
				  ```
		- ==Unstage== file
		  collapsed:: true
			- ```shell
			  git reset HEAD filename
			  ```
		- Git Reset Using [[SHA]], 回滚commit
		  collapsed:: true
			- HEAD 是 commit you currently on
			- ```shell
			  git reset commit_SHA
			  ```
			- can be used to set `HEAD` to the `comit_SHA` commit, argument is the first ==seven== digits of a previous commit’s [[SHA]]
			- diagram explanation
			  collapsed:: true
				- ![Screen Shot 2022-02-27 at 4.27.26 PM.png](../assets/Screen_Shot_2022-02-27_at_4.27.26_PM_1646008057340_0.png)
	- Merge
	  collapsed:: true
		- merge branch
		  collapsed:: true
			- ```shell
			  git merge branch_name
			  ```
		- merge fetched changes
		  collapsed:: true
			- merge fetched changes, stored in origin/branch-name to the current branch-name branch
			- ```shell
			  git merge origin/branch-name
			  ```
	- Branch
	  collapsed:: true
		- what is branch
		  collapsed:: true
			- ![CleanShot_Learn Git & GitHub  Codecademy_20220309.png](../assets/CleanShot_Learn_Git_&_GitHub_Codecademy_20220309_1646866877538_0.png)
		- create new branch
		  collapsed:: true
			- ```shell
			  git branch branch-name
			  ```
		- 切换分支, 切换到指定的快照
		  collapsed:: true
			- ```shell
			  git checkout branchName
			  # 切换的同时创建分支
			  git checkout -b newBranch
			  git checkout commitID
			  ```
		- list all branch
		  collapsed:: true
			- ```shell
			  git branch -a
			  ```
		- `git stash` 保存当前工作进度, 并且switch branch
		  collapsed:: true
			- example
			  collapsed:: true
				- ![CleanShot_Learn Git & GitHub  Codecademy 🔊_20220308.png](../assets/CleanShot_Learn_Git_&_GitHub_Codecademy_🔊_20220308_1646808003380_0.png)
			- 当workin on a file的时候, 想修改一下之前的commit
			- ```shell
			  git stash
			  ```
			- 然后switch branch to do wok elsewhere, then retrieve the code using
			- ```shell
			  git stash pop
			  ```
		- delete branch
		  collapsed:: true
			- ```shell
			  git branch -d branch_name
			  ```
	- Commit
	  collapsed:: true
		- 修改commit
		  collapsed:: true
			- 首先改动, 然后 `git add` 然后 `git commit --amend` to update previous commit
			- ```shell
			  git commit --amend --no-edit # keep the previous command message
			  ```
	- Remotes
	  collapsed:: true
		- list the remote repo
			- Git automatically names this remote origin, because it refers to the remote repository of origin. However, it is possible to safely change its name
			- ```shell
			  git remote -v
			  ```
	- Fetch
	  collapsed:: true
		- Fetching remote origin changes (download, not merge)
			- the git fetch command downloads objects from the origin remote repository. The changes, ==however, are not merged into the current branch-name branch==. Instead, they are stored in the origin/branch-name branch, waiting to be merged
			- ```shell
			  git fetch
			  ```
	- Push
	  collapsed:: true
		- pushing branch changes to remote
		  collapsed:: true
			- pushes the branch, and all committed changes, to the remote
			- ```shell
			  git push origin branch-name
			  ```
	- Cloning
	  collapsed:: true
		- cloning a remote repo
		  collapsed:: true
			- ```shell
			  git clone remote_location clone_name
			  ```
- Advance
	- Rebase
	  collapsed:: true
		- What is rebase?
		  collapsed:: true
			- 别人已经在main merge了其他的, 就是main更新了, 但是我分branch的时候main还没有那个更新, 所以用rebase更新我之前分branch的时候main没有的内容
			- ![CleanShot_Learn Git & GitHub  Codecademy 🔊_20220310.png](../assets/CleanShot_Learn_Git_&_GitHub_Codecademy_🔊_20220310_1646980390386_0.png)
			- ![CleanShot_Learn Git & GitHub  Codecademy 🔊_20220310.png](../assets/CleanShot_Learn_Git_&_GitHub_Codecademy_🔊_20220310_1646980403396_0.png)