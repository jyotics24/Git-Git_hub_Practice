# Git Hooks

## 1. What Are Git Hooks?

Git hooks are scripts that Git automatically executes when certain Git events occur.

They can be used to:

* Validate code
* Run tests
* Check formatting
* Prevent bad commits
* Automate tasks
* Enforce project rules
* Run checks before pushing code

Git hooks are useful for automating repetitive checks during development.

---

# 2. How Git Hooks Work

Git performs different operations such as:

```text
git commit
git push
git merge
git rebase
```

Certain events can trigger hooks.

For example:

```text
git commit
    ↓
pre-commit hook
    ↓
checks/tests
    ↓
commit created
```

---

# 3. Where Git Hooks Are Stored

Git hooks are stored inside:

```text
.git/hooks/
```

Check them with:

```bash
ls .git/hooks
```

You may see files such as:

```text
applypatch-msg.sample
commit-msg.sample
fsmonitor-watchman.sample
post-update.sample
pre-applypatch.sample
pre-commit.sample
pre-merge-commit.sample
pre-push.sample
pre-rebase.sample
pre-receive.sample
prepare-commit-msg.sample
push-to-checkout.sample
update.sample
```

The `.sample` files are examples.

---

# 4. Git Hook Naming

A hook becomes active when the `.sample` extension is removed.

For example:

```text
pre-commit.sample
```

becomes:

```text
pre-commit
```

The active hook must be executable.

---

# 5. Creating a Pre-Commit Hook

Navigate to the hooks directory:

```bash
cd .git/hooks
```

Create the hook:

```bash
touch pre-commit
```

Open it:

```bash
code pre-commit
```

Example:

```bash
#!/bin/sh

echo "Running pre-commit checks..."

echo "Pre-commit checks passed!"
```

---

# 6. What Is `pre-commit`?

The `pre-commit` hook runs before Git creates a commit.

Workflow:

```text
git add
   ↓
git commit
   ↓
pre-commit hook
   ↓
checks
   ↓
commit
```

If the hook exits with an error, Git can stop the commit.

---

# 7. Example Pre-Commit Hook

Example:

```bash
#!/bin/sh

echo "Running tests..."

if ! npm test; then
    echo "Tests failed. Commit stopped."
    exit 1
fi

echo "Tests passed."
exit 0
```

This prevents the commit when the tests fail.

---

# 8. Exit Codes

Shell scripts use exit codes to indicate success or failure.

Successful:

```bash
exit 0
```

Failure:

```bash
exit 1
```

For example:

```bash
#!/bin/sh

echo "Checking code..."

if [ -f "error.txt" ]; then
    echo "Error found!"
    exit 1
fi

echo "Everything looks good."
exit 0
```

---

# 9. Commit Message Hook

Another useful hook is:

```text
commit-msg
```

It runs after the commit message is entered but before the commit is completed.

Example:

```bash
#!/bin/sh

commit_message=$(cat "$1")

if [ -z "$commit_message" ]; then
    echo "Commit message cannot be empty."
    exit 1
fi

exit 0
```

---

# 10. Commit Message Validation

You can enforce a commit-message format.

Example:

```text
feat: add login page
fix: correct login validation
docs: update Git notes
```

A `commit-msg` hook can check whether the message follows a required format.

---

# 11. Pre-Push Hook

The `pre-push` hook runs before Git pushes commits to a remote repository.

Workflow:

```text
git push
   ↓
pre-push hook
   ↓
run tests
   ↓
push to GitHub
```

Example:

```bash
#!/bin/sh

echo "Running tests before push..."

npm test

if [ $? -ne 0 ]; then
    echo "Tests failed. Push cancelled."
    exit 1
fi

echo "Tests passed."
exit 0
```

---

# 12. Common Git Hooks

