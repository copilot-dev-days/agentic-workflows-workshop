# Exercise 2 — Hacker News Daily Digest

In this exercise you will create an agentic workflow that automatically pulls top Hacker News stories relevant to professional software engineers and posts them as a daily GitHub issue.

**Estimated time:** 20 minutes

## Objectives

- Write a richer, more targeted natural-language prompt for an agentic workflow
- Understand how the agent fetches data from an external API (Hacker News)
- Inspect and refine the generated workflow markdown
- Validate that the output issue is useful and well-structured

## Background

The [Hacker News API](https://hacker-news.firebaseio.com/v0/) is public and does not require authentication. It exposes endpoints like:

- `GET /v0/topstories.json` — returns up to 500 top story IDs
- `GET /v0/item/<id>.json` — returns the details of a single item (story, comment, etc.)

Your agentic workflow will call these endpoints, filter results, and format them into a readable GitHub issue.

## Part 1 — Create the Workflow

Create the workflow with `gh aw new`:

```bash
gh aw new hn-daily-digest
```

When the interactive agent session opens, provide the following description:

```
Create a daily digest workflow for professional developers, referencing
relevant top Hacker News stories on technology that can be used today
by large companies. Every weekday, fetch the top 30 stories from the
Hacker News API (https://hacker-news.firebaseio.com/v0/topstories.json),
filter to stories with a score above 100 that are about software
engineering, cloud infrastructure, AI/ML, developer tooling, or
distributed systems. For each qualifying story include: the title, the
URL, the score, the number of comments, and a one-sentence summary of
why it is relevant to enterprise developers. Create a GitHub issue
titled "HN Digest – <date>" with the results formatted as a Markdown
table.
```

The agent will confirm the trigger (weekday schedule), required tools (`web-fetch`, `github`), permissions (`issues: write`), and the network allowlist (the HN API domain), then generate the workflow files.

> [!TIP]
> You can also describe the workflow in GitHub Copilot Chat by typing `/agent` and selecting **agentic-workflows** — the agent will guide you through a conversational setup.

## Part 2 — Review and Refine the Workflow

Open the generated workflow file:

```bash
cat .github/workflows/hn-daily-digest.md
```

The file has two parts:

**YAML frontmatter** (between `---` markers) — configuration that requires recompilation:

```yaml
---
name: HN Daily Digest
on:
  schedule: daily on weekdays
  workflow_dispatch:
permissions:
  issues: write
  contents: read
network:
  - hacker-news.firebaseio.com
tools:
  - web-fetch
safe-outputs:
  create-issue:
    max: 1
---
```

**Markdown body** (after the frontmatter) — the plain-English instructions you gave to the agent. You can edit the body directly on GitHub.com or in any editor and your changes will take effect on the next run, **without recompiling**.

> [!NOTE]
> If you want to change the trigger, tools, permissions, or network rules (the frontmatter), you need to recompile: `gh aw compile hn-daily-digest`.

### Things to Check

1. **Network allowlist** — does the frontmatter include `hacker-news.firebaseio.com`? The agent needs network access to call the HN API.
2. **Schedule** — does it use fuzzy scheduling (`daily on weekdays`) rather than a fixed cron? Fuzzy scheduling is preferred because it distributes load and automatically adds `workflow_dispatch` for manual runs.
3. **Prompt body** — does the body clearly describe the filtering criteria and the desired output format?

If you want to adjust the prompt, simply edit the markdown body and the change takes effect on the next run. To update the frontmatter (e.g., add a network domain), edit the frontmatter and recompile:

```bash
gh aw compile hn-daily-digest
```

## Part 3 — Commit and Run the Workflow

Commit and push both the markdown and the lock file:

```bash
git add .github/workflows/hn-daily-digest.md .github/workflows/hn-daily-digest.lock.yml
git commit -m "Add HN daily digest workflow"
git push
```

Then trigger a manual run:

```bash
gh aw run hn-daily-digest
```

Wait for the run to complete, then open GitHub and check the **Issues** tab.

### What to Check

- The issue title contains today's date.
- The issue body is a Markdown table with story titles, URLs, scores, and comment counts.
- The stories are genuinely relevant to enterprise software development (not general news or politics).

> [!TIP]
> If the output looks good but the formatting is off, edit the markdown body of `.github/workflows/hn-daily-digest.md` to add a specific output template, then push and re-run — no recompilation needed.

## Success Criteria

- [ ] `.github/workflows/hn-daily-digest.md` exists in your repository
- [ ] `.github/workflows/hn-daily-digest.lock.yml` exists in your repository
- [ ] The workflow frontmatter includes `hacker-news.firebaseio.com` in the network allowlist
- [ ] The workflow uses fuzzy scheduling (`daily on weekdays`)
- [ ] A GitHub issue titled **HN Digest – \<today's date\>** was created with a Markdown table of stories

---

Once done, proceed to [Exercise 3: ChatOps Sentiment Analysis](./03-chatops-sentiment.md).


