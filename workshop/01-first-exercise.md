# Exercise 1 — Quick Start with Agentic Workflows

In this exercise you will bootstrap the `gh aw` tooling in your repository and create your first agentic workflow: a **daily digest** that summarises open issues and pull requests.

**Estimated time:** 20 minutes

## Objectives

- Initialise Agentic Workflows in your repository with `gh aw init`
- Understand the files and configuration that are created
- Create and trigger a daily digest workflow for issues and pull requests
- Read the output issue produced by the agent

## Part 1 — Initialise Agentic Workflows

From the root of your repository, run:

```bash
gh aw init
```

The command will:

1. Authenticate with GitHub on your behalf (if not already authenticated)
2. Create a `.github/agentic-workflows/` directory in your repository
3. Add a default `agent.yml` configuration file
4. Push the changes to your repository

> [!NOTE]
> `gh aw init` requires write access to the repository. Make sure you are working in your fork.

### Inspect the Generated Files

After `init` completes, explore what was created:

```bash
ls -la .github/agentic-workflows/
cat .github/agentic-workflows/agent.yml
```

You will see a YAML file that defines the agent's identity, the tools it can use, and the default trigger schedule.

> [!TIP]
> The `agent.yml` file is just configuration — you can edit it by hand or by giving the agent natural language instructions later.

## Part 2 — Create a Daily Digest for Issues and Pull Requests

Now create your first workflow. Run `gh aw create` and provide a plain-English description of what you want:

```bash
gh aw create \
  --name "daily-digest" \
  --prompt "Every day at 9 AM UTC, create a GitHub issue that summarises all open issues and pull requests in this repository. Group them by label. Include the total count, the title, the author, and how long each item has been open. Title the issue 'Daily Digest – <date>'."
```

> [!TIP]
> You can also run `gh aw create` interactively (without flags) and type your prompt at the prompt.

The command generates a workflow file at `.github/agentic-workflows/daily-digest.yml`. Open it:

```bash
cat .github/agentic-workflows/daily-digest.yml
```

Read through the generated YAML. Notice how the agent has translated your plain-English description into concrete steps: fetching issues and PRs via the GitHub API, formatting the output, and creating an issue.

## Part 3 — Trigger the Workflow Manually

You do not have to wait until 9 AM to test your workflow. Trigger it immediately:

```bash
gh aw run daily-digest
```

After a few seconds (up to a minute for the first run) you will see output like:

```
✓ Workflow "daily-digest" triggered
  Run ID: aw-abc123
  Watching run... done.
  ✓ Issue created: https://github.com/<org>/<repo>/issues/1
```

Open the link in your browser and confirm the digest issue looks correct.

> [!NOTE]
> If the repository has no open issues or PRs yet, the digest will say so. That is expected — the workflow is still working correctly.

## Success Criteria

- [ ] `.github/agentic-workflows/agent.yml` exists in your repository
- [ ] `.github/agentic-workflows/daily-digest.yml` exists in your repository
- [ ] Running `gh aw run daily-digest` completes without errors
- [ ] A new GitHub issue titled **Daily Digest – \<today's date\>** was created in your repository

---

Once done, proceed to [Exercise 2: Hacker News Daily Digest](./02-second-exercise.md).

