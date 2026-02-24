# Workshop Development Guidelines

This is a template workshop for GitHub Copilot Dev Days. Please follow these guidelines when contributing.

## Agent notes

- Explore the project before beginning code generation
- Create todo lists for long operations
  - Before each step in a todo list, reread the instructions to ensure you always have the right directions
- Always use instructions files when available, reviewing before generating code
- Do not generate summary markdown files upon completion of a task
- Always use absolute paths when running scripts and BASH commands
- **Do NOT commit or push changes unless explicitly instructed to do so by the user**

## Workshop content guidelines

- Workshop steps are in the `workshop/` directory as numbered markdown files
- Keep exercises focused and achievable within the stated time
- Include clear success criteria for each exercise
- Use GitHub-flavored markdown alerts (`> [!NOTE]`, `> [!TIP]`, etc.)
- Place images in `workshop/images/`

## Publishing

- The `docs/` directory contains the HTML publishing framework
- Update `docs/index.html` and `docs/step.html` when adding/removing workshop steps
- The site deploys automatically to GitHub Pages on push to `main`

## Repository Structure

- `docs/`: Published HTML site (landing page + step viewer)
- `workshop/`: Source markdown lessons (numbered `00-`, `01-`, etc.)
- `.github/workflows/deploy.yml`: GitHub Pages deployment workflow
- `.github/copilot-instructions.md`: This file — Copilot context config
- `.github/instructions/`: Language/framework-specific instruction files
