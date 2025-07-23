# Fix Git Tracking for Ignored Lock Files

## 1. Remove the files from Git tracking (but keep them locally):
```bash
git rm --cached <file>
```
Replace `<file>` with the name of the lock file you want to stop tracking, such as `package-lock.json` or `yarn.lock`.
#### Example:
```bash
git rm --cached yarn.lock
```
```bash
git rm --cached package-lock.json
```






## 2. Commit the change:
```bash
git commit -m "Stop tracking yarn.lock and package-lock.json"
```







## 3. Ensure they are in .gitignore:
Double-check that your .gitignore contains:
```plaintext
yarn.lock   
package-lock.json
``` 







## 4. Push the changes to the remote repository:
```bash
git push origin <branch-name>
```
Replace `<branch-name>` with the name of your current branch, such as `main` or `master`.
#### Example:
```bash
git push origin main
```
```bash
git push origin master
```
