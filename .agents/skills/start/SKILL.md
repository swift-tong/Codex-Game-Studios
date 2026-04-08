---
name: start
description: "First-time onboarding. Checks project state, asks where the user is starting from, and routes them to the right workflow without making assumptions."
argument-hint: "[no arguments]"
user-invocable: true
allowed-tools: Read, Glob, Grep, Write
---

# Guided Onboarding

This skill writes one file: `production/review-mode.txt`.

This is the entry point for new users. It does not assume the user has a game
idea, an engine preference, or prior studio workflow experience.

---

## Phase 1: Detect Project State

Before asking anything, silently gather context so the guidance is tailored.
Do not dump this audit unprompted.

Check:
- **Engine configured?** Read `.agents/docs/technical-preferences.md`. If the
  Engine field still contains `[TO BE CONFIGURED]`, the engine is not set.
- **Game concept exists?** Check for `design/gdd/game-concept.md`.
- **Source code exists?** Glob for source files in `src/` (`*.gd`, `*.cs`,
  `*.cpp`, `*.h`, `*.rs`, `*.py`, `*.js`, `*.ts`).
- **Prototypes exist?** Check for subdirectories in `prototypes/`.
- **Design docs exist?** Count markdown files in `design/gdd/`.
- **Production artifacts?** Check for files in `production/sprints/` or
  `production/milestones/`.

Store these findings internally so you can validate the user's self-assessment
and personalize the recommendation.

---

## Phase 2: Ask Where the User Is

This is the first thing the user sees. Ask a short plain-text question and give
these four options in the message so the user can answer with a letter or brief
phrase:

- `A. No idea yet` - no game concept yet, wants to explore
- `B. Vague idea` - has a theme, mood, or genre hint but nothing concrete
- `C. Clear concept` - knows the core idea and main mechanic, but has not formalized it
- `D. Existing work` - already has docs, prototypes, code, or planning artifacts

Use this opener:
"Welcome to Codex Game Studios. Before I suggest anything, where are you right
now with your game idea: A no idea yet, B vague idea, C clear concept, or D
existing work?"

Wait for the user's response before continuing.

---

## Phase 3: Route Based on Answer

#### If A: No idea yet

1. Acknowledge that starting from zero is normal.
2. Briefly explain what `/brainstorm` does. Mention two modes:
   - `/brainstorm open` for open exploration
   - `/brainstorm [hint]` if even a loose theme appears
3. Recommend `/brainstorm open` as the next step.
4. Show the path:

**Concept phase**
- `/brainstorm open` - discover the game concept
- `/setup-engine` - configure the engine after the concept is clearer
- `/art-bible` - define visual identity
- `/map-systems` - decompose the concept into systems
- `/design-system` - author a GDD for each MVP system
- `/review-all-gdds` - cross-system consistency check
- `/gate-check` - validate readiness before architecture work

**Architecture phase**
- `/create-architecture` - produce the master architecture blueprint and required ADR list
- `/architecture-decision (ADR-N)` - record key technical decisions
- `/create-control-manifest` - turn decisions into an actionable rules sheet
- `/architecture-review` - validate architecture coverage

**Pre-Production phase**
- `/ux-design` - author UX specs for key screens
- `/prototype` - build a throwaway prototype to validate the core mechanic
- `/playtest-report` - document vertical slice playtests
- `/create-epics` - map systems to epics
- `/create-stories` - break epics into implementable stories
- `/sprint-plan` - plan the first sprint

**Production phase**
- `/dev-story` - implement stories

#### If B: Vague idea

1. Ask them to share the vague idea in plain text. A few words is enough.
2. Validate it as a legitimate starting point.
3. Recommend `/brainstorm [their hint]`.
4. Show the same downstream path as A, but start with:
- `/brainstorm [hint]` - develop the idea into a full concept

#### If C: Clear concept

1. Ask them to describe the concept in one sentence, including genre and core mechanic.
2. Acknowledge it, then offer two plain-text paths:
   - `Formalize it first` - run `/brainstorm [concept]`
   - `Jump straight in` - go to `/setup-engine` and document afterward
