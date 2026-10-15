# Unit Test Coverage

## What is JEST

Javascript provides unit testing functions where every line of code is verified upon whether it is being executed in 
atleast one test case.

Jest, a JavaScript testing framework, provides unit testing functions. Its coverage report measures which lines of code are executed by at least one test case.

**Note:** Coverage only shows that code ran, not that it works correctly. The `expect(...)` checks in each test verify correctness.

**Test suite** is a group of test cases. Here each `.spec.tsx` test file is considered a test suite.

### `describe()` function declares all the test cases.

### `test( " ", => {})`

Takes two parameters:
1. A clear test name describing the expected behaviour.
2. A function that:
   - **Arrange:** updates the mock API response according to the test requirement
   - **Act:** renders the functional component with this data
   - **Assert:** validates the component's output by comparing it with the expected result using `expect(...)`

In this way, every statement and branch of the code is executed by changing the response of the mock API, so that each path (`if/else`, `? :`) in the functional component receives the data it needs.

## How to run unit tests

Run one test file (recommended), for example the spec you have open:

```bash
npm -w apps/finalyzerui test -- src/components/books/BookJobStatus/BookJobStatus.spec.tsx
```

Run only tests whose name matches a pattern:

```bash
npm -w apps/finalyzerui test -- --testNamePattern="my test"
```

Run a test file in another workspace:

```bash
npm -w packages/bsq-platform test -- src/path/to/file.spec.ts
npm -w packages/bsq-components test -- src/path/to/file.spec.ts
```

Run full suites (slow):

```bash
npm -w apps/finalyzerui test     # every test in the app
npm run test                     # Jest in every workspace
npm run test-ci                  # every workspace, with coverage
```

Other useful app scripts:

```bash
npm -w apps/finalyzerui run test:low-memory              # 4 GB memory limit, 2 workers
npm -w apps/finalyzerui run test:generateCoverage:html   # coverage as an HTML report
npm -w apps/finalyzerui run open-test-report             # opens logs/jest/reports/index.html
```
