# Git `.gitignore`

## 1. What is `.gitignore`?

`.gitignore` is a file used by Git to specify files and directories that Git should **not track**.

It is useful for ignoring:

* Temporary files
* Log files
* Build files
* Environment variables
* IDE/editor files
* Operating-system files
* Dependencies
* Secrets and credentials

Example:

```text
node_modules/
.env
*.log
```

---

# 2. Why Use `.gitignore`?

Without `.gitignore`, unnecessary or sensitive files may accidentally be committed to Git.

For example:

```text
.env
passwords.txt
node_modules/
*.log
```

These files usually should not be stored in a Git repository.

---

# 3. Creating a `.gitignore` File

Create the file:

```bash
touch .gitignore
```

Open it:

```bash
code .gitignore
```

Add rules such as:

```gitignore
node_modules/
.env
*.log
```

---

# 4. Basic `.gitignore` Syntax

## Ignore a Specific File

```gitignore
secret.txt
```

This ignores:

```text
secret.txt
```

---

## Ignore All Files With an Extension

```gitignore
*.log
```

This ignores:

```text
app.log
error.log
server.log
```

---

## Ignore a Directory

```gitignore
node_modules/
```

This ignores the entire `node_modules` directory.

---

## Ignore Multiple Files

```gitignore
.env
config.json
secret.txt
```

---

# 5. Ignore Files in a Specific Directory

```gitignore
logs/*.log
```

This ignores `.log` files inside the `logs` directory.

Example:

```text
logs/app.log
logs/error.log
```

---

# 6. Ignore All Files in a Directory

```gitignore
logs/
```

This ignores the entire directory.

---

# 7. Ignore Files Everywhere

Use `*` to match files with a particular extension.

```gitignore
*.tmp
```

This ignores:

```text
file.tmp
test.tmp
backup.tmp
```

---

# 8. Negating a Rule

The `!` symbol can be used to stop ignoring a file.

Example:

```gitignore
*.log
!important.log
```

This means:

* Ignore all `.log` files
* Do not ignore `important.log`

---

# 9. Common `.gitignore` Example

A typical project might use:

```gitignore
# Dependencies
node_modules/

# Environment files
.env
.env.local

# Logs
*.log

# Build output
dist/
build/

# IDE files
.vscode/
.idea/

# Operating system files
.DS_Store
Thumbs.db

# Temporary files
*.tmp
*.temp
```

---

# 10. Comments in `.gitignore`

Lines beginning with `#` are comments.

Example:

```gitignore
# Ignore dependencies
node_modules/

# Ignore environment variables
.env

# Ignore log files
*.log
```

Comments make `.gitignore` easier to understand.

---

# 11. Checking Ignored Files

Use:

```bash
git status
```

Ignored files normally do not appear in the list of untracked files.

To see ignored files:

```bash
git status --ignored
```

---

# 12. Check Why a File Is Ignored

Use:

```bash
git check-ignore -v filename
```

Example:

```bash
git check-ignore -v .env
```

Git can show which `.gitignore` rule caused the file to be ignored.

---

# 13. Important: `.gitignore` Does Not Remove Tracked Files

Suppose you already committed:

```text
secret.txt
```

Then you add:

```gitignore
secret.txt
```

Git will continue tracking the file because it is already tracked.

You must remove it from Git tracking:

```bash
git rm --cached secret.txt
```

Then commit:

```bash
git commit -m "Stop tracking secret file"
```

---

# 14. Remove a Tracked Directory From Git

For example:

```bash
git rm -r --cached node_modules/
```

Then commit:

```bash
git commit -m "Stop tracking node_modules"
```

The directory remains on your computer but is removed from Git tracking.

---

# 15. `.gitignore` vs `git rm --cached`

`.gitignore`:

```text
Prevents untracked files from being added
```

`git rm --cached`:

```text
Removes an already tracked file from Git's index
```

They are often used together.

Example:

```bash
git rm --cached .env
```

Then add:

```gitignore
.env
```

---

# 16. Global `.gitignore`

You can create a global ignore file that applies to all your repositories.

Example:

```bash
git config --global core.excludesfile ~/.gitignore_global
```

Create it:

```bash
touch ~/.gitignore_global
```

Then add common files:

```gitignore
.DS_Store
Thumbs.db
*.swp
```

---

# 17. Local vs Global Ignore

Repository `.gitignore`:

```text
Applies to one repository
```

Global ignore file:

```text
Applies to your repositories
```

Use repository `.gitignore` for project-specific files.

Use global ignore rules for files that should generally never be committed.

---

# 18. Common Files to Ignore

## Node.js

```gitignore
node_modules/
.env
npm-debug.log*
dist/
```

## Python

```gitignore
__pycache__/
*.pyc
.venv/
venv/
.env
```

## Java

```gitignore
target/
*.class
```

## Java/Maven

```gitignore
target/
```

## Java/Gradle

```gitignore
.gradle/
build/
```

---

# 19. Environment Variables

A very important use of `.gitignore` is protecting environment configuration.

Example:

```gitignore
.env
.env.local
```

An `.env` file might contain:

```text
DATABASE_PASSWORD=secret
API_KEY=123456
```

Never commit real passwords, API keys, or other secrets to a public repository.

---

# 20. Example Project

Suppose your project contains:

```text
my-project/
├── src/
├── node_modules/
├── dist/
├── .env
├── debug.log
├── package.json
└── .gitignore
```

Your `.gitignore` could contain:

```gitignore
node_modules/
dist/
.env
*.log
```

Git will track:

```text
src/
package.json
.gitignore
```

Git will ignore:

```text
node_modules/
dist/
.env
debug.log
```

---

# 21. Checking Repository Status

Run:

```bash
git status
```

If everything is configured correctly, ignored files will not appear as normal untracked files.

To display ignored files:

```bash
git status --ignored
```

---

# 22. Useful Commands

Check status:

```bash
git status
```

Show ignored files:

```bash
git status --ignored
```

Check whether a file is ignored:

```bash
git check-ignore filename
```

Show the rule responsible:

```bash
git check-ignore -v filename
```

Remove tracked file but keep it locally:

```bash
git rm --cached filename
```

Remove tracked directory but keep it locally:

```bash
git rm -r --cached directory/
```

---

# 23. Example `.gitignore`

A practical example:

```gitignore
# Dependencies
node_modules/

# Environment variables
.env
.env.local

# Logs
*.log

# Build files
dist/
build/

# Python cache
__pycache__/
*.pyc

# IDE files
.vscode/
.idea/

# OS files
.DS_Store
Thumbs.db

# Temporary files
*.tmp
*.temp
```

---

# 24. Important Interview Question

### What is `.gitignore`?

`.gitignore` is a Git configuration file that tells Git which files and directories should be ignored and not included in version control.

---

# 25. Important Interview Question

### Does `.gitignore` remove already tracked files?

No.

If a file is already tracked, adding it to `.gitignore` does not stop Git from tracking it.

Use:

```bash
git rm --cached filename
```

Then commit the change.

---

# 26. Important Interview Question

### Why should `.env` usually be ignored?

`.env` files commonly contain sensitive information such as:

* API keys
* Database passwords
* Access tokens
* Secret configuration

Therefore, they should generally not be committed to a public repository.

---

# 27. Quick Reference

| Task                    | Command                                                     |
| ----------------------- | ----------------------------------------------------------- |
| Create `.gitignore`     | `touch .gitignore`                                          |
| Check status            | `git status`                                                |
| Show ignored files      | `git status --ignored`                                      |
| Check ignored file      | `git check-ignore filename`                                 |
| Show ignore rule        | `git check-ignore -v filename`                              |
| Stop tracking file      | `git rm --cached filename`                                  |
| Stop tracking directory | `git rm -r --cached directory/`                             |
| Global ignore file      | `git config --global core.excludesfile ~/.gitignore_global` |

---

# 28. Key Takeaways

* `.gitignore` tells Git which files to ignore.
* Use it for temporary files, dependencies, build output, logs, and secrets.
* `.gitignore` does not remove files that are already tracked.
* Use `git rm --cached` to stop tracking an already committed file.
* `git status --ignored` shows ignored files.
* `git check-ignore -v` helps identify why a file is ignored.
* Use global ignore rules for files that should be ignored across repositories.
* Never commit passwords, API keys, or other sensitive credentials.

---

# 29. Simple Workflow

```bash
touch .gitignore
```

Add:

```gitignore
.env
node_modules/
*.log
```

Then:

```bash
git add .gitignore
git commit -m "Add gitignore rules"
git push origin main
```

Check:

```bash
git status
```

Your repository should now have appropriate files excluded from Git tracking.
