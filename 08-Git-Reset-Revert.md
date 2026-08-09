# Git Reset and Revert

Git provides several commands for undoing changes.

Two important commands are:

* `git reset`
* `git revert`

Although both can undo changes, they work differently.

---

## 1. What is `git reset`?

`git reset` moves the current branch pointer to another commit.

It can also change what is staged and what is present in the working directory.

Basic syntax:

```bash
git reset <commit>
```

Example:

```bash
git reset HEAD~1
```

This moves the current branch back by one commit.

---

## 2. What is `git revert`?

`git revert` creates a **new commit** that reverses the changes introduced by an earlier commit.

Example:

```bash
git revert <commit>
```

Unlike `reset`, `revert` does not remove the old commit from history.

This makes `git revert` safer when working with commits that have already been pushed to a shared remote repository.

---

## 3. Reset vs Revert

The main difference:

```text
git reset
    |
    +-- Moves branch history backward
    |
    +-- Can remove commits from the current branch history


git revert
    |
    +-- Keeps existing history
    |
    +-- Creates a new commit that undoes an earlier commit
```

### Simple rule

> `reset` changes history.

> `revert` preserves history and adds an undo commit.

---

# Git Reset Modes

Git reset has three commonly used modes:

```bash
git reset --soft
git reset --mixed
git reset --hard
```

---

## 4. `git reset --soft`

`--soft` moves the branch pointer but keeps your changes **staged**.

Example:

```bash
git reset --soft HEAD~1
```

Suppose you have:

```text
A --- B --- C
          ^
         HEAD
```

After:

```bash
git reset --soft HEAD~1
```

you get:

```text
A --- B
     ^
    HEAD

Changes from C are still staged.
```

Check with:

```bash
git status
```

You will usually see the changes under:

```text
Changes to be committed
```

### Use case

Use `--soft` when you want to undo the last commit but keep all its changes ready to commit again.

For example, you made a commit with the wrong commit message:

```bash
git commit -m "Wrong message"
```

You can do:

```bash
git reset --soft HEAD~1
```

Then create the correct commit:

```bash
git commit -m "Correct message"
```

---

## 5. `git reset --mixed`

`--mixed` is the default reset mode.

Example:

```bash
git reset --mixed HEAD~1
```

or simply:

```bash
git reset HEAD~1
```

It moves the branch pointer backward and **unstages** the changes.

The changes remain in your working directory.

Example:

```text
Before:

A --- B --- C
          ^
         HEAD


After:

A --- B
     ^
    HEAD

Changes from C remain in the working directory.
```

Check:

```bash
git status
```

You may see:

```text
Changes not staged for commit
```

### Use case

Use mixed reset when you want to undo a commit but keep the files so you can modify them before committing again.

---

## 6. `git reset --hard`

`--hard` moves the branch pointer and removes changes from the working directory and staging area.

Example:

```bash
git reset --hard HEAD~1
```

Example:

```text
Before:

A --- B --- C
          ^
         HEAD


After:

A --- B
     ^
    HEAD
```

The changes introduced by C are removed from the current working tree.

### ⚠️ Important

Be very careful with:

```bash
git reset --hard
```

It can permanently discard uncommitted work.

Never use it casually on important work.

---

# Understanding HEAD

`HEAD` points to the commit you currently have checked out.

Example:

```text
A --- B --- C
          ^
         HEAD
```

`HEAD~1` means the parent of HEAD:

```text
A --- B --- C
      ^     ^
    HEAD~1 HEAD
```

`HEAD~2` means two commits before HEAD:

```text
A --- B --- C
  ^         ^
HEAD~2     HEAD
```

---

# 7. Useful HEAD Syntax

```bash
HEAD
```

Current commit.

```bash
HEAD~1
```

One commit before HEAD.

```bash
HEAD~2
```

Two commits before HEAD.

```bash
HEAD~3
```

Three commits before HEAD.

Example:

```bash
git reset --soft HEAD~1
```

Undo the latest commit while keeping its changes staged.

---

# 8. Reset a Specific Commit

You can reset to a specific commit:

```bash
git reset --soft <commit-id>
```

Example:

```bash
git reset --soft 2f6c191
```

You can find commit IDs using:

```bash
git log --oneline
```

Example:

```text
7ae7a78 Add Git stash notes
cc3bb75 Add Git remote and GitHub notes
2f6c191 Add Git rebase notes
```

