# Task 02: Generate/Update README

Create or update the project's README.md to be comprehensive and professional.

## Context Needed

Read from the repo:

```bash
cat Makefile 2>/dev/null
find . -name "*.c" -o -name "*.cpp" -o -name "*.h" -o -name "*.hpp" | head -50
cat include/*.h 2>/dev/null | head -100
cat src/main.c 2>/dev/null || cat main.c 2>/dev/null | head -50
```

Read from the pipeline (relative to the folder containing `orchestrator.md`):
- `context/project-registry.yaml` — project metadata
- `context/42-school-conventions.md` — Makefile/build conventions

## README Template

Generate a README.md following this structure. Adapt sections based on what's relevant
to the specific project. Skip sections that don't apply.

```markdown
# [Project Name]

[1-2 sentence description of what this project does]

> 42 School project — [brief curriculum context: what this teaches]

## Overview

[2-3 paragraphs explaining the project: what it does, why it exists,
key technical concepts involved. Write for a developer who hasn't seen
42 School projects before.]

## Features

- [Key feature or capability 1]
- [Key feature or capability 2]
- [Key feature or capability 3]
- [Bonus features if applicable]

## Getting Started

### Prerequisites

- [Required tools: gcc, make, etc.]
- [Required libraries: MiniLibX, Readline, etc.]
- [OS requirements if any]

### Build

```bash
git clone https://github.com/mlrcbsousa/[repo-name].git
cd [repo-name]
make
```

### Usage

```bash
./[binary-name] [arguments]
```

[1-2 usage examples with expected output]

## Project Structure

```
[tree output showing key files/directories]
```

## Technical Details

[Brief explanation of the approach, algorithms used, or architecture.
Only include if there's something interesting to say — don't pad.]

## Resources

- [42 Subject](link) — *if publicly available*
- [Related blog post](https://manuel.software/blog/[slug]) — *if exists*
- [Documentation](docs/) — *if docs/ exists*

## License

[MIT or whatever the repo uses]
```

## Rules

- **Read the actual source code** to write accurate build instructions and usage examples.
  Don't guess — check the Makefile for the binary name, check `main.c` for argument parsing.
- **Don't include school IP** — no subject PDF content, no correction sheet details.
  You can reference the subject by name but don't reproduce its requirements verbatim.
- **Preserve existing content** — if a README already exists and has good content,
  enhance it rather than replacing it entirely. Keep any custom sections the author added.
- **Use real examples** — if the program takes input, show actual input/output.
  If it's a graphics program, mention screenshots (add placeholder paths).

## Quality Check

After writing the README, verify:
- If a nested directory is **not** part of this project’s unique logic (e.g. bundled `libft/`), the README states that clearly and documents how to build without breaking that subtree’s Makefile
- Build instructions actually match the Makefile
- Binary name matches `NAME` in Makefile
- Usage examples match the actual program behavior
- No broken markdown formatting
- Links point to real destinations

## Hand off to human (git)

Do **not** commit unless the human asked you to. Provide:

```text
Suggested commit message:
docs: comprehensive README with build instructions and usage

Files to review:
README.md
```
