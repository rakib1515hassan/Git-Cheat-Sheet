# Server-এ Force Git Pull করা (Local Changes বাদ দিয়ে)

## Purpose (উদ্দেশ্য)

Server-এ যখন `git pull` কাজ করে না কারণ server-এ local changes আছে বা merge conflict হয়েছে, তখন এই procedure follow করো। এটা করলে server-এর tracked code পুরোপুরি remote Git branch-এর সাথে match করবে।

---

## ⚠️ সতর্কতা

এই commands গুলো local code changes **permanently মুছে ফেলতে পারে**। কিছু করার আগে important files backup করে নাও। `.env`, `media/`, `uploads/`, database files বা অন্য কোনো production data **কখনো delete করো না**।

---

## 1. Project directory-তে যাও

```bash
cd /path/to/your/project
```

তোমার actual project directory-র path দিয়ে replace করো।

## 2. Current Git state check করো

```bash
git status
git branch --show-current
```

কিছু করার আগে project আর branch confirm করে নাও।

---

## 3. 🔍 দেখো কোন কোন file-এ conflict বা changes আছে এবং সেগুলো কি

### সব changed/staged/untracked files দেখো:

```bash
git status
```

### ঠিক কোন কোন line-এ কি change হয়েছে সেটা দেখো (unstaged changes):

```bash
git diff
```

### যদি কিছু staged (git add) করা থাকে, সেই changes দেখো:

```bash
git diff --staged
```

### Merge conflict চলমান থাকলে, শুধু conflict ওয়ালা files-এর নাম দেখো:

```bash
git diff --name-only --diff-filter=U
```

### প্রতিটা conflict file-এর ভেতরে ঠিক কোথায় conflict সেটা দেখো:

```bash
grep -rn "<<<<<<< " .
```

> **Conflict বুঝার নিয়ম:**
>
> ```
> <<<<<<< HEAD
> তোমার local change (server-এ যা ছিল)
> =======
> remote-এর change (GitHub/GitLab থেকে আসা code)
> >>>>>>> origin/main
> ```
>
> `<<<<<<<` থেকে `=======` পর্যন্ত = **তোমার local code**
> `=======` থেকে `>>>>>>>` পর্যন্ত = **remote-এর code**

---

## 4. (Recommended) Important server files backup করো

```bash
# .env file backup
cp .env .env.backup 2>/dev/null

# media/uploads folder backup (যদি থাকে)
cp -r media/ media_backup/ 2>/dev/null
cp -r uploads/ uploads_backup/ 2>/dev/null

# database file backup (SQLite হলে)
cp db.sqlite3 db.sqlite3.backup 2>/dev/null
```

কখনো assume করো না যে Git untracked files বা server data protect করবে।

---

## 5. যদি merge অবস্থায় আটকে থাকো, আগে সেটা abort করো

```bash
git merge --abort 2>/dev/null
git rebase --abort 2>/dev/null
```

---

## 6. Latest remote code fetch করো

```bash
git fetch origin
```

---

## 7. সব local changes মুছে server code কে remote-এর সাথে match করাও

`main` branch-এর জন্য:

```bash
git reset --hard origin/main
```

> `main` এর জায়গায় তোমার branch name বসাও। যেমন: `origin/master` বা `origin/develop`

এটা current checkout-কে `origin/main`-এর commit-এ reset করে দেয় আর tracked files-এর সব local changes মুছে ফেলে। সাথে সাথে current index/merge conflict state-ও clear হয়ে যায়।

**`git reset --hard` এর পর আর `git pull` দেওয়ার দরকার নেই** — reset already local checkout-কে fetched remote branch commit-এ point করে দিয়েছে।

---

## 8. Untracked files পরিষ্কার করো (সাবধানে)

```bash
# আগে দেখো কি কি delete হবে (dry run — কিছু মুছবে না)
git clean -fd --dry-run

# সব ঠিক মনে হলে তখন actually মুছো
git clean -fd
```

> **সাবধান:**
> - `.env`, `media/`, `uploads/` যদি `.gitignore`-এ থাকে তাহলে এই command সেগুলো মুছবে না। তবুও dry-run দিয়ে আগে check করো।
> - `git clean -fdx` ignored files-ও remove করে — এটা **especially dangerous**। `-fdx` avoid করো যদি না পুরোপুরি consequences বুঝে থাকো।

---

## 9. Result verify করো

```bash
git status
git log --oneline -3
```

Clean working tree-তে normally এরকম দেখাবে:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

---

## Quick Summary (এক নজরে)

| Command | কাজ |
|---|---|
| `git status` | কোন files changed/conflicted দেখায় |
| `git diff` | ঠিক কি change হয়েছে দেখায় |
| `git diff --staged` | staged changes দেখায় |
| `git diff --name-only --diff-filter=U` | শুধু conflict files-এর নাম দেখায় |
| `grep -rn "<<<<<<< " .` | conflict-এর exact location দেখায় |
| `git merge --abort` | চলমান merge abort করে |
| `git fetch origin` | remote-এর latest info আনে |
| `git reset --hard origin/main` | local code = remote code করে দেয় |
| `git clean -fd --dry-run` | কি কি untracked file মুছবে preview দেখায় |
| `git clean -fd` | untracked files মুছে দেয় |

---

## Quick Commands (main branch)

Project directory confirm আর important files backup করার পরেই শুধু এগুলো use করো:

```bash
git fetch origin
git reset --hard origin/main
git clean -fd
git status
```

---

## Important Notes (গুরুত্বপূর্ণ বিষয়)

- এই commands তোমার database backup বা reset করে না।
- Production secrets বা user uploads কখনো Git-এ store করো না। এগুলো source checkout-এর বাইরে secure, persistent location-এ রাখো।
- Project যদি Docker, virtual environments, Node.js বা Python dependencies use করে, তাহলে code update-এর পর project-এর deployment procedure follow করো (যেমন: `pip install -r requirements.txt`, `npm install`, `docker-compose up --build` ইত্যাদি)।
