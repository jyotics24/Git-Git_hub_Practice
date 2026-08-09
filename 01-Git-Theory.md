# Git Theory

## 1. What is Git?

Git is a **Distributed Version Control System (DVCS)**.

Git is a tool used by developers to track changes in source code and manage different versions of a project.

Git helps developers:

* Track changes
* Maintain project history
* Create branches
* Work on features independently
* Compare changes
* Restore previous versions
* Collaborate with other developers

### Simple Definition

> Git is a tool used to track and manage changes in a project.

---

# 2. What is Version Control?

**Version Control** is a system that records changes to files over time.

It allows developers to maintain the history of a project.

Example:

```text
Version 1
    ↓
Version 2
    ↓
Version 3
    ↓
Version 4
```

If something goes wrong in Version 4, we can inspect previous versions and understand what changed.

### Without Version Control

A developer might create files like:

```text
project-final.zip
project-final-new.zip
project-final-new-2.zip
project-final-really-final.zip
```

This becomes difficult to manage.

Git solves this problem by maintaining a structured history of changes.

---

# 3. Why Do We Need Git?

Software projects change constantly.

Developers may:

* Add features
* Fix bugs
* Remove code
* Modify existing functionality
* Experiment with new ideas
* Work with other developers

Git keeps track of these changes.

### Example

Suppose a project contains:

```text
Login
Payment
Database
```

A developer adds a new login feature.

Later, the feature causes a problem.

With Git, the developer can inspect the history and understand what changed.

---

# 4. What is GitHub?

**GitHub is a platform for hosting Git repositories and collaborating on software projects.**

GitHub provides features such as:

* Repository hosting
* Pull Requests
* Code reviews
* Issues
* Collaboration
* GitHub Actions
* Access control

### Simple Definition

> Git is the version control tool, while GitHub is a platform that hosts Git repositories and provides collaboration features.

---

# 5. Git vs GitHub

| Git                      | GitHub                     |
| ------------------------ | -------------------------- |
| Version control software | Online platform            |
| Runs on your computer    | Hosted online              |
| Tracks changes           | Hosts repositories         |
| Creates commits          | Stores remote repositories |
| Creates branches         | Provides Pull Requests     |
| Can work without GitHub  | Commonly used with Git     |

### Easy Memory

```text
Git    = Version Control Tool

GitHub = Platform for Git Repositories
```

---

# 6. What is a Repository?

A **repository**, commonly called a **repo**, is a project managed by Git.

Example:

```text
my-project/
├── app.py
├── README.md
├── requirements.txt
└── .git/
```

A directory becomes a Git repository when we run:

```bash
git init
```

---

# 7. What is the `.git` Directory?

When we run:

```bash
git init
```

Git creates a hidden directory:

```text
.git/
```

The `.git` directory contains Git's internal repository information.

It contains information required for things such as:

* Commit history
* Branch information
* Repository configuration
* References
* Git objects

### Important

> Do not manually modify or delete `.git` unless you understand the consequences.

Deleting `.git` removes the Git repository information from that directory.

---

# 8. Local Repository

A **local repository** is the Git repository stored on your computer.

Example:

```text
Your Computer
      ↓
Local Git Repository
```

You can create commits and view history locally without GitHub.

---

# 9. Remote Repository

A **remote repository** is another copy of a Git repository, commonly hosted on GitHub.

Example:

```text
Your Computer
      ↓
Local Repository
      ↓
GitHub
      ↓
Remote Repository
```

Local and remote repositories can exchange commits.

---

# 10. Working Directory

The **working directory** is the project directory where you create and modify files.

Example:

```text
my-project/
├── app.py
├── index.html
└── README.md
```

When you modify a file, the change initially exists in the working directory.

Git can detect these changes using:

```bash
git status
```

---

# 11. The Three Main Areas of Git

One of the most important Git concepts is the three main areas:

```text
Working Directory
       |
       | git add
       ↓
Staging Area
       |
       | git commit
       ↓
Local Repository
```

## 11.1 Working Directory

