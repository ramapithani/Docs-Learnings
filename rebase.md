# Git Rebase Command Flow

## 1. Rebase Feature Branch with Remote Sprint16

```bash
# 1. Switch to your feature branch
git switch Rama/issue-7067

# 2. Fetch the latest remote changes
git fetch origin

# 3. Check commits that are not in remote Sprint16
git log --oneline origin/Sprint16..HEAD

# 4. Rebase your feature branch onto remote Sprint16
git rebase origin/Sprint16

# 5. Push the rebased feature branch to GitHub
git push --force-with-lease origin Rama/issue-7067

# 6. Verify the result
git status
git log --oneline origin/Sprint16..HEAD
```

## 2. If Merge Conflicts Occur

```bash
# 1. Check which files have conflicts
git status

# 2. Resolve conflicts manually in the affected files

# 3. Stage the resolved files
git add .

# 4. Continue the rebase
git rebase --continue
```

Repeat the conflict-resolution steps if more conflicts occur.

### Cancel the Rebase

```bash
git rebase --abort
```

This cancels the current rebase and returns the branch to its pre-rebase state.

## 3. Understand the Workflow

```text
Fetch latest remote changes
          |
          v
Rebase feature branch onto origin/Sprint16
          |
          v
Resolve conflicts if any
          |
          v
Push feature branch using --force-with-lease
          |
          v
Verify branch status and commit history
```

## 4. Important Notes

- Always run these commands from your feature branch, not `Sprint16`.
- `git fetch origin` downloads remote updates without modifying your working files.
- `git rebase origin/Sprint16` replays your feature commits on top of the latest remote `Sprint16`.
- Rebase can change commit hashes.
- `git push --force-with-lease` updates your remote feature branch after a history rewrite while helping protect against unexpected remote changes.
- These commands do not directly modify the remote `Sprint16` branch.

**Example:** Replace `Rama/issue-7067` with your current feature branch name when working on another task.
