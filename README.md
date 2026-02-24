# Agentic Workflows Workshop

This repository contains the hands-on workshop for **Agentic Workflows with GitHub Copilot**. Visit the published site or follow the workshop steps in the `workshop/` directory.

## Start the workshop

**To begin the workshop, start at [workshop/README.md](./workshop/README.md)**

Or visit the [published workshop site](https://copilot-dev-days.github.io/agentic-workflows-workshop).

## Repository Structure

```
├── docs/           # Published HTML site (GitHub Pages)
│   ├── index.html  # Landing page
│   ├── step.html   # Step viewer (renders workshop/ markdown)
│   ├── styles.css
│   ├── light-theme.css
│   └── theme-toggle.js
├── workshop/       # Workshop content (markdown)
│   ├── README.md              # Workshop overview
│   ├── 00-prereqs.md          # Prerequisites & tooling
│   ├── 01-first-exercise.md   # Exercise 1 – Quick Start (gh aw init + daily digest)
│   ├── 02-second-exercise.md  # Exercise 2 – Hacker News Daily Digest
│   ├── 03-chatops-sentiment.md # Exercise 3 – ChatOps Sentiment Analysis
│   ├── 04-review.md           # Review & Next Steps
│   └── images/                # Screenshots and diagrams
├── .github/
│   ├── copilot-instructions.md
│   └── workflows/deploy.yml
├── README.md
└── LICENSE
```

## Publishing

The workshop site deploys automatically to GitHub Pages when you push to `main`. Enable GitHub Pages in your repository settings (Settings → Pages → Source: GitHub Actions).

## License

This project is licensed under the terms of the MIT open source license. Please refer to the [LICENSE](./LICENSE) for the full terms.

## Support

This project is provided as-is, and may be updated over time. If you have questions, please open an issue.