3. Show the path:

**Concept phase**
- `/brainstorm` or `/setup-engine` - based on the user's preference
- `/art-bible` - define visual identity
- `/design-review` - validate the concept doc
- `/map-systems` - decompose the concept into systems
- `/design-system` - author a GDD for each MVP system
- `/review-all-gdds` - cross-system consistency check
- `/gate-check` - validate readiness before architecture work

**Architecture phase**
- `/create-architecture` - produce the master architecture blueprint and required ADR list
- `/architecture-decision (ADR-N)` - record key technical decisions
- `/create-control-manifest` - compile decisions into an actionable rules sheet
- `/architecture-review` - validate architecture coverage

**Pre-Production phase**
- `/ux-design` - author UX specs for key screens
- `/prototype` - build a throwaway prototype to validate the core mechanic
- `/playtest-report` - document vertical slice playtests
- `/create-epics` - map systems to epics
- `/create-stories` - break epics into implementable stories
- `/sprint-plan` - plan the first sprint

**Production phase**
- `/dev-story` - implement stories

#### If D: Existing work

1. Share the Phase 1 findings briefly:
   - source file count
   - design doc count
   - prototype count
   - engine configured or not
2. If the engine is not configured or only a concept exists:
   - recommend `/setup-engine` first
   - then `/project-stage-detect`
3. If GDDs, ADRs, stories, or broader artifacts already exist:
   - explain that file existence is not the same as template compatibility
   - recommend:
     1. `/project-stage-detect` - identify current stage and missing artifacts
     2. `/adopt` - audit whether existing artifacts match the expected internal format
4. Show the likely remediation path:
- `/project-stage-detect` - phase detection and existence gaps
- `/adopt` - format compliance audit and migration plan
- `/setup-engine` - if engine not configured
- `/design-system retrofit [path]` - fill missing GDD sections
- `/architecture-decision retrofit [path]` - fill missing ADR sections
- `/architecture-review` - rebuild technical traceability
- `/gate-check` - validate readiness for the next phase

---

## Phase 3b: Set Review Mode

Check whether `production/review-mode.txt` already exists.

If it exists:
- Read it
- Tell the user the current mode
- Do not ask again

If it does not exist:
- Ask one plain-text question:
  "One setup choice before we continue: do you want `full`, `lean`, or `solo`
  review mode?"
- Explain the three choices briefly:
  - `full` - director review at each major workflow step
  - `lean` - director review mainly at phase gates
  - `solo` - no director reviews
- When the user answers, write the normalized value to
  `production/review-mode.txt`:
  - `full`
  - `lean`
  - `solo`
- Create `production/` first if needed

This write does not need a separate approval prompt because the user's explicit
choice is the approval.

---

## Phase 4: Confirm Before Proceeding

After showing the recommended path, ask one plain-text confirmation question.
Never auto-run the next skill.

Use this pattern:
"The best next step looks like `[recommended command]`. Do you want to start
there, or would you rather take a different step first?"

If they choose something else, adapt and hand off accordingly.

---

## Phase 5: Hand Off

When the user confirms the next step, respond with a single short line:
"Type `[skill command]` to begin."

Do not re-explain the skill or add extra coaching. The `/start` skill's job is
done.

Verdict: **COMPLETE** - user oriented and handed off.

---

## Edge Cases

- **User picks D but project is empty**: gently redirect and explain that the
  repo still looks like a fresh template.
- **User picks A but code already exists**: mention that code was detected and
  confirm whether D fits better.
- **Returning user**: if engine and concept already exist, skip onboarding and
  orient them from current project state instead.
- **User does not fit any option**: let them describe the situation in their own
  words and adapt.

---

## Collaborative Protocol

1. Ask first - never assume the user's state or intent.
2. Present options - offer clear paths, not mandates.
3. Let the user decide - they pick the direction.
4. No auto-execution - recommend the next skill, do not run it unprompted.
5. Adapt - if the user's situation is unusual, listen and adjust.