| Hook                 | When It Runs                              |
| -------------------- | ----------------------------------------- |
| `pre-commit`         | Before a commit is created                |
| `prepare-commit-msg` | Before commit message editor starts       |
| `commit-msg`         | After commit message is entered           |
| `post-commit`        | After commit is created                   |
| `pre-rebase`         | Before rebase                             |
| `pre-push`           | Before push                               |
| `post-merge`         | After merge                               |
| `post-checkout`      | After checkout                            |
| `pre-receive`        | Before receiving pushed objects on server |
| `update`             | Before updating a server-side ref         |
| `post-receive`       | After receiving pushed objects            |

---

# 13. Client-Side Hooks

Client-side hooks run on the developer's local machine.

Examples:

```text
pre-commit
commit-msg
pre-push
pre-rebase
post-commit
```

They are useful for:

* Code formatting
* Testing
* Validation
* Commit message rules

---

# 14. Server-Side Hooks

Server-side hooks run on the Git server.

Examples:

```text
pre-receive
update
post-receive
```

They can enforce rules before accepting changes.

For example:

```text
Developer
    ↓
git push
    ↓
Git server
    ↓
pre-receive
    ↓
validation
    ↓
accept/reject push
```

---

# 15. Hook to Prevent Direct Main Branch Commits

A hook can be used to enforce workflow rules.

For example, a local `pre-commit` hook could check the current branch:

```bash
#!/bin/sh

branch=$(git branch --show-current)

if [ "$branch" = "main" ]; then
    echo "Direct commits to main are not allowed."
    exit 1
fi

exit 0
```

This prevents local commits directly on `main`.

---

# 16. Hook to Check for Debug Statements

For example:

```bash
#!/bin/sh

if git diff --cached | grep -q "console.log"; then
    echo "Remove console.log before committing."
    exit 1
fi

exit 0
```

This can prevent accidental debug statements from being committed.

---

# 17. Making a Hook Executable

On Linux or Git Bash, you can use:

```bash
chmod +x .git/hooks/pre-commit
```

Check permissions:

```bash
ls -l .git/hooks/pre-commit
```

---

# 18. Testing a Hook

After creating a hook:

```bash
git add .
git commit -m "Test Git hook"
```

Git should execute the hook automatically.

You might see:

```text
Running pre-commit checks...
Pre-commit checks passed!
```

---

# 19. Bypassing Hooks

Git provides an option to bypass hooks:

```bash
git commit --no-verify
```

For push:

```bash
git push --no-verify
```

This should be used carefully because it skips important checks.

---

# 20. Removing a Hook

To remove a hook:

```bash
rm .git/hooks/pre-commit
```

Or delete it manually from:

```text
.git/hooks/
```

---

# 21. Important Limitation of `.git/hooks`

The `.git/hooks` directory is inside the local `.git` directory.

It is not normally committed to the repository.

Therefore, if another developer clones the repository, your local hooks will not automatically be installed.

For example:

```text
Developer A
    ↓
.git/hooks/pre-commit
```

Developer B clones:

```text
git clone repository
```

Developer B does not automatically receive Developer A's local hook.

---

# 22. Sharing Git Hooks

For team projects, hooks can be stored in a directory inside the repository.

For example:

```text
project/
├── .githooks/
│   └── pre-commit
├── src/
├── README.md
└── .gitignore
```

Configure Git to use that directory:

```bash
git config core.hooksPath .githooks
```

Now Git looks for hooks inside:

```text
.githooks/
```

instead of:

```text
.git/hooks/
```

---

# 23. Shared Hooks Example

Create the directory:

```bash
mkdir .githooks
```

Create a hook:

```bash
touch .githooks/pre-commit
```

Open it:

```bash
code .githooks/pre-commit
```

Example:

```bash
#!/bin/sh

echo "Running shared project checks..."

exit 0
```

Configure Git:

```bash
git config core.hooksPath .githooks
```

Make it executable:

```bash
chmod +x .githooks/pre-commit
```

---

# 24. Check Hooks Path

Run:

```bash
git config core.hooksPath
```

Expected:

```text
.githooks
```

If nothing is returned, Git is using the default:

```text
.git/hooks/
```

---

# 25. Unset Custom Hooks Path

To return to the default hooks directory:

```bash
git config --unset core.hooksPath
```

Git will again use:

```text
.git/hooks/
```