Where you create and modify files.

Example:

```text
app.py
README.md
index.html
```

---

## 11.2 Staging Area

The staging area contains changes selected for the next commit.

Example:

```bash
git add app.py
```

---

## 11.3 Local Repository

After staging changes, we create a commit:

```bash
git commit -m "Add application"
```

The commit records the staged changes in the local repository.

---

# 12. What is an Untracked File?

An **untracked file** is a file that exists in the project directory but Git is not tracking yet.

Example:

```text
app.py
```

Run:

```bash
git status
```

Git may show:

```text
Untracked files:
    app.py
```

This means Git sees the file but has not started tracking it.

To add it:

```bash
git add app.py
```

---

# 13. What is a Tracked File?

A tracked file is a file that Git is monitoring as part of the repository.

Typical flow:

```text
New File
   ↓
Untracked
   ↓
git add
   ↓
Staged
   ↓
git commit
   ↓
Tracked in Repository History
```

---

# 14. What is Staging?

**Staging** means selecting changes that should be included in the next commit.

Example:

```bash
git add app.py
```

Or add everything:

```bash
git add .
```

### Why is staging useful?

Suppose you modified three files:

```text
app.py
login.py
database.py
```

But you only want to commit `login.py`.

You can run:

```bash
git add login.py
```

Now only `login.py` is staged.

### Simple Definition

> Staging means preparing selected changes for the next commit.

---

# 15. What is a Commit?

A **commit** is a recorded snapshot of staged changes.

Example:

```bash
git commit -m "Add user authentication"
```

A commit represents a checkpoint in project history.

Example:

```text
Commit 1
   ↓
Commit 2
   ↓
Commit 3
   ↓
Commit 4
```

### Simple Definition

> A commit is a snapshot or checkpoint of the project.

---

# 16. What is a Commit Hash?

Every Git commit has a unique identifier called a **commit hash**.

Example:

```text
a82f31d
```

A full Git hash is longer, but Git often displays a shortened version.

You can see commit hashes using:

```bash
git log
```

The hash allows Git to identify a specific commit.

---

# 17. What is a Commit Message?

A commit message describes what changed.

Good example:

```bash
git commit -m "Add user authentication"
```

Another good example:

```bash
git commit -m "Fix login validation"
```

Poor example:

```bash
git commit -m "changes"
```

A good commit message should clearly communicate the purpose of the change.

---

# 18. What is Git History?

Git maintains a history of commits.

Example:

```text
Commit 1
"Initial project"
      ↓
Commit 2
"Add login"
      ↓
Commit 3
"Fix login validation"
      ↓
Commit 4
"Add logout"
```

View the history:

```bash
git log
```

Compact history:

```bash
git log --oneline
```

---

# 19. What is a Branch?

A **branch** is an independent line of development.

Branches allow developers to work on features or fixes without directly changing another branch.

Example:

```text
main
 |
 ●
 |
 ●──────── feature-login
 |              |
 ●              ●
                ●
```

---

# 20. What is the `main` Branch?

`main` is commonly used as the primary branch of a Git repository.

Example:

```text
main
 |
 ●
 |
 ●
 |
 ●
```

Developers often create feature branches from `main`.

Example:

```text
main
 |
 ├── feature-login
 ├── feature-payment
 └── bugfix-header
```

---

# 21. Why Do We Use Branches?

Branches help developers:

* Work on features independently
* Fix bugs separately
* Experiment safely
* Collaborate with other developers
* Keep the main branch stable

Example:

```text
main
 |
 ●────────●────────●
          \
           feature-login
              |
              ●
              ●
              ●
```

---

# 22. What is `HEAD`?

`HEAD` is a special reference in Git that represents the commit currently checked out.

Example:

```text
main
 |
 ● Commit 1
 |
 ● Commit 2
 |
 ● Commit 3 ← HEAD
```

If you switch branches, `HEAD` moves to the current branch.

### Simple Definition

> HEAD tells Git which commit or branch we are currently working from.

---

