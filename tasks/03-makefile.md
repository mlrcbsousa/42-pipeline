# Task 03: Standardize Makefile

Update the project's Makefile to meet 42 School standards and add useful extra targets.

## Context Needed

```bash
cat Makefile
find . -name "*.c" -o -name "*.cpp" | sort
ls include/ 2>/dev/null
ls libft/ 2>/dev/null
```

Read: `context/42-school-conventions.md`

## Applicability

- **C/C++ projects**: Full Makefile standardization
- **Infrastructure projects** (born2beroot, inception, net_practice): Skip or minimal Makefile
- **Web projects** (ft_transcendence): May use npm/package.json instead — adapt accordingly

If this is not a C/C++ project with a meaningful Makefile, skip this task.

## Required Targets

Verify and fix if missing:

### `all` (default)
- Compiles all source files and links the binary/library
- Must use `$(CC)` and `$(CFLAGS)`
- For C: `CFLAGS` must include `-Wall -Wextra -Werror`
- For C++: `CXXFLAGS` must include `-Wall -Wextra -Werror -std=c++98` (or appropriate standard)

### `clean`
- Removes all `.o` object files
- If project uses libft, also runs `make clean` in libft directory

### `fclean`
- Runs `clean` first
- Removes the final binary (`$(NAME)`) or library (`.a` file)
- If project uses libft, also runs `make fclean` in libft directory

### `re`
- Runs `fclean` then `all`
- Must be declared as: `re: fclean all`

### `bonus` (if applicable)
- Compiles bonus source files
- Only add if the project has `*_bonus.c` / `*_bonus.h` files

## Anti-Relink Check

The Makefile must not relink. Verify by:
1. Running `make` — should compile
2. Running `make` again — should print nothing (already up to date)

This is achieved by using proper prerequisite rules (`.o` depends on `.c` and `.h` files).

## Extra Targets (Add These)

### `docs` (if docs/ exists or will be created)
```makefile
docs:
	@echo "Documentation available at docs/"
```

### `test` (if tests exist)
```makefile
test: $(NAME)
	@echo "Running tests..."
	./run_tests.sh
```

Only add `test` if there are actual test files or scripts in the repo.

## Rules

- **Do NOT change the core compilation logic** if it already works correctly.
  Only fix structural issues (missing targets, wrong flags, relinking).
- **Preserve custom targets** the author may have added.
- **Keep the existing source file list** — don't add or remove source files.
- **Match the existing style** — if the Makefile uses `SRC = file1.c file2.c`,
  don't switch to `SRC = $(wildcard src/*.c)` or vice versa.

## Quality Check

```bash
make fclean
make
make          # Should produce no output (no relink)
make clean
ls *.o 2>/dev/null  # Should show nothing
make fclean
ls $(NAME) 2>/dev/null  # Should show nothing
```

## Hand off to human (git)

Do **not** commit unless the human asked you to. Provide:

```text
Suggested commit message:
build: standardize Makefile targets and flags

Files to review:
Makefile
```
