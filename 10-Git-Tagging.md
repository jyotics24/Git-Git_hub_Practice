# Git Tagging

Git tags are used to mark specific points in Git history.

Tags are commonly used to identify important versions or releases of a project.

For example:

```text
v1.0.0
v1.1.0
v2.0.0
```

A tag usually points to a specific commit.

---

## 1. What is a Git Tag?

A Git tag is a reference to a specific commit.

For example:

```text
v1.0.0
   |
   v
commit abc123
```

Tags are useful for marking:

* Software releases
* Stable versions
* Important milestones
* Production versions

---

## 2. List Tags

```bash
git tag
```

Shows all tags in the repository.

Example:

```text
v1.0.0
v1.1.0
v2.0.0
```

---

## 3. Create a Tag

```bash
git tag v1.0.0
```

Creates a lightweight tag pointing to the current commit.

Check it:

```bash
git tag
```

Output:

```text
v1.0.0
```

---

## 4. Create an Annotated Tag

Annotated tags contain additional information such as:

* Tag message
* Tagger
* Date
* Commit reference

Create one:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

This is commonly preferred for official releases.

---

## 5. View a Tag

```bash
git show v1.0.0
```

Shows information about the tag and the commit it points to.

Example:

```text
tag v1.0.0
Tagger: Jyoti
Date: ...

Release version 1.0.0

commit abc123
Author: Jyoti
...
```

---

## 6. Tag a Specific Commit

You don't have to tag the current commit.

First view the history:

```bash
git log --oneline
```

Example:

```text
1108f47 Add Git Log-Diff Note
a449e00 Add Git reset and revert notes
7ae7a78 Add Git stash notes
```

Tag a specific commit:

```bash
git tag v1.0.0 a449e00
```

Now `v1.0.0` points to commit `a449e00`.

---

## 7. Annotated Tag for a Specific Commit

```bash
git tag -a v1.0.0 a449e00 -m "Release version 1.0.0"
```

This creates an annotated tag on the specified commit.

---

## 8. Push a Tag to GitHub

Creating a tag locally does not automatically push it to GitHub.

Push a specific tag:

```bash
git push origin v1.0.0
```

Example:

```bash
git push origin v1.0.0
```

---

## 9. Push All Tags

```bash
git push origin --tags
```

This pushes all local tags that don't already exist on the remote repository.

---

## 10. Delete a Local Tag

```bash
git tag -d v1.0.0
```

Example output:

```text
Deleted tag 'v1.0.0'
```

This deletes only the local tag.

---

## 11. Delete a Remote Tag

To delete a tag from GitHub:

```bash
git push origin --delete v1.0.0
```

Example:

```bash
git push origin --delete v1.0.0
```

This removes the tag from the remote repository.

---

## 12. Alternative Remote Tag Deletion

Another syntax is:

```bash
git push origin :refs/tags/v1.0.0
```

This also deletes the remote tag.

The following is easier to remember:

```bash
git push origin --delete v1.0.0
```

---

## 13. Checkout a Tag

You can switch to a tag:

```bash
git switch --detach v1.0.0
```

This puts you in a detached HEAD state.

Example:

```text
HEAD -> v1.0.0
```

You are viewing the project exactly as it existed at that tagged commit.

---

## 14. Detached HEAD

When you switch directly to a tag:

```bash
git switch --detach v1.0.0
```

Git tells you that you are in a detached HEAD state.

This means `HEAD` is pointing directly to a commit instead of a branch.

Example:

```text
main
 |
 A
 |
 B
 |
 C  <- v1.0.0 <- HEAD
```

You can inspect the code, but you normally should not create regular development commits here.

If you want to make changes based on the tag, create a branch:

```bash
git switch -c release-fix
```

---

## 15. List Tags With Messages

```bash
git tag -n
```

Example:

```text
v1.0.0  Release version 1.0.0
v1.1.0  Add new Git notes
```

---

## 16. Search Tags

You can filter tags using a pattern:

```bash
git tag -l "v1.*"
```

Example:

```text
v1.0.0
v1.1.0
v1.2.0
```

Another example:

```bash
git tag -l "v2.*"
```

---

## 17. Tag Naming Convention

A common convention is:

```text
vMAJOR.MINOR.PATCH
```

Example:

```text
v1.0.0
v1.1.0
v1.2.0
v2.0.0
```

This is related to Semantic Versioning.

---

# Semantic Versioning

Semantic Versioning commonly uses:

```text
MAJOR.MINOR.PATCH
```

Example:

```text
2.4.1
```

Where:

```text
2 = MAJOR
4 = MINOR
1 = PATCH
```

---

## MAJOR Version

Increase the major version when you make incompatible changes.

Example:

```text
v1.0.0
   ↓
v2.0.0
```

Example:

```text
v1.0.0 → v2.0.0
```

---

## MINOR Version

Increase the minor version when adding functionality while maintaining backward compatibility.

Example:

```text
v1.0.0
   ↓
v1.1.0
```

