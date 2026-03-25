# GitHub repository verification (anonymous)

Last checked: 2026-03-24. Method: HTTP status for `https://github.com/<owner>/<repo>` (unauthenticated).

GitHub returns **404** for missing repos **and** for private repos when you are not logged in. A 404 here does **not** prove the repo does not exist.

## Registry policy (2026 refresh)

- **Removed** from `project-registry.yaml` (no pipeline): `pipex`, `so_long`, `ft_irc`, `net_practice` (NetPractice: blog-only / no meaningful repo).
- **Added**: `ft_containers`, `matrix`, `inception-of-things`, `python-piscine` (five repos via `pipeline_repos`, same pattern as `cpp-modules`).
- **ft_transcendence** canonical repo: **`brhaka/42-transcendence`** (group project).

## Results (mlrcbsousa) — historical probe

| Repository | HTTP |
| --- | --- |
| libft | 200 |
| ft_printf | 200 |
| born2beroot | 200 |
| Born2beRoot | 200 |
| CPP-Module-00 | 200 |
| pipex | 404 |
| so_long | 404 |
| net_practice | 404 |
| ft_irc | 404 |
| ft_transcendence | 404 |
| webserv (under mlrcbsousa) | 404 |
| cpp-modules (single repo name) | 404 |

## Confirmed external / collaborative

| Repository | HTTP |
| --- | --- |
| gleal42/webserv | 200 |

## Registry notes

- Canonical GitHub names for **Born2beRoot**, **Philosophers**, **Inception** (match common remote casing).
- **webserv** uses **gleal42/webserv** as `repo`.
- **cpp-modules** and **python-piscine** use `pipeline_repos` (multi-repo modules).
- Public repos confirmed separately by owner: [matrix](https://github.com/mlrcbsousa/matrix), [inception-of-things](https://github.com/mlrcbsousa/inception-of-things), Python track repos `python-0-starting` … `python-4-dod`, [ft_containers](https://github.com/mlrcbsousa/ft_containers).

If any row is wrong, confirm while logged into GitHub or via `gh repo view`.
