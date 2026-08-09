# Git Log and Diff

Git provides several commands to inspect commit history and compare changes.

Two important commands are:

* `git log` — view commit history
* `git diff` — compare changes

These commands are very useful for understanding what changed in a project and when those changes were made.

---

## 1. Git Log

```bash
git log
```

Shows the complete commit history of the current branch.

Example:

```text
commit a449e00
Author: Jyoti
Date:   ...

    Add Git reset and revert notes

commit 7ae7a78
Author: Jyoti
Date:   ...

    Add Git stash notes
```

The commit contains:

* Commit ID
* Author
* Date
* Commit message

---

## 2. Git Log Oneline

```bash
git log --oneline
```

Shows each commit in a short one-line format.

Example:

```text
a449e00 Add Git reset and revert notes
7ae7a78 Add Git stash notes
cc3bb75 Add Git remote and GitHub notes
2f6c191 Add Git rebase notes
9a85c1d Remove conflict practice file
```

This is one of the most useful commands for quickly viewing history.

---

## 3. Git Log With Graph

```bash
git log --oneline --graph
```

Displays commits using a graphical representation.

Example:

```text
* a449e00 Add Git reset and revert notes
* 7ae7a78 Add Git stash notes
* cc3bb75 Add Git remote and GitHub notes
* 2f6c191 Add Git rebase notes
* 9a85c1d Remove conflict practice file
```

The `*` represents a commit.

Branches and merges can be easier to understand using the graph.

---

## 4. Git Log All Branches

```bash
git log --oneline --all
```

Shows commits from all local and remote-tracking branches.

---

## 5. Git Log Graph All

```bash
git log --oneline --graph --all
```

This is one of the best commands for understanding Git history.

Example:

```text
* a449e00 (HEAD -> main) Add Git reset and revert notes
* 7ae7a78 Add Git stash notes
* cc3bb75 Add Git remote and GitHub notes
* 2f6c191 Add Git rebase notes
```

When branches exist, the graph shows where branches were created and merged.

---

## 6. View the Latest Commit

```bash
git log -1
```

Shows only the latest commit.

Short version:

```bash
git log -1 --oneline
```

Example:

```text
a449e00 Add Git reset and revert notes
```

---

## 7. View a Specific Number of Commits

```bash
git log -3 --oneline
```

Shows the latest three commits.

Example:

```text
a449e00 Add Git reset and revert notes
7ae7a78 Add Git stash notes
cc3bb75 Add Git remote and GitHub notes
```

---

## 8. Git Show

```bash
git show
```

Shows information about the latest commit, including:

* Commit information
* Commit message
* Files changed
* Actual changes

Example:

```bash
git show
```

---

## 9. Show a Specific Commit

```bash
git show a449e00
```

Replace `a449e00` with the commit ID you want to inspect.

Short version:

```bash
git show --stat a449e00
```

This shows a summary of the files changed.

---

## 10. Git Diff

```bash
git diff
```

Shows changes that are currently in the working directory but have not been staged.

Example:

```text
diff --git a/README.md b/README.md
index abc123..def456 100644
--- a/README.md
+++ b/README.md
@@ -1,3 +1,4 @@
 Git Practice
+Learning Git diff
```

The `+` indicates an added line.

The `-` indicates a deleted line.

---

## 11. Git Diff --staged

```bash
git diff --staged
```

Shows changes that have been staged using:

```bash
git add
```

Example workflow:

```bash
git add README.md
git diff --staged
```

This lets you review the changes before committing them.

---

## 12. Git Diff HEAD

```bash
git diff HEAD
```

Shows all changes between the current working directory/staging area and the latest commit.

It can include:

* Unstaged changes
* Staged changes

---

## 13. Git Diff Between Two Commits

```bash
git diff commit1 commit2
```

Example:

```bash
git diff 7ae7a78 a449e00
```

This compares two commits.

You can use this to see exactly what changed between two points in history.

---

## 14. Git Diff Between Branches

```bash
git diff main feature-branch
```

Compares the changes between two branches.

Example:

```bash
git diff main feature-login
```

This is useful before merging a feature branch.

---

## 15. Git Diff --stat

```bash
git diff --stat
```

Shows a summary of changed files instead of displaying every line.

Example:

```text
 README.md              | 5 +++++
 01-Git-Theory.md       | 10 +++++-----
 2 files changed, 10 insertions(+), 5 deletions(-)
```

---

## 16. Git Log With File Changes

```bash
git log --stat
```

Shows commit history together with the files changed in each commit.

Example:

```text
commit a449e00
    Add Git reset and revert notes

 08-Git-Reset-Revert.md | 964 ++++++++++++++++
 1 file changed
```

---

## 17. Git Log With Patch

```bash
git log -p
```

Shows commit history along with the actual changes introduced by each commit.

This can produce a large amount of output.

---

## 18. Search Commit Messages

```bash
git log --grep="stash"
```

Searches commit messages containing a specific word.

Example:

```bash
git log --grep="rebase"
```

This can help find commits related to a particular topic.

---

## 19. Search by Author

```bash
git log --author="Jyoti"
```

Shows commits created by an author.

---

## 20. View a File's History

```bash
git log -- README.md
```

Shows commits that changed `README.md`.

Example:

```bash
git log --oneline -- README.md
```

---

## 21. View Changes to a Specific File

```bash
git log -p -- README.md
```

Shows the history of `README.md` together with the changes made to it.

---

## 22. Compare Working Directory With HEAD

```bash
git diff HEAD
```

`HEAD` represents the current commit.

