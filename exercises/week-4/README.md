# ⚡ Week 4: Advanced Git Techniques & Workflow Mastery

Welcome to Week 4! In this advanced module, you will learn powerful Git tools used by professional developers.

---

## 🎯 Learning Goals
- Safely stash work-in-progress (`git stash`).
- Rebase branches for clean, linear commit history (`git rebase`).
- Cherry-pick specific commits across branches (`git cherry-pick`).
- Understand `git reset` (soft, mixed, hard) vs `git revert`.
- Inspect file changes line-by-line with `git blame`.

---

## 🧪 Hands-On Exercises

### Exercise 4.1: Git Stash (Saving Work In Progress)
1. Make a quick modification to a file without committing.
2. Stash your uncommitted changes:
   ```bash
   git stash save "WIP: halfway through new feature"
   ```
3. Check your stash list:
   ```bash
   git stash list
   ```
4. Restore your stashed changes later:
   ```bash
   git stash pop
   ```

---

### Exercise 4.2: Rebase vs Merge
1. Create branch `feature/linear-history` from `main`:
   ```bash
   git switch -c feature/linear-history
   ```
2. Commit 2 changes.
3. Switch to `main`, add 1 commit on `main`.
4. Switch back to `feature/linear-history` and rebase on `main`:
   ```bash
   git switch feature/linear-history
   git rebase main
   ```
5. Observe how your feature commits are smoothly replayed on top of `main`.

---

### Exercise 4.3: Cherry-Pick a Commit
1. Find a commit hash on another branch:
   ```bash
   git log --oneline another-branch
   ```
2. Apply just that specific commit onto your current branch:
   ```bash
   git cherry-pick <commit-hash>
   ```

---

### Exercise 4.4: Undo Changes: Reset vs Revert
- **`git revert <hash>`** creates a *new* commit that inverts previous changes (safe for public/shared branches).
- **`git reset --soft HEAD~1`** undoes the last commit but keeps changes staged.
- **`git reset --hard HEAD~1`** completely discards the last commit and working directory changes (caution!).

---

## 💡 Quick Command Reference

| Command | Description |
| :--- | :--- |
| `git stash` / `git stash pop` | Save uncommitted changes / restore them |
| `git rebase <base-branch>` | Reapply commits on top of another base tip |
| `git cherry-pick <commit>` | Apply changes from a single specific commit |
| `git revert <commit>` | Safely invert an existing commit with a new commit |
| `git reset --soft HEAD~1` | Undo commit, keep changes staged |
| `git blame <file>` | Show what revision and author last modified each line |
