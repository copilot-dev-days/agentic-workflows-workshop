# Exercise 1 — Quick Start with Agentic Workflows

In this exercise you will bootstrap the `gh aw` tooling in your repository and create your first agentic workflow: a **daily digest** that summarises open issues and pull requests.

**Estimated time:** 20 minutes

## Objectives

- Initialise Agentic Workflows in your repository with `gh aw init`
- Understand the files and configuration that are created
- Create and compile a daily digest workflow for issues and pull requests
- Trigger the workflow manually and read the output issue

## How Agentic Workflows Work

Agentic workflows are **natural-language markdown files** (`.github/workflows/<name>.md`) with a small YAML frontmatter block at the top. The frontmatter declares things like the trigger, required tools, and permissions. The markdown body is a plain-English prompt that instructs the AI agent what to do.

Before a workflow can run in GitHub Actions, it must be **compiled** into a lock file (`.github/workflows/<name>.lock.yml`). You commit both the `.md` (human-readable) and the `.lock.yml` (machine-readable) files.

## Part 1 — Initialise Agentic Workflows

From the root of your repository, run:

```bash
gh aw init
```

The command sets up your repository for agentic workflows. It creates several files, including:

- `.gitattributes` — marks compiled lock files as generated
- `.github/aw/github-agentic-workflows.md` — the full reference documentation
- `.github/agents/agentic-workflows.agent.md` — an AI assistant for creating and editing workflows
- `.vscode/settings.json` and `.vscode/mcp.json` — editor configuration

> [!NOTE]
> `gh aw init` requires write access to the repository. Make sure you are working in your fork.

### Inspect the Generated Files

After `init` completes, explore what was created:

```bash
git status
ls .github/aw/
ls .github/agents/
```

> [!TIP]
> The file `.github/aw/github-agentic-workflows.md` is the complete reference for all frontmatter options. Open it whenever you need to check supported triggers, tools, or permissions.

## Part 2 — Create a Daily Digest for Issues and Pull Requests

Create your first workflow using `gh aw new`:

```bash
gh aw new daily-digest
```

This opens an interactive session with the `agentic-workflows` AI agent. Describe what you want using plain English — for example:

```
Every weekday, create a GitHub issue that summarises all open issues
and pull requests in this repository. Group them by label. Include the
total count, the title, the author, and how long each item has been
open. Title the issue "Daily Digest – <date>".
```

The agent will ask clarifying questions (such as what trigger to use and whether write permissions are needed) and then generate the workflow file for you.

> [!TIP]
> You can also run `gh aw new daily-digest` non-interactively by providing your description via GitHub Copilot Chat — open Copilot Chat, type `/agent`, and select **agentic-workflows**.

### What Gets Created

After the agent finishes, you will have:

- `.github/workflows/daily-digest.md` — the human-readable workflow with YAML frontmatter and your prompt
- `.github/workflows/daily-digest.lock.yml` — the compiled machine-readable file for GitHub Actions

Open the markdown file to see what the agent wrote:

```bash
cat .github/workflows/daily-digest.md
```

The frontmatter will look similar to:

```yaml
---
name: Daily Digest
on:
  schedule: daily on weekdays
  workflow_dispatch:
permissions:
  issues: write
  contents: read
safe-outputs:
  create-issue:
    max: 1
---
```

And the body is a plain-English description of what the agent should do.

> [!NOTE]
> Agentic workflow files are regular markdown — commit them to version control just like any other code. The `.lock.yml` is auto-generated and should not be edited by hand.

## Part 3 — Trigger the Workflow Manually

Commit and push the generated files, then trigger the workflow immediately to test it:

```bash
git add .gitattributes .github/workflows/daily-digest.md .github/workflows/daily-digest.lock.yml
git commit -m "Add daily digest workflow"
git push
```

Once pushed, trigger a manual run:

```bash
gh aw run daily-digest
```

After the run completes (usually under a minute), open GitHub and check the **Issues** tab. You should see a new issue titled **Daily Digest – \<today's date\>**.

> [!NOTE]
> If the repository has no open issues or PRs yet, the digest will say so. That is expected — the workflow is still working correctly.

## Success Criteria

- [ ] `gh aw init` completed and created files in `.github/aw/` and `.github/agents/`
- [ ] `.github/workflows/daily-digest.md` exists in your repository
- [ ] `.github/workflows/daily-digest.lock.yml` exists in your repository
- [ ] The workflow was pushed and triggered without errors
- [ ] A new GitHub issue titled **Daily Digest – \<today's date\>** was created in your repository

---

Once done, proceed to [Exercise 2: Hacker News Daily Digest](./02-second-exercise.md).