---

# 26. Git Hooks and CI/CD

Git hooks and CI/CD are different.

Local hook:

```text
Developer machine
       ↓
pre-commit
       ↓
checks
```

CI/CD:

```text
Developer
    ↓
git push
    ↓
GitHub
    ↓
GitHub Actions
    ↓
tests/build/deployment
```

Local hooks provide fast feedback.

CI/CD provides centralized verification.

---

# 27. Git Hooks vs GitHub Actions

### Git Hooks

Run locally or on a Git server.

Examples:

```text
pre-commit
commit-msg
pre-push
```

### GitHub Actions

Run on GitHub infrastructure.

Examples:

```text
Run tests
Build application
Deploy application
Check code quality
```

Both can be used together.

---

# 28. Example Development Workflow

A developer makes a change:

```text
Edit code
   ↓
git add
   ↓
git commit
   ↓
pre-commit
   ↓
run tests
   ↓
commit created
   ↓
git push
   ↓
pre-push
   ↓
run additional checks
   ↓
GitHub
   ↓
CI/CD
```

---

# 29. Useful Commands

List hooks:

```bash
ls .git/hooks
```

Create hook:

```bash
touch .git/hooks/pre-commit
```

Make executable:

```bash
chmod +x .git/hooks/pre-commit
```

Configure shared hooks:

```bash
git config core.hooksPath .githooks
```

Check hooks path:

```bash
git config core.hooksPath
```

Remove custom hooks path:

```bash
git config --unset core.hooksPath
```

Bypass commit hooks:

```bash
git commit --no-verify
```

Bypass push hooks:

```bash
git push --no-verify
```

---

# 30. Interview Questions

## What are Git hooks?

Git hooks are scripts that automatically run when specific Git events occur.

---

## What is a pre-commit hook?

A `pre-commit` hook runs before Git creates a commit.

It can be used to:

* Run tests
* Check formatting
* Validate code
* Prevent invalid commits

---

## What is a pre-push hook?

A `pre-push` hook runs before Git sends commits to a remote repository.

It can be used to run tests or other validation before pushing.

---

## Can Git hooks be shared through Git?

Hooks inside `.git/hooks` are local and are not normally committed.

A shared hooks directory such as:

```text
.githooks/
```

can be committed and configured using:

```bash
git config core.hooksPath .githooks
```

---

## Can Git hooks be bypassed?

Yes.

For commits:

```bash
git commit --no-verify
```

For pushes:

```bash
git push --no-verify
```

Use this carefully.

---

# 31. Quick Reference

| Task                   | Command                               |
| ---------------------- | ------------------------------------- |
| List hooks             | `ls .git/hooks`                       |
| Create pre-commit      | `touch .git/hooks/pre-commit`         |
| Make executable        | `chmod +x .git/hooks/pre-commit`      |
| Shared hooks directory | `mkdir .githooks`                     |
| Configure hooks path   | `git config core.hooksPath .githooks` |
| Check hooks path       | `git config core.hooksPath`           |
| Remove custom path     | `git config --unset core.hooksPath`   |
| Bypass commit hook     | `git commit --no-verify`              |
| Bypass push hook       | `git push --no-verify`                |

---

# 32. Key Takeaways

* Git hooks are scripts triggered by Git events.
* `pre-commit` runs before a commit.
* `commit-msg` validates commit messages.
* `pre-push` runs before pushing.
* Hooks can automate testing and validation.
* Hooks can prevent bad commits.
* `.git/hooks/` contains local hooks.
* `.githooks/` can be used for shared project hooks.
* `core.hooksPath` tells Git where to find hooks.
* `--no-verify` can bypass certain client-side hooks.
* Git hooks and CI/CD can work together.

---

# 33. Simple Example

A basic `pre-commit` hook:

```bash
#!/bin/sh

echo "Running pre-commit check..."

if git diff --cached | grep -q "console.log"; then
    echo "Remove console.log before committing."
    exit 1
fi

echo "Check passed."
exit 0
```

This demonstrates how Git hooks can automatically check staged changes before creating a commit.
