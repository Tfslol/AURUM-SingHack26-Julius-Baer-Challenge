# AGENTS.md

## Project Status

This repository is a SingHacks 2026 hackathon project (Julius Baer wealth
intelligence).

The challenge specification is available in `docs/challenge.md` and is the
source of truth for requirements. The system architecture is documented in
`docs/ARCHITECTURE_V2.md` and the dataset fields in `docs/DATA_DICTIONARY.md`.

Do not invent product requirements that are not grounded in the challenge.

## General Rules

- Read this file before making changes.
- Read the relevant documentation before modifying code.
- Prefer small, isolated changes.
- Do not modify unrelated files.
- Do not introduce dependencies without a reason.
- Do not rewrite working code merely for stylistic reasons.
- Do not make architectural decisions without documenting them.
- Run relevant tests and checks before completing a task.

## Git

- Never commit directly to main.
- Work on a feature branch.
- Keep commits focused.
- Do not rewrite another person's branch.
- Pull/rebase from main frequently and resolve merge conflicts directly when
  landing work (no pull requests).

## Collaboration

Before implementing a substantial feature:

1. Understand the existing architecture.
2. Check the existing docs and plans.
3. Identify files and interfaces that will be affected.
4. State assumptions explicitly.
5. Implement only the requested scope.

## Python Environment

This project uses uv for Python package and environment management.

Rules:

- Use uv for all dependency management.
- Do not use pip directly.
- Do not use poetry, pipenv, or conda.
- Use `uv add <package>` to add dependencies.
- Use `uv add --dev <package>` for development dependencies.
- Use `uv remove <package>` to remove dependencies.
- Commit both `pyproject.toml` and `uv.lock` when dependencies change.
- Run `uv sync` after pulling dependency changes.
- Do not manually edit `uv.lock`.

## Challenge

The challenge specification lives at:

docs/challenge.md

Treat that document as the primary source of truth for requirements. Where it
conflicts with assumptions made elsewhere in the repository (including this
file), the challenge specification takes precedence.