# Git Commands

A practical Git command reference with examples and short explanations.

---

# 1. Git Version

Check the installed Git version.

```bash
git --version
```

Example:

```text
git version 2.x.x
```

### Remember

> `git --version` → Check Git version.

---

# 2. Git Configuration

Git needs your name and email for commits.

## Set username

```bash
git config --global user.name "Your Name"
```

## Set email

```bash
git config --global user.email "your@email.com"
```

## Check configuration

```bash
git config --list
```

### Remember

> `git config` → Configure Git.

---

# 3. Initialize a Repository

Create a new Git repository.

```bash
git init
```

Example:

```bash
mkdir my-project
cd my-project
git init
```

Git creates:

```text
.git/
```

### Remember

> `git init` → Start Git tracking in a directory.

---

# 4. Check Repository Status

```bash
git status
```

Shows:

* Current branch
* Modified files
* Untracked files
* Staged files
* Unstaged files

Example:

```bash
git status
```

### Remember

> `git status` → What is happening in my repository?

---

# 5. Add One File

Stage a specific file.

```bash
git add filename
```

Example:

```bash
git add README.md
```

### Remember

> `git add filename` → Stage one file.

---

# 6. Add All Changes

Stage all changes in the current directory.

```bash
git add .
```

### Remember

> `git add .` → Stage all changes.

---

# 7. Unstage a File

Remove a file from the staging area without deleting the file.

```bash
git restore --staged filename
```

Example:

```bash
git restore --staged README.md
```

### Remember

> `git restore --staged` → Unstage a file.

---

# 8. Commit Changes

Create a commit from staged changes.

```bash
git commit -m "Add README"
```

Example:

```bash
git commit -m "Add Git commands"
```

### Remember

> `git commit` → Save a snapshot in Git history.

---

# 9. Commit All Tracked Modified Files

You can commit modifications to already-tracked files without explicitly running `git add` first:

```bash
git commit -am "Update documentation"
```

### Important

This does **not** include new untracked files.

For new files, use:

```bash
git add .
git commit -m "Add new files"
```

---

# 10. View Git History

```bash
git log
```

Shows detailed commit history.

---

# 11. View Compact History

```bash
git log --oneline
```

Example:

```text
f6b0be6 Add Git theory and learning notes
b3a5843 add theory file
```

### Remember

> `git log --oneline` → Quick commit history.

---

# 12. View History as a Graph

```bash
git log --oneline --graph --all
```

Useful for understanding branches and merges.

Example:

```text
* abc1234 Add payment feature
|\
| * def5678 Add login feature
|/
* 1234567 Initial commit
```

### Remember

> `--graph` → Visualize branch history.

---

# 13. Git Diff

Show unstaged changes.

```bash
git diff
```

### Remember

> `git diff` → See what changed but isn't staged.

---

# 14. Staged Diff

Show changes that are already staged.

```bash
git diff --staged
```

### Remember

> `git diff --staged` → See what will go into the next commit.

---

# 15. Compare Commits

Compare two commits:

```bash
git diff commit1 commit2
```

Example:

```bash
git diff HEAD~1 HEAD
```

### Remember

> `git diff` → Compare changes.

---

# 16. Create a Branch

```bash
git branch feature-login
```

This creates a branch but does not switch to it.

---

# 17. List Branches

```bash
git branch
```

Example:

```text
* main
  feature-login
```

The `*` shows the current branch.

### Remember

> `git branch` → See local branches.

---

# 18. Create and Switch to a Branch

Recommended modern command:

```bash
git switch -c feature-login
```

This does two things:

```text
Create branch
     +
Switch branch
```

### Remember

> `git switch -c` → Create + switch.

---

# 19. Switch Branch

```bash
git switch main
```

Example:

```bash
git switch feature-login
```

### Remember

> `git switch` → Change branches.

---

# 20. Delete a Branch

After merging a branch:

```bash
git branch -d feature-login
```

Force delete:

```bash
git branch -D feature-login
```

### Important

Use `-D` carefully because it can delete a branch even when Git thinks it contains unmerged work.

---

# 21. Rename Current Branch

Rename the current branch:

```bash
git branch -M main
```

Example:

```bash
git branch -M main
```

### Remember

> `git branch -M main` → Rename current branch to `main`.

---

# 22. Merge a Branch

First switch to the branch that should receive the changes:

```bash
git switch main
```

Then merge:

```bash
git merge feature-login
```

### Workflow

