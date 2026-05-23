# ☁️ Week 3: GitHub Collaboration & Pull Requests

Welcome to Week 3! In this module, you will master collaborating with teams using GitHub remotes and Pull Requests.

---

## 🎯 Learning Goals
- Understand the concept of remotes (`origin`, upstream).
- Clone, push, and fetch/pull from remote repositories.
- Work with Pull Requests (PRs), code reviews, and discussions.
- Fork open-source projects and contribute upstream.

---

## 🧪 Hands-On Exercises

### Exercise 3.1: Connecting a Local Repo to GitHub
1. Add a remote alias:
   ```bash
   git remote add origin https://github.com/PriyanshuAgarwal1407/GitGithubLearn.git
   ```
2. Verify configured remotes:
   ```bash
   git remote -v
   ```
3. Push your `main` branch and set upstream tracking:
   ```bash
   git push -u origin main
   ```

---

### Exercise 3.2: The Feature-Branch PR Workflow
1. Pull latest changes from remote `main`:
   ```bash
   git pull origin main
   ```
2. Create your feature branch:
   ```bash
   git switch -c feature/add-calculator
   ```
3. Implement your changes in code and commit:
   ```bash
   git add .
   git commit -m "feat: implement calculator addition logic"
   ```
4. Push your branch to GitHub:
   ```bash
   git push -u origin feature/add-calculator
   ```
5. Go to GitHub and open a **Pull Request (PR)** against `main`.

---

### Exercise 3.3: Syncing with Remote (Fetch vs Pull)
1. Fetch latest commits without modifying working directory:
   ```bash
   git fetch origin
   ```
2. Inspect what is new on the remote branch:
   ```bash
   git log HEAD..origin/main --oneline
   ```
3. Merge the remote changes:
   ```bash
   git merge origin/main
   ```
   *(Note: `git pull` is shorthand for `git fetch` followed by `git merge`)*

---

## 💡 Quick Command Reference

| Command | Description |
| :--- | :--- |
| `git remote -v` | View configured remote names and URLs |
| `git remote add <name> <url>` | Add a new remote alias |
| `git fetch <remote>` | Download objects and refs from remote |
| `git pull <remote> <branch>` | Fetch and integrate remote changes into current branch |
| `git push -u <remote> <branch>` | Push commits to remote and set tracking branch |
| `git clone <url>` | Clone a remote repository locally |
