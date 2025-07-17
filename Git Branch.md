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