# 23. What is Branch Switching?

Switching means changing the branch you are currently working on.

Example:

```bash
git switch feature-login
```

You can see the current branch using:

```bash
git branch
```

---

# 24. What is Merge?

**Merge** combines changes from one branch into another branch.

Example:

```bash
git switch main
git merge feature-login
```

Concept:

```text
feature-login
      |
      | merge
      ↓
     main
```

### Simple Definition

> Merge combines changes from different branches.

---

# 25. What is Rebase?

**Rebase** reapplies your branch commits on top of another branch.

Example:

```bash
git rebase main
```

### Simple Definition

> Rebase puts my branch changes on top of the latest changes from another branch.

Rebase can create a cleaner, more linear history.

### Important

Rebase rewrites commit history, so it should be used carefully on shared branches.

---

# 26. Merge vs Rebase

| Merge                              | Rebase                                |
| ---------------------------------- | ------------------------------------- |
| Combines branches                  | Reapplies commits                     |
| Creates a merge commit when needed | Usually creates a linear history      |
| Preserves branch history           | Rewrites commit history               |
| Generally safer for shared history | Requires more care on shared branches |

Simple memory:

```text
Merge  = Combine histories

Rebase = Move/replay commits
```

---

# 27. What is a Merge Conflict?

A **merge conflict** happens when Git cannot automatically determine how to combine changes.

For example, two branches modify the same part of a file differently.

Git marks the file as conflicted.

Typical process:

```text
Conflict
   ↓
Open the file
   ↓
Choose the correct changes
   ↓
Save the file
   ↓
git add
   ↓
Complete merge
```

---

# 28. What is a Remote?

A **remote** is a reference to another Git repository.

Example:

```text
origin
   ↓
GitHub Repository
```

`origin` is the conventional name for the primary remote repository.

You can see remotes with:

```bash
git remote -v
```

---

# 29. What is `origin`?

`origin` is the commonly used name for the primary remote repository.

Example:

```text
origin
   ↓
https://github.com/username/project.git
```

`origin` is only a name. It can technically be changed.

---

# 30. What is Push?

`git push` sends local commits to a remote repository.

Example:

```bash
git push origin main
```

Concept:

```text
Local Repository
      |
      | git push
      ↓
GitHub Repository
```

### Simple Definition

> Push sends my local commits to GitHub.

---

# 31. What is Pull?

`git pull` gets changes from a remote repository and integrates them into the current branch.

Example:

```bash
git pull origin main
```

### Simple Definition

> Pull gets remote changes and integrates them into my current branch.

---

# 32. What is Fetch?

`git fetch` downloads remote changes without automatically integrating them into the current branch.

Example:

```bash
git fetch
```

### Difference

```text
git fetch
    ↓
Download remote updates
    ↓
Do not automatically integrate
```

```text
git pull
    ↓
Fetch remote updates
    ↓
Integrate changes
```

---

# 33. What is Clone?

`git clone` creates a local copy of an existing remote repository.

Example:

```bash
git clone https://github.com/username/project.git
```

Git clone generally:

* Creates a directory
* Downloads project files
* Downloads Git history
* Creates the `.git` directory
* Configures the remote as `origin`
* Checks out the appropriate branch

### Simple Definition

> Git clone creates a local copy of an existing remote Git repository.

---

# 34. What is Fork?

A **fork** is a copy of someone else's GitHub repository under your own GitHub account.

Forks are commonly used when contributing to projects where you do not have direct write access.

Example:

```text
Original Repository
        |
       Fork
        ↓
My GitHub Repository
```

### Simple Definition

> A fork is my own GitHub copy of someone else's repository.

---

# 35. Fork vs Clone

| Fork                                         | Clone                      |
| -------------------------------------------- | -------------------------- |
| GitHub operation                             | Git command                |
| GitHub → GitHub                              | GitHub → Computer          |
| Creates a repository under my GitHub account | Creates a local repository |
| Commonly used for contributing               | Used to work locally       |

Easy memory:

