# Workshop Title

<!-- TODO: Update this with your workshop details -->

This repository contains the project for a guided workshop. Visit the published site or follow the workshop steps in the `workshop/` directory.

## Start the workshop

**To begin the workshop, start at [workshop/README.md](./workshop/README.md)**

Or visit the [published workshop site](https://copilot-dev-days.github.io/REPO_NAME).

## Repository Structure

```
├── docs/           # Published HTML site (GitHub Pages)
│   ├── index.html  # Landing page
│   ├── step.html   # Step viewer (renders workshop/ markdown)
│   ├── styles.css
│   ├── light-theme.css
│   └── theme-toggle.js
├── workshop/       # Workshop content (markdown)
│   ├── README.md   # Workshop overview
│   ├── 00-prereqs.md
│   ├── 01-first-exercise.md
│   ├── 02-second-exercise.md
│   ├── 03-review.md
│   └── images/     # Screenshots and diagrams
├── .github/
│   ├── copilot-instructions.md
│   ├── instructions/
│   └── workflows/deploy.yml
├── README.md
└── LICENSE
```

## Customizing This Template

1. Update all `TODO` comments in `docs/index.html` and `docs/step.html`
2. Replace the placeholder workshop steps in `workshop/`
3. Update `REPO_NAME` references to your actual repository name
4. Add your application code alongside the workshop content

## Publishing

The workshop site deploys automatically to GitHub Pages when you push to `main`. Enable GitHub Pages in your repository settings (Settings → Pages → Source: GitHub Actions).

## License

This project is licensed under the terms of the MIT open source license. Please refer to the [LICENSE](./LICENSE) for the full terms.

## Support

This project is provided as-is, and may be updated over time. If you have questions, please open an issue.
