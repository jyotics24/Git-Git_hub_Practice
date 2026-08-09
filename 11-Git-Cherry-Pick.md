# Git Cherry-Pick

Git cherry-pick allows us to take a specific commit from one branch and apply it to another branch.

It is useful when we want only one particular change without merging the entire branch.

---

## 1. What is Git Cherry-Pick?

`git cherry-pick` applies the changes introduced by an existing commit to the current branch.

Example:

```bash
git cherry-pick <commit-hash>
```

The commit hash identifies the commit that we want to apply.

---

## 2. Why Use Cherry-Pick?

Cherry-pick is useful when:

* We need one specific commit from another branch.
* We do not want to merge the entire branch.
* We need to apply a bug fix to another branch.
* We need to move a small change between branches.
* We want to selectively apply commits.

Example:

```text
main
 |
 ● A
 |
 ● B

feature
 |
 ● A
 |
 ● B
 |
 ● C
 |
 ● D
```

Suppose commit `C` contains an important bug fix.

Instead of merging the entire `feature` branch, we can cherry-pick commit `C` into `main`.

```text
main
 |
 ● A
 |
 ● B
 |
 ● C'
```

`C'` contains the same changes as commit `C`, but it gets a new commit hash.

---

## 3. Basic Cherry-Pick Command

```bash
git cherry-pick <commit-hash>
```

Example:

```bash
git cherry-pick abc1234
```

Git takes the changes from commit `abc1234` and applies them to the current branch.

---

## 4. Find the Commit Hash

Before cherry-picking, find the commit you want.

Use:

```bash
git log --oneline --all
```

Example:

```text
abc1234 Fix login validation
def5678 Add dashboard
789abcd Update README
```

If we want the login fix:

```bash
git cherry-pick abc1234
```

---

## 5. Important: Switch to the Target Branch

Cherry-pick applies the commit to the branch you are currently on.

For example:

```bash
git switch main
```

Then:

```bash
git cherry-pick abc1234
```

The commit is now applied to `main`.

---

## 6. Cherry-Pick Workflow

A typical workflow is:

```bash
git branch
```

Find the commit:

```bash
git log --oneline --all
```

Switch to the target branch:

```bash
git switch main
```

Cherry-pick the required commit:

```bash
git cherry-pick <commit-hash>
```

Check the result:

```bash
git log --oneline --graph --all
```

Push the change:

```bash
git push origin main
```

---

## 7. Cherry-Pick a Commit from Another Branch

Suppose we have:

```text
main
 |
 ● A
 |
 ● B

feature
 |
 ● A
 |
 ● B
 |
 ● C
 |
 ● D
```

Commit `C` contains an important fix.

First switch to `main`:

```bash
git switch main
```

Then cherry-pick `C`:

```bash
git cherry-pick <C-commit-hash>
```

The result becomes:

```text
main
 |
 ● A
 |
 ● B
 |
 ● C'
```

The change from `C` is now present in `main`.

---

## 8. Cherry-Pick Multiple Commits

You can cherry-pick multiple commits.

Example:

```bash
git cherry-pick abc1234 def5678
```

This applies both commits.

Another option is to cherry-pick a range:

```bash
git cherry-pick abc1234..def5678
```

Be careful with ranges because Git's range notation determines which commits are included.

---

## 9. Cherry-Pick a Range Including the First Commit

To include the first commit in a range, use:

```bash
git cherry-pick abc1234^..def5678
```

This applies commits starting from `abc1234` through `def5678`.

---

## 10. Cherry-Pick Conflict

Cherry-pick can cause a conflict when the changes in the selected commit conflict with changes in the current branch.

Example:

```text
CONFLICT (content): Merge conflict in file.txt
error: could not apply abc1234...
```

Git pauses the cherry-pick.

Check the conflict:

```bash
git status
```

Fix the conflicted file manually.

Then stage it:

```bash
git add file.txt
```

Continue the cherry-pick:

```bash
git cherry-pick --continue
```

---

## 11. Abort a Cherry-Pick

If you do not want to continue after a conflict:

```bash
git cherry-pick --abort
```

This returns the repository to the state before the cherry-pick started.

---

## 12. Skip a Commit

During a multi-commit cherry-pick, if you want to skip the current commit:

```bash
git cherry-pick --skip
```

This tells Git to skip the commit that caused the current cherry-pick operation to stop.

---

## 13. Cherry-Pick Without Committing

You can apply the changes without immediately creating a commit:

```bash
git cherry-pick --no-commit <commit-hash>
```

Short form:

```bash
git cherry-pick -n <commit-hash>
```

This applies the changes to the working tree and staging area but does not create the commit.

You can then modify the changes and create your own commit:

```bash
git add .
git commit -m "Apply selected feature changes"
```

---

## 14. Cherry-Pick vs Merge

### Merge

Merge combines the histories of two branches.

```bash
git switch main
git merge feature
```

Use merge when you want the complete branch.

