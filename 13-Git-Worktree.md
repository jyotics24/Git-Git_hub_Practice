# Git Worktree

Git worktree allows you to have multiple working directories connected to the same Git repository.

It is useful when you need to work on multiple branches at the same time without repeatedly switching branches.

---

## 1. What is Git Worktree?

Normally, a Git repository has one working directory.

For example:

```text
Git-Git_hub/
└── main branch
```

If you want to work on another branch, you normally use:

```bash
git switch feature-login
```

Git worktree allows you to have multiple directories:

```text
Git-Git_hub/
├── main
│
├── feature-login/
│
└── bug-fix/
```

Each directory can be associated with a different branch.

---

## 2. Why Use Git Worktree?

Git worktree is useful when:

* You need to work on multiple branches simultaneously.
* You do not want to stash your current changes.
* You want to quickly test another branch.
* You need to review another branch while keeping your current work untouched.
* You want separate directories for different features.

---

## 3. Check Existing Worktrees

Use:

```bash
git worktree list
```

Example:

```text
C:/Projects/Git-Git_hub   abc1234 [main]
```

This shows the main working tree.

---

## 4. Create a New Worktree

Basic syntax:

```bash
git worktree add <path> <branch>
```

Example:

```bash
git worktree add ../feature-login feature-login
```

This creates another directory:

```text
Desktop/
├── Git-Git_hub/
└── feature-login/
```

The original repository can remain on `main`.

The new directory uses `feature-login`.

---

## 5. Create a New Branch with Worktree

You can create a new branch and worktree at the same time.

Use:

```bash
git worktree add -b feature-payment ../feature-payment
```

Here:

```text
-b feature-payment
```

creates a new branch.

And:

```text
../feature-payment
```

specifies the new working directory.

---

## 6. Example

Suppose you are currently working on:

```text
main
```

Create a worktree:

```bash
git worktree add -b feature-login ../feature-login
```

Now you have:

```text
Desktop/
├── Git-Git_hub/
└── feature-login/
```

The original directory remains on:

```text
main
```

The new directory uses:

```text
feature-login
```

---

## 7. Enter the Worktree

Move into the new directory:

```bash
cd ../feature-login
```

Check the branch:

```bash
git branch
```

You should see:

```text
* feature-login
  main
```

Check status:

```bash
git status
```

---

## 8. Work in Two Branches

Suppose your original directory is:

```text
Git-Git_hub/
```

and uses:

```text
main
```

The second directory is:

```text
feature-login/
```

and uses:

```text
feature-login
```

You can work independently:

```text
Git-Git_hub/
    main

feature-login/
    feature-login
```

Both directories belong to the same Git repository.

---

## 9. Worktree Example

Original repository:

```bash
cd ~/Desktop/Git-Git_hub
```

Create a worktree:

```bash
git worktree add -b feature-login ../feature-login
```

Enter it:

```bash
cd ../feature-login
```

Check:

```bash
git status
```

You can now make changes:

```bash
echo "Login feature" > login.txt
```

Stage:

```bash
git add login.txt
```

Commit:

```bash
git commit -m "Add login feature"
```

---

## 10. Return to Main Worktree

Go back:

```bash
cd ../Git-Git_hub
```

Check:

```bash
git status
```

Your original working directory is still on `main`.

You did not need to switch branches.

---

## 11. Worktree and Branch Switching

Without worktree:

```text
main
 ↓
git switch feature
 ↓
feature
 ↓
git switch main
 ↓
main
```

With worktree:

```text
Directory 1 → main
Directory 2 → feature
```

You can work on both at the same time.

---

## 12. List All Worktrees

Use:

```bash
git worktree list
```

Example:

```text
C:/Users/Jyoti/Desktop/Git-Git_hub
C:/Users/Jyoti/Desktop/feature-login
```

You may see branch information:

```text
C:/Users/Jyoti/Desktop/Git-Git_hub       abc1234 [main]
C:/Users/Jyoti/Desktop/feature-login     def5678 [feature-login]
```

---

## 13. Show Worktree Information

You can use:

```bash
git worktree list
```

This shows:

* Worktree path
* Current commit
* Current branch

---

## 14. Remove a Worktree

When you finish working on a worktree:

```bash
git worktree remove ../feature-login
```

This removes the worktree.

The branch itself may still exist.

---

## 15. Remove Worktree and Branch

First remove the worktree:

```bash
git worktree remove ../feature-login
```

