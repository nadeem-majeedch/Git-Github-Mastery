# Part 5: Introduction to GitHub

> **Level:** 🟢 Beginner ➡ 🔵 Expert
> **Goal:** Understand remote hosting platforms and master push, pull, and clone.

---

## 5.1 What is GitHub / GitLab / Bitbucket?

**Git** is the tool (local). **GitHub** is a *hosting platform* for Git repositories — a home for your code online, plus collaboration features.

### The Big Three

| Platform | Maker | Highlights |
|----------|-------|------------|
| **GitHub** | Microsoft | Largest community, Actions (CI/CD), Codespaces, free for open source |
| **GitLab** | GitLab Inc. | Self-hosted option, built-in CI/CD, strong DevOps focus |
| **Bitbucket** | Atlassian | Tight Jira integration, good for enterprise teams |

> 💡 **Pro Tip:** This course uses GitHub, but **90% of the commands are identical** on GitLab and Bitbucket. Learn the tool, not the website.

### What does a hosting platform give you?

- ☁️ A **remote copy** of your repo (a backup + collaboration point).
- 🎫 **Issues** — bug tracking and feature requests.
- 🔀 **Pull Requests / Merge Requests** — code review (see [Part 6](./part-6-collaboration-workflows.md)).
- ⚙️ **CI/CD** — automated tests and deployment.

```mermaid
graph LR
    L["Your Laptop (local repo)"] <-->|"push / pull"| R["GitHub (remote repo)"]
    T["Teammate laptop"] <--> R
```

---

## 5.2 Remote Repositories (`git remote`)

A **remote** is a URL/name pointing to a copy of your repo elsewhere.

```bash
git remote            # list remote names
git remote -v         # list remotes with URLs
git remote add origin https://github.com/you/repo.git
git remote remove origin
git remote rename origin github
```

- **`origin`** is the *convention* for your primary remote. It is not special — just a name.

---

## 5.3 Push, Pull, Clone

### `git clone` — copy an existing repo (remote → local)

```bash
git clone https://github.com/you/repo.git
git clone https://github.com/you/repo.git my-local-folder
```

This creates a folder, sets up `origin`, and checks out the default branch. One command = full setup.

### `git push` — send local commits (local → remote)

```bash
git push                      # push current branch to its upstream
git push -u origin main       # set upstream AND push (first time)
git push origin my-feature    # push a specific branch
```

The **`-u` / `--set-upstream`** flag links your local branch to a remote branch, so later `git push` and `git pull` know where to go.

### `git pull` — receive remote commits (remote → local)

```bash
git pull          # fetch + merge in one step
git pull origin main
```

> ⚠️ **Warning:** `git pull` can trigger a **merge** (and conflicts). If you have uncommitted work, commit or **stash** first (see [Part 7](./part-7-advanced-git.md)).

```mermaid
graph TD
    C["git clone"] --> L["Local repo"]
    L -->|"git push"| R["Remote (GitHub)"]
    R -->|"git pull"| L
```

---

## 🟢 Beginner Example — Cloning a Repo

You found a project you love on GitHub and want a local copy.

```bash
# 1. Click the green "Code" button on GitHub and copy the HTTPS URL
# 2. Clone it
git clone https://github.com/octocat/Spoon-Knife.git

# 3. Enter the folder
cd Spoon-Knife

# 4. Confirm the remote is set up
git remote -v
# origin  https://github.com/octocat/Spoon-Knife.git (fetch)
# origin  https://github.com/octocat/Spoon-Knife.git (push)

# 5. Look at the history
git log --oneline --max-count=5
```

That is it — you now have the entire repository, including **all of its history**, on your machine. 📦

---

## 🔵 Expert Example — Setting Multiple Remotes for Upstream

**Scenario:** You are contributing to the popular open-source project **`octocat/awesome-project`**. You cannot push directly, so you **fork** it to your account and add **two remotes**:

- **`origin`** → your fork (you push here).
- **`upstream`** → the original project (you pull updates from here).

```bash
# 1. Clone YOUR fork
git clone https://github.com/you/awesome-project.git
cd awesome-project

# 2. Add the upstream remote
git remote add upstream https://github.com/octocat/awesome-project.git

# 3. Verify
git remote -v
# origin    https://github.com/you/awesome-project.git   (fetch/push)
# upstream  https://github.com/octocat/awesome-project.git (fetch/push)
```

### Daily sync routine (keeps your fork current)

```bash
git fetch upstream                # get upstream's branches (no merge yet)
git switch main
git merge upstream/main           # merge upstream changes into your main
git push origin main              # update your fork
```

> 💡 **Pro Tip:** Fetching is **safe** — it only downloads new data. Merging is what changes your files. When unsure, `git fetch` first, inspect, then merge.

### Advanced: limit what you fetch

```bash
git fetch upstream main:refs/remotes/upstream/main   # fetch only main
git fetch --prune origin                             # remove deleted remote branches
```

---

## ⚠️ Common Mistakes

- ❌ **Pushing to `main` directly** when working in a team.
- ❌ **`git pull` with uncommitted local changes** → messy conflicts. Commit or stash first.
- ❌ **Forgetting `-u` on first push** → Git complains your branch has no upstream.
- ❌ **Committing credentials** — GitHub will block plain `https://user:token@...` URLs in public repos; use **SSH keys** or a credential helper.

### Authentication quick note

Use **SSH keys** (recommended) or a **personal access token (PAT)** with HTTPS:

```bash
# Check current auth method
git config --get remote.origin.url
```

---

## ✅ Key Takeaways

- **GitHub/GitLab/Bitbucket** host your repos and add issues, PRs, and CI/CD.
- **`git remote`** manages named pointers to remote copies.
- **`git clone`** copies a repo down; **`git push`** sends commits up; **`git pull`** brings commits down.
- Professionals track **both** `origin` (fork) and `upstream` (original) when contributing to open source.

---

## 📍 Next Steps

- ⏭️ Continue to **[Part 6: Collaboration Workflows](./part-6-collaboration-workflows.md)** — forks, PRs, and reviews.
- 📋 Need a command fast? Open the **[Cheat Sheet](./cheatsheet.md)**.
- 🔄 Want the full workflow at a glance? See the **[Command Sequence](./git-commands-sequence.md)**.
