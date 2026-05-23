# 📁 Week 1: Git Fundamentals & The Basics

Welcome to Week 1! In this module, you will master the fundamental building blocks of Git.

---

## 🎯 Learning Goals
- Understand what Version Control is and why it matters.
- Configure your Git identity (`user.name` and `user.email`).
- Initialize a local repository (`git init`).
- Understand the **Three Trees**: Working Directory, Staging Area (Index), and Commit History.
- Stage and commit files with descriptive commit messages.
- Inspect history with `git log` and `git status`.

---

## 🧪 Hands-On Exercises

### Exercise 1.1: Configure Your Git Identity
Run the following commands in your terminal:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --list
```

---

### Exercise 1.2: Initialize and Make Your First Commit
1. Create a new directory and navigate inside:
   ```bash
   mkdir git-practice && cd git-practice
   ```
2. Initialize a git repository:
   ```bash
   git init
   ```
3. Create a simple file:
   ```bash
   echo "# My First Project" > README.md
   ```
4. Check the repository status:
   ```bash
   git status
   ```
5. Stage the file:
   ```bash
   git add README.md
   ```
6. Commit the file:
   ```bash
   git commit -m "feat: initial commit with README"
   ```

---

### Exercise 1.3: Working with `.gitignore`
1. Create a log file:
   ```bash
   echo "secret_token=12345" > debug.log
   ```
2. Add a `.gitignore` rule:
   ```bash
   echo "*.log" >> .gitignore
   ```
3. Verify that `debug.log` is ignored:
   ```bash
   git status
   ```
   *(Notice that `debug.log` does not show up as an untracked file!)*

---

## 💡 Quick Command Reference

| Command | Description |
| :--- | :--- |
| `git init` | Initialize a new local Git repository |
| `git status` | Check status of working directory & staging area |
| `git add <file>` | Stage changes for the next commit |
| `git add .` | Stage all modified and new files |
| `git commit -m "msg"` | Save staged snapshot to repository history |
| `git log --oneline` | View compact commit history |
| `git diff` | View unstaged changes |
