# ESLint rules

## What is ESLint?

ESLint is a tool that reads our code without running it and points out problems, like a spell-checker for code.

ESLint only catches mistakes while you're writing if your editor has the ESLint extension, as in VS Code. 
Without it, you only see the problems when you run the lint command.

When we write code, ESLint reads it and warns us like : "line 42 has a problem" It catches mistakes while we're writing, 
before they become failures in the code-review or scripts-orchestrator check stage.

## What are ESLint rules?

A rule is one specific check. Each rule looks for one kind of bad pattern or a mistake. 
Some examples:
 no-unused-vars : You created a variable but never used it  
 custom-rules/no-hardcoded-literals : You typed text like "Save" directly instead of using a translation t('save')
 custom-rules/no-direct-component-usage : You used MUI Button instead of our BsqButton

Rules are both pre-defined and programmer-defined.
1. Built into ESLint: general JavaScript checks.
2. Plugins: rules other people wrote for React, TypeScript, accessibility, testing, and so on.
3. Custom rules: rules our team wrote for this project, in eslint/eslint-rules/. 

Severity: how strict a rule is

Each rule is given a level in the config files (Eg : eslint/code.config.js, eslint/tests.config.js):

- error: must be fixed. CI fails if it isn't.
- warn: you should fix it, but it won't block you.
- off: the rule is turned off.


Different files use different configs

Each kind of file is checked with its own set of rules:

┌──────────────────────────────────┬─────────────────────────────┐
│            File type             │           Config            │
├──────────────────────────────────┼─────────────────────────────┤
│ Normal code (.ts, .tsx)          │ eslint/code.config.js       │
├──────────────────────────────────┼─────────────────────────────┤
│ Unit tests (.spec.ts, .spec.tsx) │ eslint/tests.config.js      │
├──────────────────────────────────┼─────────────────────────────┤
│ Storybook stories (.stories.tsx) │ eslint/stories.config.js    │
├──────────────────────────────────┼─────────────────────────────┤
│ Playwright tests                 │ eslint/playwright.config.js │
├──────────────────────────────────┼─────────────────────────────┤
│ Form configs (*Form.config.ts)   │ eslint/formconfig.config.js │
├──────────────────────────────────┼─────────────────────────────┤
│ Themes                           │ eslint/themes.config.js     │
├──────────────────────────────────┼─────────────────────────────┤
│ Mocks (__mocks__)                │ eslint/mocks.config.js      │
└──────────────────────────────────┴─────────────────────────────┘

## How to run es-lint

npm run lint-ci          # whole project 
npm run lint-ci:fix      # same along with auto-fixes what it can

Linting the whole project is slow, so check just the file you changed:

npx eslint apps/finalyzerui/src/path/to/file.ts --config eslint/code.config.js.    
npx eslint apps/finalyzerui/src/path/to/file.spec.ts --config eslint/tests.config.js

Add --fix to auto-fix what it can.

More commands

npm run lint:pr          # lint only the files changed in your branch
npm run lint:code        # only normal code files
npm run lint:tests       # only test files

Things to know about lint-ci

- It runs a Prettier format check first, so badly formatted code also fails it.
- It uses --quiet, so it shows errors only, not warnings.
- --fix can't fix everything. Some problems you have to fix by hand.

ESLint vs Prettier

- ESLint checks for code problems, like bad patterns and bugs.
- Prettier checks formatting, like spaces, quotes and line breaks.
- Fix formatting with npx prettier --write path/to/file.ts instead of editing it by hand.

Turning off a rule for one line (use rarely)

If a rule is wrong for one particular line, you can switch it off for that line only:

// eslint-disable-next-line custom-rules/no-hardcoded-literals -- reason here
const x = 'abc';

Rules for doing this:
- Always name the rule. A bare // eslint-disable is not allowed.
- Only switch it off for one line, with eslint-disable-next-line or eslint-disable-line. Turning a rule off for a whole file or block is not allowed.
- After --, write why you're doing it.
- Remove the comment once it's no longer needed. ESLint flags a disable comment that doesn't suppress anything.
