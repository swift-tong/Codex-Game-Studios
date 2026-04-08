# Contributing

Thanks for contributing to Codex Game Studios.

## Project Shape

The active Codex-facing surface is:

- `AGENTS.md`
- `.agents/`
- nested `AGENTS.md` files in `src/`, `design/`, and `docs/`

Older Claude-oriented material is archived under `legacy/` and should not be the default target for new work.

## Contribution Guidelines

1. Keep changes Codex-first.
2. Prefer updating `.agents/` over `legacy/`.
3. Preserve the collaboration model: question, options, decision, draft, approval.
4. Avoid destructive rewrites of user-configurable project files.
5. Keep skills, docs, and templates consistent with each other.

## Typical Change Areas

- New or updated skills: `.agents/skills/<name>/SKILL.md`
- Role definitions: `.agents/agents/`
- Shared docs and templates: `.agents/docs/`
- Repo-level instructions: `AGENTS.md`
- Public project docs: `README.md`, `UPGRADING.md`, `docs/`

## Before Opening A PR

- Test the workflow you changed in Codex when possible.
- Update docs if you changed skill names, paths, or workflow expectations.
- Keep public examples aligned with the active Codex surface.
- Call out any intentional legacy-only behavior in the PR description.

## Release Discipline

If your change affects the public template shape, update:

- `README.md`
- `UPGRADING.md`
- `CHANGELOG.md`

If your change affects contribution expectations, update this file too.
