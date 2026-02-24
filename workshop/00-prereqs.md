# Prerequisites

Before starting this workshop, make sure you have the following set up.

## Required Accounts & Subscriptions

- [ ] **GitHub Account** with an active Copilot subscription (**Pro, Pro+, Business, or Enterprise**)
- [ ] Copilot Extensions enabled — check *Settings → Copilot → Extensions* in your GitHub account (or ask your org admin)

## Required Tools

- [ ] **Git** — [install guide](https://git-scm.com/downloads)
- [ ] **GitHub CLI (`gh`)** v2.40 or later — [install guide](https://cli.github.com/)
- [ ] **Node.js** v18 or later (used by some workflow steps) — [install guide](https://nodejs.org/)

### Verify the GitHub CLI

```bash
gh --version
```

You should see `gh version 2.x.x` or higher.

### Authenticate with GitHub

If you haven't already authenticated the CLI, run:

```bash
gh auth login
```

Follow the prompts and choose **GitHub.com** → **HTTPS** → **Login with a web browser**.

After logging in, verify it worked:

```bash
gh auth status
```

You should see `✓ Logged in to github.com`.

## Install the Agentic Workflows Extension

The `gh aw` CLI extension is installed via its own setup script:

```bash
curl -sL https://raw.githubusercontent.com/github/gh-aw/main/install-gh-aw.sh | bash
```

This downloads and installs the `gh-aw` binary into `~/.local/share/gh/extensions/gh-aw/`.

> [!TIP]
> To review the script before running it, open `https://raw.githubusercontent.com/github/gh-aw/main/install-gh-aw.sh` in your browser first.

Verify the extension is available:

```bash
gh aw version
```

> [!TIP]
> If `gh aw version` shows "unknown command", verify GitHub CLI is installed with `gh --version`, then re-run the installation script.

## Fork or Clone This Repository

This workshop uses a GitHub repository as the workspace for all agentic workflows.

1. **Fork** this repository on GitHub (click **Fork** in the top-right corner), or
2. **Clone** your fork locally:

```bash
gh repo clone <your-username>/agentic-workflows-workshop
cd agentic-workflows-workshop
```

> [!NOTE]
> All `gh aw` commands must be run from inside a Git repository that is linked to a GitHub remote. The commands above ensure that is the case.

## Verify Your Setup

Run the following checklist to confirm everything is ready:

```bash
git --version          # Should print: git version 2.x.x
gh --version           # Should print: gh version 2.x.x
gh auth status         # Should print: ✓ Logged in to github.com
gh aw version          # Should print the aw extension version
```

> [!IMPORTANT]
> If any of the checks fail, resolve them before proceeding. Ask a facilitator for help if needed.

---

Once everything is set up, proceed to [Exercise 1: Quick Start](./01-first-exercise.md).

