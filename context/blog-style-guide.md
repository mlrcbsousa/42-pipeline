# Blog Style Guide for manuel.software

Reference for generating blog posts about 42 School projects.

## Voice & Tone

- **First person** — "I built", "I learned", not "the developer" or "one might"
- **Technical but accessible** — assume the reader knows basic programming but may not know C, systems programming, or the specific domain
- **Honest about challenges** — mention what was hard, what you got wrong, what you'd do differently
- **Not a tutorial** — it's a project retrospective, not a how-to guide. Show interesting parts, don't walk through every line
- **Conversational** — write like you're explaining the project to a fellow developer over coffee

## Structure

Every project blog post follows this skeleton:

```mdx
---
title: "Project Name — one-line hook"
date: "YYYY-MM-DD"
excerpt: "2-3 sentence summary for the blog feed preview"
tags: ["tag1", "tag2", "tag3"]
published: true
---

## What is [project]?

Brief context: what the project is, why 42 School assigns it, what you learn from it.
Link to the official 42 curriculum description if public, or describe the constraints.

## The Interesting Problem

Pick ONE technical challenge that was the most interesting or difficult.
Go deep on this — explain the problem, your approach, the tradeoffs.
Include code snippets (keep them short, 10-20 lines max).

## How It Works

High-level architecture or flow. A diagram if it helps (mermaid or image).
Don't explain every function — focus on the design decisions.

## What I Learned

2-3 concrete takeaways. Not platitudes ("I learned to code better") but specifics
("I learned why mutex ordering matters for deadlock prevention").

## Try It Yourself

Build instructions, link to the GitHub repo, maybe a screenshot or GIF.
```

## Formatting

- **Headings**: H2 for main sections, H3 for subsections. No H1 (the title is H1).
- **Code blocks**: Use fenced code blocks with language tags. Keep snippets focused — 10-20 lines.
- **Images**: Reference from `/public/images/blog/` in the manuel.software repo. Use `next/image` via MDX component.
- **Links**: Internal links use relative paths (`/blog/other-post`, `/projects/project-slug`).
- **Callouts**: Use `<Callout type="info|warning|tip">` for sidebars.

## Tags

Use consistent tags from this set (add new ones sparingly):

**Languages**: `c`, `cpp`, `rust`, `typescript`, `javascript`, `ruby`, `python`
**Domains**: `systems`, `graphics`, `networking`, `web`, `algorithms`, `devops`
**Concepts**: `42-school`, `data-structures`, `concurrency`, `parsing`, `math`
**Meta**: `learning`, `internship`, `career`

## Frontmatter

```yaml
title: string       # Project name + hook (e.g., "minishell — Building a Shell from Scratch")
date: string        # YYYY-MM-DD format, use today's date
excerpt: string     # 2-3 sentences for blog feed preview
tags: string[]      # Array of tags from the set above
published: boolean  # true when ready, false for drafts
```

## Length

- Target **800-1500 words** per project post
- Shorter (500-800) is fine for simpler projects (libft, ft_printf)
- Longer (1500-2500) is fine for complex projects (cub3d, minishell, ft_transcendence)

## Output Location

Blog post drafts should be written to:
```
/Users/manuel-sousa/Code/Business/manuel.software/content/blog/<project-slug>.mdx
```

If the file already exists (migrated from mlrcbsousa.com), update it rather than overwrite.
Existing posts to preserve: 42-matrix, grpc-web, investing, javascript-performance-1,
javascript-performance-2, karatsuba-algorithm, keyrock-internship, node-migrate,
praise-frontend-masters, rspec-factories, rspec-how-to-write-a-spec, rust-typescript-devs,
vitepress-bookmark, vue-sortable, websummit-2024.
