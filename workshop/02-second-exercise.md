# Exercise 2 — Hacker News Daily Digest

In this exercise you will create an agentic workflow that automatically pulls top Hacker News stories relevant to professional software engineers and posts them as a daily GitHub issue.

**Estimated time:** 20 minutes

## Objectives

- Write a richer, more targeted prompt for an agentic workflow
- Understand how the agent fetches data from an external API (Hacker News)
- Customise the generated workflow to adjust content and formatting
- Validate that the output issue is useful and well-structured

## Background

The [Hacker News API](https://hacker-news.firebaseio.com/v0/) is public and does not require authentication. It exposes endpoints like:

- `GET /v0/topstories.json` — returns up to 500 top story IDs
- `GET /v0/item/<id>.json` — returns the details of a single item (story, comment, etc.)

Your agentic workflow will call these endpoints, filter results, and format them into a readable GitHub issue.

## Part 1 — Create the Workflow

Run `gh aw create` with the following prompt. Copy it exactly — the detail helps the agent produce a high-quality result:

```bash
gh aw create \
  --name "hn-daily-digest" \
  --prompt "Create a daily digest workflow for professional developers, referencing relevant top Hacker News stories on technology that can be used today by large companies. Every day at 8 AM UTC, fetch the top 30 stories from the Hacker News API (https://hacker-news.firebaseio.com/v0/topstories.json), filter to stories with a score above 100 that are about software engineering, cloud infrastructure, AI/ML, developer tooling, or distributed systems. For each qualifying story include: the title, the URL, the score, the number of comments, and a one-sentence summary of why it is relevant to enterprise developers. Create a GitHub issue titled 'HN Digest – <date>' with the results formatted as a Markdown table."
```

> [!TIP]
> You can always edit the resulting YAML file manually. Think of `gh aw create` as a fast first draft — iterate from there.

Inspect the generated file:

```bash
cat .github/agentic-workflows/hn-daily-digest.yml
```

## Part 2 — Review and Refine the Workflow

Open `.github/agentic-workflows/hn-daily-digest.yml` in your editor and look for the following:

1. **Data fetching step** — how does the agent call the Hacker News API?
2. **Filtering logic** — how does the agent decide which stories are relevant?
3. **Issue creation step** — what does the issue body look like?

If you want to adjust the prompt (for example, to change the score threshold or add more topic categories), edit the `prompt:` field in the YAML or re-run `gh aw create` with an updated `--prompt`.

> [!NOTE]
> Agentic workflow YAML files are regular text files — commit them to version control just like any other code. Other team members can review, adjust, and improve them via pull requests.

## Part 3 — Run the Workflow

Trigger the workflow immediately to test it:

```bash
gh aw run hn-daily-digest
```

Wait for the run to complete, then open the created issue in your browser.

### What to Check

- The issue title contains today's date.
- The issue body is a Markdown table with story titles, URLs, scores, and comment counts.
- The stories are genuinely relevant to enterprise software development (not general news or politics).

> [!TIP]
> If the output looks good but the formatting is off, add a note to the `prompt:` field asking for a specific Markdown structure, then re-run.

## Part 4 — Schedule It

Confirm that the workflow is scheduled to run at 8 AM UTC daily. Check the `schedule:` section of `.github/agentic-workflows/hn-daily-digest.yml`. It should look similar to:

```yaml
schedule:
  cron: "0 8 * * *"
```

If it is missing or different, update it manually.

## Success Criteria

- [ ] `.github/agentic-workflows/hn-daily-digest.yml` exists in your repository
- [ ] Running `gh aw run hn-daily-digest` completes without errors
- [ ] A GitHub issue titled **HN Digest – \<today's date\>** was created
- [ ] The issue contains a table of Hacker News stories with scores, URLs, and relevance notes
- [ ] The workflow is scheduled to run at 8 AM UTC daily

---

Once done, proceed to [Exercise 3: ChatOps Sentiment Analysis](./03-chatops-sentiment.md).

