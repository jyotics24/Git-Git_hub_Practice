# Git Config

Git configuration allows us to customize Git's behavior and define settings such as username, email, default branch, editor, aliases, line-ending behavior, and other preferences.

Git configuration can be applied at different levels:

* System
* Global
* Local

---

## 1. What is Git Config?

Git Config is used to view and change Git configuration settings.

Basic command:

```bash
git config
```

Git stores configuration values as key-value pairs.

Example:

```bash
git config user.name "Jyoti"
```

---

## 2. Configuration Levels

Git has three main configuration levels.

### System

Applies to every user on the computer.

```bash
git config --system
```

Example:

```bash
git config --system user.name "User"
```

Usually requires administrator permissions.

---

### Global

Applies to the current user across all repositories.

```bash
git config --global
```

Example:

```bash
git config --global user.name "Jyoti"
git config --global user.email "jyoti@example.com"
```

This is the most commonly used level for personal Git settings.

---

### Local

Applies only to the current repository.

```bash
git config --local
```

Example:

```bash
git config --local user.name "Project User"
git config --local user.email "project@example.com"
```

Local configuration overrides global configuration for that repository.

---

## 3. Set Username

Set your Git username globally:

```bash
git config --global user.name "Jyoti"
```

Check it:

```bash
git config --global user.name
```

Example output:

```text
Jyoti
```

---

## 4. Set Email

Set your Git email globally:

```bash
git config --global user.email "jyoti@example.com"
```

Check it:

```bash
git config --global user.email
```

Example output:

```text
jyoti@example.com
```

The email configured in Git is associated with the author information stored in commits.

---

## 5. View All Configuration

To see all Git configuration settings:

```bash
git config --list
```

Example:

```text
user.name=Jyoti
user.email=jyoti@example.com
core.repositoryformatversion=0
core.filemode=false
core.bare=false
```

---

## 6. View Global Configuration

To view only global settings:

```bash
git config --global --list
```

Short form:

```bash
git config --global -l
```

---

## 7. View Local Configuration

To view configuration for the current repository:

```bash
git config --local --list
```

Short form:

```bash
git config --local -l
```

---

## 8. View System Configuration

To view system-level configuration:

```bash
git config --system --list
```

Administrator permissions may be required.

---

## 9. Get a Specific Configuration Value

You can retrieve a specific setting.

Example:

```bash
git config --get user.name
```

Another example:

```bash
git config --get user.email
```

---

## 10. Check Where a Setting Comes From

You can find which configuration file defines a setting:

```bash
git config --show-origin --list
```

Example:

```text
file:C:/Users/Jyoti/.gitconfig user.name=Jyoti
file:.git/config core.repositoryformatversion=0
```

This is useful when a setting is behaving unexpectedly.

---

## 11. Configuration Files

Git configuration can be stored in different files.

### System configuration

Applies to the entire system.

Typical location:

```text
/etc/gitconfig
```

On Windows, the exact location can vary depending on how Git was installed.

---

### Global configuration

Applies to the current user.

Typical location:

```text
~/.gitconfig
```

or:

```text
~/.config/git/config
```

---

### Local configuration

Stored inside the repository:

```text
.git/config
```

Local configuration applies only to that repository.

---

## 12. Configuration Priority

When the same setting exists at multiple levels, the more specific configuration takes precedence.

General priority:

```text
System
   ↓
Global
   ↓
Local
```

Local settings override global settings.

Example:

Global:

```bash
git config --global user.name "Jyoti"
```

Repository-specific:

```bash
git config --local user.name "Project User"
```

Inside that repository, Git uses:

```text
Project User
```

---

## 13. Set Default Branch Name

When creating a new repository with:

```bash
git init
```

Git can be configured to use `main` as the initial branch.

Command:

```bash
git config --global init.defaultBranch main
```

Check it:

```bash
git config --global init.defaultBranch
```

---

## 14. Why Use main?

Many modern repositories use:

```text
main
```

as the default branch.

Using a consistent default branch name makes workflows easier to understand.

Example:

```bash
git init
```

Then:

```bash
git branch
```

may show:

```text
* main
```

---

## 15. Git Editor

Git sometimes opens an editor when creating or editing commits.

You can configure the default editor.

For Visual Studio Code:

```bash
git config --global core.editor "code --wait"
```

For Vim:

```bash
git config --global core.editor "vim"
```

For Nano:

```bash
git config --global core.editor "nano"
```

---

## 16. Git Alias

Aliases allow you to create shortcuts for frequently used commands.

Example:

```bash
git config --global alias.st status
```

Now instead of:

```bash
git status
```

you can use:

```bash
git st
```

---

