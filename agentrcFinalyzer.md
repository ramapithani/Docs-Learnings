# AgentRC: General Guide

## 1. What is AgentRC?

AgentRC is an open-source tool that helps prepare software repositories for AI-assisted development. It helps AI coding assistants, such as GitHub Copilot and Claude Code, understand a project's structure, conventions, and development workflows.

In simple terms, AgentRC helps make project guidance clearer so AI assistants can work more effectively with a codebase.

## 2. How AgentRC works

AgentRC follows three main stages:

1. **Measure** — Analyze a repository's AI readiness and identify gaps in project guidance.
2. **Generate** — Create project-specific instruction files, evaluation cases, and development configuration.
3. **Maintain** — Evaluate whether instructions are useful and help identify when they may need updating.

These stages form a cycle: measure the repository, improve its guidance, and review that guidance as the project evolves.

## 3. Main commands

AgentRC can be run from a repository's root directory using `npx`. The README specifies Node.js 22 or later.

Check the environment:

```bash
node --version
npm --version
```

Check AI readiness:

```bash
npx github:microsoft/agentrc readiness
```

Initialize AgentRC:

```bash
npx github:microsoft/agentrc init
```

Generate instruction files:

```bash
npx github:microsoft/agentrc instructions
```

Evaluate instruction quality:

```bash
npx github:microsoft/agentrc eval
```

Generate an `AGENTS.md` file for multi-agent support, as described in the repository README:

```bash
npx github:microsoft/agentrc instructions --output AGENTS.md
```

Commands and options may change because AgentRC is experimental and under active development. Check the current documentation and command help before using them.

## 4. Important generated files

| File | Purpose |
|---|---|
| `.github/copilot-instructions.md` | Provides repository-specific guidance to GitHub Copilot. |
| `AGENTS.md` | Provides shared instructions for supported AI coding agents. |
| `.vscode/mcp.json` | Configures MCP server connections for supported workflows. |
| `.vscode/settings.json` | Contains VS Code settings. |
| `agentrc.eval.json` | Defines evaluation cases used to assess instruction quality. |

The files generated depend on the command, configuration, and repository. Generated content should be reviewed for accuracy before it is adopted.

## 5. Using AgentRC with an existing project

AgentRC does not need to be cloned into the target project. It can be invoked with `npx` from the root of an existing repository.

A typical workflow is:

1. Open the repository's root directory.
2. Check that Node.js 22 or later is available.
3. Run the readiness command to identify gaps.
4. Generate or initialize project guidance where appropriate.
5. Review the generated and modified files.
6. Test the instructions and commit approved changes according to the team's workflow.

For example, to analyze an existing React project:

```bash
cd /path/to/project
npx github:microsoft/agentrc readiness
```

Replace `/path/to/project` with the repository's actual local path.

## 6. How AI coding assistants use the generated instructions

AI coding assistants can use applicable instruction files as context while working in a repository. Instructions may describe:

- Project structure and architecture.
- Coding conventions and patterns.
- Existing components and utilities to reuse.
- Commands for linting, testing, and building.
- Restrictions on unrelated or risky changes.

For example, a project instruction might tell an assistant to reuse existing UI components and run relevant lint checks after modifying a component. Such instructions should reflect actual team practices; they are not guaranteed to be generated exactly this way.

Instructions guide an AI assistant but do not guarantee that every code change will be correct. Code review, tests, and other normal engineering checks remain necessary.

## 7. When should AgentRC be run again?

AgentRC does not need to be run for every coding task.

- **Initial setup:** Analyze the repository and generate or improve instructions.
- **Routine development:** The saved instructions can be used by supported AI coding assistants.
- **When conventions or architecture change:** Review and update the relevant instructions, then evaluate them as needed.
- **Ongoing maintenance:** CI workflows can be configured to help detect instruction drift.

Instructions are not automatically rewritten every time code changes unless an appropriate automation workflow is configured.

## 8. AgentRC and APM

AgentRC and APM have different roles:

- **AgentRC** generates and evaluates repository-specific AI guidance.
- **APM (Agent Package Manager)** distributes reusable instructions, skills, and prompts across repositories.

For example, AgentRC can help tailor guidance to one codebase, while APM can help share common engineering standards across a team or organization.

## 9. AgentRC and GitHub Agentic Workflows

The AgentRC repository also uses GitHub Agentic Workflows to automate maintenance tasks, such as readiness reporting, issue triage, and CI failure diagnosis.

According to the repository README, workflow definitions are written in Markdown, and `gh aw compile` generates the `.lock.yml` files used by GitHub Actions. CI checks whether the generated files remain consistent with their source definitions.

Automated findings and proposed changes still require appropriate validation and review.

## 10. Recommended practices

- Read the repository's documentation before running setup or generation commands.
- Review all generated files before committing them.
- Keep instructions concise, accurate, and aligned with the team's real conventions.
- Re-evaluate instructions when architecture, tooling, or development practices change.
- Use tests, linting, code review, and CI alongside AI-generated guidance.
- Follow organizational security and approval policies, especially when configuring MCP servers or automation.

## Summary

AgentRC helps make a software repository more suitable for AI-assisted development by measuring AI readiness, generating tailored project guidance, and evaluating whether that guidance remains useful. It can be run against an existing repository without cloning the AgentRC source code into it. Generated instructions can help AI coding assistants follow project conventions, while regular review and appropriate automation help keep those instructions accurate as the codebase evolves.
