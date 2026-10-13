# Pull Requests
## WHat is pull request

A pull request is to tell the peer developers about the changes you made to the existing code and ask them to review before merging the changes with the actual project branch.
The PR raise has a systematic approach that makes it easy and a standard process for a developer.This is available at PULL_REQUEST_TEMPLATE.md .
The detailing of the sripts-orchestrator and code-reviewer are separetely documented clearly agentic-code-reviewer.md and PULL_REQUEST_TEMPLATE.md .

## How to raise a PR

1. **Get a ticket number.** Every PR is linked to a GitHub issue (see
   [Creating a ticket](#creating-a-ticket-github-issue) below).
2. **Work on your own branch.** Commit your changes there, not on the sprint branch.
3. **Run the checks** and fix everything required:
   - `npm run scripts-orchestrator`: must pass with no errors
   - `npm run code-review`: fix every **[HIGH]** finding
4 **Open the PR on GitHub:**
   - Go to the repo's **Pull requests** tab → **New pull request** (or click **Compare & pull
     request** on the banner GitHub shows after a push).
   - Give it a clear title, then fill in the template .
6. **Request reviewers** and do the required changes based on their comments by fixing them.


## Creating a ticket (GitHub issue)

1. Open the repo on GitHub and go to the **Issues** tab.
2. Click **New issue**.
3. Add a clear **title** and a **description** (what and why; for bugs, steps to reproduce).
4. Click **Submit new issue**.

The ticket number is the `#` number next to the title, e.g. **#482**.

