# Codex Skills Home

This repository is a Codex home snapshot that mainly tracks the `skills/` tree.

## What This Repo Contains

- `skills/`: installable and built-in Codex skills
- `skills/*/SKILL.md`: human-readable usage instructions for a skill
- `skills/*/skill.yaml`: machine-readable runtime requirements and healthcheck
- `skills/package.json`: shared Node dependencies used by some skills

Most other Codex home files are intentionally ignored by git.

## Install Location

This repo is intended to live at:

```bash
~/.codex
```


## Shared Setup

Some skills require local runtimes or tools. Install the shared dependencies you need:

```bash
# Node-based skills
cd ~/.codex/skills
npm install

# Browser automation skills
npx playwright install chromium
```

Common tools used by different skills include:

- `node`, `npm`, `npx`
- `python3`
- `git`
- `gh`
- `soffice`
- `pdftoppm`

Not every skill needs all of them.

## How To Check a Skill

Each skill declares its runtime requirements in `skill.yaml`.

Examples:

- `skills/playwright/skill.yaml`: requires `node`, `npx`, `bash`
- `skills/playwright-interactive/skill.yaml`: requires the `playwright` Node module
- `skills/doc/skill.yaml`: requires `python3`, `soffice`, `pdftoppm`, and Python packages
- `skills/gh-fix-ci/skill.yaml`: requires `gh`, `git`, and `python3`

Each skill also includes a healthcheck command. Run it from the repo root or inspect the YAML directly.

Examples:

```bash
# Check a GitHub-related skill
gh auth status

# Check the Playwright CLI skill
command -v npx && npx playwright --version

# Check Playwright interactive
node -e "import('playwright').then(() => console.log('ok')).catch(() => process.exit(1))"
```

## Playwright Notes

Some skills rely on Playwright but use it in different ways:

- `skills/playwright/` uses a wrapper script around `npx --package @playwright/cli playwright-cli`
- `skills/playwright-interactive/` imports the `playwright` Node package directly
- `skills/develop-web-game/` uses Playwright-based helper scripts during development loops

That is why `npm install` in `skills/` and `npx playwright install chromium` are the main shared setup steps.

## Git Notes

This repo is configured to track `skills/` and ignore most of the rest of the Codex home.

Ignored examples:

- local Codex state files
- logs and session files
- `__pycache__/`
- `skills/node_modules/`

