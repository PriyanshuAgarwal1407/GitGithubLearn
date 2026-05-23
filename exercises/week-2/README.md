# 🌿 Week 2: Branching, Merging & Conflict Resolution

Welcome to Week 2! In this module, you will learn how to isolate work using branches and merge them cleanly.

---

## 🎯 Learning Goals
- Understand what branches are (lightweight pointers to commits).
- Create, list, switch, and delete branches.
- Merge branches using Fast-Forward and 3-Way Merges.
- Simulate, identify, and resolve merge conflicts with confidence.

---

## 🧪 Hands-On Exercises

### Exercise 2.1: Creating and Switching Branches
1. Check existing branches:
   ```bash
   git branch
   ```
2. Create and switch to a new feature branch:
   ```bash
   git checkout -b feature/user-profile
   # OR with modern Git:
   git switch -c feature/user-profile
   ```
3. Create a new file `profile.js`:
   ```javascript
   function getProfile(name) {
       return `User: ${name}`;
   }
   ```
4. Stage and commit:
   ```bash
   git add profile.js
   git commit -m "feat: add user profile function"
   ```

---

### Exercise 2.2: Merging Branches
1. Switch back to the `main` branch:
   ```bash
   git switch main
   ```
2. Merge the feature branch:
   ```bash
   git merge feature/user-profile
   ```
3. Verify the commit history:
   ```bash
   git log --graph --oneline
   ```
4. Clean up the branch after merging:
   ```bash
   git branch -d feature/user-profile
   ```

---

### Exercise 2.3: Resolving a Merge Conflict
1. On `main`, edit line 1 of a file `greeting.txt` to say:
   ```
   Hello from Main Branch
   ```
   Commit this change: `git commit -am "chore: update greeting on main"`

2. Create and switch to branch `feature/greeting`:
   ```bash
   git switch -c feature/greeting HEAD~1
   ```
3. Edit the same line 1 of `greeting.txt` to say:
   ```
   Hello from Feature Branch
   ```
   Commit this change: `git commit -am "chore: update greeting on feature"`

4. Switch back to `main` and attempt to merge:
   ```bash
   git switch main
   git merge feature/greeting
   ```
   *(Git will report a Merge Conflict!)*

5. Open `greeting.txt`, resolve the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), stage and complete the merge:
   ```bash
   git add greeting.txt
   git commit -m "fix: resolve greeting merge conflict"
   ```

---

## 💡 Quick Command Reference

| Command | Description |
| :--- | :--- |
| `git branch` | List all local branches |
| `git branch <name>` | Create a new branch |
| `git switch <name>` | Switch to an existing branch |
| `git switch -c <name>` | Create and switch to a new branch |
| `git merge <name>` | Merge specified branch into current branch |
| `git branch -d <name>` | Safely delete a merged branch |
| `git branch -D <name>` | Force delete an unmerged branch |
