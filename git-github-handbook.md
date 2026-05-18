# 🚀 Git & GitHub Handbook — 2026 Edition
> *From Zero to Production-Ready. Built for Java developers and beyond.*

---

## 📖 Table of Contents

1. [What is Git & Why It Matters](#1-what-is-git--why-it-matters)
2. [Installation & First-Time Setup](#2-installation--first-time-setup)
3. [Core Concepts Visualized](#3-core-concepts-visualized)
4. [Essential Commands](#4-essential-commands)
5. [Branching Like a Pro](#5-branching-like-a-pro)
6. [GitHub — Working with Remote Repos](#6-github--working-with-remote-repos)
7. [Pull Requests & Code Reviews](#7-pull-requests--code-reviews)
8. [Merging & Resolving Conflicts](#8-merging--resolving-conflicts)
9. [Advanced Git Commands](#9-advanced-git-commands)
10. [Undoing Mistakes](#10-undoing-mistakes)
11. [Git Flags Cheatsheet](#11-git-flags-cheatsheet)
12. [Commit Messages — The Right Way](#12-commit-messages--the-right-way)
13. [.gitignore — Production-Level Setup](#13-gitignore--production-level-setup)
14. [Branch Naming Conventions](#14-branch-naming-conventions)
15. [Git Shortcuts & Aliases](#15-git-shortcuts--aliases)
16. [Git for Java Developers](#16-git-for-java-developers)
17. [Real-World Workflows](#17-real-world-workflows)
18. [AI-Era Git Tips (2026)](#18-ai-era-git-tips-2026)
19. [Quick Reference Cheatsheet](#19-quick-reference-cheatsheet)

---

## 1. What is Git & Why It Matters

**Git** is a free, distributed version control system. Think of it as a *time machine* for your code — you can save checkpoints, go back in time, and work on different versions simultaneously.

**GitHub** is a cloud platform that hosts your Git repositories so you can collaborate, share code, and contribute to open source.

### Why Every Developer Needs Git

| Without Git | With Git |
|---|---|
| "final_v3_FINAL.java" | Clean commit history |
| Emailing code to teammates | Pull Requests |
| Accidentally deleting work | `git revert` saves you |
| Only one person works at a time | Parallel branches |
| No idea who broke what | `git blame` |

---

## 2. Installation & First-Time Setup

### Install Git

- **Windows:** Download from [git-scm.com](https://git-scm.com)
- **Mac:** Run `xcode-select --install` or install via Homebrew: `brew install git`
- **Linux (Ubuntu/Debian):** `sudo apt install git`

### Verify Installation

```bash
git --version
# git version 2.47.x
```

### Configure Your Identity (Do This First!)

```bash
# Your name and email will appear on every commit
git config --global user.name "Priyanshu"
git config --global user.email "you@example.com"

# Set VS Code as default editor (or any editor you prefer)
git config --global core.editor "code --wait"

# Set the default branch name to 'main'
git config --global init.defaultBranch main

# Auto-convert line endings (important on Windows)
git config --global core.autocrlf true   # Windows
git config --global core.autocrlf input  # Mac/Linux
```

### Check Your Config

```bash
git config --list
```

---

## 3. Core Concepts Visualized

### The Three Zones

```
┌──────────────────┐    git add     ┌──────────────────┐   git commit   ┌──────────────────┐
│  Working         │ ─────────────► │  Staging Area    │ ─────────────► │  Repository      │
│  Directory       │                │  (Index)         │                │  (.git folder)   │
│                  │ ◄───────────── │                  │ ◄───────────── │                  │
│  Your code files │  git restore   │  Files ready to  │  git reset     │  Saved snapshots │
│                  │                │  be committed    │                │  (commits)       │
└──────────────────┘                └──────────────────┘                └──────────────────┘
```

### What a Commit Actually Is

A commit is a **snapshot**, not a diff. Git stores the complete state of your files at that moment, along with:
- A unique hash (e.g., `a3f9d21`)
- Author name & email
- Timestamp
- Commit message
- Pointer to the parent commit

### How Branches Work

```
main:    A ── B ── C ──────────── F (merge commit)
                    \            /
feature:             D ── E ────
```

Each branch is just a lightweight **pointer** to a commit. Creating a branch costs almost nothing.

---

## 4. Essential Commands

### Starting a Project

```bash
# Initialize a new repo in the current folder
git init

# Clone an existing repo from GitHub
git clone https://github.com/username/repo-name.git

# Clone into a specific folder name
git clone https://github.com/username/repo-name.git my-project
```

### The Daily Workflow

```bash
# 1. Check what's changed
git status

# 2. See the actual changes (line by line)
git diff                    # unstaged changes
git diff --staged           # staged changes (what will be committed)

# 3. Stage files
git add filename.java       # specific file
git add src/                # entire folder
git add .                   # everything (use carefully)
git add -u                  # only already-tracked files (skips new files)
git add -p                  # interactive: choose which chunks to stage

# 4. Commit
git commit -m "feat: add user authentication"
git commit -am "fix: correct null pointer in UserService"  # stage + commit tracked files

# 5. Push to remote
git push origin main
git push origin feature/login  # push specific branch
```

### Checking History

```bash
git log                          # full log
git log --oneline                # compact one line per commit
git log --oneline --graph        # visual branch tree
git log --oneline -10            # last 10 commits
git log --author="Priyanshu"     # filter by author
git log --since="2 weeks ago"    # filter by time
git log -- src/UserService.java  # commits touching a specific file
git show a3f9d21                 # show details of one commit
```

---

## 5. Branching Like a Pro

### Creating & Switching Branches

```bash
# Create a new branch
git branch feature/user-login

# Switch to it
git checkout feature/user-login

# ✅ Better: create AND switch in one command
git checkout -b feature/user-login

# Modern syntax (Git 2.23+)
git switch -c feature/user-login

# List all branches
git branch          # local only
git branch -a       # local + remote
git branch -v       # with last commit info

# Delete a branch (after merging)
git branch -d feature/user-login

# Force delete (even if not merged — be careful!)
git branch -D feature/user-login
```

### Renaming a Branch

```bash
# Rename current branch
git branch -m new-name

# Rename a specific branch
git branch -m old-name new-name
```

### Checking Out a Previous Commit (Detached HEAD)

```bash
# Look at old code without changing anything
git checkout a3f9d21

# ⚠️ This puts you in "detached HEAD" state — go back with:
git checkout main
```

---

## 6. GitHub — Working with Remote Repos

### Connecting to GitHub

```bash
# Add a remote (called 'origin' by convention)
git remote add origin https://github.com/username/repo.git

# See your remotes
git remote -v

# Change remote URL (e.g., switching from HTTPS to SSH)
git remote set-url origin git@github.com:username/repo.git

# Remove a remote
git remote remove origin
```

### Syncing with Remote

```bash
# Download changes WITHOUT merging
git fetch origin

# Download + merge (pull = fetch + merge)
git pull origin main

# ✅ Cleaner history: pull with rebase
git pull --rebase origin main

# Push your branch
git push origin feature/login

# First push of a new branch (sets upstream tracking)
git push -u origin feature/login
# After this, just:
git push
```

### Cloning a Specific Branch

```bash
git clone -b feature/login https://github.com/username/repo.git
```

---

## 7. Pull Requests & Code Reviews

A **Pull Request (PR)** is GitHub's way of saying: *"I want to merge my branch into yours — please review it first."*

### PR Workflow

```
1. Create a branch      → git checkout -b feature/payment
2. Make your commits    → git commit -m "feat: add Razorpay integration"
3. Push branch          → git push -u origin feature/payment
4. Open PR on GitHub    → base: main  ← compare: feature/payment
5. Team reviews code    → Comments, approvals, requested changes
6. Address feedback     → More commits on same branch (auto-updates PR)
7. Merge PR             → Squash merge / Regular merge / Rebase merge
8. Delete branch        → Cleanup after merge
```

### Three Ways to Merge a PR

| Method | When to Use | Result |
|--------|-------------|--------|
| **Merge commit** | Preserving full history | Extra merge commit created |
| **Squash and merge** | Clean main branch | All commits squashed to 1 |
| **Rebase and merge** | Linear history | Commits replayed on top of main |

> 💡 **For solo/small team projects:** Squash merge keeps history clean.  
> **For open source contributions:** Rebase merge is often preferred.

---

## 8. Merging & Resolving Conflicts

### Merging a Branch

```bash
# Switch to the branch you want to merge INTO
git checkout main

# Merge the feature branch
git merge feature/login

# Merge without fast-forward (preserves branch history)
git merge --no-ff feature/login

# Squash all feature commits into one before merging
git merge --squash feature/login
git commit -m "feat: complete user login feature"
```

### Understanding Merge Conflicts

A conflict happens when two branches changed the **same line** differently:

```
<<<<<<< HEAD (your current branch - main)
    return "Hello, Admin";
=======
    return "Hello, User";
>>>>>>> feature/login (incoming branch)
```

**You must choose one or combine them**, then remove the markers.

### Resolving Conflicts Step by Step

```bash
# 1. Start the merge
git merge feature/login
# CONFLICT (content): Merge conflict in src/UserService.java

# 2. See which files have conflicts
git status

# 3. Open the conflicting file and fix it manually
#    (or use VS Code's built-in merge editor — highly recommended)

# 4. After fixing, stage the resolved file
git add src/UserService.java

# 5. Complete the merge
git commit
# Git auto-generates a merge commit message

# 6. If you want to ABORT the merge instead
git merge --abort
```

### VS Code Merge Editor Tip

When a conflict occurs, VS Code shows **"Accept Current Change"**, **"Accept Incoming Change"**, or **"Accept Both Changes"** buttons. Use them — much easier than editing raw conflict markers!

---

## 9. Advanced Git Commands

### Stash — Save Work Temporarily

```bash
# Stash your uncommitted changes (gives your working dir a clean slate)
git stash

# Stash with a description
git stash push -m "WIP: payment gateway half done"

# See all stashes
git stash list
# stash@{0}: WIP: payment gateway half done
# stash@{1}: On main: fix navbar

# Apply most recent stash (keeps it in the list)
git stash apply

# Apply a specific stash
git stash apply stash@{2}

# Apply AND remove from list
git stash pop

# Delete a specific stash
git stash drop stash@{0}

# Delete ALL stashes
git stash clear
```

### Cherry-Pick — Take One Commit from Another Branch

```bash
# Apply a specific commit to your current branch
git cherry-pick a3f9d21

# Cherry-pick without auto-committing (review first)
git cherry-pick --no-commit a3f9d21
```

> **Real use case:** A critical bug was fixed on `develop`. You need that fix on `main` RIGHT NOW without merging everything else. Cherry-pick is your answer.

### Rebase — Replay Commits on Top of Another Branch

```bash
# Rebase current branch onto main (keeps your commits on top)
git rebase main

# Interactive rebase — rewrite last 3 commits
git rebase -i HEAD~3
```

In interactive mode you can:
- `pick` — keep commit as-is
- `squash` / `s` — merge into previous commit
- `reword` / `r` — change commit message
- `edit` / `e` — amend the commit
- `drop` / `d` — delete the commit

### Git Bisect — Find the Broken Commit

```bash
# Start bisect
git bisect start

# Mark current commit as bad (has the bug)
git bisect bad

# Mark a known-good commit
git bisect good v1.0.0

# Git automatically checks out commits between them
# You test, then tell Git:
git bisect good   # or
git bisect bad

# Git narrows it down until it finds the exact bad commit
# When done:
git bisect reset
```

### Git Blame — Who Wrote That Line?

```bash
git blame src/UserService.java

# Show only lines 10 to 30
git blame -L 10,30 src/UserService.java
```

### Git Reflog — Your Safety Net

```bash
# See EVERY action Git has tracked (including deleted branches, reset commits)
git reflog

# Recover a "lost" commit
git checkout -b recovery-branch a3f9d21
```

> `reflog` keeps history for ~90 days. It has saved thousands of developers from disaster.

### Git Worktree — Two Branches at Once

```bash
# Check out a branch in a SEPARATE folder (no stashing needed!)
git worktree add ../hotfix-branch hotfix/critical-bug

# List worktrees
git worktree list

# Remove when done
git worktree remove ../hotfix-branch
```

---

## 10. Undoing Mistakes

This is the section you'll come back to most often. 😄

### Decision Tree

```
Did you commit yet?
├── NO  → git restore (discard working dir changes)
│        git restore --staged (unstage)
└── YES → Did you push?
          ├── NO  → git reset (rewrite local history)
          └── YES → git revert (safe, creates a new commit)
```

### Restore — Undo Before Committing

```bash
# Discard changes to a file (⚠️ unrecoverable!)
git restore filename.java

# Unstage a file (remove from staging area, keep changes)
git restore --staged filename.java

# Unstage all staged files
git restore --staged .
```

### Reset — Undo After Committing (Local Only)

```bash
# --soft: undo commit, keep changes staged
git reset --soft HEAD~1

# --mixed (default): undo commit, unstage changes, keep files
git reset HEAD~1
git reset --mixed HEAD~1

# --hard: undo commit AND discard changes (⚠️ dangerous!)
git reset --hard HEAD~1

# Go back to a specific commit
git reset --hard a3f9d21
```

> ⚠️ **Never `reset` commits that have been pushed to a shared branch.** Use `revert` instead.

### Revert — Safe Undo for Pushed Commits

```bash
# Create a NEW commit that undoes a specific commit
git revert a3f9d21

# Revert without auto-opening the editor
git revert a3f9d21 --no-edit

# Revert but don't commit immediately (review first)
git revert a3f9d21 --no-commit
git revert --continue  # after reviewing
```

### Amend — Fix Your Last Commit

```bash
# Change the last commit message
git commit --amend -m "fix: corrected null pointer in UserService"

# Add a forgotten file to the last commit
git add forgotten-file.java
git commit --amend --no-edit  # keeps the same message
```

> ⚠️ Only amend commits that **haven't been pushed** yet.

---

## 11. Git Flags Cheatsheet

| Flag | Command | What It Does |
|------|---------|--------------|
| `-m` | `git commit -m "msg"` | Inline commit message |
| `-a` | `git commit -a` | Stage all tracked files + commit |
| `-am` | `git commit -am "msg"` | Stage tracked + commit with message |
| `-b` | `git checkout -b branch` | Create + switch branch |
| `-d` | `git branch -d branch` | Delete merged branch |
| `-D` | `git branch -D branch` | Force delete branch |
| `-u` | `git push -u origin main` | Set upstream tracking |
| `-v` | `git branch -v` | Branch + last commit |
| `-p` | `git add -p` | Interactive staging by hunks |
| `--oneline` | `git log --oneline` | Compact log |
| `--graph` | `git log --graph` | Visual branch tree |
| `--all` | `git log --all` | All branches in log |
| `--no-ff` | `git merge --no-ff` | Force merge commit |
| `--squash` | `git merge --squash` | Squash commits on merge |
| `--rebase` | `git pull --rebase` | Pull with rebase |
| `--force` | `git push --force` | Force push (dangerous!) |
| `--force-with-lease` | `git push --force-with-lease` | Safer force push |
| `--soft` | `git reset --soft HEAD~1` | Undo commit, keep staged |
| `--hard` | `git reset --hard HEAD~1` | Undo commit + discard changes |
| `--amend` | `git commit --amend` | Modify last commit |
| `--no-edit` | `git commit --amend --no-edit` | Amend without changing message |

---

## 12. Commit Messages — The Right Way

Good commit messages are **documentation**. Your future self (and teammates) will thank you.

### The Conventional Commits Standard

This is used by most professional teams and tools (GitHub, Jira integrations, changelogs, CI/CD pipelines).

```
<type>(<scope>): <short description>

[optional body]

[optional footer]
```

### Commit Types

| Type | When to Use | Example |
|------|------------|---------|
| `feat` | New feature | `feat: add JWT authentication` |
| `fix` | Bug fix | `fix: null pointer in UserService` |
| `docs` | Documentation only | `docs: update README setup steps` |
| `style` | Formatting, no logic change | `style: fix indentation in Main.java` |
| `refactor` | Code restructure, no new feature | `refactor: extract payment logic to service` |
| `perf` | Performance improvement | `perf: cache database queries` |
| `test` | Adding or fixing tests | `test: add unit tests for UserRepository` |
| `chore` | Build process, dependencies | `chore: upgrade Spring Boot to 3.3` |
| `ci` | CI/CD changes | `ci: add GitHub Actions workflow` |
| `revert` | Reverting a commit | `revert: revert feat: add JWT auth` |
| `build` | Build system changes | `build: configure Maven for production` |

### Real Examples

```bash
# ✅ Good
git commit -m "feat(auth): add Google OAuth2 login"
git commit -m "fix(api): handle 404 when user not found"
git commit -m "refactor(payment): extract Razorpay logic into PaymentService"
git commit -m "chore: add .gitignore for Java Maven project"

# ❌ Bad
git commit -m "fix"
git commit -m "updated stuff"
git commit -m "WIP"
git commit -m "asdfgh"
```

### Multi-Line Commit (When You Need More Detail)

```bash
git commit -m "feat(auth): add JWT token refresh mechanism

- Access tokens expire in 15 minutes
- Refresh tokens valid for 7 days
- Added /api/auth/refresh endpoint

Closes #42"
```

### Breaking Changes (Important for APIs/Libraries)

```bash
git commit -m "feat!: change UserService.getUser() return type to Optional<User>

BREAKING CHANGE: callers must handle Optional now.
Update all usages before upgrading."
```

---

## 13. .gitignore — Production-Level Setup

The `.gitignore` file tells Git which files/folders to **never track**.

### Java/Maven Project (Production-Ready)

```gitignore
# ──────────────────────────────────────────────
# JAVA — COMPILED OUTPUT
# ──────────────────────────────────────────────
*.class
*.jar
*.war
*.ear
*.nar

# ──────────────────────────────────────────────
# BUILD DIRECTORIES
# ──────────────────────────────────────────────
target/
build/
out/
bin/

# ──────────────────────────────────────────────
# MAVEN
# ──────────────────────────────────────────────
.mvn/timing.properties
.mvn/wrapper/maven-wrapper.jar
pom.xml.tag
pom.xml.releaseBackup
pom.xml.versionsBackup
release.properties

# ──────────────────────────────────────────────
# GRADLE (if you use it)
# ──────────────────────────────────────────────
.gradle/
gradle-app.setting
!gradle-wrapper.jar

# ──────────────────────────────────────────────
# IDE FILES — Never commit these
# ──────────────────────────────────────────────
# IntelliJ IDEA
.idea/
*.iml
*.iws
*.ipr

# Eclipse
.classpath
.project
.settings/

# VS Code
.vscode/
!.vscode/extensions.json    # ← exception: share recommended extensions

# NetBeans
nbproject/private/
nbbuild/
nbdist/
nb-configuration.xml

# ──────────────────────────────────────────────
# ENVIRONMENT & SECRETS (CRITICAL!)
# ──────────────────────────────────────────────
.env
.env.local
.env.production
.env.*.local
application-secrets.properties
application-prod.properties
**/secrets/
*.pem
*.key
*.p12
*.jks

# ──────────────────────────────────────────────
# OS FILES
# ──────────────────────────────────────────────
# macOS
.DS_Store
.AppleDouble
.LSOverride

# Windows
Thumbs.db
ehthumbs.db
Desktop.ini

# Linux
*~

# ──────────────────────────────────────────────
# LOGS & TEMP
# ──────────────────────────────────────────────
logs/
*.log
*.tmp
*.temp
*.pid
*.seed

# ──────────────────────────────────────────────
# NODE (if you have a frontend in the same repo)
# ──────────────────────────────────────────────
node_modules/
dist/
.next/
.nuxt/

# ──────────────────────────────────────────────
# DOCKER (usually commit these, but ignore local overrides)
# ──────────────────────────────────────────────
docker-compose.override.yml
```

### Pro Tips for .gitignore

```bash
# Apply .gitignore to files already being tracked (if you forgot earlier)
git rm -r --cached .
git add .
git commit -m "chore: apply .gitignore to tracked files"

# Check why a file is being ignored
git check-ignore -v filename.txt

# Force-add a file that's being ignored (when you really need to)
git add -f important-file.jar

# Global gitignore for YOUR machine (IDE files, OS files)
git config --global core.excludesfile ~/.gitignore_global
# Then add .DS_Store, .idea/, Thumbs.db to ~/.gitignore_global
```

> 💡 **Never commit:**
> - `.env` files with secrets, API keys, passwords
> - `node_modules/` or `target/` (can be regenerated)
> - IDE-specific files (different devs use different IDEs)

---

## 14. Branch Naming Conventions

### Standard Prefixes

| Prefix | Purpose | Example |
|--------|---------|---------|
| `feature/` | New functionality | `feature/user-authentication` |
| `fix/` or `bugfix/` | Bug fixes | `fix/null-pointer-userservice` |
| `hotfix/` | Critical production fix | `hotfix/payment-gateway-down` |
| `release/` | Release preparation | `release/v2.1.0` |
| `docs/` | Documentation only | `docs/api-endpoints-readme` |
| `refactor/` | Code cleanup | `refactor/extract-payment-service` |
| `test/` | Adding tests | `test/unit-tests-authservice` |
| `chore/` | Dependencies, tooling | `chore/upgrade-spring-boot-3.3` |

### Rules

```bash
# ✅ Good branch names
feature/user-profile-page
fix/login-timeout-issue
hotfix/critical-sql-injection
release/v1.5.0
docs/setup-guide-update

# ❌ Bad branch names
my-branch
fix
test123
Priyanshu_Work
NEW_FEATURE_AUTH
```

### With Ticket Numbers (Jira/GitHub Issues)

```bash
feature/PROJ-123-user-authentication
fix/PROJ-456-null-pointer-crash
hotfix/PROJ-789-payment-failure
```

### Protected Branches

In a real project, these branches should be **protected** (require PR + review to merge into):
- `main` — production code
- `develop` — integration branch
- `release/*` — release candidates

---

## 15. Git Shortcuts & Aliases

### Setting Up Aliases

```bash
# Basic shortcuts
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit

# Power aliases
git config --global alias.lg "log --oneline --graph --all --decorate"
git config --global alias.last "log -1 HEAD --stat"
git config --global alias.unstage "restore --staged"
git config --global alias.undo "reset --soft HEAD~1"
git config --global alias.aliases "config --get-regexp alias"

# Stage all and commit in one shot
git config --global alias.save '!git add -A && git commit -m'
```

### Usage After Setting Aliases

```bash
git st              # git status
git co -b feature/x # git checkout -b feature/x
git br -a           # git branch -a
git lg              # beautiful log tree
git last            # show last commit details
git unstage file.java  # unstage a file
git undo            # undo last commit (keep changes)
git save "feat: quick save"  # add all + commit
```

### View All Your Aliases

```bash
git aliases
# or
git config --get-regexp alias
```

### One-Liner Shortcuts (No Config Needed)

```bash
# Quick log overview
git log --oneline --graph --all

# See what changed in last commit
git show HEAD

# See diff of staged changes
git diff --cached

# Quickly switch back to previous branch
git checkout -

# List remote branches
git branch -r

# Delete remote branch
git push origin --delete feature/old-branch

# Rename current branch
git branch -m new-name
```

---

## 16. Git for Java Developers

### Recommended Project Structure to Commit

```
my-java-project/
├── src/
│   ├── main/
│   │   ├── java/          ✅ Always commit
│   │   └── resources/
│   │       ├── application.properties  ✅ (no secrets)
│   │       └── application-dev.properties  ✅ (dev only, no prod secrets)
│   └── test/              ✅ Always commit
├── pom.xml                ✅ Always commit
├── .gitignore             ✅ Always commit
├── README.md              ✅ Always commit
├── Dockerfile             ✅ Commit
├── docker-compose.yml     ✅ Commit
├── target/                ❌ Never (auto-generated)
├── .idea/                 ❌ Never (IDE specific)
└── .env                   ❌ NEVER (contains secrets)
```

### Spring Boot Specific Tips

```bash
# Your application.properties should NOT have secrets
# Instead use: application-{profile}.properties
# and add them to .gitignore

# Safe to commit:
application.properties           # base config, no secrets
application-dev.properties       # dev config (mock values ok)

# NEVER commit:
application-prod.properties      # real DB passwords
application-secrets.properties   # API keys
.env                             # environment variables
```

### Tagging Releases

```bash
# Create a version tag (like v1.0.0, v2.3.1)
git tag v1.0.0

# Annotated tag with message (recommended)
git tag -a v1.0.0 -m "Release version 1.0.0 — initial stable build"

# Push tags to GitHub
git push origin v1.0.0
git push origin --tags   # push all tags

# List tags
git tag

# Delete a tag
git tag -d v1.0.0
git push origin --delete v1.0.0  # delete from remote
```

### GitHub Actions for Java CI (Quick Example)

```yaml
# .github/workflows/build.yml
name: Java CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up JDK 21
        uses: actions/setup-java@v4
        with:
          java-version: '21'
          distribution: 'temurin'
      - name: Build with Maven
        run: mvn clean verify
```

This auto-runs your tests on every push and PR. Set up branch protection to **require this check to pass** before merging.

---

## 17. Real-World Workflows

### Workflow 1: Solo Developer (You)

```bash
# Start work
git pull origin main
git checkout -b feature/new-api

# Work, work, work...
git add .
git commit -m "feat: add /api/users endpoint"

# Push and create PR (even solo — keeps history clean)
git push -u origin feature/new-api
# Open PR on GitHub, review your own diff, merge, delete branch

# Back to main
git checkout main
git pull origin main
```

### Workflow 2: Team Project

```bash
# Always pull before starting
git pull --rebase origin main

# Create branch
git checkout -b feature/payment-gateway

# Commit often
git commit -m "feat(payment): add Razorpay order creation"
git commit -m "feat(payment): add webhook handler"
git commit -m "test(payment): add integration tests"

# Keep branch updated with main (avoid big merge conflicts)
git fetch origin
git rebase origin/main

# Push and open PR
git push -u origin feature/payment-gateway
```

### Workflow 3: Hotfix on Production

```bash
# Bug in production! Quick fix needed.

# Checkout from main (not develop)
git checkout main
git pull origin main
git checkout -b hotfix/payment-timeout

# Fix the bug
git commit -m "fix(payment): increase gateway timeout to 30s"

# Push and merge FAST
git push -u origin hotfix/payment-timeout
# Merge PR into main → deploy
# Also merge into develop:
git checkout develop
git merge hotfix/payment-timeout
git push origin develop

# Tag the fix
git tag -a v1.2.1 -m "hotfix: payment timeout fix"
git push origin --tags
```

### Workflow 4: Open Source Contribution

```bash
# 1. Fork the repo on GitHub (creates your own copy)

# 2. Clone your fork
git clone https://github.com/YOUR-USERNAME/project.git

# 3. Add original repo as 'upstream'
git remote add upstream https://github.com/ORIGINAL-OWNER/project.git

# 4. Keep your fork updated
git fetch upstream
git checkout main
git merge upstream/main
git push origin main

# 5. Create feature branch and do your work
git checkout -b fix/typo-in-readme
git commit -m "docs: fix typo in installation guide"
git push origin fix/typo-in-readme

# 6. Open PR from your fork to the original repo
```

---

## 18. AI-Era Git Tips (2026)

### Using AI with Git

**GitHub Copilot / AI assistants** can now help you:
- Generate commit messages from your diff
- Auto-complete `.gitignore` for your tech stack
- Suggest PR descriptions
- Review code before you push

### AI-Assisted Commit Messages

```bash
# Some tools (like lazygit, gh CLI) can generate messages:
gh copilot suggest "write a commit message for these changes"

# VS Code GitHub Copilot: click the sparkle icon in Source Control panel
# It reads your staged diff and suggests a commit message
```

### GitHub Copilot Workspace

In 2025-2026, GitHub Copilot Workspace can:
- Take a GitHub issue and generate all the code changes needed
- Create branches, write code, run tests, open PRs automatically

You still review and approve — **you are the senior dev.**

### Protecting Secrets with Git in the AI Era

With AI tools generating code, be extra careful:

```bash
# Install git-secrets to prevent committing AWS keys, passwords, etc.
# https://github.com/awslabs/git-secrets
git secrets --install
git secrets --register-aws  # blocks AWS key patterns

# Pre-commit hooks (runs checks before every commit)
# Install pre-commit: https://pre-commit.com
# .pre-commit-config.yaml:
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    hooks:
      - id: detect-private-key
      - id: check-added-large-files
      - id: check-json
```

### Git + AI Code Review Checklist (Before Every PR)

Before opening a PR, ask yourself (or your AI assistant):

- [ ] Are there any hardcoded secrets or API keys?
- [ ] Are there any `TODO` comments that should be tickets?
- [ ] Is the commit history clean and meaningful?
- [ ] Does the branch name follow conventions?
- [ ] Is the `.gitignore` up to date?
- [ ] Are all tests passing?

---

## 19. Quick Reference Cheatsheet

```
┌─────────────────────────────────────────────────────────────────┐
│                    GIT QUICK REFERENCE                          │
├─────────────────────┬───────────────────────────────────────────┤
│ SETUP               │                                           │
│ git init            │ Initialize new repo                       │
│ git clone <url>     │ Clone a repo                              │
├─────────────────────┼───────────────────────────────────────────┤
│ DAILY WORKFLOW      │                                           │
│ git status          │ See what's changed                        │
│ git add .           │ Stage all changes                         │
│ git add -p          │ Stage by hunks (interactive)              │
│ git commit -m ""    │ Commit with message                       │
│ git push            │ Push to remote                            │
│ git pull --rebase   │ Pull + rebase (clean history)             │
├─────────────────────┼───────────────────────────────────────────┤
│ BRANCHING           │                                           │
│ git checkout -b x   │ Create + switch branch                    │
│ git checkout -      │ Switch to previous branch                 │
│ git branch -a       │ List all branches                         │
│ git branch -d x     │ Delete merged branch                      │
│ git merge x         │ Merge branch x into current               │
│ git rebase main     │ Rebase current onto main                  │
├─────────────────────┼───────────────────────────────────────────┤
│ UNDOING             │                                           │
│ git restore f       │ Discard file changes                      │
│ git restore --staged│ Unstage a file                            │
│ git reset --soft ~1 │ Undo commit, keep staged                  │
│ git reset --hard ~1 │ Undo commit + discard (DANGER)            │
│ git revert <hash>   │ Safe undo (creates new commit)            │
│ git commit --amend  │ Fix last commit                           │
├─────────────────────┼───────────────────────────────────────────┤
│ ADVANCED            │                                           │
│ git stash           │ Save work temporarily                     │
│ git stash pop       │ Re-apply saved work                       │
│ git cherry-pick h   │ Apply single commit                       │
│ git rebase -i ~3    │ Interactive rebase last 3 commits         │
│ git bisect          │ Binary search for bug commit              │
│ git blame f         │ See who changed each line                 │
│ git reflog          │ Full history — emergency recovery         │
├─────────────────────┼───────────────────────────────────────────┤
│ REMOTE              │                                           │
│ git remote -v       │ List remotes                              │
│ git fetch           │ Download without merging                  │
│ git push -u origin  │ Push + set upstream                       │
│ git push --tags     │ Push all tags                             │
└─────────────────────┴───────────────────────────────────────────┘
```

---

## 🎓 What to Learn Next

Now that you know Git, level up your developer toolkit:

| Topic | Why It Matters |
|-------|---------------|
| **GitHub Actions** | Automate builds, tests, deployments |
| **Docker + Git** | Consistent environments across machines |
| **Semantic Versioning** | Proper `v1.2.3` version numbering |
| **Git Hooks** | Run scripts automatically on commit/push |
| **Trunk-Based Development** | Modern team workflow used at Google, Meta |
| **Monorepo Patterns** | Multiple projects in one repo |

---

*Made with ❤️ for developers who want to ship great software.*  
*Reference: JS Mastery Git & GitHub Handbook + Tutorial (2024) — updated for 2026.*