```text
Fork  = GitHub → GitHub

Clone = GitHub → Computer
```

---

# 36. What is a Pull Request?

A **Pull Request (PR)** is a GitHub feature used to propose changes from one branch or repository to another.

Typical workflow:

```text
Feature Branch
      |
      | git push
      ↓
GitHub
      |
      | Pull Request
      ↓
main
```

Pull Requests allow teams to:

* Review code
* Discuss changes
* Suggest improvements
* Run automated checks
* Approve changes
* Merge changes

---

# 37. Fork + Clone + Pull Request Workflow

When contributing to someone else's project:

```text
Original Repository
        |
       Fork
        ↓
My GitHub Repository
        |
      Clone
        ↓
My Computer
        |
   Make Changes
        |
      Commit
        |
       Push
        ↓
My GitHub Repository
        |
 Pull Request
        ↓
Original Repository
```

---

# 38. What is `.gitignore`?

`.gitignore` is a special file that tells Git which files and directories should normally not be tracked.

Example:

```text
.env
node_modules/
*.log
build/
dist/
```

Common things to ignore:

* Passwords
* API keys
* Cloud credentials
* Environment files
* Dependency directories
* Build output
* Temporary files
* Log files

### Important

> Never commit passwords, API keys, private tokens, or cloud credentials.

---

# 39. What is Git Diff?

`git diff` shows differences between versions of files or commits.

Show unstaged changes:

```bash
git diff
```

Show staged changes:

```bash
git diff --staged
```

### Simple Definition

> `git diff` shows what changed.

---

# 40. What is Git Stash?

`git stash` temporarily saves uncommitted changes.

Example:

```bash
git stash
```

Restore the changes:

```bash
git stash pop
```

### Simple Definition

> Git stash temporarily stores unfinished changes.

Example situation:

```text
Working on Feature A
       ↓
Urgent work arrives
       ↓
git stash
       ↓
Work on urgent task
       ↓
git stash pop
       ↓
Continue Feature A
```

---

# 41. What is Git Restore?

`git restore` can restore files or remove files from the staging area.

Discard unstaged changes:

```bash
git restore filename
```

Unstage a file:

```bash
git restore --staged filename
```

### Simple Definition

> `git restore` restores files or unstages changes.

---

# 42. What is Git Reset?

`git reset` moves the current branch to another commit and can also change the staging area or working files depending on the option used.

Example:

```bash
git reset HEAD~1
```

Common modes:

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

### Important

Be careful with `git reset`, especially:

```bash
git reset --hard
```

because it can permanently discard local changes.

### Simple Definition

> `git reset` moves the current branch to another commit and can modify staged or working changes.

---

# 43. What is Git Revert?

`git revert` creates a new commit that reverses the changes introduced by an earlier commit.

Example:

```bash
git revert <commit-hash>
```

### Simple Definition

> `git revert` undoes a previous commit by creating a new commit.

This is generally safer than rewriting shared history.

---

# 44. Reset vs Revert

| Reset                         | Revert                           |
| ----------------------------- | -------------------------------- |
| Moves branch history          | Creates a new commit             |
| Can rewrite history           | Preserves existing history       |
| Can be destructive            | Generally safer                  |
| Be careful on shared branches | Commonly used on shared branches |

Easy memory:

```text
Reset  = Move history

Revert = Undo with a new commit
```

---

# 45. What are Git Tags?

A **tag** is a named reference to a specific commit.

Tags are commonly used for releases.

Example:

```bash
git tag v1.0.0
```

Example:

```text
v1.0.0
   ↓
Specific Commit
```

### Simple Definition

> A Git tag marks a specific version of a project.

---

# 46. What is `git checkout`?

`git checkout` is an older Git command that can be used for several purposes, including switching branches and restoring files.

Example:

```bash
git checkout main
```

Modern Git generally recommends:

```bash
git switch main
```

for switching branches, and:

```bash
git restore filename
```

for restoring files.

### Simple Definition

> `git checkout` is a legacy/multi-purpose command; `git switch` and `git restore` provide clearer alternatives for common tasks.

