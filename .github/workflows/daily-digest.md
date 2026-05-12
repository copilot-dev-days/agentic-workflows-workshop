---
# Trigger - when should this workflow run?
on:
  schedule: daily on weekdays
  workflow_dispatch:  # Manual trigger

# Permissions - what can this workflow access?
permissions:
  contents: read
  issues: read
  pull-requests: read

# Outputs - what APIs and tools can the AI use?
safe-outputs:
  create-issue:          # Creates issues (default max: 1)
    max: 1               # Optional: specify maximum number
---

# Daily Digest

Every weekday, create a GitHub issue that summarises all open issues
and pull requests in this repository. Group them by label. Include the
total count, the title, the author, and how long each item has been
open. Title the issue "Daily Digest – <date>".

## Instructions

Every weekday, create a GitHub issue that summarises all open issues and pull requests in this repository.

1. Fetch all open issues (excluding pull requests) and all open pull requests.
2. Group them by label. Items with no label should appear under an "Unlabelled" group.
3. For each item include: the title (as a link to the item), the author, and how long it has been open (e.g. "3 days", "2 weeks").
4. Include a total count of open issues and open pull requests at the top of the issue body.
5. Create a new GitHub issue titled `Daily Digest – <today's date in YYYY-MM-DD format>` with the formatted summary as the body.

## Notes

- Run `gh aw compile` to generate the GitHub Actions workflow
- See https://github.github.com/gh-aw/ for complete configuration options and tools documentation
