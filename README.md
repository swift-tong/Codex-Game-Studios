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

## Prerequisites

Before using this repository, make sure you have:

- Codex installed and working in your local environment
- Git available in your shell
- A workspace where you can open this repository in Codex

Optional but useful:

- Python 3 for projects or checks that rely on Python tooling
- Node.js for projects or scripts that rely on JavaScript tooling

## How To Use It

This repository is meant to be opened in Codex and driven through chat.
You do not "run" it like a game runtime. You use it as the instruction,
workflow, and template surface for planning and building a game project.

### Basic Setup

1. Clone the repo into a workspace.
2. Open it in Codex.
3. Start from [AGENTS.md](./AGENTS.md).
4. Read the quick references if needed:
   - [Quick Start](./.agents/docs/quick-start.md)
   - [Workflow Guide](./docs/WORKFLOW-GUIDE.md)
   - [Technical Preferences](./.agents/docs/technical-preferences.md)
5. Invoke a skill naturally in chat, for example:
   - `$start`
   - `$brainstorm`
   - `$setup-engine godot 4.6`
   - `$project-stage-detect`
6. Let Codex follow the local `AGENTS.md` and `.agents/skills` guidance.

### What Codex Reads

When you work inside this repository, Codex primarily uses:

- [AGENTS.md](./AGENTS.md) as the root instruction file
- [`.agents/skills`](./.agents/skills) for reusable workflows
- [`.agents/agents`](./.agents/agents) for role definitions
- [`.agents/docs`](./.agents/docs) for templates, standards, and process docs
- nested `AGENTS.md` files in [`design/`](./design/AGENTS.md), [`docs/`](./docs/AGENTS.md), and [`src/`](./src/AGENTS.md)

### What To Say In Codex

Typical prompts look like:

- `Run $start`
- `Use $brainstorm to help me define a 2D roguelike`
- `Run $setup-engine godot 4.6`
- `Use $design-system for combat`
- `Run $project-stage-detect on this repo`
- `Read AGENTS.md and tell me the next step`

You can either name a skill directly or describe the task in plain language.

## Usage By Scenario

### Scenario 1: Starting A New Game From Scratch

Use this path if you have no existing game repo or only a rough idea.

1. Run `$start`
2. Run `$brainstorm` to generate and narrow the concept
3. Run `$setup-engine` to pick and configure the engine
4. Run `$map-systems` to identify the game's systems and dependencies
5. Run `$design-system <system-name>` for each major system
6. Run `$review-all-gdds`
7. Run `$create-architecture`
8. Run `$create-epics`
9. Run `$create-stories`
10. Run `$dev-story` to implement work

### Scenario 2: Adopting It In An Existing Game Project

Use this path if you already have code, design docs, or production files.

1. Copy or merge this template into the existing repository
2. Make sure the root [AGENTS.md](./AGENTS.md) and [`.agents`](./.agents) tree are present
3. Open the repo in Codex
4. Run `$project-stage-detect`
5. Run `$adopt`
6. Run `$gate-check` to see what is missing before the next phase
7. Fill gaps using the recommended skills

### Scenario 3: Using Only Part Of The Template

You do not need to use the full end-to-end workflow.

Common partial uses:

- Use only the design flow: `$brainstorm`, `$map-systems`, `$design-system`
- Use only the architecture flow: `$create-architecture`, `$architecture-decision`
- Use only the production flow: `$create-epics`, `$create-stories`, `$sprint-plan`
- Use only the QA/release flow: `$team-qa`, `$smoke-check`, `$release-checklist`

## Minimal Example

If you want the shortest possible path to verify the template works:

1. Open the repo in Codex
2. Say `Run $start`
3. Then say `Run $brainstorm for a small 2D action game`
4. Then say `Run $setup-engine godot 4.6`
5. Then say `Run $map-systems`

If those steps work, the repository is installed and usable in Codex.

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

## Common Outputs

As you use the workflow, Codex will typically create or update:

- design documents under `design/`
- technical and architecture docs under `docs/`
- production planning docs under `production/`
- source code and implementation files under `src/`

This repository provides the process and templates. Your actual game-specific content is expected to be created on top of it.

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
