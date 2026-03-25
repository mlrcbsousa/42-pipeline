# Task 05: Draft Blog Post

Write a blog post about this project for the manuel.software portfolio site.

## Context Needed

```bash
cat README.md 2>/dev/null
cat docs/architecture.md 2>/dev/null
find . -name "*.c" -o -name "*.cpp" -o -name "*.h" -o -name "*.hpp" | head -30
git log --oneline -20
```

Read from the pipeline:
- `context/project-registry.yaml` — project metadata
- `context/blog-style-guide.md` — writing style, structure, and frontmatter format

## Pre-Check

Check if a blog post already exists:

```bash
# From the manuel.software site repository root (path depends on your machine):
ls content/blog/ 2>/dev/null || echo "Open the site repo and check content/blog/"
```

If a file for this project already exists, read it and decide:
- If it's a full post (migrated from mlrcbsousa.com), skip this task
- If it's a stub ("Content to be written"), replace it with a full post

## Writing the Post

Follow the structure in `blog-style-guide.md` exactly. Key reminders:

1. **Read the source code** before writing. Identify the most interesting technical
   challenge — the part that would make another developer say "oh, that's clever" or
   "I didn't know you could do that."

2. **Pick ONE deep topic** per post. Don't try to cover everything.
   - For `libft`: memory management decisions, or reimplementing a tricky libc function
   - For `minishell`: the parser, or signal handling, or pipe/redirect architecture
   - For `cub3d`: the raycasting math, or texture mapping, or the map parser
   - For `philosophers`: deadlock prevention strategy
   - For `ft_irc`: the event loop, or RFC compliance challenges

3. **Include 2-3 code snippets** (10-20 lines each) that illustrate the interesting parts.
   Copy from the actual source — don't write pseudocode.

4. **Be honest** about what was hard and what you'd do differently.

## Output

Write the blog post to the **manuel.software** site repository (not the 42 project repo):

```
content/blog/<project-slug>.mdx
```

Use the slug from the project registry. If the agent only has the project repo open, output the full post in chat or as a patch and tell the human where to save it.

## Frontmatter Format

```yaml
---
title: "[Project Name] — [Hook]"
date: "YYYY-MM-DD"
excerpt: "[2-3 sentence summary]"
tags: ["tag1", "tag2", "42-school"]
published: true
---
```

Always include `42-school` in the tags array.
Use today's date for the `date` field.

## Quality Check

- Post follows the structure in the style guide
- Frontmatter has all required fields and valid YAML
- Code snippets are from the actual source (not invented)
- Tags are from the approved set in the style guide
- Length is within the target range (500-2500 words depending on project complexity)
- No school IP content (don't reproduce the subject requirements)

## Commit

Do NOT commit blog posts directly. They need human review first.
Instead, report:

```
Blog post drafted: content/blog/<slug>.mdx
Status: Ready for review
Word count: [N]
```

The author will review, edit, and commit the post themselves.