---

## PATCH Version

Increase the patch version for bug fixes or small compatible changes.

Example:

```text
v1.1.0
   ↓
v1.1.1
```

---

# Version Examples

```text
v1.0.0
```

Initial stable release.

```text
v1.1.0
```

New backward-compatible feature.

```text
v1.1.1
```

Bug fix.

```text
v2.0.0
```

Major breaking change.

---

# Tagging Workflow

A common release workflow is:

### Step 1: Check status

```bash
git status
```

Make sure the working tree is clean.

---

### Step 2: View recent commits

```bash
git log --oneline
```

Example:

```text
1108f47 Add Git Log-Diff Note
a449e00 Add Git reset and revert notes
7ae7a78 Add Git stash notes
```

---

### Step 3: Create an annotated tag

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

---

### Step 4: Check the tag

```bash
git tag
```

---

### Step 5: Inspect the tag

```bash
git show v1.0.0
```

---

### Step 6: Push the tag

```bash
git push origin v1.0.0
```

---

### Step 7: Verify

```bash
git ls-remote --tags origin
```

This displays tags available on the remote repository.

---

# Git Tag vs Git Branch

| Git Tag                           | Git Branch                                |
| --------------------------------- | ----------------------------------------- |
| Marks a specific point in history | Represents a line of development          |
| Usually does not move             | Moves as new commits are added            |
| Commonly used for releases        | Used for feature development              |
| Example: `v1.0.0`                 | Example: `feature-login`                  |
| Usually points to a fixed commit  | Points to the latest commit on the branch |

Example:

```text
main
 |
 A
 |
 B
 |
 C ← v1.0.0
 |
 D
 |
 E ← main
```

The tag `v1.0.0` continues to point to commit `C`.

The `main` branch moves forward to commit `E`.

---

# Useful Tag Commands

```bash
# List tags
git tag

# Create lightweight tag
git tag v1.0.0

# Create annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# Show tag
git show v1.0.0

# Tag a specific commit
git tag v1.0.0 <commit>

# List tags with messages
git tag -n

# Search tags
git tag -l "v1.*"

# Delete local tag
git tag -d v1.0.0

# Push one tag
git push origin v1.0.0

# Push all tags
git push origin --tags

# Delete remote tag
git push origin --delete v1.0.0

# Switch to tag
git switch --detach v1.0.0

# View remote tags
git ls-remote --tags origin
```

---

# Practical Example

Suppose your project currently has:

```text
1108f47 Add Git Log-Diff Note
```

You decide that this is your first release.

Create a tag:

```bash
git tag -a v1.0.0 -m "First Git practice release"
```

Check it:

```bash
git tag
```

Output:

```text
v1.0.0
```

Inspect it:

```bash
git show v1.0.0
```

Push it:

```bash
git push origin v1.0.0
```

Now GitHub has the release tag.

---

# Release Example

Imagine your project develops through these versions:

```text
v1.0.0
   |
   | Add new notes
   v
v1.1.0
   |
   | Fix documentation
   v
v1.1.1
   |
   | Major project changes
   v
v2.0.0
```

Each tag identifies an important version of the project.

---

# Important Interview Questions

## What is a Git tag?

> A Git tag is a reference that points to a specific commit, commonly used to mark releases or important versions.

## Why are Git tags used?

> Git tags are used to mark important points in Git history, especially software releases and stable versions.

## What is the difference between a tag and a branch?

> A branch is used for ongoing development and moves forward with new commits, while a tag normally marks a fixed point in Git history.

## What is an annotated tag?

> An annotated tag is a Git object containing additional information such as the tag message, author, and date.

## How do you create an annotated tag?

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

## How do you push a tag to GitHub?

```bash
git push origin v1.0.0
```

## How do you push all tags?

```bash
git push origin --tags
```

## How do you delete a local tag?

```bash
git tag -d v1.0.0
```

## How do you delete a remote tag?

```bash
git push origin --delete v1.0.0
```

## What does `v1.0.0` mean?

> It commonly represents version 1.0.0 using the MAJOR.MINOR.PATCH versioning convention.

## What is Semantic Versioning?

> Semantic Versioning is a versioning convention that uses MAJOR, MINOR, and PATCH numbers to communicate the type of changes in a release.

---

# Key Takeaways

1. `git tag` lists tags.
2. Tags mark specific commits.
3. Tags are commonly used for releases.
4. `git tag v1.0.0` creates a lightweight tag.
5. `git tag -a` creates an annotated tag.
6. `git show v1.0.0` displays tag information.
7. `git push origin v1.0.0` pushes one tag.
8. `git push origin --tags` pushes all tags.
9. `git tag -d` deletes a local tag.
10. `git push origin --delete` deletes a remote tag.
11. `v1.0.0` is a common release naming convention.
12. Tags normally remain fixed while branches continue moving.
13. Semantic Versioning uses MAJOR.MINOR.PATCH.
14. Tags are useful for identifying stable releases.