Then delete the branch if it is no longer needed:

```bash
git branch -d feature-login
```

---

## 16. Force Remove a Worktree

If the worktree contains changes and you are certain you do not need them:

```bash
git worktree remove --force ../feature-login
```

Use `--force` carefully because uncommitted work may be lost.

---

## 17. Prune Worktree Information

Sometimes a worktree directory is manually deleted.

For example:

```bash
rm -rf ../feature-login
```

Git may still have information about that worktree.

You can clean up stale worktree information:

```bash
git worktree prune
```

---

## 18. Worktree Lock

A worktree can be locked:

```bash
git worktree lock ../feature-login
```

A locked worktree is protected from certain automatic cleanup operations.

Unlock it:

```bash
git worktree unlock ../feature-login
```

---

## 19. Worktree Directory Structure

Git maintains worktree information inside:

```text
.git/worktrees/
```

You normally do not need to edit these files manually.

Git manages them through:

```bash
git worktree
```

commands.

---

## 20. Worktree vs Clone

Git worktree and Git clone are different.

### Git Clone

Creates another copy of the repository:

```bash
git clone <repository-url>
```

Each clone has its own `.git` repository data.

### Git Worktree

Creates another working directory connected to the same Git repository.

```bash
git worktree add ../feature feature
```

---

## 21. Worktree vs Clone Comparison

| Feature                            | Worktree    | Clone           |
| ---------------------------------- | ----------- | --------------- |
| Separate directory                 | Yes         | Yes             |
| Same Git repository                | Yes         | No              |
| Separate `.git` repository         | No          | Yes             |
| Multiple branches simultaneously   | Yes         | Yes             |
| Uses additional repository storage | Less        | More            |
| Useful for quick branch switching  | Very useful | Less convenient |

---

## 22. Worktree vs Stash

Git stash temporarily stores uncommitted changes.

Example:

```bash
git stash
git switch another-branch
```

Git worktree avoids the need to stash in many situations.

Instead:

```text
main directory → main
second directory → feature
```

Both can contain different work.

---

## 23. Example: Code Review

Suppose you are developing a feature on:

```text
feature-payment
```

You have uncommitted work.

A teammate asks you to review:

```text
feature-login
```

Normally, you might need to stash your work:

```bash
git stash
git switch feature-login
```

With worktree:

```bash
git worktree add ../review-login feature-login
```

Now you can review the other branch without touching your current work.

---

## 24. Example: Bug Fix While Developing

You are working on:

```text
feature-dashboard
```

Suddenly, a production bug needs fixing.

Instead of:

```bash
git stash
git switch main
git switch -c hotfix
```

You can create a separate worktree:

```bash
git worktree add -b hotfix ../hotfix main
```

Now:

```text
Git-Git_hub/ → feature-dashboard

hotfix/ → hotfix
```

You can fix the bug independently.

---

## 25. Worktree with Existing Branch

If the branch already exists:

```bash
git worktree add ../feature-login feature-login
```

Git creates a new working directory for that existing branch.

---

## 26. Worktree with New Branch

If the branch does not exist:

```bash
git worktree add -b feature-login ../feature-login
```

This:

1. Creates the branch.
2. Creates the worktree.
3. Checks out the branch in that worktree.

---

## 27. Worktree from a Specific Commit

You can also create a detached worktree:

```bash
git worktree add --detach ../testing abc1234
```

This checks out a specific commit without creating a branch.

Useful for:

* Testing old versions
* Debugging
* Inspecting historical code
* Running experiments

---

## 28. Detached Worktree Example

```bash
git worktree add --detach ../old-version abc1234
```

Then:

```bash
cd ../old-version
```

Check:

```bash
git status
```

You are working from that specific commit.

---

## 29. Worktree Workflow

A common workflow:

```bash
git worktree list
```

Create:

```bash
git worktree add -b feature-login ../feature-login
```

Enter:

```bash
cd ../feature-login
```

Work:

```bash
git add .
git commit -m "Add login feature"
```

Return:

```bash
cd ../Git-Git_hub
```

Check:

```bash
git worktree list
```

When finished:

```bash
git worktree remove ../feature-login
```

---

## 30. Important Worktree Rules

Remember:

1. One branch cannot normally be checked out in two worktrees at the same time.
2. Worktrees share the same Git repository.
3. Each worktree has its own working directory.
4. Worktrees are useful for parallel branch development.
5. Use `git worktree remove` to properly remove a worktree.
6. Use `git worktree prune` to clean stale worktree metadata.

