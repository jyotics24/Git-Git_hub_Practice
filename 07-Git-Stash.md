# Git Stash

Git stash is used to temporarily save changes that are not ready to be committed.

It is useful when you are working on something and suddenly need to switch branches without committing incomplete work.

---

## 1. What is Git Stash?

`git stash` temporarily stores your modified tracked files and returns your working directory to a clean state.

Example:

```bash
git stash
```

This allows you to switch branches or perform other Git operations without committing unfinished changes.

---

## 2. Check Git Status Before Stashing

First check your current changes:

```bash
git status
```

Example:

```text
On branch main
Changes not staged for commit:
  modified: README.md
```

---

## 3. Stash Changes

Use:

```bash
git stash
```

Example:

```bash
git stash
```

Git temporarily saves your changes.

After stashing:

```bash
git status
```

You should see:

```text
On branch main
nothing to commit, working tree clean
```

---

## 4. Stash with a Message

You can give your stash a meaningful name:

```bash
git stash push -m "Update README"
```

Example:

```bash
git stash push -m "Work on login feature"
```

This makes it easier to identify the stash later.

---

## 5. View Stashes

To see all saved stashes:

```bash
git stash list
```

Example:

```text
stash@{0}: On main: Work on login feature
stash@{1}: On main: Update documentation
```

The newest stash is usually `stash@{0}`.

---

## 6. Apply a Stash

To restore a stash without deleting it:

```bash
git stash apply
```

This applies the most recent stash.

You can also apply a specific stash:

```bash
git stash apply stash@{1}
```

After applying the stash, check:

```bash
git status
```

Your previous changes should appear again.

---

## 7. Apply and Remove a Stash

Use:

```bash
git stash pop
```

`git stash pop` restores the most recent stash and removes it from the stash list.

Example:

```bash
git stash pop
```

Difference:

```text
git stash apply
```

Restores the changes but keeps the stash.

```text
git stash pop
```

Restores the changes and removes the stash if the operation succeeds.

---

## 8. Remove a Specific Stash

To delete a specific stash:

```bash
git stash drop stash@{0}
```

Example:

```bash
git stash drop stash@{1}
```

Be careful because the deleted stash cannot normally be restored through the normal stash commands.

---

## 9. Delete All Stashes

To remove all saved stashes:

```bash
git stash clear
```

Example:

```bash
git stash clear
```

This permanently removes all stash entries.

Use this command carefully.

---

## 10. Stash Untracked Files

By default, `git stash` does not include untracked files.

Suppose you have:

```text
README.md
new-file.txt
```

and `new-file.txt` is untracked.

Use:

```bash
git stash -u
```

or:

```bash
git stash --include-untracked
```

This stashes both tracked modifications and untracked files.

---

## 11. Stash Everything Including Ignored Files

To stash tracked, untracked, and ignored files:

```bash
git stash -a
```

or:

```bash
git stash --all
```

This is more aggressive than `git stash -u`.

---

## 12. View Stash Details

To see the changes stored in a stash:

```bash
git stash show
```

To see the full diff:

```bash
git stash show -p
```

Example:

```bash
git stash show -p stash@{0}
```

---

## 13. Create a Branch from a Stash

Sometimes your stashed changes belong to a new feature.

You can create a branch directly from a stash:

```bash
git stash branch feature-login stash@{0}
```

Example:

```bash
git stash branch feature-login stash@{0}
```

Git creates the new branch and applies the stash to it.

This is useful when you realize that your unfinished work should actually be developed on a separate branch.

---

## 14. Stash Only Part of Your Changes

You can interactively choose which changes to stash:

```bash
git stash -p
```

or:

```bash
git stash --patch
```

Git will ask which changes you want to stash.

Common options include:

```text
y - stash this change
n - do not stash this change
q - quit
```

This is useful when you have multiple changes but only want to temporarily save some of them.

---

## 15. Stash Workflow

A common workflow looks like this:

```text
Start working
     |
     v
Modify files
     |
     v
git status
     |
     v
Need to switch branches?
     |
     v
git stash
     |
     v
Switch branch
     |
     v
Do other work
     |
     v
Return to original branch
     |
     v
git stash pop
     |
     v
Continue working
```

