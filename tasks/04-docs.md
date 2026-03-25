# Task 04: Generate Project Documentation

Create a `docs/` directory with architecture overview and function/module reference.

## Context Needed

```bash
find . -name "*.h" -o -name "*.hpp" | xargs cat 2>/dev/null
find . -name "*.c" -o -name "*.cpp" | head -30
cat Makefile 2>/dev/null
cat README.md 2>/dev/null
```

Read: `context/project-registry.yaml` for project metadata.

## Output Structure

Create a `docs/` directory with markdown files:

```
docs/
  index.md          # Overview and navigation
  architecture.md   # Design decisions and component overview
  api.md            # Function/module reference (for libraries/utilities)
  usage.md          # Extended usage guide with examples
```

**Adapt the structure to the project type:**
- **Library projects** (libft, ft_printf): Focus on `api.md` with function reference
- **Application projects** (minishell, cub3d): Focus on `architecture.md` with component design
- **Infrastructure projects** (inception, born2beroot): Focus on `usage.md` with setup/config guide
- **Web projects** (ft_transcendence, webserv): Both architecture and API

## File Contents

### `docs/index.md`

```markdown
# [Project Name] Documentation

[One paragraph overview]

## Contents

- [Architecture](architecture.md) — design decisions and component overview
- [API Reference](api.md) — function and module documentation
- [Usage Guide](usage.md) — extended examples and configuration
```

### `docs/architecture.md`

Write 300-800 words covering:
- High-level design: what are the main components/modules?
- Data flow: how does data move through the system?
- Key decisions: why was this approach chosen over alternatives?
- Diagrams: use mermaid for flow/component diagrams where helpful

**Read the actual source code** to understand the architecture. Look at:
- Header files for module interfaces
- `main.c`/`main.cpp` for the entry point and initialization flow
- Directory structure for module boundaries

### `docs/api.md`

For library projects, document each public function:

```markdown
## `ft_strlen`

```c
size_t ft_strlen(const char *s);
```

Returns the length of the string `s`, not including the null terminator.

**Parameters:**
- `s` — null-terminated string to measure

**Return value:**
- Length of the string

**Example:**
```c
ft_strlen("hello"); // returns 5
```
```

For application projects, document the main modules and their public interfaces.

### `docs/usage.md`

Extended usage examples beyond what's in the README:
- All command-line options and flags
- Configuration file format (if applicable)
- Common use cases with input/output examples
- Troubleshooting common issues

## Rules

- **Read the actual header files** to document functions accurately.
  Don't invent function signatures — copy them from the source.
- **Don't document static/internal functions** — only public API (declared in `.h` files).
- **Use the project's actual types** — if it defines `t_list`, use that, not `struct s_list`.
- **Keep it maintainable** — documentation that's too detailed becomes stale quickly.
  Focus on "what" and "why", not line-by-line "how".

## Quality Check

- All documented functions exist in the actual source code
- Function signatures match the header files exactly
- Mermaid diagrams render correctly (valid syntax)
- All internal links between docs files work

## Hand off to human (git)

Do **not** commit unless the human asked you to. Provide:

```text
Suggested commit message:
docs: add project documentation — architecture, API reference, usage guide

Files to review:
docs/
```
