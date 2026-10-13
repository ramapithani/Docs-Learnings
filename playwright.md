## Why?

We use [playwright](https://playwright.dev/) to simulate user interactions in a real browser environment (e.g., navigation, form submissions, API calls, etc.)

## Run Playwright tests

1. Start the app in dev mode (from the repo root). The tests run against http://localhost:5173:

   ```sh
   npm run dev
   ```

2. In a second terminal, go to the app folder. All the commands below run from here:

   ```sh
   cd apps/finalyzerui
   ```

3. Install the browsers (only needed once):

   ```sh
   npx playwright install
   ```

4. Pick how you want to run the tests.

   **UI mode opens a window where you can pick tests, run them and watch each step:**

   ```sh
   npm run playwright
   ```

   **One test file (fastest):**

   ```sh
   npm run playwright:dev -- playwright/path/to/file.spec.ts
   ```

   **Tests whose name matches:**

   ```sh
   npm run playwright:dev -- --grep "test name"
   ```

   **One browser only:**

   ```sh
   npm run playwright:dev -- playwright/path/to/file.spec.ts --project=chromium
   ```

   **See the browser while the test runs:**

   ```sh
   npm run playwright:dev -- playwright/path/to/file.spec.ts --headed
   ```

   **Debug step by step:**

   ```sh
   npm run playwright:dev -- --debug
   ```

5. Run tests in CI mode (the same way CI runs them).

   **All tests (slow):**

   ```sh
   npm run playwright_ci
   ```

   **One group only:**

   ```sh
   npm run playwright_ci:books
   ```

   The other groups are admin, reports, user, common, edit_mode, access_control and other.

   **Re-run only the tests that failed last time:**

   ```sh
   npm run playwright_ci:failures
   ```

### Tips

* Don't run two Playwright suites at the same time.
* If a test keeps showing old mock data after you edit a mock, restart the dev server.
* If reports or filter tests are missing in UI mode, open the Projects dropdown and tick chromium-platform-specs.

## Record a new Playwright test

1. Start the app in dev mode (from the repo root):

   ```sh
   npm run dev
   ```

2. In a second terminal, start the Playwright **code generator**. It opens a browser and writes test code for the interactions performed with the website:

   ```sh
   npx playwright codegen http://localhost:5173/react/login
   ```

3. Copy the generated code into a new `.spec.ts` file and clean it up:

   * Add the import: `import { test, expect } from '@playwright/test';`
   * Give the test and its variables clear names.
   * Add assertions (`expect(...)`). Codegen records only actions but not the validations and checks.

   A good test follows this flow: **check the element exists → do the user action → assert the result**.

4. Run the new test to make sure it passes (from `apps/finalyzerui`):

   ```sh
   npm run playwright:dev -- <your-file>.spec.ts
   ```
