# Task 06: Set Up CI/CD and GitHub Pages

Configure GitHub Actions for build verification and documentation deployment.

## Context Needed

```bash
cat Makefile 2>/dev/null
ls .github/workflows/ 2>/dev/null
ls docs/ 2>/dev/null
cat package.json 2>/dev/null
```

Read: `context/project-registry.yaml` for project metadata.

## Pre-Check

If `.github/workflows/` already exists and has working workflows, audit them
rather than replacing. Only create new workflows if they're missing.

## Workflow 1: Build CI (`ci.yml`)

For C/C++ projects:

```yaml
name: CI

on:
  push:
    branches: [main, master]
  pull_request:
    branches: [main, master]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: recursive

      - name: Install dependencies
        run: |
          sudo apt-get update
          sudo apt-get install -y build-essential

      - name: Build
        run: make

      - name: Build bonus
        run: make bonus
        continue-on-error: true

      - name: Clean build
        run: |
          make fclean
          make
          make > /tmp/relink_check.txt 2>&1
          if [ -s /tmp/relink_check.txt ]; then
            echo "WARNING: Makefile relinks"
          fi
```

**Adapt for specific projects:**
- **Graphics projects** (so_long, fract-ol, cub3d): Add MiniLibX/X11 dependencies:
  ```yaml
  - name: Install dependencies
    run: |
      sudo apt-get update
      sudo apt-get install -y build-essential libx11-dev libxext-dev libbsd-dev
  ```
- **minishell**: Add readline:
  ```yaml
  - name: Install dependencies
    run: |
      sudo apt-get update
      sudo apt-get install -y build-essential libreadline-dev
  ```
- **Infrastructure projects** (inception): Use Docker-based CI:
  ```yaml
  - name: Validate docker-compose
    run: docker compose config
  ```
- **Web projects** (ft_transcendence): Use Node.js CI:
  ```yaml
  - uses: actions/setup-node@v4
    with:
      node-version: 20
  - run: npm ci
  - run: npm run build
  ```

## Workflow 2: Deploy Docs (`docs.yml`)

Only create this if `docs/` exists in the repo.

```yaml
name: Deploy Docs

on:
  push:
    branches: [main, master]
    paths:
      - 'docs/**'
      - 'README.md'

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/checkout@v4

      - name: Setup Pages
        uses: actions/configure-pages@v4

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: docs/

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

**Note:** The repo owner needs to enable GitHub Pages in the repo settings
(Settings → Pages → Source: GitHub Actions) after the workflows are merged (human commit).

## .gitignore Update

Ensure `.gitignore` exists and covers common patterns:

```gitignore
# Object files
*.o
*.d

# Libraries
*.a

# Binary (add the actual NAME from Makefile)
[binary-name]

# macOS
.DS_Store

# IDE
.vscode/
.idea/

# Environment
.env
```

If `.gitignore` already exists, only add missing patterns — don't overwrite.

## Rules

- **Don't replace working workflows** — if CI already exists and passes, leave it alone.
- **Test the workflow YAML syntax** — ensure valid YAML before the human commits.
  Run: `python3 -c "import yaml; yaml.safe_load(open('.github/workflows/ci.yml'))"` or similar.
- **Keep workflows simple** — these are small C projects, not production services.
  A build check is sufficient; no need for coverage reports, linting, or deployment pipelines.
- **Adapt to the project** — a `Dockerfile`-based project needs different CI than a C project.
  Read the project metadata from the registry to know what type of project this is.

## Quality Check

- YAML files are valid (no syntax errors)
- Workflow references correct branch name (`main` vs `master` — check `git branch`)
- CI workflow actually runs the right build command for this project
- Docs workflow only created if `docs/` directory exists
- `.gitignore` includes the actual binary name from the Makefile

## Hand off to human (git)

Do **not** commit unless the human asked you to. Provide:

```text
Suggested commit message:
ci: add build and docs deployment workflows

Files to review:
.github/workflows/
.gitignore
```
