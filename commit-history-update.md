# Git Commands for Reviewing and Cleaning Up Commit History (Here PR7041)

## 1. View PR Details

```sh
gh pr view 7041 --json headRefName,baseRefName,state
```

This shows the source branch, target branch, and PR state of PR 7041.

## 2. View Commits Not in the Remote Sprint16 Branch

```sh
git log --oneline --decorate origin/Sprint16..HEAD
```

Shows commits on your current branch that aren't in the remote Sprint16 branch.

## 3. Create a Backup Branch

```sh
git branch backup/pr-7041-before-cleanup
```

This command creates a backup branch of your current commit.

* `git branch` — creates a new branch.
* `backup/pr-7041-before-cleanup` — the name of the backup branch.

## 4. Interactively Rebase Your Branch

```sh
git rebase -i origin/Sprint16
```

Git will open an editor containing the commits in your branch, usually in oldest-to-newest order.

Git opens a list of your branch's commits. You can choose to:

* `pick` — keep a commit.
* `drop` — remove a commit.
* `reword` — change a commit message.
* `squash` — combine a commit with the previous commit.

### Your list should look like this:

```text
drop 08dcf13e4 # docs: update playwright.md with steps to record a new test
drop 474a948e7 # docs: add agentic-code-reviwer guide
drop bddcfbf80 # docs: add scripts-orchestrator guide
drop c30462dc4 # add docs/process/scripts-orchestrator.md
drop 3148f599c # add docs/process/pull-request.md
drop 5549ec3dd # add docs/eslint-rules
drop 84d56a58a # add docs/eslint-rules.md
drop 8e2a5d9a8 # docs/process/agentic-code-reviewer
drop 093b7de90 # add docs/process/scripts-orchestrator.md
drop dbf98ee19 # add docs/testing/playwright.md
pick c751760e5 # added tests for BookJobStatus.tsx statements and branches
drop be0c5aa0b # add learnings on JEST-Javascript unit testing
drop 10ce825f0 # add learnings on JEST-Javascript unit testing
drop 67001f7cf # add learnings on JEST-Javascript unit testing
```

### Save and exit Vim

1. Press `i` to enter insert mode.
2. Edit the lines as shown above.
3. Press `Esc`.
4. Type `:wq` and press Enter.

Git will start the rebase.


## 5. Push the Updated Branch After Rebasing

After the rebase finishes, push your branch using --force-with-lease because the commit history has been rewritten.

```sh
git push --force-with-lease origin my-branch
```

git push —> pushes your changes to GitHub.
--force-with-lease —> safely updates the remote branch with the rewritten commit history, provided the remote branch has not changed unexpectedly.
origin —> the remote repository.
my-branch —> your feature branch name.

## 6. Verify the Result After Rebasing

```sh
git log --oneline origin/Sprint16..HEAD
```

Verify: shows commits on your current branch that aren't in the remote Sprint16 branch.
