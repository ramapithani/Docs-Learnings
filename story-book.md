# What

Storybook is a separate workshop app where you build and view UI components outside the real app. Each saved state of a component is a story. A story is the component plus a fixed set of props, called args.

# Why

- See every state instantly: loading, empty, error, disabled, dark theme, long text.
- No backend or login needed: API data is faked with MSW.
- Catch UI bugs early, in isolation.
- Living documentation of components for the team.
- Automated tests: stories run as tests here, through Vitest and Playwright.

# How (in short)

A story file sits next to the component, named Button.stories.tsx:

```tsx
const meta: Meta<typeof Button> = { component: Button, args: { label: 'Save' } };
export default meta;

export const Primary:  Story = { args: { variant: 'primary' } };
export const Disabled: Story = { args: { disabled: true } };
```

- Default export (meta): which component, plus default props.
- Each named export: one story, meaning one state.
- Controls panel: change props live in the browser.
- Toolbar: switch theme and viewport size.

---

## Commands to run Storybook (from the repo root)

### Start Storybook (view in the browser)

| Command | What it opens | URL |
|---|---|---|
| `npm -w apps/finlease run storybook` | Finlease stories | http://localhost:6009 |
| `npm -w apps/finalyzerui run storybook` | FinalyzerUI stories | http://localhost:6006 |
| `npm -w packages/bsq-platform run storybook` | bsq-platform stories | http://localhost:6007 |
| `npm -w packages/bsq-components run storybook` | bsq-components stories | http://localhost:6008 |
| `npm run storybook` | All of the above together | each on its own port |

Add `_silent` to any of these (for example `npm -w apps/finlease run storybook_silent`) to start without opening a browser and with less log output.

### Test stories

| Command | What it does |
|---|---|
| `node scripts/storybook/test-story.js <path/to/X.stories.tsx> [StoryName]` | Tests one story file, or one story inside it. This is the closest thing to "run one file" |
| `npm -w apps/finlease run test-storybook` | Runs every finlease story as a test |
| `npm run test-storybook` | Runs story tests in every workspace |

Example:

```bash
node scripts/storybook/test-story.js apps/finlease/src/router/GuardedAdminOutlet.stories.tsx
```

### Build and check

| Command | What it does |
|---|---|
| `npm -w apps/finlease run build-storybook` | Builds a static Storybook site for finlease |
| `npm run build-storybook` | Builds static sites for all workspaces |
| `npm run validate-stories` | Checks story files for problems |
| `npm run clean:storybook-cache` | Clears the FinalyzerUI Storybook cache, useful when it acts strangely |

---

## One line to remember

Storybook = a catalogue of a component's states, each defined by its props, that you can view, tweak and test without running the real app.
