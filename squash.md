# Git Squash — Command Flow for Easy Revision

## Goal
Combine all commits on your feature branch into **one commit** before pushing to GitHub.

### Step 1: Switch to your feature branch

```bash
git switch Rama/issue-7067
```

### Step 2: Check your working tree

```bash
git status
```

Make sure your changes are committed and the working tree is clean.

### Step 3: Create a backup branch

Run this before squashing, using a new backup name if one already exists.

```bash
git branch backup/issue-7067-before-squash
```

### Step 4: Fetch the latest remote changes

```bash
git fetch origin
```

This updates your remote-tracking branches without changing your current branch's files.

### Step 5: View your feature commits

```bash
git log --oneline origin/Sprint16..HEAD
```

This shows commits on your feature branch that are not in the remote `Sprint16` branch.

### Step 6: Start interactive rebase

```bash
git rebase -i origin/Sprint16
```

An editor opens with your commits listed from oldest to newest.

### Step 7: Change `pick` to `squash`

Keep `pick` for the **first commit** and change every remaining `pick` to `squash`.

Example:

```text
pick   abc1234 First commit message
squash def5678 Second commit message
squash ghi9012 Third commit message
squash jkl3456 Fourth commit message
```

Save and exit Vim:

1. Press `Esc`.
2. Type `:wq`.
3. Press `Enter`.

### Step 8: Enter one combined commit message

Git opens another editor.

1. Press `Esc`.
2. Type `:%d` and press `Enter` to clear the old messages.
3. Type `i` to enter Insert mode.
4. Enter your new commit message, for example:

```text
fix(theme): improve dark theme contrast and add story coverage
```

5. Press `Esc`.
6. Type `:wq` and press `Enter`.

### Step 9: Verify the squash

```bash
git log --oneline origin/Sprint16..HEAD
git status
```

Expected result: one feature commit and a clean working tree.

### Step 10: Push the squashed history

```bash
git push --force-with-lease origin Rama/issue-7067
```

**Important:** Squashing rewrites commit history, so a force push is needed to update the existing remote feature branch. `--force-with-lease` checks that the remote has not changed unexpectedly.

### Step 11: Confirm the push

```bash
git status
git log --oneline origin/Sprint16..HEAD
```

Expected:
- One commit ahead of `origin/Sprint16`.
- Working tree clean.
- Local branch up to date with `origin/Rama/issue-7067`.

## If something goes wrong

**Rebase conflict:**

```bash
# Fix the conflicted files, then:
git add <file>
git rebase --continue
```

To cancel the rebase:

```bash
git rebase --abort
```

**Remember:** Rebase and push your feature branch only. Do not push to `Sprint16`.
