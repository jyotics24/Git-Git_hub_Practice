    # Git Remote and GitHub

Git allows us to work with remote repositories such as GitHub.

A **remote repository** is a repository stored on a server such as GitHub.

A **local repository** is the Git repository on our computer.

---

# 1. Local Repository vs Remote Repository

### Local Repository

The repository on your computer.

Example:

```bash
git status
git log
git branch
```

### Remote Repository

The repository hosted on GitHub.

Example:

```text
GitHub
   |
   └── jyotics24/Git-Git_hub_Practice
```

---

# 2. What is `origin`?

`origin` is the default name Git gives to the remote repository when we clone a repository or add a remote.

Example:

```bash
git remote -v
```

Output may look like:

```text
origin  https://github.com/username/repository.git (fetch)
origin  https://github.com/username/repository.git (push)
```

### Remember

> `origin` → Name of the remote repository.

---

# 3. Check Remote Repositories

Use:

```bash
git remote
```

This displays the names of configured remotes.

Example:

```text
origin
```

To see the remote URLs:

```bash
git remote -v
```

Example:

```text
origin  https://github.com/username/repository.git (fetch)
origin  https://github.com/username/repository.git (push)
```

---

# 4. Add a Remote

A remote can be added using:

```bash
git remote add origin https://github.com/username/repository.git
```

Now check:

```bash
git remote -v
```

---

# 5. Change a Remote URL

Use:

```bash
git remote set-url origin https://github.com/username/new-repository.git
```

Then verify:

```bash
git remote -v
```

---

# 6. Remove a Remote

Use:

```bash
git remote remove origin
```

This removes the remote configuration from your local repository.

It does **not** delete the GitHub repository.

---

# 7. Push

`git push` sends local commits to a remote repository.

Example:

```bash
git push origin main
```

This means:

```text
local main
     |
     | push
     v
origin/main
```

---

# 8. First Push of a New Branch

When pushing a new branch for the first time:

```bash
git push -u origin feature-login
```

The `-u` option sets the upstream branch.

After that, you can usually use:

```bash
git push
```

---

# 9. What is Upstream?

An upstream branch connects your local branch with a remote branch.

Example:

```text
local branch
feature-login
      |
      v
origin/feature-login
```

When you run:

```bash
git push -u origin feature-login
```

Git remembers the relationship.

Then:

```bash
git push
```

is enough for future pushes.

---

# 10. Fetch

`git fetch` downloads information about changes from the remote repository.

Example:

```bash
git fetch origin
```

Important:

> `git fetch` downloads remote changes but does not automatically change your working files.

Example:

```text
GitHub
  |
  | fetch
  v
Local repository
```

---

# 11. Fetch All Remotes

Use:

```bash
git fetch --all
```

This fetches information from all configured remotes.

---

# 12. Pull

`git pull` gets changes from the remote repository and integrates them into the current local branch.

Example:

```bash
git pull origin main
```

Conceptually:

```text
git pull
   =
git fetch
   +
git merge
```

Depending on configuration and options, Git may also use rebase instead of merge.

---

# 13. Fetch vs Pull

| Command     | Purpose                               |
| ----------- | ------------------------------------- |
| `git fetch` | Download remote changes               |
| `git pull`  | Download and integrate remote changes |

### Simple explanation

```text
fetch → Look at remote changes
pull  → Bring remote changes into your branch
```

---

# 14. Push vs Pull

| Command    | Direction      |
| ---------- | -------------- |
| `git push` | Local → Remote |
| `git pull` | Remote → Local |

Example:

```text
git push

Computer
   |
   v
 GitHub
```

```text
git pull

GitHub
   |
   v
Computer
```

---

# 15. Remote Branches

To see local branches:

```bash
git branch
```

To see remote branches:

```bash
git branch -r
```

To see both local and remote branches:

```bash
git branch -a
```

Example:

```text
* main
  feature-login
  remotes/origin/main
  remotes/origin/feature-login
```

---

# 16. Understanding `origin/main`

Consider:

```text
origin/main
```

It means:

```text
origin → remote repository
main   → branch
```

So:

```text
origin/main
```

means the remote-tracking branch for `main` on the `origin` remote.

---

# 17. Clone

`git clone` creates a local copy of a remote repository.

Example:

```bash
git clone https://github.com/username/repository.git
```

Git will:

1. Download the repository.
2. Create a local directory.
3. Download the commit history.
4. Configure the remote as `origin`.

After cloning:

```bash
cd repository
```

Check:

```bash
git remote -v
```

---

# 18. Clone a Repository into a Specific Folder

You can specify the local folder name:

```bash
git clone https://github.com/username/repository.git my-project
```

The repository will be cloned into:

```text
my-project/
```

---

# 19. GitHub Workflow

A common GitHub workflow is:

```text
Clone repository
      |
      v
Create branch
      |
      v
Make changes
      |
      v
git add
      |
      v
git commit
      |
      v
git push
      |
      v
Create Pull Request
      |
      v
Review
      |
      v
Merge into main
      |
      v
git switch main
      |
      v
git pull
```

---

# 20. Check Remote Information

Use:

```bash
git remote -v
```

For more detailed information:

```bash
git remote show origin
```

This can show information such as:

* Remote URL
* Remote branches
* Tracking information
* Local branches connected to remote branches

---