---

## 16. Practical Example

Suppose you are working on the `main` branch:

```bash
git status
```

You modify `README.md`.

Before committing, you suddenly need to switch branches.

First stash your work:

```bash
git stash push -m "README work"
```

Check your status:

```bash
git status
```

The working tree should now be clean.

Switch branches:

```bash
git switch feature-login
```

Do your work:

```bash
git status
```

Return to `main`:

```bash
git switch main
```

View your stashes:

```bash
git stash list
```

Restore your work:

```bash
git stash pop
```

Now continue working on `README.md`.

---

## 17. Stash vs Commit

`git stash` and `git commit` are different.

### Git Stash

Used for temporarily saving unfinished work.

```bash
git stash
```

The changes are stored locally and are not part of the project history.

### Git Commit

Used for permanently recording a logical change in Git history.

```bash
git add .
git commit -m "Update README"
```

A commit becomes part of the branch history.

---

## 18. Stash vs Branch

A stash is generally temporary.

A branch is used for ongoing development.

Example:

```text
Stash
  |
  +-- Temporarily save unfinished changes


Branch
  |
  +-- Develop a feature independently
```

If you are going to work on something for a while, creating a branch is usually better than repeatedly using stash.

---

## 19. Common Stash Commands

| Command                           | Purpose                       |
| --------------------------------- | ----------------------------- |
| `git stash`                       | Stash current changes         |
| `git stash push -m "message"`     | Stash with a message          |
| `git stash list`                  | Show all stashes              |
| `git stash apply`                 | Apply latest stash            |
| `git stash apply stash@{0}`       | Apply specific stash          |
| `git stash pop`                   | Apply and remove latest stash |
| `git stash drop stash@{0}`        | Delete specific stash         |
| `git stash clear`                 | Delete all stashes            |
| `git stash show`                  | Show stash summary            |
| `git stash show -p`               | Show complete stash diff      |
| `git stash -u`                    | Include untracked files       |
| `git stash -a`                    | Include ignored files         |
| `git stash -p`                    | Interactively select changes  |
| `git stash branch name stash@{0}` | Create branch from stash      |

---

## 20. Important Git Stash Interview Questions

### What is `git stash`?

> `git stash` temporarily saves uncommitted changes so that you can work on another branch or perform other Git operations without committing unfinished work.

### What is the difference between `git stash apply` and `git stash pop`?

> `git stash apply` restores the stash but keeps it in the stash list. `git stash pop` restores the stash and removes it from the stash list if the operation succeeds.

### Does `git stash` include untracked files?

> By default, no. Use `git stash -u` or `git stash --include-untracked` to include untracked files.

### How do you see all stashes?

```bash
git stash list
```

### How do you remove a stash?

```bash
git stash drop stash@{0}
```

### How do you remove all stashes?

```bash
git stash clear
```

### Can you create a branch from a stash?

Yes:

```bash
git stash branch feature-name stash@{0}
```

---

## 21. Simple Stash Cheat Sheet

```bash
# Check changes
git status

# Save changes
git stash

# Save with a message
git stash push -m "My work"

# Include untracked files
git stash -u

# View stashes
git stash list

# Apply latest stash
git stash apply

# Apply specific stash
git stash apply stash@{0}

# Apply and remove latest stash
git stash pop

# Show stash details
git stash show -p

# Delete one stash
git stash drop stash@{0}

# Delete all stashes
git stash clear

# Create branch from stash
git stash branch feature-name stash@{0}
```

---

## 22. Key Point to Remember

The basic Git stash workflow is:

```text
git status
     |
     v
git stash
     |
     v
Switch branch / do other work
     |
     v
Return to original branch
     |
     v
git stash pop
     |
     v
Continue working
```

**Remember:**

> `git stash` = temporarily save unfinished changes.

> `git stash apply` = restore changes and keep the stash.

> `git stash pop` = restore changes and remove the stash.

> `git stash list` = see saved stashes.

> `git stash clear` = remove all stashes.