Then:

```bash
git reset --soft cc3bb75
```

---

# 9. Git Revert Example

Suppose your history is:

```text
A --- B --- C
```

You discover that C introduced a problem.

Instead of deleting C, use:

```bash
git revert C
```

Git creates a new commit:

```text
A --- B --- C --- D
                ^
          Revert C
```

Commit D reverses the changes made by C.

The original commit C remains in history.

---

# 10. Revert a Specific Commit

First find the commit:

```bash
git log --oneline
```

Example:

```text
8a12345 Add incorrect configuration
7b23456 Add documentation
6c34567 Initial project setup
```

Revert it:

```bash
git revert 8a12345
```

Git may open an editor for the revert commit message.

Save and close the editor.

Then check:

```bash
git log --oneline
```

You will see a new revert commit.

---

# 11. Revert the Latest Commit

To revert the most recent commit:

```bash
git revert HEAD
```

Git creates a new commit that reverses the latest commit.

---

# 12. Reset vs Revert in Shared Repositories

Suppose you already pushed this history:

```text
A --- B --- C
          ^
        origin/main
```

If other developers have already pulled C, changing history with reset can cause problems.

Instead:

```bash
git revert C
```

creates:

```text
A --- B --- C --- D
                ^
              revert
```

This preserves the shared history.

### General rule

For commits already pushed to a shared branch such as `main`:

```text
Prefer:

git revert
```

instead of:

```text
git reset
```

---

# 13. Reset Before Pushing

Reset is commonly safer when the commit has not been pushed yet.

Example:

```text
Local:

A --- B --- C
          ^
         HEAD
```

You realize C should not exist.

You can use:

```bash
git reset --soft HEAD~1
```

Then make corrections and commit again.

---

# 14. Practical Reset Workflow

Create a safe practice branch:

```bash
git switch -c reset-practice
```

Create a file:

```bash
echo "Reset practice 1" > reset-practice.txt
```

Stage it:

```bash
git add reset-practice.txt
```

Commit it:

```bash
git commit -m "Add reset practice 1"
```

Create another change:

```bash
echo "Reset practice 2" >> reset-practice.txt
```

Stage and commit:

```bash
git add reset-practice.txt
git commit -m "Add reset practice 2"
```

Check history:

```bash
git log --oneline --graph
```

You should have two practice commits.

---

# 15. Practice `reset --soft`

Check the current history:

```bash
git log --oneline --graph
```

Then:

```bash
git reset --soft HEAD~1
```

Check:

```bash
git status
```

The latest commit should be removed from the branch history, but its changes should remain staged.

You can recommit:

```bash
git commit -m "Recommit reset practice 2"
```

---

# 16. Practice `reset --mixed`

Create another commit:

```bash
echo "Mixed reset practice" >> reset-practice.txt
git add reset-practice.txt
git commit -m "Add mixed reset practice"
```

Now run:

```bash
git reset --mixed HEAD~1
```

Check:

```bash
git status
```

The commit is removed from the current branch history, but the file changes remain unstaged.

You can stage them again:

```bash
git add reset-practice.txt
```

Then commit:

```bash
git commit -m "Recommit mixed reset practice"
```

---

# 17. Practice `reset --hard`

⚠️ Use a practice branch only.

First create a commit:

```bash
echo "Hard reset practice" >> reset-practice.txt
git add reset-practice.txt
git commit -m "Add hard reset practice"
```

Check the history:

```bash
git log --oneline --graph
```

Then:

```bash
git reset --hard HEAD~1
```

Check:

```bash
git status
```

The commit and its working-tree changes are removed from the current branch.

### Important

Do not practice this on important uncommitted work.

---

# 18. Practice `git revert`

Create a new commit:

```bash
echo "Revert practice" >> reset-practice.txt
git add reset-practice.txt
git commit -m "Add revert practice"
```

Check the commit:

```bash
git log --oneline --graph
```

Now revert it:

```bash
git revert HEAD
```

Check history:

```bash
git log --oneline --graph
```

You should see something similar to:

```text
A --- B --- C --- D
          Add    Revert
```

The original commit remains, and Git creates a new commit to undo it.

---

# 19. Difference Between Reset Modes

