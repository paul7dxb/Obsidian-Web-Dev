# Branches
[Git Branches](https://geo-jobe.com/mapthis/git-good-with-visual-studio-code/)

Swith back to master and then merge from other branch

[VSCode merge back to main](https://stackoverflow.com/questions/61755744/git-how-to-merge-feature-branch-into-master-using-vs-code-source-control)

# Branch

- Create branch
- Make change
- Merge change

- install vscode

- Open folder in vscode
	- `code .`

- modules
	- my_module

- Merge
	- git status
		- Show files that aren't being tracked
	- git add filename.py
	- git status
		- Files will now be displayed
	- git commit -m 'commit message'
	- git status
		- Will now be ahead
	- git push
		- Publish local changes
		- If there is changes since you will get message to pull change
		- git pull

Working on the same branch causes issues
- Set global
	- git config pull.rebase false

# Create Branch

- git branch
	- Shows known branches
- git checkout -b branchName
	- Switches to branch
	- Creates if new
- git branch
	- Shows new branch
- Make changes to files in branch
	- git add fileName

## Merge changes back to main

- Make sure files are added
- git commit -m 'commit message'
- If new branch
	- Create new branch origin
	- git push --set-upstream origin branch
- git pull
- git checkout main
- git pull
- git merge --no-ff --no-commit branchName
	- --no-ff no fast forward
	- --no-commit
		- stops before commiting
- git status
- git commit -m 'merged branchName into main'
- git push

# Protecting main
- Only maintainers of the project can make changes on that branch
