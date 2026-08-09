# Git Bisect

Git bisect is a Git tool used to find the commit that introduced a bug.

It works by using **binary search** between a known good commit and a known bad commit.

Instead of checking every commit one by one, Git helps us quickly narrow down the commit responsible for the problem.

---

## 1. What is Git Bisect?

`git bisect` helps identify which commit introduced a bug.

The basic idea is:

```text
Known Good Commit
       |
       ●
       |
       ●
       |
       ●
       |
       ●
       |
Known Bad Commit
```

Git selects a commit in the middle.

We test that commit and tell Git whether it is:

```text
good
```

or:

```text
bad
```

Git then continues narrowing down the range until it finds the first bad commit.

---

## 2. Why Use Git Bisect?

Git bisect is useful when:

* A bug appeared somewhere in Git history.
* You know a commit where the project worked.
* You know a commit where the bug exists.
* There are many commits between those points.
* You want to find the exact commit responsible for the bug.

For example:

```text
Commit A → Good
Commit B → Good
Commit C → Good
Commit D → Bad
Commit E → Bad
Commit F → Bad
```

Git bisect can help determine that:

```text
Commit D
```

introduced the problem.

---

## 3. Binary Search

Git bisect uses binary search.

Suppose there are 64 commits between the known good and bad points.

Checking every commit could require up to 64 tests.

Binary search reduces this significantly.

Approximately:

```text
64 commits
    ↓
32
    ↓
16
    ↓
8
    ↓
4
    ↓
2
    ↓
1
```

Only about 6 tests are needed to identify the problematic commit.

This makes `git bisect` very efficient.

---

## 4. Start Git Bisect

Start the bisect process:

```bash
git bisect start
```

Git enters bisect mode.

You can check the status with:

```bash
git bisect status
```

---

## 5. Mark the Current Commit as Bad

If the current commit contains the bug:

```bash
git bisect bad
```

This tells Git:

> The current commit is bad.

---

## 6. Mark a Known Good Commit

Find a commit where the project was working correctly.

For example:

```bash
git log --oneline
```

Suppose you find:

```text
abc1234 Add feature
def5678 Update documentation
789abcd Working version
```

If `789abcd` is known to be good:

```bash
git bisect good 789abcd
```

Now Git knows:

```text
Good → 789abcd
Bad  → current commit
```

---

## 7. Git Selects a Commit

After marking good and bad commits, Git automatically checks out a commit somewhere between them.

You may see something similar to:

```text
Bisecting: 5 revisions left to test after this
[abc4567] Some commit
```

Now test the application.

If the bug exists:

```bash
git bisect bad
```

If the bug does not exist:

```bash
git bisect good
```

Git will select another commit.

---

## 8. Continue the Process

The typical process looks like:

```bash
git bisect start
git bisect bad
git bisect good <good-commit>
```

Then test the selected commit.

If bad:

```bash
git bisect bad
```

If good:

```bash
git bisect good
```

Repeat until Git identifies the first bad commit.

---

## 9. Example

Suppose our history is:

```text
A → B → C → D → E → F → G
```

We know:

```text
A = Good
G = Bad
```

Start:

```bash
git bisect start
```

Mark bad:

```bash
git bisect bad G
```

Mark good:

```bash
git bisect good A
```

Git may select:

```text
D
```

Test D.

Suppose D is good:

```bash
git bisect good
```

Git now searches:

```text
E → F → G
```

It may select F.

Suppose F is bad:

```bash
git bisect bad
```

Git narrows the search:

```text
E → F
```

Suppose E is bad:

```bash
git bisect bad
```

Git identifies:

```text
E
```

as the first bad commit.

---

## 10. Check the Current Commit

During bisect, check the current commit with:

```bash
git log -1
```

Or:

```bash
git show
```

You can also use:

```bash
git status
```

Git will indicate that you are currently in a bisect operation.

---

## 11. Finish the Bisect

After Git identifies the first bad commit, exit bisect mode:

```bash
git bisect reset
```

This returns you to the branch and commit you were on before starting bisect.

Example:

```bash
git bisect reset
```

After resetting, check:

```bash
git status
```

---

## 12. Important Git Bisect Commands

| Command                    | Purpose                                  |
| -------------------------- | ---------------------------------------- |
| `git bisect start`         | Start bisect                             |
| `git bisect bad`           | Mark current commit as bad               |
| `git bisect good`          | Mark current commit as good              |
| `git bisect good <commit>` | Mark a specific commit as good           |
| `git bisect bad <commit>`  | Mark a specific commit as bad            |
| `git bisect status`        | Show bisect status                       |
| `git bisect reset`         | End bisect and return to previous branch |
| `git log --oneline`        | View commit history                      |
| `git show`                 | Inspect a commit                         |

