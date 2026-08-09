# Git Merge Conflicts

A **merge conflict** happens when Git cannot automatically combine changes from two branches.

This usually happens when two branches modify the **same part of the same file** differently.

---

# 1. What Is a Merge Conflict?

Suppose two branches change the same line:

```text
main:
Hello from main

feature:
Hello from feature
```

Git does not know which version you want.

Therefore, Git reports a **merge conflict**.

---

# 2. Why Do Merge Conflicts Happen?

Common reasons:

* Two branches modify the same line.
* Two branches modify the same section of a file.
* One branch deletes a file while another modifies it.
* Different changes overlap during a merge or rebase.

Example:

```text
main
 |
 |---- change A
 |
feature
 |
 |---- change B
```

If both changes affect the same code, Git may need your help.

---

# 3. Create a Merge Conflict

We can intentionally create a conflict for practice.

First make sure you are on `main`:

```bash
git switch main
```

Create a practice branch:

```bash
git switch -c conflict-practice
```

Create or modify a file:

```bash
echo "Hello from feature branch" > conflict.txt
```

Check the file:

```bash
cat conflict.txt
```

Add and commit:

```bash
git add conflict.txt
git commit -m "Add feature branch message"
```

Switch back to `main`:

```bash
git switch main
```

Create a different version of the same file:

```bash
echo "Hello from main branch" > conflict.txt
```

Add and commit:

```bash
git add conflict.txt
git commit -m "Add main branch message"
```

Now try to merge the feature branch:

```bash
git merge conflict-practice
```

Git should report a conflict.

---

# 4. Check the Conflict

Run:

```bash
git status
```

Git will tell you which files have conflicts.

You may see something similar to:

```text
both modified: conflict.txt
```

---

# 5. Conflict Markers

Open the conflicted file:

```bash
cat conflict.txt
```

You may see:

```text
<<<<<<< HEAD
Hello from main branch
=======
Hello from feature branch
>>>>>>> conflict-practice
```

These are called **conflict markers**.

---

# 6. Understanding Conflict Markers

### `<<<<<<< HEAD`

This represents the version from your current branch.

In this example:

```text
Hello from main branch
```

### `=======`

This separates the two versions.

### `>>>>>>> conflict-practice`

This represents the incoming branch's version.

In this example:

```text
Hello from feature branch
```

---

# 7. Resolve the Conflict

Open the file:

```bash
code conflict.txt
```

Choose the content you want.

For example:

```text
Hello from the combined project
```

Make sure you remove all conflict markers:

```text
<<<<<<<
=======
>>>>>>>
```

Save the file.

---

# 8. Check the Resolution

Run:

```bash
git status
```

Git should show that the file is still unmerged until you stage it.

Then stage the resolved file:

```bash
git add conflict.txt
```

Check again:

```bash
git status
```

The conflict should now be resolved.

---

# 9. Complete the Merge

After resolving the conflict:

```bash
git commit -m "Resolve merge conflict"
```

The merge is now complete.

Check the history:

```bash
git log --oneline --graph --all
```

You should see the branches coming together.

---

# 10. Abort a Merge

If you realize that you do not want to continue the merge, you can cancel it:

```bash
git merge --abort
```

This returns your working tree to the state before the merge started.

Use this when you want to completely abandon the current merge.

---

# 11. Useful Commands During Conflicts

Check repository status:

```bash
git status
```

See unstaged changes:

```bash
git diff
```

See staged changes:

```bash
git diff --staged
```

Stage a resolved file:

```bash
git add filename
```

Abort a merge:

```bash
git merge --abort
```

Complete the merge:

```bash
git commit
```

---

# 12. Conflict Resolution Workflow

The basic workflow is:

```text
Create branches
      ↓
Make different changes
      ↓
Merge branches
      ↓
Conflict occurs
      ↓
git status
      ↓
Open conflicted file
      ↓
Choose the correct changes
      ↓
Remove conflict markers
      ↓
git add
      ↓
git commit
      ↓
Merge completed
```

---

# 13. Important Rule

Git does **not** decide which code is correct during a conflict.

Git only detects that the changes overlap.

**You decide which version should remain.**

---

# 14. Merge Conflict vs Normal Merge

### Normal merge

Git can automatically combine the changes.

```text
Branch A
   \
    → Merge → Success
   /
Branch B
```

### Merge conflict

Git cannot automatically decide what to keep.

```text
Branch A
   \
    → Merge → Conflict
   /
Branch B
```

You must manually resolve the conflict.

---

# 15. Interview Questions

### What is a merge conflict?

> A merge conflict occurs when Git cannot automatically combine changes from different branches, usually because the same part of a file was modified differently.

### Why do merge conflicts happen?

> They happen when changes from different branches overlap and Git cannot determine which changes should be kept.

### How do you resolve a merge conflict?

> I check the conflicted files, open them, choose the correct changes, remove the conflict markers, save the files, run `git add`, and complete the merge with a commit.

### What does `git merge --abort` do?

> It cancels the current merge and returns the working tree to the state it was in before the merge started.

### What are conflict markers?

> Conflict markers are special lines added by Git to show the conflicting versions of a file.

Example:

```text
<<<<<<< HEAD
Current branch
=======
Incoming branch
>>>>>>> feature
```

---

# 16. Quick Cheat Sheet

| Command                           | Purpose                   |
| --------------------------------- | ------------------------- |
| `git status`                      | Check conflict status     |
| `git diff`                        | View changes              |
| `git add file`                    | Mark conflict as resolved |
| `git commit`                      | Complete merge            |
| `git merge --abort`               | Cancel merge              |
| `git log --oneline --graph --all` | View branch history       |

---

# Remember

```text
Conflict
   ↓
git status
   ↓
Open conflicted file
   ↓
Choose correct changes
   ↓
Remove <<<<<<< ======= >>>>>>>
   ↓
git add .
   ↓
git commit
   ↓
Conflict resolved
```

**Simple interview answer:**

> A merge conflict occurs when Git cannot automatically combine changes from two branches. I resolve it by reviewing the conflicting file, choosing the correct changes, removing the conflict markers, staging the file, and completing the merge.
