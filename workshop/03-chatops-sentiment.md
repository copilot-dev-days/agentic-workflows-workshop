# Exercise 3 — ChatOps: Sentiment Analysis Slash Command

In this exercise you will use the **ChatOps pattern** to create a slash command that performs sentiment analysis on the comments of a Hacker News story. A team member pastes the URL of a Hacker News story as a comment on a GitHub issue, the agent fetches and analyses the comments, and then replies directly in the thread.

**Estimated time:** 20 minutes

## Objectives

- Understand the ChatOps pattern for agentic workflows
- Create a slash command (`/hn-sentiment`) triggered by an issue comment
- Have the agent fetch Hacker News comments, run sentiment analysis, and reply inline
- Test the command end-to-end in a real GitHub issue

## Background: The ChatOps Pattern

The ChatOps pattern lets team members trigger agentic workflows by posting a **slash command** in a GitHub issue or pull request comment. The pattern works like this:

1. A user posts a comment containing a slash command and arguments (e.g., `/hn-sentiment https://news.ycombinator.com/item?id=12345`).
2. GitHub fires an `issue_comment` webhook event.
3. The agentic workflow detects the slash command, extracts the arguments, runs its logic, and posts the result as a reply in the same thread.

This is powerful because it keeps context inside GitHub — no need to switch to a separate tool.

For more details, see the [ChatOps pattern documentation](https://github.github.com/gh-aw/patterns/chat-ops/).

## Part 1 — Create the Slash Command Workflow

Create the workflow with `gh aw new`:

```bash
gh aw new hn-sentiment
```

When the interactive session opens, describe what you want:

```
Create a ChatOps slash command called /hn-sentiment. When a user posts
a comment on a GitHub issue that starts with "/hn-sentiment <url>",
where <url> is a Hacker News story URL (e.g.
https://news.ycombinator.com/item?id=12345), do the following:
1) Extract the Hacker News item ID from the URL.
2) Fetch up to 50 top-level comments for that story from the Hacker
   News API.
3) Perform sentiment analysis on the comment text, classifying each
   comment as Positive, Negative, or Neutral.
4) Produce a summary that shows: the overall sentiment (with percentage
   breakdown), the top 3 most positive comments (with excerpt), and
   the top 3 most negative comments (with excerpt).
5) Reply to the original issue comment with the analysis formatted in
   Markdown.
If no URL is provided or the URL is not a valid Hacker News item,
reply with a helpful error message.
```

The agent will configure:
- **Trigger**: `issue_comment` with a condition that filters for comments starting with `/hn-sentiment`
- **Tools**: `web-fetch` to call the Hacker News API
- **Network**: `hacker-news.firebaseio.com` in the allowlist
- **Safe outputs**: `add-comment` to reply to the issue

## Part 2 — Review the Generated Workflow

Open the generated file:

```bash
cat .github/workflows/hn-sentiment.md
```

The frontmatter will look similar to:

```yaml
---
name: HN Sentiment Analysis
on:
  issue_comment:
    types: [created]
    if: startsWith(github.event.comment.body, '/hn-sentiment')
permissions:
  issues: write
  contents: read
network:
  - hacker-news.firebaseio.com
tools:
  - web-fetch
safe-outputs:
  add-comment:
    max: 1
---
```

Things to verify:

1. **Trigger condition** — the `if:` clause filters so the workflow only runs when someone types `/hn-sentiment`, not on every comment.
2. **Network allowlist** — `hacker-news.firebaseio.com` must be listed so the agent can fetch story comments.
3. **Safe output** — `add-comment` is declared so the agent can post the analysis back to the issue.
4. **Prompt body** — the markdown body describes how to parse the URL, call the API, classify sentiment, and format the reply.

> [!TIP]
> You can edit the markdown body of `.github/workflows/hn-sentiment.md` directly (on GitHub.com or locally) without recompiling. For example, you can tweak the output template or adjust how excerpts are formatted.

## Part 3 — Compile, Commit, and Push

If the agent did not compile the workflow automatically, compile it now:

```bash
gh aw compile hn-sentiment
```

Commit and push both the markdown and the lock file:

```bash
git add .github/workflows/hn-sentiment.md .github/workflows/hn-sentiment.lock.yml
git commit -m "Add hn-sentiment ChatOps slash command"
git push
```

> [!IMPORTANT]
> The `issue_comment` trigger only fires when the workflow lock file is on the **default branch** of the repository (usually `main`). Make sure you push to `main` (or merge a PR into `main`) before testing.

## Part 4 — Test the Slash Command

1. Open any issue in your repository (or create a new one titled "Testing ChatOps").
2. Post a comment with a real Hacker News story URL, for example:

   ```
   /hn-sentiment https://news.ycombinator.com/item?id=40942509
   ```

   > [!TIP]
   > To find a good story to test with, open [Hacker News](https://news.ycombinator.com/) and pick any story that has 50+ comments. Copy the URL from the browser address bar.

3. Wait 20–60 seconds. The agentic workflow will run in the background.
4. Refresh the issue page. You should see a new comment from the agent containing:
   - An overall sentiment score (% Positive / Negative / Neutral)
   - A table or list of the top positive and negative comment excerpts
   - The story title for context

### Example Expected Output

```markdown
## 🔍 Hacker News Sentiment Analysis

**Story:** Why We Moved From Kubernetes to Nomad

| Sentiment | Count | Percentage |
|-----------|-------|------------|
| 😊 Positive | 23 | 46% |
| 😐 Neutral  | 18 | 36% |
| 😠 Negative |  9 | 18% |

**Overall: Mostly Positive**

### Top Positive Comments
> "This is exactly what we needed at our company — the operational simplicity of Nomad is underrated."

### Top Negative Comments
> "I don't see how this scales beyond a few hundred nodes."
```

## Troubleshooting

| Problem | Solution |
|---------|---------|
| Agent doesn't reply | Check that the lock file is on the default branch and that the trigger condition matches. |
| "Item not found" error | Verify the Hacker News item ID is correct and the story is not deleted. |
| Empty comments list | Some stories have no top-level comments fetched yet; try a story with 50+ comments. |
| Permission denied | Ensure `issues: write` is in the workflow frontmatter and the lock file is recompiled. |

## Success Criteria

- [ ] `.github/workflows/hn-sentiment.md` exists and is pushed to `main`
- [ ] `.github/workflows/hn-sentiment.lock.yml` exists and is pushed to `main`
- [ ] Posting `/hn-sentiment <hn-url>` in a GitHub issue triggers the workflow
- [ ] The agent replies with a sentiment analysis breakdown
- [ ] The reply includes positive and negative comment excerpts

---

Once done, proceed to [Review & Next Steps](./04-review.md).

