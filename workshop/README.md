# Agentic Workflows Workshop

Welcome to the **Agentic Workflows** workshop! In this hands-on session you will use GitHub Copilot's agentic workflow capability (`gh aw`) to automate real-world tasks directly inside your GitHub repository — no servers, no pipelines to maintain.

## Workshop Overview

Agentic Workflows let you describe *what* you want done in plain English. Copilot figures out *how* to do it, runs the necessary tools, and posts the results back to GitHub. In this workshop you will bootstrap the tooling, build two practical workflows, and wire up a ChatOps slash command — all from the command line.

### Learning Objectives

By the end of this workshop, you will be able to:

1. **Bootstrap Agentic Workflows** — Install the `gh aw` extension and initialise it in a repository, and set up a daily digest for issues and pull requests.
2. **Build a Hacker News digest** — Create a daily workflow that surfaces relevant Hacker News stories as GitHub issues.
3. **Use the ChatOps pattern** — Implement a slash command that runs sentiment analysis on Hacker News story comments and replies inline.

## Prerequisites

Before attending this workshop, please ensure you have:

- [ ] A GitHub account with an active **Copilot Pro, Pro+, Business, or Enterprise** subscription
- [ ] **Git** installed and configured
- [ ] **GitHub CLI (`gh`)** installed and authenticated (`gh auth login`)
- [ ] Basic comfort with a terminal

> [!NOTE]
> If you are using Copilot Business or Copilot Enterprise, ensure your organisation admin has enabled **Copilot Extensions** and **Agentic Workflows** in the policy settings.

## Workshop Exercises

| Exercise | Topic | Duration |
|----------|-------|----------|
| [0. Prerequisites][ex0] | Setup & tooling | 10 min |
| [1. Quick Start][ex1] | `gh aw init` + daily issue/PR digest | 20 min |
| [2. Hacker News Digest][ex2] | Custom agentic workflow for HN stories | 20 min |
| [3. ChatOps Sentiment Analysis][ex3] | Slash command with `gh aw` ChatOps pattern | 20 min |
| [4. Review & Next Steps][ex4] | Recap and further reading | 5 min |

## Tips for Success

1. **Be specific in your prompts** — the more context you give, the better the agent performs.
2. **Read the generated workflow file** — understanding what the agent writes helps you tune it.
3. **Iterate** — if the first result isn't quite right, add constraints and re-run.
4. **Check the issue/PR it creates** — agentic workflows post their output to GitHub, so watch for new issues.

## Support

- **During the workshop**: Raise your hand or use the chat to ask questions.
- **After the workshop**: Open an issue in this repository.

---

*Happy automating with GitHub Copilot! 🤖🚀*

[ex0]: ./00-prereqs.md
[ex1]: ./01-first-exercise.md
[ex2]: ./02-second-exercise.md
[ex3]: ./03-chatops-sentiment.md
[ex4]: ./04-review.md
