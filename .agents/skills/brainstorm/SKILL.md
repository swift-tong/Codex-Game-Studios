---
name: brainstorm
description: "Guided game concept ideation from zero idea to a structured game concept document. Uses professional studio ideation techniques, player psychology frameworks, and structured creative exploration."
argument-hint: "[genre or theme hint, or 'open'] [--review full|lean|solo]"
user-invocable: true
allowed-tools: Read, Glob, Grep, Write, WebSearch, spawn_agent
---

When this skill is invoked:

1. Parse the argument for an optional genre or theme hint. If `open` or no
   argument is given, start from scratch. Resolve review mode once for the whole
   run:
   - if `--review [full|lean|solo]` was passed, use that
   - else if `production/review-mode.txt` exists, use that value
   - else default to `lean`
   See `.agents/docs/director-gates.md` for gate behavior.

2. Check for existing concept work:
   - read `design/gdd/game-concept.md` if it exists
   - read `design/gdd/game-pillars.md` if it exists

3. Run through the ideation phases interactively. Do not generate the whole
   concept silently. The goal is collaborative exploration where Codex acts as a
   creative facilitator.

   At constrained decision points, ask plain-text choice questions. Present
   3-5 concise options in the message and let the user reply with an option or a
   custom answer.

   Professional studio brainstorming principles:
   - Withhold judgment.
   - Encourage unusual ideas.
   - Build with "yes, and..." rather than "but...".
   - Use constraints as creative fuel.
   - Time-box each phase to keep momentum.

---

### Phase 1: Creative Discovery

Start by understanding the person, not the game. Ask conversationally:

**Emotional anchors**
- What moment in a game genuinely moved, thrilled, or absorbed you?
- What specifically created that feeling?
- Is there a fantasy or power trip you have always wanted in a game?

**Taste profile**
- What 3 games have you spent the most time with, and what kept you coming back?
- What genres do you love or avoid, and why?
- Do you prefer games that challenge you, relax you, tell stories, or let you express yourself?

**Practical constraints**
- What kind of experience do you most want players to have?
  Suggested options: `Challenge & Mastery`, `Story & Discovery`,
  `Expression & Creativity`, `Relaxation & Flow`
- What is your realistic development timeline?
  Suggested options: `Weeks`, `Months`, `1-2 years`, `Multi-year`
- Where are you in your dev journey?
  Suggested options: `First game`, `Shipped before`, `Professional background`

Synthesize the answers into a **Creative Brief** in 3-5 sentences and confirm
it matches the user's intent.

---

### Phase 2: Concept Generation

Use the creative brief to generate **3 distinct concepts**. Each should use a
different ideation angle:

- **Verb-First Design**: start from the dominant player verb
- **Mashup Method**: combine two unexpected elements
- **Experience-First Design**: start from the target emotion and work backward

For each concept, present:
- **Working Title**
- **Elevator Pitch**
- **Core Verb**
- **Core Fantasy**
- **Unique Hook**
- **Primary MDA Aesthetic**
- **Estimated Scope**
- **Why It Could Work**
- **Biggest Risk**

After presenting all three, ask:
"Which concept resonates most? You can pick one, combine elements, or ask for
fresh directions."

Offer these plain-text options:
- `Concept 1 - [Title]`
- `Concept 2 - [Title]`
- `Concept 3 - [Title]`
- `Combine elements across concepts`
- `Generate fresh directions`

Never pressure the user toward a choice.

---

### Phase 3: Core Loop Design

For the chosen concept, collaboratively define the core loop.

**30-second loop**
- Ask what the primary feel of the core action should be.
- Generate 3-4 concept-specific options and include `I'll describe it`.
- Identify the single most important design dimension for this concept and ask
  the user to choose or describe it.

**5-minute loop**
- What structures the moment-to-moment play into cycles?
- Where does the "one more turn" or "one more run" pull come from?
- What decisions happen at this level?

**Session loop**
- What does a complete session look like?
- Where are the natural stopping points?
- What thought or goal keeps the game in the player's head between sessions?

**Progression loop**
- How does the player grow: power, knowledge, options, story, or something else?
- What is the long-term goal?
- When is the game "done"?

**Player motivation analysis**
- **Autonomy**: what meaningful choices does the player have?
- **Competence**: how does the player feel skill growth?
- **Relatedness**: how does the player feel connected to people, characters, or world?

---

### Phase 4: Pillars and Boundaries

