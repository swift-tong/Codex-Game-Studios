# Upgrading Codex Game Studios

This guide explains how to pull newer template changes into a game project that already uses Codex Game Studios.

## Recommended Strategy

Use a template remote and merge selectively.

```bash
git remote add template <your-codex-game-studios-repo-url>
git fetch template
git merge template/main
```

If you only want a specific improvement, cherry-pick the relevant commit instead:

```bash
git fetch template
git cherry-pick <commit-sha>
```

## Files To Review Carefully

These usually contain project-specific decisions and should not be overwritten blindly:

- `AGENTS.md`
- `design/AGENTS.md`
- `docs/AGENTS.md`
- `src/AGENTS.md`
- `.agents/docs/technical-preferences.md`
- Any files under `design/`, `docs/architecture/`, `production/`, or `src/` that you have customized for your game

## Files Usually Safe To Replace

These are template infrastructure files and can usually be updated from the new version:

- `.agents/agents/**`
- `.agents/rules/**`
- Most of `.agents/docs/templates/**`
- Most of `.agents/skills/**`
- `README.md`
- This `UPGRADING.md`

Review skill changes before replacing them if you have edited any skill locally.

## Recommended Upgrade Flow

1. Create a backup branch.
2. Merge or cherry-pick the new template changes.
3. Resolve conflicts in `AGENTS.md` and technical preferences by keeping your project-specific choices.
4. Re-scan the repository for outdated paths or legacy references.
5. Run a quick smoke pass on the skills you use most often.

## Publishing Advice

If you are forking this repository into your own public template:

1. Update the repository name and clone URL examples.
2. Replace any remaining historical references in `docs/examples/` and optional framework docs.