```text
feature-login
      ↓
    merge
      ↓
main
```

### Remember

> `git merge` → Combine branch histories.

---

# 23. Rebase

Rebase your current branch onto `main`:

```bash
git rebase main
```

Example:

```text
Before:

main:    A---B
              \
feature:       C---D

After rebase:

main:    A---B
              \
feature:       C'---D'
```

### Remember

> `git rebase` → Replay your commits on another base.

### Important

Be careful rebasing commits that other people are already using.

---

# 24. Clone a Repository

Download an existing Git repository.

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/username/project.git
```

### Remember

> `git clone` → Copy a remote repository to your computer.

---

# 25. View Remote Repositories

```bash
git remote -v
```

Example:

```text
origin  https://github.com/username/project.git (fetch)
origin  https://github.com/username/project.git (push)
```

### Remember

> `git remote -v` → Show remote URLs.

---

# 26. Add a Remote

Connect your local repository to GitHub:

```bash
git remote add origin <repository-url>
```

Example:

```bash
git remote add origin https://github.com/username/project.git
```

### Remember

> `origin` → Common name for the main remote repository.

---

# 27. Remove a Remote

```bash
git remote remove origin
```

### Remember

> `git remote remove` → Remove a remote connection.

---

# 28. Rename a Remote

```bash
git remote rename origin upstream
```

---

# 29. Push to GitHub

Push your local `main` branch:

```bash
git push origin main
```

### Remember

> `git push` → Send local commits to the remote repository.

---

# 30. Push and Set Upstream

```bash
git push -u origin main
```

The `-u` sets the upstream relationship.

After this, you can normally use:

```bash
git push
```

### Remember

> `-u` → Remember the upstream branch.

---

# 31. Push a New Branch

```bash
git push -u origin feature-login
```

After the upstream is configured:

```bash
git push
```

---

# 32. Fetch Remote Changes

```bash
git fetch
```

Fetch from a specific remote:

```bash
git fetch origin
```

### Important

`git fetch` downloads remote information but does not automatically merge it into your current branch.

### Remember

> `git fetch` → Download remote updates without integrating them.

---

# 33. Pull Changes

```bash
git pull
```

Or:

```bash
git pull origin main
```

`git pull` generally performs:

```text
git fetch
   +
integration
```

### Remember

> `git pull` → Get remote changes and integrate them.

---

# 34. Git Pull vs Fetch

```text
git fetch
    ↓
Download updates
    ↓
No automatic integration
```

```text
git pull
    ↓
Fetch updates
    ↓
Integrate updates
```

### Easy Memory

> Fetch = Download

> Pull = Download + Integrate

---

# 35. Git Restore

Restore an unstaged change:

```bash
git restore filename
```

Example:

```bash
git restore README.md
```

This can discard the file's current unstaged changes.

### Important

Be careful because you may lose local changes.

---

# 36. Git Reset

Unstage a file:

```bash
git reset HEAD filename
```

Modern alternative:

```bash
git restore --staged filename
```

Reset the current branch one commit backward:

```bash
git reset HEAD~1
```

### Reset modes

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

### Important

Be very careful with:

```bash
git reset --hard
```

because it can discard local changes.

---

# 37. Git Revert

Undo a commit by creating a new commit:

```bash
git revert <commit-hash>
```

Example:

```bash
git revert f6b0be6
```

### Remember

> `git revert` → Undo a commit safely by creating another commit.

---

# 38. Reset vs Revert

```text
reset
  ↓
Move/rewrite history
```

```text
revert
  ↓
