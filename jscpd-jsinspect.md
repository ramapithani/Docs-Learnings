# jscpd and jsinspect

## jscpd & jsinspect: Revision Notes

### What they are

**Both tools detect duplicated code in the codebase.**

| Tool      | How it compares                               | Catches                                      |
| --------- | --------------------------------------------- | -------------------------------------------- |
| jscpd     | Tokens (keywords, names, symbols, values)     | Copy-pasted blocks (min 5 lines / 20 tokens) |
| jsinspect | Code structure (AST), the "shape" of the code | Same structure even if formatting differs    |

**Why:** if duplicated code has a bug, you have to fix it in every copy. Shared code means you fix it once.

## How the gate works

* The existing duplications are saved in baseline files: `jscpd-baseline.json` and `jsinspect-baseline.json`.
* scripts-orchestrator runs both tools and compares the results to the baselines.
* Old duplications → OK. New duplications → the orchestrator fails.
* ⚠️ **"New" means a file pair + line count that isn't in the baseline.** If you shrink an old d
  uplication (for example 10 lines → 9), it looks "new" even though it isn't.

## When it fails

1. Read the output. It shows which files and lines are duplicated.

2. Can it be fixed sensibly? → Fix it. Move the shared code into a shared function or component, and pass in the parts that differ as props.

3. Not worth fixing? (very small, test/mock data, or fixing it breaks another rule) → update the baselines:

   ```sh
   npm run update_jscpd
   ```

   ```sh
   npm run update_jsinspect
   ```

4. Always commit the baseline in the same commit as the code change. check-jscpd-baseline-edit fails if the baseline changes on its own.

## Useful commands

```sh
npm run jscpd
```

Check for new duplications.

```sh
npm run jsinspect
```

Check for new structural duplications.

```sh
node scripts/duplication/list-new-jscpd-duplications.mjs 25
```

Top 25 biggest duplications.

```sh
npm run open-jscpd-report
```

Visual HTML report.

## Lessons from my first fix

* Pick an easy first target: small, display-only code, with a shared file already available.
* Fixing one duplication can create smaller new ones. Check again after each change.
* Write props as constants, not inline `sx={{...}}` (lint rule: no-inline-jsx-expressions).
* `../` imports are not allowed. Use aliases like `@bsq/platform/...`.
* Passing styles as one prop can make find-unused-scss-module-classes think a CSS class is unused.
* Don't fight tooling over tiny leftovers. Fix the big duplication, accept the small rest in the baseline, and explain it in the PR.

---