---

# 47. What is `git remote -v`?

This command displays the URLs of configured remote repositories.

```bash
git remote -v
```

Example:

```text
origin  https://github.com/username/project.git (fetch)
origin  https://github.com/username/project.git (push)
```

### Simple Definition

> `git remote -v` shows where my local repository is connected.

---

# 48. What is `git show`?

`git show` displays information about a specific Git object, commonly a commit.

Example:

```bash
git show <commit-hash>
```

It can show:

* Commit information
* Author
* Commit message
* Changes introduced by the commit

### Simple Definition

> `git show` displays details about a commit.

---

# 49. What is `git reflog`?

`git reflog` records movements of references such as `HEAD`.

Example:

```bash
git reflog
```

It can help find commits or previous states after operations such as:

* Reset
* Rebase
* Branch switching

### Simple Definition

> `git reflog` helps track where Git references have been and can help recover lost commits.

---

# 50. What is a Detached HEAD?

Normally:

```text
main
 |
 ●
 |
 ● ← HEAD
```

In a detached HEAD state, `HEAD` points directly to a commit instead of a branch.

Example:

```bash
git checkout <commit-hash>
```

or:

```bash
git switch --detach <commit-hash>
```

### Simple Definition

> Detached HEAD means HEAD is pointing directly to a commit instead of a branch.

---

# 51. What is Cherry-Pick?

`git cherry-pick` applies the changes from a specific commit onto the current branch.

Example:

```bash
git cherry-pick <commit-hash>
```

### Simple Definition

> Cherry-pick copies the changes from a specific commit onto my current branch.

---

# 52. What is a Working Tree?

The **working tree** represents the files currently checked out in your repository.

It is essentially the set of project files you are currently working with.

Example:

```text
Repository
   ↓
Working Tree
   ↓
Files you edit
```

---

# 53. What is HEAD~1?

`HEAD~1` means the parent commit of the current `HEAD`.

Example:

```text
Commit A
   ↓
Commit B ← HEAD
```

Then:

```text
HEAD~1 = Commit A
```

Similarly:

```text
HEAD~2
```

means two commits before the current `HEAD`.

---

# 54. What is HEAD^?

`HEAD^` generally refers to the first parent of the current `HEAD`.

For a normal linear history:

```text
Commit A
   ↓
Commit B ← HEAD
```

Then:

```text
HEAD^ = Commit A
```

---

# 55. What is a Merge Commit?

A **merge commit** is a commit that combines histories from two or more branches.

Example:

```text
      ● Feature
     / \
●───●───●
     \ /
      ●
```

A merge commit can have multiple parents.

---

# 56. What is Fast-Forward Merge?

A **fast-forward merge** happens when the target branch has no new commits since the feature branch was created.

Example:

```text
main
 |
 A
 |
 B
 |
 C
```

If `main` has not changed and the feature branch contains the new commits, Git can simply move the `main` pointer forward.

```text
A → B → C
         ↑
        main
```

No merge commit is required.

---

# 57. What is a Git Object?

Git stores repository information using objects.

Important Git object types include:

* Blob
* Tree
* Commit
* Tag

### Blob

Stores file content.

### Tree

Represents directories and filenames.

### Commit

Stores information about a snapshot and its parents.

### Tag

Stores information about a tagged object.

---

# 58. Git is Distributed

Git is called a **Distributed Version Control System** because every cloned repository contains its own complete Git history.

Concept:

```text
Developer A
    ↓
Full Repository

Developer B
    ↓
Full Repository

Developer C
    ↓
Full Repository
```

Each developer can work independently and later synchronize changes.

---

# 59. GitHub is Not Git

Remember:

```text
Git
 ↓
Software installed on your computer
```

```text
GitHub
 ↓
Online platform
```

Git can work without GitHub.

GitHub commonly uses Git repositories for collaboration.

---

# 60. Basic Git Workflow

The basic workflow is:

```text
Create / Modify Files
        ↓
Working Directory
        ↓
git status
        ↓
git add
        ↓
Staging Area
        ↓
git commit
        ↓
Local Repository
        ↓
git push
        ↓
GitHub
```

---

# 61. Typical GitHub Workflow

A common team workflow is:

```text
Clone Repository
       ↓
Create Branch
       ↓
Modify Files
       ↓
git status
       ↓
git diff
       ↓
git add
       ↓
git commit
       ↓
git push
       ↓
Pull Request
       ↓
Code Review
       ↓
Merge
```

---

# 62. Beginner Git Learning Order

Learn Git in this order:

## Level 1 — Fundamentals

1. Git
2. Version Control
3. GitHub
4. Repository
5. `.git`
6. Local Repository
7. Remote Repository

## Level 2 — Core Git

8. Working Directory
9. Staging Area
10. Untracked Files
11. Tracked Files
12. `git status`
13. `git add`
14. `git commit`
15. `git log`
16. `git diff`

## Level 3 — Branching

17. Branch
18. `main`
19. `HEAD`
20. `git branch`
21. `git switch`
22. Merge
23. Rebase
24. Merge Conflicts

## Level 4 — Remote Git

25. Remote
26. `origin`
27. Clone
28. Fetch
29. Pull
30. Push

## Level 5 — GitHub

31. GitHub Repository
32. Fork
33. Pull Request
34. Code Review
35. Issues
36. GitHub Actions

## Level 6 — Advanced Git

37. Restore
38. Reset
39. Revert
40. Stash
41. Cherry-pick
42. Tags
43. Reflog
44. Detached HEAD
45. Interactive Rebase

---

# 63. Important Commands — Quick Reference

```bash
# Check Git version
git --version

# Configure Git
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Create repository
git init

# Check status
git status

# Stage one file
git add filename

# Stage everything
git add .

# Commit changes
git commit -m "message"

# View history
git log

# View compact history
git log --oneline

# View changes
git diff

# View staged changes
git diff --staged

# View branches
git branch

# Create branch
git branch feature-name

# Create and switch branch
git switch -c feature-name

# Switch branch
git switch main

# Merge branch
git merge feature-name

# Rebase branch
git rebase main

# Clone repository
git clone <repository-url>

# View remotes
git remote -v

# Add remote
git remote add origin <repository-url>

# Fetch changes
git fetch

# Pull changes
git pull origin main

# Push changes
git push origin main

# Temporarily save changes
git stash

# Restore stash
git stash pop

# Restore file
git restore filename

# Unstage file
git restore --staged filename

# Revert commit
git revert <commit-hash>

# View commit
git show <commit-hash>

# View reference history
git reflog

# Create tag
git tag v1.0.0
```

---

# 64. Most Important Commands to Memorize

```text
git init
    → Start Git in a project

git status
    → Check what changed

git add
    → Stage changes

git commit
    → Save a snapshot

git log
    → See commit history

git branch
    → Manage branches

git switch
    → Change branches

git merge
    → Combine branches

git rebase
    → Reapply commits on another base

git clone
    → Copy a remote repository to my computer

git fetch
    → Download remote updates

git pull
    → Get and integrate remote changes

git push
    → Send commits to GitHub

git stash
    → Temporarily save unfinished work

git restore
    → Restore or unstage changes

git revert
    → Undo a commit with a new commit
```

---

# 65. Final Git Mental Model

Remember this flow:

```text
                  GIT
                   |
        ┌──────────┴──────────┐
        ↓                     ↓
Working Directory       Local Repository
        |
     git add
        ↓
Staging Area
        |
    git commit
        ↓
Local Repository
        |
     git push
        ↓
      GitHub
        |
   git pull/fetch
        ↓
Local Repository
```

### The simplest way to remember Git

```text
WORK
 ↓
STATUS
 ↓
ADD
 ↓
COMMIT
 ↓
PUSH
```

> **Git tracks changes, staging selects changes, commits save snapshots, branches isolate work, and GitHub helps us share and collaborate on repositories.**