Create a new commit that reverses changes
```

For shared branches, `revert` is generally safer than rewriting published history.

---

# 39. Git Stash

Temporarily save unfinished changes:

```bash
git stash
```

View stashes:

```bash
git stash list
```

Restore the latest stash and remove it from the stash list:

```bash
git stash pop
```

Apply a stash without removing it:

```bash
git stash apply
```

### Remember

> `git stash` → Temporarily put unfinished work aside.

---

# 40. Git Show

Show details of a commit:

```bash
git show <commit-hash>
```

Example:

```bash
git show f6b0be6
```

### Remember

> `git show` → Show details of a commit.

---

# 41. Git Reflog

View movements of `HEAD` and other references:

```bash
git reflog
```

Useful when recovering from:

* Reset
* Rebase
* Deleted branch
* Other history-changing operations

### Remember

> `git reflog` → Track where Git references have been.

---

# 42. Git Tag

Create a tag:

```bash
git tag v1.0.0
```

List tags:

```bash
git tag
```

Push a tag:

```bash
git push origin v1.0.0
```

Push all tags:

```bash
git push origin --tags
```

### Remember

> Tag → Mark a specific version/commit.

---

# 43. Git Cherry-Pick

Apply the changes from a specific commit to your current branch:

```bash
git cherry-pick <commit-hash>
```

Example:

```bash
git cherry-pick f6b0be6
```

### Remember

> Cherry-pick → Apply one specific commit to the current branch.

---

# 44. Git Remote Rename

Rename a remote:

```bash
git remote rename origin upstream
```

Check:

```bash
git remote -v
```

---

# 45. Git Remote Show

Show information about a remote:

```bash
git remote show origin
```

This can show:

* Remote URL
* Tracked branches
* Local branches
* Push/pull information

---

# 46. Delete a Remote Branch

Delete a branch from GitHub:

```bash
git push origin --delete feature-login
```

### Remember

> `git push origin --delete` → Delete a remote branch.

---

# 47. Delete a Local Branch

```bash
git branch -d feature-login
```

Force:

```bash
git branch -D feature-login
```

---

# 48. Git Ignore

Create a file named:

```text
.gitignore
```

Example:

```text
.env
*.log
node_modules/
dist/
build/
```

Git will normally ignore matching files.

### Check ignored files

```bash
git status --ignored
```

### Remember

> `.gitignore` → Tell Git what not to track.

---

# 49. Check Which Files Are Tracked

```bash
git ls-files
```

This shows files currently tracked by Git.

---

# 50. Search Git History

Search commit messages:

```bash
git log --grep="login"
```

Example:

```bash
git log --grep="authentication"
```

---

# 51. See Who Changed Each Line

```bash
git blame filename
```

Example:

```bash
git blame README.md
```

This shows which commit/author last changed each line.

---

# 52. Check Branch Tracking

```bash
git branch -vv
```

This shows local branches and their upstream branches.

Example:

```text
* main abc1234 [origin/main] Add Git commands
```

---

# 53. Check Current Branch

```bash
git branch --show-current
```

Example:

```text
main
```

### Remember

> `git branch --show-current` → Show current branch.

---

# 54. Git Status Short Format

```bash
git status --short
```

Example:

```text
 M README.md
?? new-file.txt
```

Meaning:

```text
M  = Modified
?? = Untracked
A  = Added
D  = Deleted
```

---

# 55. Delete a File Through Git

```bash
git rm filename
```

Example:

```bash
git rm old-file.txt
```

Then commit:

```bash
git commit -m "Remove old file"
```

---

# 56. Rename a File Through Git

```bash
git mv old-name.txt new-name.txt
```

Then:

```bash
git commit -m "Rename file"
```

---

# 57. View Git Configuration

Global configuration:

```bash
git config --global --list
```

Repository configuration:

```bash
git config --local --list
```

---

# 58. Set the Default Branch Name

```bash
git config --global init.defaultBranch main
```

Now new repositories initialized with:

```bash
git init
```

will use `main` as the initial branch name.

---

# 59. Git Help

General help:

```bash
git help
```

Help for a command:

```bash
git help commit
```

Short command help:

```bash
git commit --help
```

---

# 60. Common Git Workflow

This is the workflow you should practice repeatedly:

```bash
git status
git add .
git status
git commit -m "Describe the change"
git log --oneline
git push
```

### Flow

```text
Modify
  ↓
git status
  ↓
git add
  ↓
git status
  ↓
git commit
  ↓
git log
  ↓