## 17. Useful Git Aliases

### Status

```bash
git config --global alias.st status
```

Usage:

```bash
git st
```

---

### Checkout

```bash
git config --global alias.co checkout
```

Usage:

```bash
git co main
```

---

### Branch

```bash
git config --global alias.br branch
```

Usage:

```bash
git br
```

---

### Commit

```bash
git config --global alias.ci commit
```

Usage:

```bash
git ci -m "Update documentation"
```

---

### Short Log

```bash
git config --global alias.lg "log --oneline --graph --decorate --all"
```

Usage:

```bash
git lg
```

This produces a useful graphical commit history.

---

## 18. Create a Custom Log Alias

A popular alias is:

```bash
git config --global alias.graph "log --oneline --graph --decorate --all"
```

Then:

```bash
git graph
```

Example:

```text
* 123abcd Add feature
* 456efgh Update README
* 789ijkl Initial commit
```

---

## 19. Remove an Alias

To remove an alias:

```bash
git config --global --unset alias.st
```

Check:

```bash
git config --global --list
```

---

## 20. List Git Aliases

You can search for aliases:

```bash
git config --global --get-regexp alias
```

Example:

```text
alias.st status
alias.co checkout
alias.br branch
alias.ci commit
alias.lg log --oneline --graph --decorate --all
```

---

## 21. Core Autocrlf

Git handles line endings differently on different operating systems.

Windows commonly uses:

```text
CRLF
```

Linux and macOS commonly use:

```text
LF
```

Git can automatically manage line endings using:

```bash
core.autocrlf
```

---

## 22. Windows autocrlf

A common Windows configuration is:

```bash
git config --global core.autocrlf true
```

This converts LF to CRLF in the working directory and converts CRLF to LF when committing.

Check:

```bash
git config --global core.autocrlf
```

---

## 23. Linux and macOS autocrlf

A common configuration is:

```bash
git config --global core.autocrlf input
```

This converts CRLF to LF when committing but does not modify LF files in the working directory.

---

## 24. Disable autocrlf

You can disable automatic conversion:

```bash
git config --global core.autocrlf false
```

The correct setting depends on your operating system and project requirements.

---

## 25. Git Safe Directory

Git may report a repository as unsafe when ownership or permissions appear unusual.

You can explicitly mark a directory as safe:

```bash
git config --global --add safe.directory "/path/to/repository"
```

Use this only for repositories you trust.

---

## 26. Credential Helper

Git can use credential helpers to remember authentication credentials.

View the current setting:

```bash
git config --global credential.helper
```

Git Credential Manager is commonly used on Windows installations of Git.

Configuration can vary depending on the operating system and Git installation.

---

## 27. Git Configuration for GitHub

For GitHub repositories, configure your Git identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Then verify:

```bash
git config --global user.name
git config --global user.email
```

Remember that Git identity configuration and GitHub authentication are separate concepts.

---

## 28. Git Identity vs GitHub Authentication

These two concepts are different.

### Git Identity

Controls the author information stored in commits:

```bash
git config --global user.name
git config --global user.email
```

### GitHub Authentication

Controls whether you are allowed to access a GitHub repository.

Authentication may use methods such as:

* GitHub CLI authentication
* HTTPS credentials
* SSH keys
* Credential managers

Changing `user.name` does not automatically authenticate you to GitHub.

---

## 29. Change Configuration

To change a value:

```bash
git config --global user.name "New Name"
```

For email:

```bash
git config --global user.email "new@example.com"
```

The new setting replaces the previous value at that configuration level.

---

## 30. Remove a Configuration Setting

Example:

```bash
git config --global --unset user.name
```

Remove email:

```bash
git config --global --unset user.email
```

Then verify:

```bash
git config --global --list
```

---

## 31. Edit the Global Configuration File

You can open the global Git configuration file:

```bash
git config --global --edit
```

Git opens the configuration file in your configured editor.

Example:

```text
[user]
    name = Jyoti
    email = jyoti@example.com

[init]
    defaultBranch = main
```

---

## 32. Edit Local Repository Configuration

To edit the configuration for the current repository:

```bash
git config --local --edit
```

The configuration is stored in:

```text
.git/config
```

---

## 33. Example Configuration

A Git configuration may look like:

```ini
[user]
    name = Jyoti
    email = jyoti@example.com

[init]
    defaultBranch = main

[core]
    editor = code --wait
    autocrlf = true

[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    lg = log --oneline --graph --decorate --all
```

---

## 34. Check a Configuration Value

Use:

```bash
git config --get user.name
```

Example:

```text
Jyoti
```

For the default branch:

```bash
git config --get init.defaultBranch
```

