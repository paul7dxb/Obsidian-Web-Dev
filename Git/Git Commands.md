
# Basics

- Make new repo and commit to it
```bash
git init .
git add .
git commit -m "commit message"
# Set up remote repo
# Origin is what remote will be called
git remote add origin <urlOfRepo>
git branch -M main
# Tell it where to push to for first push
# -u is upstream
git push -u origin main
```

# Git Local
## Git Branch

- Create Branch and then checkout
```bash
git branch <branchName>
git checkout <branchName>
```

```bash
# One line to create and checkout
git checkout -b <branchName>
```

## Git Merge

```bash
git merge <branchName>
```

## Git Status

 - Tells commit
 - Tells current changes since commit
``` bash
git status
```

# Git Remote

## Upload to new repo

- Create repo on github

```bash

```
## Git Fetch

- Bring in remote changes but don't move HEAD 

## Git Pull

- Syncs HEAD with remote

# Git Push


# Git Discard local changes

- Get rid of local changes

```bash
git reset --hard
```


# Git Review Requests

- Pull

# Get latest changes

```bash

git checkout main
git pull
git checkout <your-branch-name>
git merge main

git checkout -b mm-38-404-page-2

git checkout -b mm-65-quiz-answer-hover

git checkout -b mm-64-quiz-over-button

git checkout MM-31-Quiz-page
git checkout mm-38-404-page-2
git merge mm-51-area-51-page

git checkout mm-51-area-51-page

git merge MM-31-Quiz-page

journey-planner-map
```

# Git Get All branches

```
git branch -a
```