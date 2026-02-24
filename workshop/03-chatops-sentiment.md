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

Run `gh aw create` with the following prompt:

```bash
gh aw create \
  --name "hn-sentiment" \
  --trigger "issue_comment" \
  --prompt "Create a ChatOps slash command called /hn-sentiment. When a user posts a comment on a GitHub issue containing '/hn-sentiment <url>' where <url> is a Hacker News story URL (e.g. https://news.ycombinator.com/item?id=12345), do the following: 1) Extract the Hacker News item ID from the URL. 2) Fetch up to 50 top-level comments for that story from the Hacker News API (https://hacker-news.firebaseio.com/v0/item/<id>.json, recursively fetching kids). 3) Perform sentiment analysis on the comment text, classifying each comment as Positive, Negative, or Neutral. 4) Produce a summary that shows: the overall sentiment (with percentage breakdown), the top 3 most positive comments (with excerpt), and the top 3 most negative comments (with excerpt). 5) Reply to the original issue comment with the analysis formatted in Markdown. If no URL is provided or the URL is not a valid Hacker News item, reply with a helpful error message."
```

Inspect the generated file:

```bash
cat .github/agentic-workflows/hn-sentiment.yml
```

> [!NOTE]
> The `--trigger issue_comment` flag tells `gh aw` to generate a workflow that listens for `issue_comment` events rather than running on a schedule.

## Part 2 — Review the Generated Workflow

Open `.github/agentic-workflows/hn-sentiment.yml` and find:

1. **Trigger** — The `on: issue_comment` section with a condition that checks for the `/hn-sentiment` prefix.
2. **Command parsing** — How the agent extracts the Hacker News URL from the comment body.
3. **API calls** — The steps that fetch the story and its comments from the Hacker News API.
4. **Sentiment logic** — How sentiment is classified (look for a prompt or a call to a model).
5. **Reply step** — The step that posts the result back to the issue using the GitHub API.

> [!TIP]
> If the generated workflow does not include a comment-body check (to avoid running on every comment), add a condition like:
> ```yaml
> if: contains(github.event.comment.body, '/hn-sentiment')
> ```

## Part 3 — Push the Workflow

Commit and push the new workflow file so GitHub can act on it:

```bash
git add .github/agentic-workflows/hn-sentiment.yml
git commit -m "Add hn-sentiment ChatOps slash command"
git push
```

> [!IMPORTANT]
> The `issue_comment` trigger only fires when the workflow file is on the **default branch** of the repository (usually `main`). Make sure you push to `main` (or merge a PR into `main`) before testing.

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
| Agent doesn't reply | Check that the workflow file is on the default branch and that the trigger condition matches. |
| "Item not found" error | Verify the Hacker News item ID is correct and the story is not deleted. |
| Empty comments list | Some stories have no top-level comments fetched yet; try a story with 50+ comments. |
| Permission denied | Ensure the `GITHUB_TOKEN` in the workflow has `issues: write` permission. |

## Success Criteria

- [ ] `.github/agentic-workflows/hn-sentiment.yml` exists and is pushed to `main`
- [ ] Posting `/hn-sentiment <hn-url>` in a GitHub issue triggers the workflow
- [ ] The agent replies with a sentiment analysis breakdown
- [ ] The reply includes positive and negative comment excerpts

---

Once done, proceed to [Review & Next Steps](./04-review.md).
