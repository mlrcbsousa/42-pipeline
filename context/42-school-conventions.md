# 42 School Conventions

Reference document for Claude Code sessions working on 42 School project repositories.

## Code Style (Norminette)

42 School enforces a strict C coding standard called the Norm (checked by `norminette`):

- Functions must not exceed 25 lines (excluding braces)
- Maximum 4 parameters per function
- Maximum 5 variables per function
- No `for` loops — only `while` is allowed
- No variable declarations after the first line of code in a scope
- All variables declared at the top of the function
- Lines must not exceed 80 columns
- Header comment block required (42 header) at the top of every `.c` and `.h` file
- No comments inside function bodies
- Tabs for indentation (width 4)
- Function names use `snake_case`
- Type names use `t_` prefix (e.g., `t_list`, `t_data`)
- Global variables use `g_` prefix
- Macros and enums are `UPPER_SNAKE_CASE`

**Note:** Norminette applies to C projects only. C++ projects follow their own style guide (typically closer to standard C++ conventions).

## Makefile Standards

Every 42 project Makefile must include:

### Required Targets

- `all` — build the project (default target)
- `clean` — remove object files
- `fclean` — remove object files AND the binary/library
- `re` — `fclean` + `all`

### Optional Targets

- `bonus` — build bonus part (if applicable)
- `test` — run tests (if any)
- `docs` — generate documentation (if any)

### Required Variables

- `NAME` — output binary or library name
- `CC` — compiler (typically `cc` or `gcc`)
- `CFLAGS` — must include `-Wall -Wextra -Werror`

### Rules

- Makefile must not relink (rebuilding without changes should produce no output)
- Library dependencies (e.g., libft) should be built automatically
- Use `-I` for include paths, `-L` and `-l` for library linking

## Project Structure Patterns

### C Projects (typical)

```
project/
  Makefile
  include/           # or just project.h at root
    project.h
  src/               # or srcs/
    main.c
    module1.c
    module2.c
  libft/             # if using libft as submodule or copy
    Makefile
    ...
```

### C++ Projects

```
project/
  Makefile
  include/
    Class.hpp
  src/
    main.cpp
    Class.cpp
```

### Infrastructure Projects

```
project/
  Makefile           # may be minimal or absent
  Dockerfile(s)
  docker-compose.yml
  conf/ or config/
  scripts/
```

## Repository Conventions

- The `main` or `master` branch contains the final submission
- Subject PDF should NOT be in the repo (it's school IP)
- No compiled binaries committed
- `.gitignore` should exclude: `*.o`, `*.a`, binary name, `.DS_Store`
- Bonus files are typically suffixed with `_bonus.c` / `_bonus.h`

## Grading

- Projects are graded by peer review (other students)
- Passing grade varies but is typically 100/100 for mandatory + bonus points
- Some projects have a "defense" component where you explain your code

## Common Libraries

- **libft**: Custom C standard library (most projects depend on it)
- **MiniLibX**: X11-based graphics library for graphics projects (works on macOS via XQuartz)
- **MLX42**: Modern OpenGL/GLFW alternative to MiniLibX (macOS native)
- **Readline**: Used in minishell for input handling