For example:

```text
HEAD
 |
 v
Latest commit
 |
 +---- Working directory changes
```

The command lets you see what has changed since the latest commit.

---

## 23. HEAD, HEAD~1 and HEAD~2

Git allows us to refer to previous commits using `~`.

Current commit:

```bash
HEAD
```

Previous commit:

```bash
HEAD~1
```

Two commits before:

```bash
HEAD~2
```

Three commits before:

```bash
HEAD~3
```

Example:

```bash
git show HEAD~1
```

Shows the previous commit.

---

## 24. Compare Current Commit With Previous Commit

```bash
git diff HEAD~1 HEAD
```

This compares the previous commit with the current commit.

Example:

```text
HEAD~1
  |
  | changes
  v
HEAD
```

---

## 25. Git Log With Dates

```bash
git log --date=short
```

Shows commit dates in a shorter format.

Example:

```text
commit a449e00
Date: 2026-08-09
```

---

## 26. Useful Git Log Format

```bash
git log --pretty=format:"%h - %an - %s"
```

Example:

```text
a449e00 - Jyoti - Add Git reset and revert notes
7ae7a78 - Jyoti - Add Git stash notes
cc3bb75 - Jyoti - Add Git remote and GitHub notes
```

Here:

* `%h` = short commit hash
* `%an` = author name
* `%s` = commit subject

---

## 27. Useful History Command

A very useful command for practice is:

```bash
git log --oneline --graph --decorate --all
```

Example:

```text
* a449e00 (HEAD -> main, origin/main) Add Git reset and revert notes
* 7ae7a78 Add Git stash notes
* cc3bb75 Add Git remote and GitHub notes
* 2f6c191 Add Git rebase notes
```

Meaning:

* `*` = commit
* `HEAD` = current location
* `main` = local main branch
* `origin/main` = remote-tracking main branch

---

# Git Diff Symbols

When using `git diff`, Git commonly uses these symbols:

```text
+ Added line
- Removed line
```

Example:

```diff
 Hello Git
+This line was added.
-This line was removed.
```

---

# Git Log vs Git Diff

| Command                | Purpose                       |
| ---------------------- | ----------------------------- |
| `git log`              | View commit history           |
| `git log --oneline`    | View short commit history     |
| `git log --graph`      | View commit graph             |
| `git log --all`        | View all branch history       |
| `git show`             | Inspect a commit              |
| `git diff`             | View unstaged changes         |
| `git diff --staged`    | View staged changes           |
| `git diff HEAD`        | Compare changes with HEAD     |
| `git diff A B`         | Compare two commits           |
| `git diff main branch` | Compare branches              |
| `git log --stat`       | Show files changed in commits |
| `git log -p`           | Show commit changes           |

---

# Common Workflow

A common workflow for reviewing changes is:

```bash
git status
```

Check the current state.

Then:

```bash
git diff
```

Review unstaged changes.

Stage the changes:

```bash
git add .
```

Review staged changes:

```bash
git diff --staged
```

Commit:

```bash
git commit -m "Update documentation"
```

View the commit:

```bash
git log -1 --oneline
```

View the complete history:

```bash
git log --oneline --graph --all
```

---

# Practical Example

Suppose you modify `README.md`.

First check the status:

```bash
git status
```

Then inspect the changes:

```bash
git diff
```

Stage the file:

```bash
git add README.md
```

Review the staged version:

```bash
git diff --staged
```

Commit:

```bash
git commit -m "Update README"
```

View the new commit:

```bash
git log -1 --oneline
```

---

# Important Interview Questions

## What is `git log`?

> `git log` is used to view the commit history of a Git repository.

## What is `git diff`?

> `git diff` is used to compare changes between files, commits, branches, or the working directory.

## What is `git diff --staged`?

> `git diff --staged` shows changes that have been added to the staging area but have not yet been committed.

## What is `git show`?

> `git show` displays information and changes associated with a specific commit.

## What is `HEAD`?

> `HEAD` is a reference that points to the currently checked-out commit or branch.

## What does `HEAD~1` mean?

> `HEAD~1` refers to the commit immediately before the current commit.

## How do you see a short Git history?

```bash
git log --oneline
```

## How do you see the branch history graph?

```bash
git log --oneline --graph --all
```

## How do you compare two commits?

```bash
git diff commit1 commit2
```

## How do you compare two branches?

```bash
git diff main feature-branch
```

---

# Quick Reference

```bash
# Commit history
git log

# Short history
git log --oneline

# History with graph
git log --oneline --graph --all

# Latest commit
git log -1

# Show commit
git show <commit>

# Working directory changes
git diff

# Staged changes
git diff --staged

# Changes compared with HEAD
git diff HEAD

# Compare commits
git diff <commit1> <commit2>

# Compare branches
git diff main feature-branch

# Commit statistics
git log --stat

# Search commit messages
git log --grep="keyword"

# File history
git log --oneline -- <file>
```

---

# Key Takeaways

1. `git log` is used to inspect commit history.
2. `git log --oneline` gives a compact history.
3. `git log --graph --all` helps visualize branches.
4. `git show` lets you inspect a commit.
5. `git diff` shows unstaged changes.
6. `git diff --staged` shows staged changes.
7. `git diff HEAD` compares the working state with the latest commit.
8. `git diff commit1 commit2` compares two commits.
9. `git diff main feature-branch` compares branches.
10. `HEAD` represents the current commit.
11. `HEAD~1` represents the previous commit.
12. Reviewing changes with `git diff` before committing is a good Git practice.