# 21. Rename a Remote

To rename a remote:

```bash
git remote rename origin upstream
```

Check:

```bash
git remote -v
```

Now the remote is named:

```text
upstream
```

---

# 22. Delete a Remote Branch

To delete a branch from GitHub:

```bash
git push origin --delete feature-login
```

Example:

```text
local branch
      |
      X

remote branch
      |
      X
```

This deletes the branch from the remote repository.

---

# 23. Local Branch vs Remote Branch

A local branch:

```text
main
```

belongs to your local repository.

A remote-tracking branch:

```text
origin/main
```

represents the state of the remote branch known to your local Git repository.

They are related but are not the same branch.

---

# 24. Check Branch Tracking

Use:

```bash
git branch -vv
```

Example:

```text
* main  abc1234 [origin/main] Latest commit
```

This tells us that local `main` is tracking `origin/main`.

---

# 25. Set Upstream Manually

You can connect a local branch to a remote branch with:

```bash
git branch --set-upstream-to=origin/main main
```

After that:

```bash
git pull
```

and:

```bash
git push
```

can be used without specifying the remote and branch.

---

# 26. Git Remote Workflow Example

Start with:

```bash
git remote -v
```

Create a branch:

```bash
git switch -c feature-login
```

Make changes.

Check:

```bash
git status
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

After the Pull Request is merged:

```bash
git switch main
```

Update local main:

```bash
git pull origin main
```

Delete the local branch:

```bash
git branch -d feature-login
```

Delete the remote branch if necessary:

```bash
git push origin --delete feature-login
```

---

# 27. Important Commands

| Command                    | Purpose                        |
| -------------------------- | ------------------------------ |
| `git remote`               | List remotes                   |
| `git remote -v`            | Show remote URLs               |
| `git remote show origin`   | Show remote details            |
| `git remote add`           | Add a remote                   |
| `git remote remove`        | Remove a remote                |
| `git remote set-url`       | Change remote URL              |
| `git fetch`                | Download remote changes        |
| `git fetch --all`          | Fetch all remotes              |
| `git pull`                 | Fetch and integrate changes    |
| `git push`                 | Upload commits                 |
| `git branch -r`            | List remote branches           |
| `git branch -a`            | List local and remote branches |
| `git branch -vv`           | Show tracking information      |
| `git clone`                | Copy a remote repository       |
| `git push origin --delete` | Delete remote branch           |

---

# 28. Interview Questions

### What is a remote repository?

> A remote repository is a Git repository hosted on another computer or service such as GitHub.

### What is `origin`?

> `origin` is the default name commonly assigned to the remote repository.

### What is `git push`?

> `git push` uploads local commits to a remote repository.

### What is `git pull`?

> `git pull` downloads changes from a remote repository and integrates them into the current branch.

### What is `git fetch`?

> `git fetch` downloads information about remote changes without automatically integrating those changes into the current branch.

### What is the difference between fetch and pull?

> `git fetch` downloads remote changes without integrating them, while `git pull` downloads and integrates them.

### What is `origin/main`?

> `origin/main` is a remote-tracking branch representing the `main` branch on the `origin` remote.

### What does `git push -u` do?

> It pushes the branch and establishes an upstream relationship between the local branch and its remote branch.

### What does `git clone` do?

> `git clone` creates a local copy of a remote Git repository, including its history and remote configuration.

---

# 29. Remember

```text
git clone
    ↓
Get repository

git fetch
    ↓
Download remote information

git pull
    ↓
Fetch + integrate

git push
    ↓
Upload commits

origin
    ↓
Remote repository name

origin/main
    ↓
Remote-tracking main branch
```

---

# 30. Practical Exercise

Practice the following workflow.

### Step 1 — Check the remote

```bash
git remote -v
```

### Step 2 — Check branches

```bash
git branch -a
```

### Step 3 — Fetch from GitHub

```bash
git fetch origin
```

### Step 4 — Check status

```bash
git status
```

### Step 5 — Create a practice branch

```bash
git switch -c remote-practice
```

### Step 6 — Create a file

```bash
touch remote-practice.txt
```

### Step 7 — Add content

```bash
echo "Remote practice" > remote-practice.txt
```

### Step 8 — Stage

```bash
git add remote-practice.txt
```

### Step 9 — Commit

```bash
git commit -m "Add remote practice"
```

### Step 10 — Push the branch

```bash
git push -u origin remote-practice
```

### Step 11 — Check branches

```bash
git branch -a
```

You should see something similar to:

```text
* remote-practice
  main
  remotes/origin/main
  remotes/origin/remote-practice
```

### Step 12 — Switch back to main

```bash
git switch main
```

### Step 13 — Delete the local practice branch

```bash
git branch -d remote-practice
```

### Step 14 — Delete the remote practice branch

```bash
git push origin --delete remote-practice
```

### Step 15 — Fetch again

```bash
git fetch --prune
```

### Step 16 — Verify

```bash
git branch -a
```

Finally:

```bash
git status
```

Expected:

```text
On branch main
nothing to commit, working tree clean
```

---

# Summary

The most important remote commands are:

```bash
git remote -v
git fetch
git pull
git push
git clone
git branch -r
git branch -a
git branch -vv
```

Remember:

```text
Local → GitHub
       git push

GitHub → Local
       git pull

GitHub → Local information
       git fetch
```
