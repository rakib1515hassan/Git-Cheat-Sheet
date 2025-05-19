# Generate SSH Key

## 1. Generate a New SSH Key (on Ubuntu Server)
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
### Generate a new key with a custom name:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/id_ed25519_echallan
```



## 2. Display & Copy the SSH Public Key
### Run this command to show your public key (id_ed25519.pub):
```bash
cat ~/.ssh/id_ed25519.pub
```



## 3. Add the SSH Key to the SSH Agent
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```


## 4. Copy the SSH Public Key
```bash
cat ~/.ssh/id_ed25519.pub
```



## 5. Add the SSH Key to GitHub
```bash
1. Go to GitHub → Settings → SSH and GPG Keys (direct link).

2. Click "New SSH Key".

3. Paste the copied key and give it a name (e.g., Ubuntu Server - EChallan Project).

4. Click "Add SSH Key".
```


## 6. Configure Git to Use SSH (for existing projects)
```bash
git remote set-url origin git@github.com:username/repo.git
```



## 7. Verify SSH Connection
```bash
ssh -T git@github.com
```
### Hi username! You've successfully authenticated...




# Switch Git Remote URL to SSH (If Needed)

## 1. Check Your Remote URL
```bash
git remote -v
```


## 2. Change HTTPS Remote to SSH

### Update the remote URL to use SSH instead of HTTPS:
```bash
git remote set-url origin git@github.com:username/repo.git
```
### (Replace username/repo.git with your actual GitHub username and repository name.)


### Example:
```bash
git remote set-url origin git@github.com:rakib1515hassan/e-challan-web.git
```


## 3. Verify SSH Authentication

```bash
ssh -T git@github.com
```
### Expected output: Hi rakib1515hassan! You've successfully authenticated...