For the editor:

```bash
git config --get core.editor
```

---

## 35. Git Config Commands Cheat Sheet

| Command                                         | Purpose                       |
| ----------------------------------------------- | ----------------------------- |
| `git config --list`                             | Show configuration            |
| `git config --global --list`                    | Show global configuration     |
| `git config --local --list`                     | Show repository configuration |
| `git config --system --list`                    | Show system configuration     |
| `git config --get user.name`                    | Get username                  |
| `git config --get user.email`                   | Get email                     |
| `git config --global user.name "Name"`          | Set global username           |
| `git config --global user.email "email"`        | Set global email              |
| `git config --global init.defaultBranch main`   | Set default branch            |
| `git config --global core.editor "code --wait"` | Set editor                    |
| `git config --global alias.st status`           | Create alias                  |
| `git config --global --unset alias.st`          | Remove alias                  |
| `git config --global --edit`                    | Edit global config            |
| `git config --local --edit`                     | Edit local config             |
| `git config --show-origin --list`               | Show config source            |

---

## 36. Practical Setup

A basic Git setup can be:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
git config --global init.defaultBranch main
git config --global core.editor "code --wait"
```

Then verify:

```bash
git config --global --list
```

---

## 37. Recommended Aliases

You can configure:

```bash
git config --global alias.st status
git config --global alias.br branch
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --decorate --all"
```

Then:

```bash
git st
git br
git co main
git ci -m "Update file"
git lg
```

---

## 38. Common Mistakes

### Mistake 1: Using the wrong option

Incorrect:

```bash
git config user.name "Jyoti"
```

This modifies the configuration at the default level, which is normally the local repository when inside a repository.

For a global setting, use:

```bash
git config --global user.name "Jyoti"
```

---

### Mistake 2: Wrong email

If your commits are not associated with the expected identity on GitHub, verify:

```bash
git config --global user.email
```

---

### Mistake 3: Confusing Git identity with authentication

This:

```bash
git config --global user.name "Jyoti"
```

does not log you into GitHub.

---

### Mistake 4: Forgetting configuration priority

A local setting can override a global setting.

Check the source:

```bash
git config --show-origin --list
```

---

## 39. Useful Troubleshooting

If you want to know which username Git is using:

```bash
git config user.name
```

If you want to know which email Git is using:

```bash
git config user.email
```

If you want to see everything:

```bash
git config --list
```

If you need to know where settings came from:

```bash
git config --show-origin --list
```

---

## 40. Interview Questions

### What is Git config?

> Git config is used to configure Git settings such as username, email, editor, aliases, default branch, and other Git behavior.

### What are the three Git configuration levels?

> System, global, and local.

### What is global configuration?

> Global configuration applies to the current user across all repositories.

### What is local configuration?

> Local configuration applies only to the current repository.

### Which configuration has higher priority: global or local?

> Local configuration has higher priority than global configuration.

### How do you set your Git username?

```bash
git config --global user.name "Your Name"
```

### How do you set your Git email?

```bash
git config --global user.email "your-email@example.com"
```

### How do you see all Git configuration?

```bash
git config --list
```

### How do you see where a configuration comes from?

```bash
git config --show-origin --list
```

### How do you set the default branch to main?

```bash
git config --global init.defaultBranch main
```

### What is a Git alias?

> A Git alias is a custom shortcut for a Git command.

Example:

```bash
git config --global alias.st status
```

Then:

```bash
git st
```

### What is `core.autocrlf`?

> `core.autocrlf` controls automatic conversion between LF and CRLF line endings.

### Does `git config user.name` authenticate you to GitHub?

> No. Git identity configuration controls commit author information, while GitHub authentication controls repository access.

---

## 41. Important Commands to Remember

```bash
git config --list
```

```bash
git config --global --list
```

```bash
git config --get user.name
```

```bash
git config --get user.email
```

```bash
git config --global user.name "Your Name"
```

```bash
git config --global user.email "your-email@example.com"
```

```bash
git config --global init.defaultBranch main
```

```bash
git config --global core.editor "code --wait"
```

```bash
git config --global alias.st status
```

```bash
git config --show-origin --list
```

---

## 42. Quick Summary

```text
Git Config
   |
   +-- System
   |
   +-- Global
   |
   +-- Local
```

Important settings:

```text
user.name
user.email
init.defaultBranch
core.editor
core.autocrlf
alias.*
```

Most important commands:

```bash
git config --list
git config --global --list
git config --get user.name
git config --get user.email
git config --global user.name "Name"
git config --global user.email "Email"
git config --global init.defaultBranch main
```

Git configuration helps make Git consistent, efficient, and easier to use across projects.
