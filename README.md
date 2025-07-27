# Git Recovery Demo

## 🔍 Project Overview

This project demonstrates how to recover lost Git commits after an accidental `git push --force` using `git reflog` and `git rebase`. The scenario simulates a junior developer force-pushing an outdated branch, wiping out a week’s worth of feature work (auth, login, logout, middleware, tests).

The goal is to:
- Recover lost commits using `git reflog`
- Restore a clean history using `git rebase -i`
- Safely force-push the corrected branch using `--force-with-lease`

---

## 🛠️ Recovery Steps (Commands Executed)

```bash
# Simulate outdated force push
git checkout -b outdated-branch HEAD~3  
git push origin outdated-branch  
git checkout development

git reset --hard outdated-branch
git push origin development --force  

# Recover using reflog
git reflog
git checkout e2fd796
git checkout -b recovered-dev
git rebase -i HEAD~5

# Replace broken branch with recovered one
git checkout development
git reset --hard recovered-dev
git push origin development --force-with-lease
```

---

## 🔍 Git Log (git log)

This shows the restored commit history after recovery:
```bash
* e2fd796 (HEAD -> development, origin/development, recovered-development) day5: feat: tests
* 6e3c8c3 day4: feat: middleware
* 921092c day3: feat: logout
* 7f83356 (origin/outdated-branch, outdated-branch) day2: feat: login
* 34ebb5b day1: feat: auth
* d931ad6 (origin/main, main) Initial commit
```

![Screenshot-Reflog](http://aideck.eu/course-git/Git3.JPG)

---

## 🔍 Git Reflog (git reflog)

This shows the restored commit history after recovery:
```bash
e2fd796 (HEAD -> development, origin/development, recovered-development) HEAD@{0}: reset: moving to recovered-development
7f83356 (origin/outdated-branch, outdated-branch) HEAD@{1}: checkout: moving from recovered-development to development
e2fd796 (HEAD -> development, origin/development, recovered-development) HEAD@{2}: rebase (finish): returning to refs/heads/recovered-development
e2fd796 (HEAD -> development, origin/development, recovered-development) HEAD@{3}: rebase (start): checkout HEAD~5
e2fd796 (HEAD -> development, origin/development, recovered-development) HEAD@{4}: checkout: moving from e2fd79635fa706464c67ce07f73d0d232bf91f5e to recovered-de
velopment
e2fd796 (HEAD -> development, origin/development, recovered-development) HEAD@{5}: checkout: moving from development to e2fd796
7f83356 (origin/outdated-branch, outdated-branch) HEAD@{6}: reset: moving to outdated-branch
e2fd796 (HEAD -> development, origin/development, recovered-development) HEAD@{7}: checkout: moving from outdated-branch to development
7f83356 (origin/outdated-branch, outdated-branch) HEAD@{8}: checkout: moving from development to outdated-branch
e2fd796 (HEAD -> development, origin/development, recovered-development) HEAD@{9}: checkout: moving from main to development
d931ad6 (origin/main, main) HEAD@{10}: checkout: moving from outdated-branch to main
7f83356 (origin/outdated-branch, outdated-branch) HEAD@{11}: checkout: moving from development to outdated-branch
e2fd796 (HEAD -> development, origin/development, recovered-development) HEAD@{12}: commit: day5: feat: tests
6e3c8c3 HEAD@{13}: commit: day4: feat: middleware
921092c HEAD@{14}: commit: day3: feat: logout
7f83356 (origin/outdated-branch, outdated-branch) HEAD@{15}: commit: day2: feat: login
34ebb5b HEAD@{16}: commit: day1: feat: auth
d931ad6 (origin/main, main) HEAD@{17}: checkout: moving from main to development
d931ad6 (origin/main, main) HEAD@{18}: commit (initial): Initial commit
```

![Screenshot-Reflog](http://aideck.eu/course-git/Git4.JPG)
