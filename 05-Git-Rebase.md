# Git Rebase

Git rebase is used to move or replay commits from one branch onto another branch.

It helps create a clean and linear Git history.

---

## 1. What is Git Rebase?

In simple words:

> Git rebase moves your branch commits and places them on top of another branch.

Example:

```text
Before rebase:

A---B---C  main
     \
      D---E  feature
```

After rebase:

```text
A---B---C---D'---E'  feature
```

The feature commits are replayed on top of the latest `main`.

---

## 2. Basic Rebase Command

First switch to your feature branch:

```bash
git switch feature-login
```

Then run:

```bash
git rebase main
```

This replays the feature branch commits on top of `main`.

---

## 3. Common Rebase Workflow

A common workflow is:

```bash
git switch main
git pull origin main
git switch feature-login
git rebase main
```

After the rebase, if the feature branch was already pushed to GitHub, you may need:

```bash
git push --force-with-lease
```

`--force-with-lease` is safer than `--force`.

---

## 4. Rebase vs Merge

### Merge

```bash
git switch main
git merge feature-login
```

Merge combines the branches.

Example:

```text
A---B---C-------M  main
     \           /
      D---E-----/
```

A merge commit may be created.

### Rebase

```bash
git switch feature-login
git rebase main
```

Rebase creates a more linear history:

```text
A---B---C---D'---E'
```

---

## 5. Interactive Rebase

Interactive rebase allows you to modify previous commits.

```bash
git rebase -i HEAD~3
```

You can use interactive rebase to:

* Reorder commits
* Edit commits
* Combine commits
* Remove commits
* Change commit messages

---

## 6. Rebase Conflict

Sometimes Git cannot automatically apply a commit during a rebase.

Check the status:

```bash
git status
```

Git will show which file has a conflict.

Open the conflicted file and resolve the conflict.

Then stage the resolved file:

```bash
git add <file>
```

Continue the rebase:

```bash
git rebase --continue
```

If another conflict occurs, resolve it and repeat the process.

---

## 7. Abort a Rebase

If you want to cancel the rebase:

```bash
git rebase --abort
```

This returns your branch to its state before the rebase started.

---

## 8. Skip a Commit During Rebase

If you want Git to skip the current commit:

```bash
git rebase --skip
```

Use this only when you understand that the commit will not be included in the rebased history.

---

## 9. Rebase Workflow Example

Suppose we have:

```text
main:

A---B---C

feature:

A---B---C---D---E
```

If `main` receives a new commit:

```text
A---B---C---F  main
     \
      D---E    feature
```

Switch to the feature branch:

```bash
git switch feature
```

Run:

```bash
git rebase main
```

After rebase:

```text
A---B---C---F---D'---E'  feature
```

The feature commits are replayed on top of the latest `main`.

---

## 10. Important Rebase Commands

| Command                       | Purpose                               |
| ----------------------------- | ------------------------------------- |
| `git rebase main`             | Rebase current branch onto main       |
| `git rebase -i HEAD~3`        | Start interactive rebase              |
| `git rebase --continue`       | Continue after resolving a conflict   |
| `git rebase --abort`          | Cancel the rebase                     |
| `git rebase --skip`           | Skip the current commit               |
| `git status`                  | Check rebase status                   |
| `git push --force-with-lease` | Safely update a rebased remote branch |

---

## 11. Rebase and Remote Branches

Rebase changes commit history.

If a branch has already been pushed to GitHub and you rebase it, a normal push may be rejected.

Use:

```bash
git push --force-with-lease
```

Avoid using:

```bash
git push --force
```

unless you understand the consequences.

---

## 12. Important Interview Questions

### What is Git rebase?

> Git rebase moves or replays commits from one branch onto another branch to create a cleaner and more linear history.

### What is the difference between merge and rebase?

> Merge combines branches and may create a merge commit, while rebase replays commits on top of another branch and creates a linear history.

### What does `git rebase --continue` do?

> It continues the rebase after resolving a conflict and staging the resolved files.

### How do you cancel a rebase?

```bash
git rebase --abort
```

### What is interactive rebase?

> Interactive rebase allows you to modify, reorder, combine, remove, or edit previous commits.

### Why is force push sometimes needed after rebase?

> Rebase changes commit history, so the remote branch history may no longer match the local branch. `git push --force-with-lease` can update the remote branch safely.

---

## 13. Important Rule

> Avoid rebasing shared branches that other developers are already using.

Rebase is generally safer on your own feature branch before it is merged into `main`.

---

## 14. Easy Interview Answer

If someone asks:

**"What is Git rebase?"**

You can say:

> Git rebase is a Git command used to move the commits of one branch on top of another branch. It helps maintain a clean and linear project history.