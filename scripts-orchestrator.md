# Scripts Orchestrator

`npm run scripts-orchestrator` is the one command that runs the automated checks in the repo, so you catch problems
before a reviewer or CI does.

Running it is a **required step on the PR checklist**. Do it before you raise a PR.

## Why run it

- **Catches common issues automatically.** Type errors, build failures, lint problems, failing
  tests, coverage drops, and team-specific rule violations are found by the scripts, not
  by your reviewer.
- **Lets reviewers focus on what matters.** Since the routine checks have already passed, the
  PR review can focus on unusual bugs and edge cases.
- **Same checks as CI.** CI runs the same gate on every change. Passing it locally means your PR has less chances to fail in CI.

## How to run it

From the repo root:

```sh
npm run scripts-orchestrator
```

When it finishes, it opens a summary report in your browser.


| Command                                       | When to use it                                                   |
| --------------------------------------------- | ---------------------------------------------------------------- |
| `npm run scripts-orchestrator`                | Default, before every PR                                         |
| `npm run scripts-orchestrator:affected`       | Faster: only checks workspaces your changes affect               |
| `npm run scripts-orchestrator:silent`         | Same as default, but doesn't open the report in the browser      |
| `npm run scripts-orchestrator:no-cache`       | Forces every check to re-run instead of reusing cached results   |
| `npm run scripts-orchestrator-full`           | Heavier: adds Storybook and Playwright (browser) tests           |


## Reading the results

- **Summary report:** `coverage/monorepo-quality-report.html` (re-open it with
  `npm run open:scripts-orchestrator-report`)
- **Detailed logs:** the `logs/` folder, e.g. `logs/scripts-orchestrator-logs/`. Each
  failing check has its own log file with the error.

## Relation to a pull request

1. Finish your changes and commit them.
2. Run `npm run scripts-orchestrator`.
3. If anything fails, open the report/logs, fix the issue, and **run it again**.
4. Repeat until the run passes with no errorss,then commit your fixes and push your branch.
5. Raise the PR and tick "I have run the sanity automation `npm run scripts-orchestrator`" in the
   PR checklist.
