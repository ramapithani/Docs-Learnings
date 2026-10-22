# Git Command Flow — Create a Feature Branch for Bug 7068

## Goal
Create a new feature branch for bug **#7068** from the latest remote `Sprint16` branch without making changes directly to `Sprint16` or mixing work from bug #7067.

## Step 1: Check Current Branch and Changes

```bash
git branch
git status
```

- `git branch` — Shows local branches and the current branch.
- `git status` — Shows uncommitted changes.

**Important:** If you have uncommitted work for bug #7067, commit or safely stash it before proceeding.

## Step 2: Fetch the Latest Remote Updates

```bash
git fetch origin
```

- Downloads the latest branch information from GitHub.
- Does not switch branches or change your current working files.

## Step 3: Create a New Branch from Remote Sprint16

```bash
git switch -c Rama/issue-7068 origin/Sprint16
```

This command:
- Creates a new branch named `Rama/issue-7068`.
- Starts it from the latest fetched `origin/Sprint16`.
- Switches to the new branch.
- Does not modify your local `Sprint16` branch.

## Step 4: Verify the New Branch

```bash
git branch
git status
git log -1 --oneline
```

Expected branch output:

```text
  Sprint16
  Rama/issue-7067
* Rama/issue-7068
```

The `*` indicates the branch you are currently working on.

## Step 5: Push the New Branch to GitHub

```bash
git push -u origin Rama/issue-7068
```

- Pushes the branch to GitHub.
- Sets the upstream branch for future pushes and pulls.

After this, you can normally push future commits using:

```bash
git push
```

## Quick Revision — Complete Command Flow

```bash
git status
git fetch origin
git switch -c Rama/issue-7068 origin/Sprint16
git branch
git push -u origin Rama/issue-7068
```

## Remember

- `git fetch origin` — Get the latest remote branch information.
- `git switch -c` — Create and switch to a new branch.
- `origin/Sprint16` — Use the remote Sprint16 branch as the starting point.
- `git push -u origin <branch-name>` — Push the new branch and set its upstream.
- Always check `git status` before switching branches to protect uncommitted work.
- Do all bug #7068 changes on `Rama/issue-7068`, not directly on `Sprint16`.
