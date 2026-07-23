# Remove a file from git

## 1. Git tracking থেকে remove করুন
```bash
git rm --cached celerybeat-schedule-wal
git rm --cached celerybeat-schedule-shm
```

## 2. যদি অন্য path-এ থাকে, তাহলে সেই path ব্যবহার করুন, যেমন:
```bash
git rm --cached path/to/celerybeat-schedule-wal
git rm --cached path/to/celerybeat-schedule-shm
```

## 3. `.gitignore`-এ যোগ করুন
```bash
celerybeat-schedule*
```
এতে celerybeat-schedule, celerybeat-schedule-wal, celerybeat-schedule-shm—সবগুলো ignore হবে।

## 4. Commit করুন
```bash
git add .gitignore
git commit -m "Ignore Celery Beat schedule files"
git push
```