# 42-pipeline

Single source of truth for the 42 School project pipeline prompts.

Reusable prompt system for automating documentation, CI/CD, and blog post generation
across 42 School project repositories.

## Quick Start

### From Desktop (Cursor / Claude Code)

When working on any 42 School project repo locally, point at the 42-pipeline clone:

```
Read and follow orchestrator.md from the 42-pipeline repo for this repository.
```

Example absolute path:

```
Read and follow /Users/manuel-sousa/Code/Business/42-pipeline/orchestrator.md for this repository.
```

### From Mobile (Claude Code Cloud)

Cloud sessions only see the **connected** repo. Use raw GitHub URLs to fetch prompts from this public repository.

When starting a session on a project repo, paste (replace `main` if your default branch differs):

```
Fetch and follow the orchestrator prompt from:
https://raw.githubusercontent.com/mlrcbsousa/42-pipeline/main/orchestrator.md

For context files, fetch from the same repo:
- https://raw.githubusercontent.com/mlrcbsousa/42-pipeline/main/context/project-registry.yaml
- https://raw.githubusercontent.com/mlrcbsousa/42-pipeline/main/context/42-school-conventions.md
- https://raw.githubusercontent.com/mlrcbsousa/42-pipeline/main/context/blog-style-guide.md
- https://raw.githubusercontent.com/mlrcbsousa/42-pipeline/main/context/GITHUB-VERIFICATION.md

For each sub-task referenced by the orchestrator, fetch from:
https://raw.githubusercontent.com/mlrcbsousa/42-pipeline/main/tasks/<filename>

Apply all instructions to the current repository.
```

### Run a Single Task

```
Fetch and follow https://raw.githubusercontent.com/mlrcbsousa/42-pipeline/main/tasks/02-readme.md
Also fetch:
https://raw.githubusercontent.com/mlrcbsousa/42-pipeline/main/context/project-registry.yaml
and https://raw.githubusercontent.com/mlrcbsousa/42-pipeline/main/context/42-school-conventions.md
```

## Pipeline Overview

```
orchestrator.md
  │
  ├── 01-audit.md      → Read-only assessment, produces gap checklist
  ├── 02-readme.md     → Creates/updates README.md
  ├── 03-makefile.md   → Standardizes Makefile targets and flags
  ├── 04-docs.md       → Generates docs/ folder (architecture, API, usage)
  ├── 05-blog-post.md  → Drafts blog post MDX for manuel.software
  └── 06-deploy.md     → Sets up GitHub Actions CI + docs deployment
```

The orchestrator runs the audit first, then only executes sub-tasks where gaps were found.

## File Structure

```
42-pipeline/    # repository root on GitHub
  README.md
  orchestrator.md
  tasks/
    01-audit.md … 06-deploy.md
  context/
    42-school-conventions.md
    project-registry.yaml
    blog-style-guide.md
    GITHUB-VERIFICATION.md
```

## What Each Task Does

| Task | Creates/Modifies | Git |
|------|------------------|-----|
| 01-audit | Nothing (read-only) | No |
| 02-readme | `README.md` | Human reviews/commits (suggested message in task) |
| 03-makefile | `Makefile` | Human reviews/commits |
| 04-docs | `docs/*.md` | Human reviews/commits |
| 05-blog-post | `content/blog/<slug>.mdx` in **site** repo | Human review required |
| 06-deploy | `.github/workflows/*`, `.gitignore` | Human reviews/commits |

Agents should **not** run `git commit` / `git push` unless the human explicitly asked in that session.

## Batch Execution

1. Open each project repo in a separate Claude Code session  
2. Paste the mobile prompt (above) in each  
3. Each session runs independently — produce file changes; **you** commit after review  
4. Review blog post drafts before publishing  

## Updating the Registry

After running the pipeline on a repo, update `project-registry.yaml` status:

- `needs-audit` — pipeline hasn't run yet  
- `audited` — audit done, gaps identified  
- `readme-done` — README created/updated  
- `docs-done` — documentation generated  
- `blog-done` — blog post drafted  
- `complete` — all pipeline tasks done  

## Safety

- The pipeline never modifies source code (`.c`, `.cpp`, `.h`, `.hpp`)  
- Prefer not deleting existing files (only creates or targeted infra edits)  
- Do not add school IP (subject PDFs, correction sheets)  
- Blog posts need human review before publication  
- The orchestrator is idempotent — safe to run multiple times  
