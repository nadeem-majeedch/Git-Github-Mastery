# 📋 Git Cheat Sheet

> Quick reference for the most common Git commands, grouped by category.
> Pair this with the [Command Sequence](./git-commands-sequence.md) to see them in workflow order.

---

## ⚙️ Setup & Config

```bash
git config --global user.name "Your Name"     # set your name
git config --global user.email "you@email.com" # set your email
git config --list                              # view all settings
git config user.name                           # view one setting
git config --global core.editor "code --wait"  # set editor
git config --global init.defaultBranch main    # default branch = main
git config --global core.autocrlf input        # avoid line-ending issues
git help --config                              # open docs
```

---

## 📝 Local Changes

```bash
git init                 # create a new repo
git status               # show current state
git status --short       # condensed state
git add file.txt         # stage one file
git add .                # stage everything
git add -p               # stage changes hunk by hunk
git commit -m "message"  # commit staged changes
git commit -am "message" # stage tracked changes + commit
git diff                 # unstaged changes
git diff --cached        # staged changes
git diff HEAD            # all changes vs last commit
```

---

## 🕘 History & Logs

```bash
git log                      # full history
git log --oneline            # compact history
git log --oneline --graph    # visual branch history
git log --oneline --all      # all branches
git log -p                   # history with diffs
git log --stat               # files changed per commit
git log --author="Name"      # filter by author
git log --since="2 weeks ago" # filter by date
git show <sha>               # details of one commit
git blame file.txt           # who changed each line
```

---

## 🌿 Branching & Merging

```bash
git branch                    # list local branches
git branch -a                 # list all branches
git branch <name>             # create a branch
git branch -d <name>          # delete a merged branch
git branch -D <name>          # force-delete a branch
git switch <name>             # switch branch
git switch -c <name>          # create + switch
git checkout -b <name>        # create + switch (old style)
git merge <branch>            # merge branch into current
git merge --abort             # abort a merge
git mergetool                 # resolve conflicts with a tool
```

---

## 🌐 Remote Repositories

```bash
git clone <url>               # copy a remote repo
git remote -v                 # list remotes
git remote add origin <url>   # add a remote
git remote remove origin      # remove a remote
git remote rename origin up   # rename a remote
git push                      # push current branch
git push -u origin main       # push + set upstream
git push origin <branch>      # push a branch
git push --delete origin <b>  # delete remote branch
git pull                      # fetch + merge
git fetch                     # fetch without merging
git fetch upstream            # fetch from another remote
git ls-remote origin          # list remote refs
```

---

## ↩️ Undoing & Recovery

```bash
git restore file.txt          # discard unstaged changes (working tree)
git restore --staged file.txt # unstage a file
git checkout -- file.txt      # discard changes (old style)
git reset HEAD~1              # undo last commit, keep changes
git reset --soft HEAD~1       # undo last commit, keep staged
git reset --hard HEAD~1       # undo last commit, DISCARD changes ⚠️
git revert <sha>              # new commit that undoes <sha> (safe)
git stash                     # save uncommitted work
git stash list                # list stashes
git stash pop                 # restore latest stash
git stash drop stash@{0}      # delete a stash
git cherry-pick <sha>         # copy a commit onto current branch
git reflog                    # local HEAD movement log
git fsck --lost-found         # find dangling (lost) objects
```

---

## 🧪 Advanced

```bash
git rebase <branch>           # replay current branch on top
git rebase -i HEAD~3          # interactive rebase (clean up commits)
git rebase --continue         # continue after resolving conflicts
git rebase --abort            # abort a rebase
git tag v1.0.0                # tag the current commit
git tag -a v1.0.0 -m "..."    # annotated tag
git show-ref                  # list all refs
git cat-file -t <sha>         # object type
git cat-file -p <sha>         # object content
git log --grep="fix"          # search commit messages
git clean -fd                 # remove untracked files ⚠️
```

---

## 🔑 Authentication (HTTPS)

```bash
git config --global credential.helper store   # remember credentials
# Or use SSH keys:
ssh-keygen -t ed25519 -C "you@email.com"      # generate key
cat ~/.ssh/id_ed25519.pub                     # copy to GitHub -> Settings -> SSH keys
```

---

> 💡 **Remember:** When in doubt, run **`git status`** first — it tells you exactly what is going on.
>
> ⚠️ **Danger zone:** `reset --hard`, `clean -fd`, and force-push (`push --force`) permanently delete or overwrite work. Double-check before running.