---

## 31. Common Commands

| Command                               | Purpose                           |
| ------------------------------------- | --------------------------------- |
| `git worktree list`                   | List worktrees                    |
| `git worktree add <path> <branch>`    | Create worktree                   |
| `git worktree add -b <branch> <path>` | Create branch and worktree        |
| `git worktree remove <path>`          | Remove worktree                   |
| `git worktree prune`                  | Remove stale worktree information |
| `git worktree lock <path>`            | Lock worktree                     |
| `git worktree unlock <path>`          | Unlock worktree                   |

---

## 32. Common Mistakes

### Mistake 1: Using the Same Branch Twice

You generally cannot check out the same branch in two worktrees simultaneously.

For example:

```bash
git worktree add ../another-main main
```

may fail if `main` is already checked out in your existing worktree.

---

### Mistake 2: Deleting a Worktree Manually

Avoid simply deleting the directory when possible.

Instead of:

```bash
rm -rf ../feature-login
```

prefer:

```bash
git worktree remove ../feature-login
```

If the directory was already deleted:

```bash
git worktree prune
```

---

### Mistake 3: Forgetting the Worktree Location

Always check:

```bash
git worktree list
```

This shows where your worktrees are located.

---

## 33. Practical Exercise

From your repository:

```bash
cd ~/Desktop/Git-Git_hub
```

Check:

```bash
git status
```

Create a practice worktree:

```bash
git worktree add -b worktree-practice ../worktree-practice
```

List worktrees:

```bash
git worktree list
```

Enter the new directory:

```bash
cd ../worktree-practice
```

Check the branch:

```bash
git branch
```

Create a file:

```bash
echo "Git Worktree Practice" > worktree.txt
```

Check:

```bash
git status
```

Commit:

```bash
git add worktree.txt
git commit -m "Practice Git worktree"
```

Return to your main repository:

```bash
cd ../Git-Git_hub
```

List worktrees:

```bash
git worktree list
```

Remove the practice worktree:

```bash
git worktree remove ../worktree-practice
```

Delete the local branch:

```bash
git branch -d worktree-practice
```

Check:

```bash
git status
```

---

## 34. Git Worktree Interview Questions

### What is Git worktree?

> Git worktree allows multiple working directories to be connected to the same Git repository, allowing different branches to be checked out simultaneously.

### Why use Git worktree?

> It allows developers to work on multiple branches at the same time without repeatedly switching branches or stashing changes.

### How do you create a worktree?

```bash
git worktree add <path> <branch>
```

### How do you create a new branch with a worktree?

```bash
git worktree add -b <branch> <path>
```

### How do you list worktrees?

```bash
git worktree list
```

### How do you remove a worktree?

```bash
git worktree remove <path>
```

### What is `git worktree prune`?

> It removes stale worktree information when a worktree directory has been deleted without using Git's worktree commands.

### Can the same branch be checked out in multiple worktrees?

> Normally, no. Git prevents the same branch from being checked out in multiple worktrees simultaneously.

### Worktree vs clone?

> A clone creates another copy of the repository, while a worktree creates another working directory connected to the same Git repository.

### Worktree vs stash?

> Stash temporarily stores changes so you can switch branches, while worktree allows you to work on multiple branches in separate directories simultaneously.

---

## 35. Quick Reference

```bash
# List worktrees
git worktree list

# Create worktree for existing branch
git worktree add ../feature-login feature-login

# Create new branch and worktree
git worktree add -b feature-login ../feature-login

# Create detached worktree
git worktree add --detach ../testing <commit>

# Remove worktree
git worktree remove ../feature-login

# Force remove worktree
git worktree remove --force ../feature-login

# Clean stale worktree information
git worktree prune

# Lock worktree
git worktree lock ../feature-login

# Unlock worktree
git worktree unlock ../feature-login
```

---

## 36. Interview Summary

Remember:

```text
Git Worktree
     ↓
Multiple working directories
     ↓
Same Git repository
     ↓
Different branches
     ↓
Work simultaneously
```

The most important commands are:

```bash
git worktree list
git worktree add
git worktree remove
git worktree prune
```

### Simple Interview Answer

> Git worktree is a Git feature that allows multiple working directories to be associated with the same repository. Each worktree can have a different branch checked out, making it useful for working on multiple features, reviewing code, or fixing bugs without constantly switching branches.
