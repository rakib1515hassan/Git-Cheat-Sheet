# Git Branch 

## 1. To see list all branches on your repository.
```bash 
git branch
```



## 2. Create a new branch.
```bash 
git branch <branch_name>
```
#### Example:
```bash 
git branch dev_rakib
```



## 3. Delete a merged branch.
```bash 
git branch -d <branch_name>
```
#### Example:
```bash 
git branch dev_rakib
```



## 4. Force delete an unmerged branch.
```bash 
git branch -D <branch>
```



## 5. Switch to a different branch.
`
git checkout <branch>
`
```bash 
git checkout <branch>
```



## 6. Create and switch to a new branch.
`
git checkout -b <new-branch>
`
```bash 
git checkout -b dev_rakib
```



## 7. Merge changes from a branch into the current branch.
`
git merge <branch>
`
>[!NOTE]
> If I am in the main branch and I want to merge with dev_rakib
```bash 
git merge dev_rakib
```



## 8. Set the upstream branch for the current local branch.
`
git push --set-upstream <remote> <branch>
`
#### Example
```bash 
git push --set-upstream origin dev_rakib
```
#### Example (Shorter Version)
```bash 
git push -u origin dev_rakib
```



## 9. Delete a remote tracking branch.
```bash 
git branch -dr <remote>/<branch>
```

# Fetch branches from git
## 1. Fetch the latest branches from the remote
```bash
git fetch origin
```
## 2. Check whether the branch exists
```bash
git branch -r
```
Look for origin/dev_rakib in the list.
## 3. Create a local branch and switch to it
```bash
git switch -c dev_rakib --track origin/dev_rakib
```
This creates a local dev_rakib branch that tracks the remote branch.
## 4. Verify your current branch
```bash
git branch
```
