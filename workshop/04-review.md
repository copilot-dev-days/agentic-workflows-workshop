# Review & Next Steps

Congratulations on completing the Agentic Workflows workshop! 🎉🤖

## What You Learned

In this workshop, you:

1. **Bootstrapped Agentic Workflows** — Installed `gh aw`, ran `gh aw init`, and set up a daily digest of issues and pull requests.
2. **Built a Hacker News Digest** — Wrote a targeted prompt that fetches top HN stories, filters by relevance, and creates a formatted GitHub issue on a daily schedule.
3. **Implemented a ChatOps Slash Command** — Used the ChatOps pattern to create `/hn-sentiment`, which fetches and analyses the sentiment of Hacker News story comments and replies inline.

## Key Takeaways

- **Prompts are code** — The prompt you write determines the quality of the generated workflow. Be specific about data sources, filtering criteria, output format, and schedule.
- **Workflows live in Git** — All agentic workflow YAML files live in `.github/agentic-workflows/` and are version-controlled. Review and improve them like any other code.
- **ChatOps keeps context in GitHub** — Slash commands triggered by issue comments mean your team never has to leave GitHub to run an agent.
- **Iterate quickly** — `gh aw run <name>` lets you test any workflow instantly without waiting for a scheduled trigger.

## Continue Your Learning

- 📖 [Agentic Workflows Quick Start](https://github.github.com/gh-aw/setup/quick-start/) — the official guide this workshop is based on
- 🔌 [ChatOps Pattern Reference](https://github.github.com/gh-aw/patterns/chat-ops/) — full documentation for the slash-command pattern
- 🤖 [GitHub Copilot Documentation](https://docs.github.com/en/copilot) — everything Copilot
- 🌟 [Awesome Copilot](https://github.com/github/awesome-copilot) — community resources and examples
- 💬 [GitHub Community Discussions](https://github.com/orgs/community/discussions) — ask questions and share ideas

## Ideas for Further Exploration

Try extending what you built today:

- **Customise the HN digest** — Add a category breakdown (AI, cloud, open-source, etc.) or link to the top story of the week.
- **Expand the sentiment command** — Return a word-cloud of the most common terms, or compare sentiment across two HN threads.
- **Add more slash commands** — Try `/summarise-pr <url>` to get an AI summary of a pull request posted as a comment.
- **Connect to other APIs** — Swap Hacker News for Reddit, Dev.to, or an internal Jira board.

## Feedback

We'd love to hear your feedback! Please share your thoughts with the workshop facilitators or open an issue in this repository.

---

*Thank you for participating! Happy automating with GitHub Copilot! 🚀*
