# Task 01: Audit Repository

Assess the current state of the repository and produce a checklist of gaps.

## Context Needed

Read these files/paths from the repo:

```bash
cat README.md 2>/dev/null
cat Makefile 2>/dev/null
ls -la .github/workflows/ 2>/dev/null
ls docs/ 2>/dev/null
cat .gitignore 2>/dev/null
find . -name "*.c" -o -name "*.cpp" -o -name "*.h" -o -name "*.hpp" | wc -l
git remote -v
```

Also check the project registry for metadata about this project:
`context/project-registry.yaml` (relative to the prompt bundle root — same folder as `orchestrator.md`)

## Audit Checklist

Evaluate each area and mark as PASS, FAIL, or N/A:

### README

- [ ] README.md exists
- [ ] If the project **vendors** another project (e.g. `libft/` inside `ft_printf`), README explains the relationship, build order, and whether it is a copy vs submodule
- [ ] Has project title and description
- [ ] Has build/install instructions
- [ ] Has usage examples or demo
- [ ] Has badge for 42 grade (if known)
- [ ] Has link to project documentation (if docs exist)
- [ ] Has link to GitHub repo
- [ ] No school IP (subject PDF links, correction sheets)

### Makefile

- [ ] Makefile exists (N/A for non-C/C++ projects)
- [ ] Has `all` target
- [ ] Has `clean` target
- [ ] Has `fclean` target
- [ ] Has `re` target
- [ ] Uses `-Wall -Wextra -Werror` flags
- [ ] Does not relink (running `make` twice shows no recompilation)
- [ ] Has `NAME` variable
- [ ] Has `bonus` target (if project has bonus)

### Documentation

- [ ] `docs/` directory exists
- [ ] Has architecture or design overview
- [ ] Has function/module reference (for library projects)
- [ ] Has usage guide with examples

### CI/CD

- [ ] `.github/workflows/` directory exists
- [ ] Has build/test workflow
- [ ] Has docs deployment workflow (GitHub Pages)

### Git Hygiene

- [ ] `.gitignore` exists
- [ ] `.gitignore` covers `*.o`, `*.a`, binary name, `.DS_Store`
- [ ] No compiled binaries in the repo
- [ ] No school IP PDFs in the repo
- [ ] No `.env` or secrets committed

### Blog Post

- [ ] Blog post exists in the **manuel.software** site repo at `content/blog/<project-slug>.mdx`

### Project Page

- [ ] Project detail page exists in the **manuel.software** site repo at `content/projects/<project-slug>.mdx`
- [ ] Frontmatter has `title`, `description`, `tech`, `category`, `github`, `featured`, `order`
- [ ] If missing, flag for creation during blog post task (05) or as a standalone stub

## Output

Produce a summary like this:

```
## Audit: [project-name]

README:       [PASS|FAIL] — [brief note]
Makefile:     [PASS|FAIL|N/A] — [brief note]
Docs:         [PASS|FAIL] — [brief note]
CI/CD:        [PASS|FAIL] — [brief note]
Git:          [PASS|FAIL] — [brief note]
Blog Post:    [PASS|FAIL] — [brief note]
Project Page: [PASS|FAIL] — [brief note]

Sub-tasks needed: [list of 02-06 numbers]
```

This output drives the orchestrator's decision about which sub-tasks to run.

## No Commits

This task is read-only. Do not modify any files or make any commits.
