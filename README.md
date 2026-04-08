# Codex Game Studios

[Chinese README](./README.zh-CN.md)

Turn a single Codex workspace into a structured indie game studio.

`49` role definitions. `72` reusable skills. A complete workflow from concept to release.

Start here: [AGENTS.md](./AGENTS.md) | [Quick Start](./.agents/docs/quick-start.md) | [Workflow Guide](./docs/WORKFLOW-GUIDE.md)

## What This Repo Is

Codex Game Studios is a Codex-first game development template. It gives your project:

- A studio-shaped workflow for design, architecture, implementation, QA, and release
- Reusable skills under [`.agents/skills`](./.agents/skills)
- Role definitions under [`.agents/agents`](./.agents/agents)
- Shared rules, templates, and workflow docs under [`.agents/docs`](./.agents/docs)
- Project-local instructions through [AGENTS.md](./AGENTS.md) and nested `AGENTS.md` files

This repository is designed to be published as its own Codex project. The `.agents/` tree is the primary integration surface.

## Included

| Category | Count | Notes |
|---|---:|---|
| Agent role specs | 49 | Directors, leads, specialists, and engine experts |
| Skills | 72 | Concepting, GDDs, ADRs, stories, QA, release, audits |
| Rules | 11 | Path-scoped standards for code, data, tests, design docs |
| Templates | 39 | GDD, ADR, sprint, UX, release, and audit templates |
| Engine references | 3 stacks | Godot, Unity, Unreal snapshots and best-practice notes |

## Repository Layout

```text
AGENTS.md
.agents/
  agents/        # Role definitions and role prompts
  docs/          # Workflow docs, templates, references
  rules/         # Path-specific standards
  skills/        # Codex skills
design/
  AGENTS.md
docs/
  AGENTS.md
  engine-reference/
production/
src/
  AGENTS.md
```

## Using It In Codex

1. Clone the repo into a workspace.
2. Open it in Codex.
3. Start from [AGENTS.md](./AGENTS.md).
4. Invoke a skill naturally in chat, for example:
   - `$start`
   - `$brainstorm`
   - `$setup-engine godot 4.6`
   - `$project-stage-detect`
5. Let Codex follow the local `AGENTS.md` and `.agents/skills` guidance.

If you are adapting an existing game project instead of starting from scratch, begin with `$project-stage-detect` and `$adopt`.

## Recommended Workflow

1. `$start`
2. `$brainstorm` or bring an existing concept
3. `$setup-engine`
4. `$map-systems`
5. `$design-system`
6. `$review-all-gdds`
7. `$create-architecture`
8. `$architecture-decision`
9. `$create-control-manifest`
10. `$create-epics`
11. `$create-stories`
12. `$dev-story`
13. `$code-review`
14. `$story-done`
15. `$team-qa`
16. `$release-checklist`

## Codex-Native Notes

- The Codex-facing assets live in [`.agents`](./.agents).
- Root and nested [AGENTS.md](./AGENTS.md) files are the instruction entry points.
- Skills were migrated to Codex path conventions and should reference `.agents/docs/...`.

## Key Files To Read First

- [AGENTS.md](./AGENTS.md)
- [.agents/docs/quick-start.md](./.agents/docs/quick-start.md)
- [.agents/docs/coordination-rules.md](./.agents/docs/coordination-rules.md)
- [.agents/docs/technical-preferences.md](./.agents/docs/technical-preferences.md)
- [docs/COLLABORATIVE-DESIGN-PRINCIPLE.md](./docs/COLLABORATIVE-DESIGN-PRINCIPLE.md)

## Migration Status

This repository has been reshaped so it can stand alone as a Codex project, with `AGENTS.md` and `.agents/` as the only active instruction surface.

## License

[MIT](https://opensource.org/licenses/MIT)