---

## 13. Complete Git Bisect Workflow

The normal workflow is:

```bash
git bisect start
```

Mark the current commit as bad:

```bash
git bisect bad
```

Find a known good commit:

```bash
git log --oneline
```

Mark it:

```bash
git bisect good <commit-hash>
```

Test the selected commit.

If the bug exists:

```bash
git bisect bad
```

If the bug does not exist:

```bash
git bisect good
```

Continue until Git identifies the first bad commit.

Then exit:

```bash
git bisect reset
```

---

## 14. Git Bisect with a Real Test

Suppose an application has a test command:

```bash
npm test
```

You can manually test each commit.

Start:

```bash
git bisect start
```

Mark bad:

```bash
git bisect bad
```

Mark good:

```bash
git bisect good <good-commit>
```

Git checks out a commit.

Run:

```bash
npm test
```

If the test fails:

```bash
git bisect bad
```

If the test passes:

```bash
git bisect good
```

Repeat until Git finds the problematic commit.

---

## 15. Automated Git Bisect

Git bisect can also automate the process.

Suppose you have a test script:

```bash
./test.sh
```

You can run:

```bash
git bisect run ./test.sh
```

Git automatically executes the script on each selected commit.

The script should return:

```text
0
```

when the commit is good.

A non-zero exit status generally means the commit is bad.

Example:

```bash
git bisect start
git bisect bad
git bisect good <good-commit>
git bisect run ./test.sh
```

Git will automatically search for the first bad commit.

---

## 16. Automated Example

Suppose we have:

```bash
./test.sh
```

The script checks whether the application works.

Start bisect:

```bash
git bisect start
```

Mark the current version as bad:

```bash
git bisect bad
```

Mark a known working version:

```bash
git bisect good abc1234
```

Run the automated test:

```bash
git bisect run ./test.sh
```

Git performs the binary search automatically.

When finished:

```bash
git bisect reset
```

---

## 17. Git Bisect and Merge Commits

Sometimes the commit history contains merge commits.

For example:

```text
A ─ B ─ C ─ D
     \       /
      E ─ F
```

Git bisect can still work through the history.

However, testing merge commits can sometimes be more complicated because the bug may depend on changes from multiple branches.

When troubleshooting complex histories, inspect the selected commit carefully:

```bash
git show
```

---

## 18. What if a Commit Cannot Be Tested?

Sometimes a selected commit cannot be tested.

For example:

* The project does not build.
* Dependencies are missing.
* The test environment is broken.
* The commit is unrelated to the application.

You can skip that commit:

```bash
git bisect skip
```

Git will try to continue the search using the remaining commits.

You can also specify multiple commits:

```bash
git bisect skip <commit1> <commit2>
```

Use this carefully because skipping commits can make the final result less precise.

---

## 19. Git Bisect Conflict

Sometimes checking out a commit during bisect may expose a problem that prevents testing.

For example:

```text
The project does not build.
```

First investigate the selected commit.

You can inspect it:

```bash
git show
```

If the commit cannot be tested, you may skip it:

```bash
git bisect skip
```

Then continue the bisect process.

---

## 20. Finding the First Bad Commit

The most important result of Git bisect is:

```text
<commit-hash> is the first bad commit
```

For example:

```text
abc1234 is the first bad commit
```

You can inspect it:

```bash
git show abc1234
```

Or:

```bash
git show --stat abc1234
```

You can see the commit message:

```bash
git log -1 abc1234
```

---

## 21. Practical Example

Create a practice branch:

```bash
git switch -c bisect-practice
```

Create the first version:

```bash
echo "Version 1 - working" > bisect-practice.txt
```

Check it:

```bash
cat bisect-practice.txt
```

Commit:

```bash
git add bisect-practice.txt
git commit -m "Add working version"
```

Create another commit:

```bash
echo "Version 2 - working" >> bisect-practice.txt
```

Commit:

```bash
git add bisect-practice.txt
git commit -m "Add second working version"
```

Create another commit:

```bash
echo "Version 3 - bug introduced" >> bisect-practice.txt
```

Commit:

```bash
git add bisect-practice.txt
git commit -m "Introduce practice bug"
```

Create another commit:

```bash
echo "Version 4" >> bisect-practice.txt
```

Commit:

```bash
git add bisect-practice.txt
git commit -m "Add version 4"
```

Now the history contains several commits.

---

## 22. Practice Git Bisect

View the history:

```bash
git log --oneline
```

Suppose the history looks like:

```text
abcd444 Add version 4
abcd333 Introduce practice bug
abcd222 Add second working version
abcd111 Add working version
```