### Cherry-Pick

Cherry-pick applies selected commits.

```bash
git switch main
git cherry-pick <commit-hash>
```

Use cherry-pick when you only need specific changes.

---

## 15. Cherry-Pick vs Rebase

### Cherry-Pick

Selects specific commits and applies them to another branch.

```bash
git cherry-pick <commit>
```

### Rebase

Moves or replays a series of commits onto another base.

```bash
git rebase main
```

Cherry-pick is selective.

Rebase is generally used to reorganize or update a branch's history.

---

## 16. Common Cherry-Pick Commands

| Command                       | Purpose                           |
| ----------------------------- | --------------------------------- |
| `git cherry-pick <commit>`    | Apply one commit                  |
| `git cherry-pick A B`         | Apply multiple commits            |
| `git cherry-pick A..B`        | Apply a commit range              |
| `git cherry-pick --continue`  | Continue after resolving conflict |
| `git cherry-pick --abort`     | Cancel cherry-pick                |
| `git cherry-pick --skip`      | Skip current commit               |
| `git cherry-pick -n <commit>` | Apply without committing          |
| `git log --oneline --all`     | Find commits                      |

---

## 17. Practical Example

Create a practice branch:

```bash
git switch -c cherry-pick-practice
```

Create a file:

```bash
echo "Important bug fix" > cherry-pick.txt
```

Check it:

```bash
cat cherry-pick.txt
```

Stage it:

```bash
git add cherry-pick.txt
```

Commit it:

```bash
git commit -m "Add important bug fix"
```

Find the commit:

```bash
git log --oneline
```

Example:

```text
abc1234 Add important bug fix
4d80291 Add Git tagging notes
```

Copy the commit hash.

Switch back to main:

```bash
git switch main
```

Cherry-pick the commit:

```bash
git cherry-pick abc1234
```

Check the log:

```bash
git log --oneline --graph --all
```

You should see the selected change applied to `main`.

---

## 18. Verify the Cherry-Pick

Check the status:

```bash
git status
```

Expected:

```text
On branch main
nothing to commit, working tree clean
```

Check the file:

```bash
ls
```

You should see:

```text
cherry-pick.txt
```

Check its contents:

```bash
cat cherry-pick.txt
```

Expected:

```text
Important bug fix
```

---

## 19. Push the Cherry-Picked Change

After successfully cherry-picking:

```bash
git push origin main
```

Then verify:

```bash
git status
```

Expected:

```text
On branch main
nothing to commit, working tree clean
```

---

## 20. Delete the Practice Branch

If the practice branch has been merged or its commit has been cherry-picked:

```bash
git branch -d cherry-pick-practice
```

If Git says the branch is not fully merged and you are sure you no longer need it:

```bash
git branch -D cherry-pick-practice
```

Use `-D` carefully.

---

## 21. Important Interview Questions

### What is Git cherry-pick?

> Git cherry-pick applies the changes from a specific existing commit to the current branch.

### Why would you use cherry-pick?

> Cherry-pick is useful when we need a specific commit or bug fix from another branch without merging the entire branch.

### Does cherry-pick create a new commit?

Yes.

When Git successfully cherry-picks a commit, it normally creates a new commit on the current branch.

The new commit contains the same changes, but it usually has a different commit hash.

### What happens if cherry-pick causes a conflict?

Resolve the conflicted files, stage them, and continue:

```bash
git add .
git cherry-pick --continue
```

Or cancel the operation:

```bash
git cherry-pick --abort
```

### What is the difference between merge and cherry-pick?

> Merge combines branch histories, while cherry-pick selectively applies individual commits.

### What is the difference between cherry-pick and rebase?

> Cherry-pick applies selected commits to the current branch, while rebase replays a branch's commits onto a new base.

---

## 22. Important Warning

Avoid repeatedly cherry-picking the same commit into branches unless you understand the resulting history.

Cherry-picking creates a new commit, so the new commit has a different hash from the original.

For example:

```text
Original branch:

A -- B -- C

After cherry-pick:

A -- B -- C'
```

`C` and `C'` may contain the same changes, but they are different commits.

---

## 23. Quick Cheat Sheet

```bash
# Find commits
git log --oneline --all

# Switch to target branch
git switch main

# Apply one commit
git cherry-pick <commit-hash>

# Apply multiple commits
git cherry-pick <commit1> <commit2>

# Continue after conflict
git add .
git cherry-pick --continue

# Abort
git cherry-pick --abort

# Skip current commit
git cherry-pick --skip

# Apply without committing
git cherry-pick -n <commit-hash>

# Check history
git log --oneline --graph --all

# Push
git push origin main
```

---

## 24. Key Takeaway

Remember:

```text
MERGE
→ Bring the branch together.

REBASE
→ Replay commits onto a new base.

CHERRY-PICK
→ Select specific commits.
```

The easiest way to remember cherry-pick is:

> **"I don't need the whole branch. I only need this particular commit."**
