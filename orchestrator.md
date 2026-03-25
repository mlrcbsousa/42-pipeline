# Project Pipeline Orchestrator

You are running an automated pipeline on a 42 School project repository.
Your job is to audit the repo, identify what's missing, and execute the appropriate
sub-tasks to bring it up to standard.

## Setup

**`PIPELINE_HOME`** is the directory that contains this `orchestrator.md` file (the root of the prompt bundle — e.g. `manuel.software/prompts` or the `42-pipeline` repo after clone).

All paths below are relative to `PIPELINE_HOME`:

- `context/project-registry.yaml`
- `context/42-school-conventions.md`
- `context/GITHUB-VERIFICATION.md` (optional — GitHub URL sanity notes)
- `tasks/*.md`

Read these context files before doing anything else:

1. `context/project-registry.yaml` — find this repo in the registry
2. `context/42-school-conventions.md` — 42 School norms and standards

If the current repo is not in the project registry, stop and report:
"This repo is not in the project registry. Add it to project-registry.yaml first."

## Step 1: Identify the Project

Run these commands to understand the repo:

```bash
pwd
ls -la
cat README.md 2>/dev/null || echo "NO README"
cat Makefile 2>/dev/null | head -30 || echo "NO MAKEFILE"
find . -name "*.c" -o -name "*.cpp" -o -name "*.h" -o -name "*.hpp" | head -30
git remote -v 2>/dev/null || true
git log --oneline -10
```

Match the repo against the project registry by checking:

- **`git remote` URL** — normalize to `owner/repo` (strip `.git`, `git@`, `https://github.com/`).
- **`pipeline_repos`** — if the registry entry lists multiple repos (e.g. C++ modules), match if the remote equals **any** listed repo, or if the directory name matches a module folder (e.g. `CPP-Module-04`).
- Directory name, Makefile `NAME`, and source patterns (`.c` vs `.cpp` vs `Dockerfile`).

Once identified, load the project's metadata (slug, name, category, tech, description).

## Step 1.5: Prepare Working Branch

Look up `linear_issue` and `linear_branch` from the registry entry for this project.

**If `linear_branch` is set** (e.g. `mlrcbsousa/man-18-printf`):

Print this message for the human before making any changes:

```
## Branch Required

Before I make any changes, please create and check out the Linear-tracked branch:

  git checkout -b mlrcbsousa/man-XX-slug

This ties all pipeline commits to Linear issue MAN-XX.
Reply "branch ready" (or just continue) once you've done this — or tell me to skip if you're running a dry-run.
```

**If `linear_branch` is null** (e.g. philosophers, ft_containers, inception-of-things):

Print this message instead:

```
## No Linear Issue Found

This project has no Linear issue linked in the registry yet.
Options:
  1. Create a MAN-XX issue in Linear for this project, update project-registry.yaml, then re-run.
  2. Continue without a Linear branch (commits land on current branch).

Reply with the Linear issue ID (e.g. "MAN-82") to auto-set the branch name, or "continue" to proceed without one.
```

Wait for the human to confirm before proceeding to the audit.

## Step 2: Audit

Read and follow: `tasks/01-audit.md`

This produces a checklist of what needs work. Save the checklist mentally — it drives
which sub-tasks to run.

## Step 3: Execute Sub-Tasks

For each gap identified in the audit, run the corresponding sub-task prompt.
Execute them in order:

| Gap Found | Sub-Task |
|-----------|----------|
| README missing or inadequate | `tasks/02-readme.md` |
| Makefile missing targets or non-standard | `tasks/03-makefile.md` |
| No docs/ folder or documentation | `tasks/04-docs.md` |
| No blog post exists for this project | `tasks/05-blog-post.md` |
| No CI/CD or GitHub Pages setup | `tasks/06-deploy.md` |

**Skip sub-tasks where the audit found no issues.** Don't fix what isn't broken.

**Git writes:** Do **not** run `git commit`, `git push`, or other history-changing commands unless the human explicitly asked for them in this session. After each sub-task, list the changed files and a **suggested commit message** for the human to run locally.

## Step 4: Update Registry

After completing all applicable sub-tasks, report what was done:

```
## Pipeline Report: [project-name]

**Repo:** [repo-path]
**Project:** [name] ([category])

### Completed
- [ ] Audit
- [ ] README (created/updated/skipped)
- [ ] Makefile (updated/skipped)
- [ ] Docs (created/skipped)
- [ ] Blog post (drafted/skipped)
- [ ] Deploy (configured/skipped)

### Manual Review Needed
- [list anything that needs human judgment]

### Suggested Next Status
- [recommend new status value for project-registry.yaml]
```

## Idempotency

If you run this pipeline again on the same repo:
- Re-run the audit to check current state
- Skip sub-tasks whose outputs already exist and are up to standard
- Only re-run sub-tasks where the audit still finds gaps

## Error Handling

- If a sub-task fails or produces unclear results, note it in the report under
  "Manual Review Needed" and continue with the next sub-task
- Never force-push or rewrite git history
- If the repo has uncommitted changes, **do not** `git stash` unless the human explicitly approves — note the dirty tree in the report instead

## Important Rules

- Do NOT modify source code (`.c`, `.cpp`, `.h`, `.hpp` files) — this pipeline
  handles documentation and infrastructure only
- Do NOT delete existing files unless they're clearly broken config files being replaced
- Do NOT add school IP (subject PDFs, correction sheets) to any committed material
- Always preserve the existing git history