We know:

```text
abcd111 = Good
abcd444 = Bad
```

Start bisect:

```bash
git bisect start
```

Mark the current commit as bad:

```bash
git bisect bad
```

Mark the first commit as good:

```bash
git bisect good abcd111
```

Git checks out a commit between them.

Inspect the file:

```bash
cat bisect-practice.txt
```

Decide whether the bug exists.

If the selected commit is good:

```bash
git bisect good
```

If the selected commit is bad:

```bash
git bisect bad
```

Continue until Git identifies:

```text
abcd333 Introduce practice bug
```

Then reset:

```bash
git bisect reset
```

---

## 23. Verify After Bisect

Check your branch:

```bash
git branch
```

Check status:

```bash
git status
```

Check history:

```bash
git log --oneline --graph --all
```

You should be back on your original branch after:

```bash
git bisect reset
```

---

## 24. Delete the Practice Branch

After completing the exercise:

```bash
git branch -d bisect-practice
```

If Git does not allow deletion and you are certain the branch is no longer needed:

```bash
git branch -D bisect-practice
```

Use `-D` carefully because it can delete unmerged work.

---

## 25. Git Bisect vs Git Log

### Git Log

Used to inspect commit history:

```bash
git log --oneline
```

It helps you understand what changed.

### Git Bisect

Used to find which commit introduced a specific problem:

```bash
git bisect start
```

Git bisect is especially useful when there are many commits and you do not know which one introduced the bug.

---

## 26. Git Bisect vs Git Revert

These commands solve different problems.

### Git Bisect

Finds the commit that introduced a bug.

```bash
git bisect start
```

### Git Revert

Creates a new commit that reverses the changes from an earlier commit.

```bash
git revert <commit>
```

Remember:

```text
Bisect → Find the bad commit.

Revert → Undo the changes safely with a new commit.
```

---

## 27. Common Mistakes

### Mistake 1: Forgetting to mark the bad commit

You need to tell Git which commit is bad:

```bash
git bisect bad
```

### Mistake 2: Forgetting the known good commit

You need a known working point:

```bash
git bisect good <commit>
```

### Mistake 3: Forgetting to reset

After the investigation, exit bisect mode:

```bash
git bisect reset
```

### Mistake 4: Marking a commit incorrectly

If you accidentally mark a good commit as bad, the bisect result can be incorrect.

Always test the selected commit carefully.

---

## 28. Useful Commands During Bisect

Check current commit:

```bash
git log -1
```

Inspect changes:

```bash
git show
```

Check status:

```bash
git status
```

View history:

```bash
git log --oneline --graph --all
```

See bisect state:

```bash
git bisect status
```

---

## 29. Interview Questions

### What is Git bisect?

> Git bisect is a Git command used to find the commit that introduced a bug by performing a binary search through the commit history.

### Why is Git bisect useful?

> It is useful when we know a working commit and a broken commit but do not know which commit introduced the problem.

### How does Git bisect work?

> Git bisect repeatedly divides the range of commits between a known good and known bad commit and asks us to identify whether each selected commit is good or bad.

### What command starts bisect?

```bash
git bisect start
```

### How do you mark a commit as bad?

```bash
git bisect bad
```

### How do you mark a commit as good?

```bash
git bisect good <commit>
```

### How do you stop bisect?

```bash
git bisect reset
```

### What does `git bisect skip` do?

> It tells Git that the selected commit cannot be tested and should be skipped.

### Can Git bisect be automated?

Yes.

For example:

```bash
git bisect run ./test.sh
```

Git can automatically execute the test on each commit.

---

## 30. Quick Cheat Sheet

```bash
# Start
git bisect start

# Mark current commit as bad
git bisect bad

# Mark known commit as good
git bisect good <commit>

# Check current commit
git log -1

# Test the selected commit
# Then mark it:
git bisect good
# OR
git bisect bad

# Skip an untestable commit
git bisect skip

# Check bisect status
git bisect status

# Inspect selected commit
git show

# Automated bisect
git bisect run ./test.sh

# Finish
git bisect reset
```

---

## 31. Key Takeaway

Remember:

```text
GIT BISECT
     |
     ↓
Known Good Commit
     |
     ↓
Binary Search
     |
     ↓
Test Commit
     |
   Good? ──────── Yes → Search later commits
     |
     No
     ↓
Search earlier commits
     |
     ↓
First Bad Commit
```

The easiest way to remember Git bisect is:

> **"I know when it worked and when it broke, but I don't know which commit caused it."**

Use:

```bash
git bisect start
git bisect bad
git bisect good <commit>
```

Then repeatedly mark commits as `good` or `bad` until Git finds the first bad commit.
