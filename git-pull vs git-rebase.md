# Git Pull vs Git Rebase — Quick Reference

## 1. Git Rebase
### Purpose: Replay local feature branch commits on top of the latest target branch commits.
git fetch origin
git switch Rama/my-task
git rebase origin/Sprint16
If conflicts occur:
### Resolve conflicts in the files, then:
git add path/to/file
git rebase --continue
### Push changes to GitHub:
git push --force-with-lease origin Rama/my-task
* Rebase rewrites commit history; replayed commits get new hashes.
** Use --force-with-lease if the rewritten commits were already pushed to GitHub. **
  
## 2. Git Pull (Merge)
### Purpose: Merge remote target branch commits into your local feature branch.
git switch Rama/my-task
git pull origin Sprint16
If conflicts occur:
### Resolve conflicts in the files, then:
git add path/to/file
git commit
### Push changes to GitHub:
git push origin Rama/my-task
* Merge preserves existing commit hashes and usually creates a merge commit when the branches have diverged.
* A normal push is usually sufficient because existing history is preserved.
  
## Remember during conflict
* Rebase: git add → git rebase --continue → force-push with lease if needed.
* Merge: git add → git commit → normal push.