git push
```

---

# 61. First Git Repository Workflow

```bash
mkdir my-project
cd my-project
git init
```

Create files:

```bash
touch README.md
```

Check:

```bash
git status
```

Stage:

```bash
git add README.md
```

Commit:

```bash
git commit -m "Initial commit"
```

View history:

```bash
git log --oneline
```

---

# 62. GitHub Repository Workflow

Create a repository on GitHub.

Then connect your local repository:

```bash
git remote add origin https://github.com/USERNAME/REPOSITORY.git
```

Check:

```bash
git remote -v
```

Push:

```bash
git push -u origin main
```

After that:

```bash
git push
```

---

# 63. Feature Branch Workflow

Create a branch:

```bash
git switch -c feature-login
```

Check:

```bash
git branch
```

Modify files.

Check:

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

Then create a Pull Request on GitHub.

---

# 64. Merge Workflow

Switch to main:

```bash
git switch main
```

Get latest changes:

```bash
git pull
```

Merge feature branch:

```bash
git merge feature-login
```

Push:

```bash
git push
```

Delete local branch if no longer needed:

```bash
git branch -d feature-login
```

Delete remote branch if no longer needed:

```bash
git push origin --delete feature-login
```

---

# 65. Git Command Cheat Sheet

| Command                     | Purpose                  |
| --------------------------- | ------------------------ |
| `git --version`             | Check Git version        |
| `git init`                  | Initialize repository    |
| `git status`                | Check repository status  |
| `git add file`              | Stage a file             |
| `git add .`                 | Stage all changes        |
| `git commit -m "message"`   | Create commit            |
| `git log`                   | View history             |
| `git log --oneline`         | Compact history          |
| `git diff`                  | View unstaged changes    |
| `git diff --staged`         | View staged changes      |
| `git branch`                | List branches            |
| `git switch branch`         | Switch branch            |
| `git switch -c branch`      | Create and switch branch |
| `git merge branch`          | Merge branch             |
| `git rebase main`           | Rebase onto main         |
| `git clone URL`             | Clone repository         |
| `git remote -v`             | View remotes             |
| `git remote add origin URL` | Add remote               |
| `git fetch`                 | Download remote updates  |
| `git pull`                  | Fetch and integrate      |
| `git push`                  | Upload commits           |
| `git stash`                 | Temporarily save changes |
| `git stash pop`             | Restore latest stash     |
| `git restore file`          | Restore file             |
| `git revert HASH`           | Reverse a commit         |
| `git reset`                 | Move/reset history       |
| `git tag`                   | Manage tags              |
| `git reflog`                | View reference history   |
| `git cherry-pick HASH`      | Apply a specific commit  |
| `git show HASH`             | Show commit details      |
| `git rm file`               | Delete tracked file      |
| `git mv old new`            | Rename file              |

---

# 66. Most Important Commands to Memorize

Start with these commands first:

```bash
git init
git status
git add .
git commit -m "message"
git log --oneline
git branch
git switch -c feature-name
git switch main
git merge feature-name
git remote -v
git remote add origin URL
git push
git pull
git fetch
git clone URL
```

Don't try to memorize every Git command at once.

Master these first:

```text
STATUS
   ↓
ADD
   ↓
COMMIT
   ↓
LOG
   ↓
PUSH
   ↓
PULL
```

Then learn:

```text
BRANCH
   ↓
SWITCH
   ↓
MERGE
   ↓
REBASE
   ↓
PULL REQUEST
```

---

# 67. Short Interview Answers

### What is Git?

> Git is a distributed version control system used to track and manage changes in source code.

### What is GitHub?

> GitHub is a platform for hosting Git repositories and collaborating on software projects.

### What is a repository?

> A repository is a project managed by Git that contains files and their version history.

### What is `git init`?

> `git init` initializes a new Git repository.

### What is `git add`?

> `git add` stages changes for the next commit.

### What is a commit?

> A commit is a snapshot of staged changes in Git history.

### What is `git push`?

> `git push` sends local commits to a remote repository.

### What is `git pull`?

> `git pull` fetches remote changes and integrates them into the current branch.

### What is `git fetch`?

> `git fetch` downloads remote changes without automatically integrating them.

### What is `git clone`?

> `git clone` creates a local copy of an existing remote repository.

### What is a branch?

> A branch is an independent line of development.

### What is merge?

> Merge combines changes from one branch into another.

### What is rebase?

> Rebase reapplies commits on top of another base commit or branch.

### What is fork?

> A fork is a GitHub copy of another repository under your own account.

### What is a Pull Request?

> A Pull Request is a GitHub mechanism for proposing, reviewing, and merging changes.

### What is `origin`?

> `origin` is the conventional name for a remote repository.

### What is `.gitignore`?

> `.gitignore` specifies files and directories that Git should normally ignore.

---

# 68. Golden Git Workflow

Remember this:

```text
1. MODIFY
      ↓
2. git status
      ↓
3. git diff
      ↓
4. git add .
      ↓
5. git diff --staged
      ↓
6. git commit -m "message"
      ↓
7. git log --oneline
      ↓
8. git push
```

For team development:

```text
Clone
  ↓
Branch
  ↓
Modify
  ↓
Status
  ↓
Diff
  ↓
Add
  ↓
Commit
  ↓
Push
  ↓
Pull Request
  ↓
Review
  ↓
Merge
```