| Command                    | Commit | Staging Area        | Working Directory |
| -------------------------- | ------ | ------------------- | ----------------- |
| `git reset --soft HEAD~1`  | Moved  | Changes kept staged | Changes kept      |
| `git reset --mixed HEAD~1` | Moved  | Changes unstaged    | Changes kept      |
| `git reset --hard HEAD~1`  | Moved  | Changes removed     | Changes removed   |

Simple memory trick:

```text
SOFT
  ↓
Keep everything staged


MIXED
  ↓
Keep files, unstage changes


HARD
  ↓
Throw changes away
```

---

# 20. Difference Between Reset and Revert

| Feature                  | `git reset`               | `git revert`                  |
| ------------------------ | ------------------------- | ----------------------------- |
| Moves branch pointer     | Yes                       | No                            |
| Creates new commit       | Usually no                | Yes                           |
| Changes existing history | Yes                       | No                            |
| Good for shared branches | Usually avoid             | Yes                           |
| Can discard changes      | `--hard` can              | No, it creates an undo commit |
| Common use               | Local/unpublished commits | Public/pushed commits         |

---

# 21. Common Mistakes

### Mistake 1: Using reset on shared main

Avoid:

```bash
git reset --hard HEAD~1
git push origin main
```

This can create history problems, especially if the remote branch has commits that your local branch no longer contains.

Prefer:

```bash
git revert <commit>
git push origin main
```

---

### Mistake 2: Using `--hard` without checking

This is dangerous:

```bash
git reset --hard
```

Always understand what changes will be removed before using it.

---

### Mistake 3: Confusing reset and revert

Remember:

```text
reset  = move branch history
revert = create an undo commit
```

---

# 22. Common Commands

```bash
# View history
git log --oneline --graph

# Undo latest commit, keep changes staged
git reset --soft HEAD~1

# Undo latest commit, keep changes unstaged
git reset --mixed HEAD~1

# Undo latest commit and discard changes
git reset --hard HEAD~1

# Revert latest commit
git revert HEAD

# Revert a specific commit
git revert <commit-id>

# Check status
git status

# Check differences
git diff

# Check staged differences
git diff --staged
```

---

# 23. Interview Questions

### What is `git reset`?

> `git reset` moves the current branch pointer to another commit and can modify the staging area and working directory depending on the reset mode.

### What is `git revert`?

> `git revert` creates a new commit that reverses the changes introduced by an earlier commit.

### What is the difference between reset and revert?

> Reset changes the existing branch history, while revert preserves the existing history and creates a new commit that undoes previous changes.

### What does `git reset --soft` do?

> It moves the branch pointer while keeping the changes staged.

### What does `git reset --mixed` do?

> It moves the branch pointer and unstages the changes while keeping them in the working directory.

### What does `git reset --hard` do?

> It moves the branch pointer and removes changes from the staging area and working directory. It should be used carefully.

### Which is safer for a pushed commit: reset or revert?

> `git revert` is generally safer because it preserves the existing shared history and creates a new commit.

### What does `HEAD~1` mean?

> `HEAD~1` refers to the parent of the current HEAD commit.

---

# 24. Reset and Revert Cheat Sheet

```bash
# View commits
git log --oneline

# Soft reset
git reset --soft HEAD~1

# Mixed reset
git reset --mixed HEAD~1

# Default mixed reset
git reset HEAD~1

# Hard reset
git reset --hard HEAD~1

# Revert latest commit
git revert HEAD

# Revert specific commit
git revert <commit-id>

# Check status
git status

# Check working changes
git diff

# Check staged changes
git diff --staged
```

---

# 25. Key Points to Remember

```text
git reset
    ↓
Changes branch history

git reset --soft
    ↓
Keep changes staged

git reset --mixed
    ↓
Keep changes unstaged

git reset --hard
    ↓
Discard changes

git revert
    ↓
Create a new commit that undoes an old commit
```

### Golden Rule

> Use `reset` mainly for local/unpublished history.

> Use `revert` when you need to undo changes that are already part of shared history.

---

# 26. Recommended Workflow

For local work:

```text
Make changes
     ↓
Commit
     ↓
Realize commit is wrong
     ↓
git reset
     ↓
Fix changes
     ↓
Commit again
```

For shared/pushed work:

```text
Make changes
     ↓
Commit
     ↓
Push to GitHub
     ↓
Problem discovered
     ↓
git revert
     ↓
Push the new revert commit
```

This keeps shared Git history safer and easier for other developers to understand.
