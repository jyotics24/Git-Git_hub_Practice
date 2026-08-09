# Git Branching

Git branches allow us to work on different features or changes independently.

A branch is a separate line of development.

---

## 1. List Branches

```bash
git branch
```

Shows the local branches.

Example:

```text
* main
  feature-login
```

The `*` indicates the current branch.

---

## 2. Create a Branch

```bash
git branch feature-login
```

Creates a new branch but does not switch to it.

---

## 3. Create and Switch to a Branch

```bash
git switch -c feature-login
```

This creates the branch and immediately switches to it.

---

## 4. Switch Branch

```bash
git switch main
```

Switches to the `main` branch.

Another example:

```bash
git switch feature-login
```

---

## 5. Merge a Branch

First switch to the branch that should receive the changes:

```bash
git switch main
```

Then merge:

```bash
git merge feature-login
```

This combines the changes from `feature-login` into `main`.

---

## 6. Delete a Local Branch

```bash
git branch -d feature-login
```

Deletes a branch after it has been merged.

Force delete:

```bash
git branch -D feature-login
```

Use `-D` carefully because it can delete a branch with unmerged work.

---

## 7. Push a Branch to GitHub

```bash
git push -u origin feature-login
```

This uploads the branch to GitHub and sets its upstream branch.

After that:

```bash
git push
```

can be used.

---

## 8. Branch Workflow

A common feature workflow is:

```text
main
  |
  ●
  |
  ●
  |
  ├──── feature-login
  |          |
  |          ●
  |          ●
  |
  ●
```

Commands:

```bash
git switch -c feature-login
```

Make changes.

```bash
git status
```

Review changes:

```bash
git diff
```

Stage:

```bash
git add .
```

Commit:

```bash
git commit -m "Add login feature"
```

Push:

```bash
git push -u origin feature-login
```

Create a Pull Request on GitHub.

After review, merge the Pull Request into `main`.

Then:

```bash
git switch main
git pull origin main
```

Delete the local feature branch:

```bash
git branch -d feature-login
```

Delete the remote branch:

```bash
git push origin --delete feature-login
```

---

## 9. Branch vs Main

### Main

`main` usually contains the stable version of the project.

### Feature Branch

A feature branch is used to develop a particular feature or change without directly changing `main`.

Example:

```text
main
  |
  ├──── feature-login
  |
  ├──── feature-payment
  |
  └──── feature-dashboard
```

Each feature can be developed separately.

---

## 10. Common Branch Commands

| Command                         | Purpose                   |
| ------------------------------- | ------------------------- |
| `git branch`                    | List branches             |
| `git branch name`               | Create branch             |
| `git switch name`               | Switch branch             |
| `git switch -c name`            | Create and switch         |
| `git merge name`                | Merge branch              |
| `git branch -d name`            | Delete local branch       |
| `git branch -D name`            | Force delete local branch |
| `git push -u origin name`       | Push new branch           |
| `git push origin --delete name` | Delete remote branch      |

---

## 11. Important Interview Answer

### What is a Git branch?

> A Git branch is an independent line of development that allows developers to work on features or changes without directly modifying the main branch.

### Why use branches?

> Branches allow developers to isolate features, fixes, and experiments before merging them into the main branch.

### What is `git merge`?

> `git merge` combines the changes from one branch into another branch.

### What is `git switch -c`?

> `git switch -c` creates a new branch and switches to it.
