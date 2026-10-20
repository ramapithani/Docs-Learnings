# 1. Switch to your feature branch
git switch Rama/issue-7067

# 2. Fetch the latest remote changes
git fetch origin

# 3. Check your commits before rebasing
git log --oneline origin/Sprint16..HEAD

# 4. Rebase your commits onto the latest remote Sprint16
git rebase origin/Sprint16

# 5. Push the rebased feature branch to GitHub
git push --force-with-lease origin Rama/issue-7067

# 6. Verify the result
git status
git log --oneline origin/Sprint16..HEAD
