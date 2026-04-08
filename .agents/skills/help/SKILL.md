---
name: help
description: "Analyzes current project state and the user's question, then recommends the most useful next step."
argument-hint: "[optional: what you just finished, e.g. 'finished design-review' or 'stuck on ADRs']"
user-invocable: true
allowed-tools: Read, Glob, Grep
model: haiku
---

# Studio Help - What Do I Do Next?

This skill is read-only. It reports findings but writes no files.

Use it for quick orientation, not a full audit. For a deeper project inventory,
use `/project-stage-detect`.

---

## Step 1: Read the Workflow Catalog

Read `.agents/docs/workflow-catalog.yaml`. This is the authoritative source for:
- phases
- step order
- required vs optional steps
- artifact globs that indicate completion

---

## Step 2: Find Installed Skills Not in the Catalog

Glob `.agents/skills/*/SKILL.md` and extract the `name:` field from each
frontmatter block.

Compare those names against the catalog `command:` values. Any installed skill
that is not in the workflow catalog is an **uncataloged skill**. It is still
usable, but it is not part of the main phase-gated workflow.

If any exist, show them in a footer block at the end:

```markdown
### Also installed (not in workflow)
- `/skill-name` - [description]
- `/skill-name` - [description]
```

Only show the most relevant ones for the user's current phase, capped at 10.

---

## Step 3: Determine Current Phase

Check in this order:

1. Read `production/stage.txt`. If it exists and has content, it is the
   authoritative phase:
   - "Concept" -> `concept`
   - "Systems Design" -> `systems-design`
   - "Technical Setup" -> `technical-setup`
   - "Pre-Production" -> `pre-production`
   - "Production" -> `production`
   - "Polish" -> `polish`
   - "Release" -> `release`

2. If `production/stage.txt` is missing, infer phase from artifacts using the
   most advanced match:
   - `src/` has 10+ source files -> `production`
   - `production/stories/*.md` exists -> `pre-production`
   - `docs/architecture/adr-*.md` exists -> `technical-setup`
   - `design/gdd/systems-index.md` exists -> `systems-design`
   - `design/gdd/game-concept.md` exists -> `concept`
   - otherwise -> `concept`

---

## Step 4: Read Session Context

Read `production/session-state/active.md` if it exists. Extract:
- what was worked on most recently
- any in-progress task or open question
- the current epic, feature, or task from any status block

Use this to personalize the recommendation.

---

## Step 5: Check Completion for the Current Phase

For each step in the current phase:

If the step has `artifact.glob`:
- use Glob to check whether matching files exist
- respect `min_count` if specified
- if `artifact.pattern` exists, use Grep to confirm the expected content
- mark as **Complete** when the artifact condition is satisfied
- mark as **Incomplete** when it is missing

If the step has `artifact.note` but no glob:
- mark as **Manual**
- if needed, ask the user in plain text whether it has been completed

If the step has no artifact:
- mark as **Unknown**

Special case for production:
- if `production/sprint-status.yaml` exists, read it before any story glob checks
- treat it as authoritative for current story state
- use:
  - `in-progress` -> currently active
  - `ready-for-dev` -> next up
  - `done` -> complete
  - `blocked` -> blocker

For repeatable steps outside production, make it clear that detected artifacts
mean work has started, not necessarily finished.

---

## Step 6: Identify Position and Next Actions

Determine:
1. the last confirmed complete required step
2. the current blocker, meaning the first incomplete required step
3. optional steps available now
4. required steps coming up next

If the user passed an argument such as "just finished design-review", use that
to disambiguate the current position.

---

## Step 7: Present Output

Keep the answer short and direct.

Use this structure:

```markdown
## Where You Are: [Phase Label]

**In progress:** [from active.md, if any]

### Done
- [completed step]
- [completed step]

### Next up (REQUIRED)
**[Step name]** - [description]
Command: `[/command]`

### Also available (OPTIONAL)
- **[Step name]** - [description] -> `/command`
- **[Step name]** - [description] -> `/command`

### Coming up after that
- [next required step] (`/command`)
- [next required step] (`/command`)

---
Approaching **[next phase]** gate -> run `/gate-check` when ready.
```

Formatting rules:
- show only one primary required next step
- commands should be inline code
- if a step has no command, explain what action to take instead
- for manual steps, ask a plain-text confirmation question if necessary

Verdict: **COMPLETE** - next steps identified.

---

## Step 8: Optional Escalation Paths

If the user sounds stuck or lost, add:

```markdown
---
Need more detail?
- `/project-stage-detect` - full gap analysis
- `/gate-check` - readiness check for the next phase
- `/start` - re-orient from scratch
```

Do not show this for a straightforward "what's next?" request unless the user
sounds unsure.

---

## Collaborative Protocol

- Never auto-run the next skill.
- Ask about manual steps rather than guessing.
- Match the user's tone.
- Give one primary recommendation, with optional items as secondary context.
