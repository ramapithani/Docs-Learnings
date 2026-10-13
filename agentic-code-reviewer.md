# Agentic Code Reviewer

An AI review of your branch, checked against the team's coding rules. Running it is a **required
step on the PR checklist** — do it before you raise a PR.

## Why run it

- **Catches rule violations early.** It checks your changes against the team's review checklists
  (UI, state/queries, tests, Playwright, general), so you fix them before a reviewer has to point
  them out.
- **Faster human review.** Reviewers can focus on design and logic instead of common issues.

## How to run it

From the repo root:

```sh
npm run code-review
```

This reviews your current branch against the default target branch and level set in
`scripts/code-review/code-review-config.json` (`run.target_branch`, `run.default_level`).

To pick the target branch and/or level yourself:

```sh
npm run code-review -- <target-branch> [low|medium|high]

# example
npm run code-review -- Sprint16 medium
```

### Prerequisites

- The `claude` CLI is installed and you are logged in .
- Your changes are committed on your branch.

### Review levels

The level controls **how much** of the review runs — it is not the severity of findings.

| Level    | What runs                                                           |
| -------- | ------------------------------------------------------------------- |
| `low`    | Triage, UI, state/queries, tests, Playwright, wrap-up, final report |
| `medium` | Everything in `low` + the general-code phase                        |
| `high`   | Everything in `medium` + a generic correctness/efficiency review    |

Higher levels take longer and cost more. A run is capped by the budget in
`code-review-config.json` (`budget.max_cost_usd`, `budget.max_tokens`) and stops if it goes over.

## How it works

1. Scripts take the diff between your branch and the target branch and
   group the changed files into categories: General, UI, State/Queries, Tests, Playwright.
2. A separate Claude run reviews each category, using only that
   category's diff and its checklist. Empty categories are skipped.
3. Checks overall design and lists the items that need attention and geneartes a report at code-review-logs/code_review_comments.md.

## Reading the results

Results are labelled by severity:

- **[HIGH]** — must be fixed. Any HIGH finding means the review **fails**.
- **[MEDIUM]** — should be fixed, but doesn't fail the review.

## After the review

1. Fix every **[HIGH]** finding. Fix **[MEDIUM]** findings or note why you're leaving them.
2. Re-run the review if you made significant changes.
3. Add the final review as a comment on your PR, as the PR checklist asks.