Collaboratively define **3-5 game pillars**:
- Each pillar needs a name and one-sentence definition.
- Each pillar needs a design test: "If we are debating between X and Y, this
  pillar says choose __."
- Pillars should create useful tension, not repeat the same value.

Then define **3 or more anti-pillars**:
- What the game will not do
- Why each exclusion protects a pillar

After presenting the pillars, ask whether to:
- `Lock these in`
- `Rename or reframe one`
- `Swap a pillar out`
- `Something else`

If revisions are needed, iterate until the user explicitly locks them in.

**Review mode**
- `solo`: skip director review gates
- `lean`: skip non-phase-gate reviews
- `full`: run both gates below

In `full` mode, spawn both in parallel:
- `creative-director` using gate `CD-PILLARS`
- `art-director` using gate `AD-CONCEPT-VISUAL`

Pass the agreed pillars, anti-pillars, core fantasy, unique hook, and any
visual touchstones the user mentioned.

When the feedback returns:
- summarize creative-director feedback and resolve pillar concerns first
- summarize the art-director's 2-3 named visual directions
- let the user pick one, combine elements, or describe their own direction

Store the chosen result as the **Visual Identity Anchor**.

---

### Phase 5: Player Type Validation

Use Bartle taxonomy and Quantic Foundry style thinking to validate who the game
is for:
- who will love it most
- who may also enjoy it
- who it is not for
- which comparable games suggest real audience demand

---

### Phase 6: Scope and Feasibility

Ground the concept in reality:

- **Target platform**: ask what platforms the game is targeting.
  Suggested options: `PC`, `Mobile`, `Console`, `Web`, `Multiple platforms`
- **Engine experience**: ask whether the user already prefers `Godot`, `Unity`,
  `Unreal Engine 5`, or has `No preference`
  - if they pick an engine, record it and move on
  - if they have no preference, tell them `/setup-engine` will handle the full decision later
- **Art pipeline**: what style is needed and how expensive is it to produce?
- **Content scope**: estimate levels, areas, items, and playtime
- **MVP definition**: what is the smallest build that proves the core loop works?
- **Biggest risks**: technical, design, production, and market risks
- **Scope tiers**: what is full vision vs. reduced-but-shippable scope?

**Review mode**
- `solo`: skip `TD-FEASIBILITY` and `PR-SCOPE`
- `lean`: skip both
- `full`: run both

In `full` mode:
- spawn `technical-director` with gate `TD-FEASIBILITY` after technical risks are identified
- spawn `producer` with gate `PR-SCOPE` after scope tiers are defined

If feedback says the concept is high risk or unrealistic, offer to reduce scope
before generating the final document.

---

### Phase 7: Draft and Write Approval

Generate the concept document using `.agents/docs/templates/game-concept.md`.
Fill in all sections from the brainstorm conversation, including:
- MDA analysis
- player motivation profile
- flow state design
- Visual Identity Anchor

**Scope consistency rule**
- The `Estimated Scope` field in the summary table must match the full-vision
  timeline from the scope tiers section.
- Write it in a concrete form such as `Large (12-18 months, solo)` or
  `Large (8-12 months, team of 3)`.

Before writing:
1. Show a concise concept summary.
2. Ask: "Game concept is ready. May I write it to `design/gdd/game-concept.md`?"
3. If the user wants changes, ask which section to revise:
   - `Elevator Pitch`
   - `Core Fantasy & Unique Hook`
   - `Pillars`
   - `Core Loop`
   - `MVP Definition`
   - `Scope Tiers`
   - `Risks`
   - `Something else`
4. Revise, show the change clearly, and ask again.
5. Only write after explicit approval.

---

### Phase 8: Next Steps

After writing the concept, recommend this pipeline:
1. `/setup-engine`
2. `/art-bible`
3. `/design-review design/gdd/game-concept.md`
4. `/map-systems`
5. `/design-system`
6. `/create-architecture`
7. `/architecture-decision (ADR-N)`
8. `/gate-check`
9. `/prototype [core-mechanic]`
10. `/playtest-report`
11. `/sprint-plan new`

End with a short summary containing:
- elevator pitch
- pillars
- primary player type
- engine preference or undecided state
- biggest risk
- file path

Verdict: **COMPLETE** - game concept created and handed off for next steps.

---

## Context Window Awareness

If context reaches or exceeds 70% during the workflow, append this notice to the
current response:

> **Context is approaching the limit (>=70%).** The game concept document is
> saved to `design/gdd/game-concept.md`. Open a fresh Codex session to continue
> if needed - progress is not lost.
