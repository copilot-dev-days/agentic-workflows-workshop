---
name: daily-digest
on:
  schedule:
    - cron: '0 9 * * *' # daily at 09:00 UTC
description: "Daily Digest - summarize recent PR and issue activity and post to Discussions"
permissions:
  contents: read
  discussions: read
safe-outputs:
  create-discussion: null
  create-issue: null
---

# Daily Digest

This agentic workflow compiles a short summary of pull request and issue activity from the repository during the previous 24 hours and posts the summary as a new Discussion in the "Daily Digest" category (or creates an Issue when Discussions are unavailable).

## Prompt

You are an assistant that will:

- Gather PRs merged, PRs opened, and issues opened or closed in the last 24 hours.
- Produce a concise bullet-list summary including counts and 2–3 notable items with links.
- Suggest labels or next-actions when applicable.

Output MUST be a markdown-formatted body suitable for posting as a GitHub Discussion or Issue.

## Run

This workflow is intended to run on the schedule above. To run locally or on-demand use the CLI:

```bash
gh aw compile daily-digest
gh aw run daily-digest --ref main
```

## Usage

To change the publish target, edit the `permissions.discussions` and `safe-outputs` entries in this file. Keep this file as a single `.md` workflow per gh-aw guidelines.
