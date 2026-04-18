---
name: hermes-onboard
description: "Full onboarding for a new Hermes user. Covers personal profile, family, communication preferences, mental model, AND vault structure — with an integrated LLM Wiki. Trigger whenever onboarding a new user, setting up a second brain, or building a user profile for the first time."
tags: [onboarding, vault, profile, wiki, knowledge-base]
category: setup
---

# Hermes Onboard

Full onboarding for a new Hermes user. Build a rich personal profile, capture how the user thinks and organizes, design a personalized vault structure, and initialize the integrated LLM Wiki as the knowledge backbone.

## Run-once guard and recovery

Before asking onboarding questions:

1. Check for `~/.hermes/.onboarding-state.json`.
   - If it exists, onboarding was interrupted.
   - Read it, inspect what has already been created, and repair or finish the missing pieces instead of starting over.
   - Preserve existing user-authored content. Do not clobber a partially built workspace during recovery.
2. If no onboarding-state file exists, check whether `~/.hermes/AGENTS.md` already exists.
   - If it does, onboarding has already completed. Stop and tell the user not to re-run this skill.
3. As soon as onboarding begins, create `~/.hermes/.onboarding-state.json` with:
   - `schema_version`
   - `started_at`
   - `completed_steps`
   - `required_artifacts`
4. Update the manifest each time a required artifact is successfully created.
5. Delete the manifest only after all scaffold files, directory creation, and memory writes succeed.

Recommended manifest shape:

```json
{
  "schema_version": 1,
  "started_at": "YYYY-MM-DDTHH:MM:SSZ",
  "completed_steps": [],
  "required_artifacts": [
    "AGENTS.md",
    "SOUL.md",
    "memory:user",
    "memory:memory",
    "family/",
    "brain/",
    "areas/",
    "knowledge/",
    "templates/optional"
  ]
}
```

Re-running onboarding after completion is not allowed. Life changes get handled through normal file updates in the workspace, not by restarting the onboarding skill.

## Conversation Style

Run this as a conversation, not a survey.

- Ask 2-3 questions at a time, then wait.
- Follow the user's energy and wording.
- Do not rigidly force the outline order.
- Summarize occasionally so the user can correct you.
- Use `none yet` for unknowns instead of fabricating.
- The user must choose an agent name before you scaffold files. This is required because the agent identity is written into `AGENTS.md`, `SOUL.md`, and the session-start protocol.
- If the user is stuck on the agent name, offer a few short suggestions with meaning.

## Minimum Viable Onboarding Threshold

The goal is not an exhaustive profile. Gather enough to scaffold safely, then build.

Once you have the following, stop broad discovery and create the scaffold:

- preferred name
- location or timezone
- chosen agent name
- communication style and quiet hours, or an explicit `none set`
- basic household map
- work summary or current focus
- 2-6 life areas
- current goals or north star
- any explicitly named active projects

Anything missing gets `none yet`.

If the user becomes terse, says "that's enough," or gives partial answers, scaffold immediately with what is known. Do not keep interviewing just to make the profile feel complete.

## Phase 1: Personal Profile

Cover these topics naturally. Let the conversation flow; do not force a checklist order.

### Identity and Basics
- name and what they prefer to be called
- location and timezone
- phone number, optional

### Daily Life
- typical day: wake time, work hours, evening rhythm
- morning ritual
- currently watching, reading, or playing
- food relationship: foodie or fuel

### Work and Projects
- what they do and how long they have done it
- active projects or businesses
- work style: planner or builder, deep focus or context-switching
- strengths and energy drains

### Family and Household
- who lives in the house: partner, kids, pets
- names, birthdays, relationships
- notable details: hobbies, schools, schedules
- extended family worth knowing about

### Interests and Hobbies
- fun, music, sports, collections, creative outlets
- travel preferences
- hidden passions or guilty pleasures

### Communication Preferences
- brief or detailed delivery
- tone: formal, casual, snarky, warm, etc.
- when to proactively reach out vs. stay quiet
- what annoys them in an AI assistant
- quiet hours: when to never message
- required: agent name

### Goals and Aspirations
- what they are working toward now
- long-term dreams or someday projects
- what success looks like to them

### Pet Peeves and Boundaries
- things they hate in AI responses or in general
- off-limits or sensitive topics
- privacy boundaries for group chats

## Phase 2: Mental Model and Vault Structure

Transition naturally: "Now let's talk about how things should be organized so the agent can find what matters."

The vault is always **agent-first**. Do not ask the user whether they want a human-browsed setup.

### Vault Posture

Rules:
- templates exist so the agent stays consistent, not for manual template-picking
- `AGENTS.md` must include `Primary Consumer: {agent-name}` and a session-start protocol
- `knowledge/index.md` and `knowledge/SCHEMA.md` are operational references; keep them readable, but do not design the vault around manual browsing

### Life Categories
- how they mentally bucket life: areas, roles, projects, or organic
- work and personal: separate or blended
- which categories feel most important to track

### Information Habits
- existing system: GTD, PARA, Zettelkasten, bullet journal, all in my head, etc.
- where things currently live
- what they wish they could find but cannot
- whether saved information is meant for return visits or just-in-case parking

### Task and Project Flow
- how they track what they are working on
- how they decide what to do next: urgency, energy, deadlines, gut feel
- plan ahead or react in the moment
- quick sprints or slow burns

### What Falls Through the Cracks
- what they forget most often
- where good ideas go to die
- whether the real problem is capturing, organizing, or retrieving

### Reference vs. Action
- searchable knowledge base, task-driving system, or both
- archiving finished work vs. clearing the deck

### Note Types
- note types they actually take: meeting notes, ideas, research, journal, project plans, checklists, etc.
- this determines which templates to create

## Vault Architecture

The vault has three conceptual layers:

```text
~/.hermes/obsidian/
├── family/               # Layer 1: People — household overview + per-person files
├── brain/                # Layer 1: Agent operational memory
│   ├── North Star.md     #   Current top-level goals and focus
│   ├── Memories.md       #   Index of all brain files
│   ├── Key Decisions.md  #   Big choices that define the landscape
│   ├── Patterns.md       #   Repeating behaviors and tendencies
│   └── Gotchas.md        #   Things NOT to do, quirks to work around
├── {area}/               # Layer 2: User life domains (career/, health/, finances/, etc.)
│   ├── {area}.md         #   Area index — the front door to this area
│   └── {project}/        #   Projects within this area
│       ├── {project}.md  #     Project file
│       └── docs/         #     Project-specific research (raw, immutable)
└── knowledge/            # Layer 3: LLM Wiki — evergreen cross-project knowledge
    ├── SCHEMA.md         #   Wiki conventions, tag taxonomy, page thresholds
    ├── index.md          #   Sectioned content catalog — every wiki page listed
    ├── log.md            #   Chronological action log — append-only
    ├── raw/              #   Immutable sources (articles, papers, transcripts, assets)
    │   ├── articles/
    │   ├── papers/
    │   ├── transcripts/
    │   └── assets/
    ├── entities/         #   People, orgs, products
    ├── concepts/         #   Topics, techniques, ideas
    ├── comparisons/      #   Side-by-side analyses
    └── queries/           #   Filed query results worth keeping
```

## Area ↔ Wiki Bidirectional Link

This is the core integration principle.

### Area files link to wiki pages
- each area index file (`{area}/{area}.md`) links to relevant `knowledge/concepts/` and `knowledge/entities/` pages
- project files link to wiki concepts that inform them

### Wiki pages link back to area files
Every `knowledge/entities/*.md` and `knowledge/concepts/*.md` must link back to their owning area in both places:

1. frontmatter: `areas: [{area-slug}]`
2. body: inline `[[{area}/{area}]]` wikilink

Both are required. Frontmatter alone does not create a navigable backlink, and a wikilink alone is not queryable.

### Research split is the boundary
- project-specific research → `{project}/docs/` (raw, immutable)
- evergreen knowledge worth keeping → `knowledge/entities/`, `knowledge/concepts/`
- rule: "If you'd want this info again for a different project, it's knowledge. If it only matters for this one thing, it's docs. When in doubt, start in docs/ and promote it later."

## brain/ Files

Create and maintain these six files:

- `North Star.md` — current top-level goals and focus areas
- `Memories.md` — index of all brain files; read at session start
- `Key Decisions.md` — major choices about vault, workflow, or life direction
- `Patterns.md` — recurring habits, tendencies, leverage points, and pitfalls
- `Gotchas.md` — explicit do-not-dos and quirks to work around

## AGENTS.md vs. SCHEMA.md Ownership

`AGENTS.md` is the workspace operating manual.
`knowledge/SCHEMA.md` is the wiki schema authority.

Write into `AGENTS.md`:
- session-start protocol
- vault structure
- naming rules
- research-split rule
- area ↔ wiki integration principle
- orientation step that points to `knowledge/SCHEMA.md`, `knowledge/index.md`, and `knowledge/log.md`
- maintenance rules and update matrix

Write into `knowledge/SCHEMA.md`:
- full wiki frontmatter schema
- tag taxonomy
- page creation thresholds
- cross-linking rules
- contradiction handling
- page split rules
- raw-source immutability rule

Do not duplicate detailed wiki schema text in both places.

On conflict:
- workspace-level operating rules → `AGENTS.md`
- wiki-internal structure and taxonomy → `knowledge/SCHEMA.md`

## File Creation Checklist

After the conversation reaches the minimum viable threshold, create everything in the same session. Do not promise to do it later.

Treat each numbered item below as a required artifact in the onboarding-state manifest.

### 1. `~/.hermes/AGENTS.md` (critical — do first)

This is the workspace operating manual for any agent that enters the Hermes environment.

Write it first and write it completely.

Use this structure, customized with the user's real details:

```markdown
# AGENTS.md — Operating Context for {user-first-name}'s Hermes workspace

> Note: "Hermes" is the system. The agent operating inside it is named `{agent-name}`. Use `{agent-name}` in persona-facing contexts and "Hermes" only for system-level behavior.

## Primary Consumer
Primary consumer is `{agent-name}`. This vault is agent-facing and optimized for retrieval, not manual browsing.

## Session Start Protocol
When starting a session, read in order:
1. `~/.hermes/SOUL.md`
2. `~/.hermes/memories/` via memory tool
3. `~/.hermes/obsidian/brain/Memories.md`
4. `~/.hermes/obsidian/brain/North Star.md`
5. relevant area index files
6. for wiki work: `knowledge/SCHEMA.md`, `knowledge/index.md`, and the last 20 lines of `knowledge/log.md`

## Vault Structure

`~/.hermes/obsidian/`
- `family/` — household members and upcoming dates
- `brain/` — always-read operational memory
- `{area}/` — life domains (enumerated below)
- `knowledge/` — evergreen wiki
- `templates/` — only for note types the user actually takes

### Areas

| Area | What's in it |
|------|-------------|
| `brain/` | Agent operational memory — goals, patterns, decisions, skills (root-level, always loaded) |
| `{area}/` | (fill from Phase 2 — e.g., career, health, finances, side-projects, family) |

### Primary Consumer Implications

- No Home.md, no landing pages.
- No dashboards/ folder. Open tasks are found by grepping for `- [ ]`.
- No plugin dependencies (Tasks, Dataview, etc.). Retrieval is direct file reading and grep.
- Templates exist so the agent stays consistent when creating notes — not for manual picking.
- Frontmatter is structured metadata for filtering, not for plugin queries.

### Tasks

Tasks live inline in project files as `- [ ]`. Mark complete with `- [x]`.
No separate task files. No plugins.

Example:
```markdown
## Implementation
- [x] Write SPEC.md
- [ ] Set up repository
- [ ] Implement auth
```

### Project File Frontmatter

```yaml
---
area: {area-slug}
status: active | paused | done
priority: high | normal | low
created: YYYY-MM-DD
tags: []
---
```

Priority: `high` = do first, `normal` = steady progress, `low` = when bandwidth allows.

### Cross-Project Linking

Use Obsidian wikilinks `[[note-name]]`. Folder location doesn't matter — backlinks just work.

## Folder Conventions

### Naming
- files: lowercase-kebab-case inside areas, projects, templates, and wiki pages unless a control document has a fixed conventional name
- folders: lowercase-kebab-case

### Research Split
- project-specific research → `{project}/docs/`
- evergreen knowledge → `knowledge/entities/`, `knowledge/concepts/`
- when in doubt, start in docs and promote later

### Area ↔ Wiki Linking
- area indexes link to relevant wiki concepts and entities
- wiki entity and concept pages link back to their owning area in both places:
  1. frontmatter `areas: [{area-slug}]`
  2. body `[[{area}/{area}]]`

### Template Usage
- create templates only for note types the user actually takes
- templates are for agent consistency, not manual browsing workflows

## Wiki Orientation
Before any wiki operation, read:
1. `knowledge/SCHEMA.md` — wiki conventions and tag taxonomy
2. `knowledge/index.md` — what wiki pages exist
3. last 20 lines of `knowledge/log.md` — recent activity

When performing wiki operations (ingest, query, lint, create, or update wiki pages), load the `llm-wiki` skill for the full operational reference. The skill is the authoritative procedure; AGENTS.md holds the high-level ownership rules.

## AGENTS.md vs. SCHEMA.md Ownership
- `AGENTS.md` owns workspace-level operating rules
- `knowledge/SCHEMA.md` owns wiki schema and taxonomy
- on conflict, the owner above wins

## Maintenance Rules

### Canonical Source on Conflict
- workspace operating rules → this file
- wiki schema and taxonomy → `knowledge/SCHEMA.md`
- personal profile → newer verified edit wins; memory is the always-loaded mirror, not the long-form source
- family composition and household facts → `family/README.md` and `family/*.md`
- area and project context → area indexes and project files

### Update Matrix
- memory target `user` → name, location, family snapshot, work summary, communication preferences, agent name, quiet hours
- memory target `memory` → vault path, `AGENTS.md` as control plane, research split, naming conventions, durable workflow facts
- `brain/North Star.md` → goals and priorities
- `brain/Patterns.md` → work and decision tendencies
- `brain/Gotchas.md` → hard boundaries, pet peeves, explicit do-not-dos
- `brain/Key Decisions.md` → major structural or life decisions
- `brain/Skills.md` → reusable solved workflows
- `family/` → people details, dates, gift ideas, notes
- `knowledge/SCHEMA.md` → taxonomy and schema updates
- `knowledge/index.md` → new wiki pages
- `knowledge/log.md` → every wiki action

### File in Real Time
Do not leave durable facts trapped in chat history. File them immediately into their canonical location.
- decisions, blockers, progress → project file
- durable preferences or corrections → `brain/Gotchas.md` or `SOUL.md`
- goals or strategic shifts → `brain/North Star.md`
- family changes → `family/`
- reusable workflows → `brain/Skills.md`

### Gap Filling
Ask one natural follow-up when conversation creates room. Do not run scheduled profile interviews.

## System Principles

Default principles (customize for the user, but these are strong defaults):
- **Agent-first.** No plugin dependencies. Retrieval is grep + direct read.
- **Areas → projects → tasks.** Clean hierarchy, no detours.
- **Action over archive.** The active stuff matters more than the historical record.
- **Knowledge is reusable, docs are not.** Promote aggressively from `docs/` to `knowledge/` when something starts mattering across projects.
- **No empty folders for the future.** Build only what maps to something real.
- This structure is a starting point and will evolve.
```

### 2. `~/.hermes/SOUL.md`

Write the persona file.

Persona only. No vault structure, no wiki rules, no file-maintenance rules.

Include:
- agent name and meaning, if chosen
- how to talk: tone, length, markdown usage, formality
- how to think: framing, when to push back, when to ask vs. decide
- hard rules: pet peeves and boundaries as absolutes
- quiet hours
- the user's north star in 1-2 sentences

Keep it lean, under about 4 KB.

### 3. Memory tool (critical — do early)

Use the `memory` tool.

- `target: user` → name, location, household snapshot, work summary, communication preferences, agent name, quiet hours
- `target: memory` → vault path, that `AGENTS.md` is the workspace operating manual, the research-split rule, naming conventions, and other durable workflow facts

Memory is tight. Keep only always-loaded retrieval handles in memory.

Before writing, ask whether the fact truly needs to be loaded every session.

Route overflow by content type:
- household, birthdays, person-specific details → `family/`
- goals and current priorities → `brain/North Star.md`
- behavior patterns and energy rhythms → `brain/Patterns.md`
- boundaries, pet peeves, and do-not-dos → `brain/Gotchas.md`
- workspace conventions → `AGENTS.md`
- work, areas, and projects → area index or project file

Use `replace` when updating memory entries rather than creating duplicates.

### 4. `family/` files

Create:

- `~/.hermes/obsidian/family/README.md` — household overview table plus upcoming dates for the current year
- `~/.hermes/obsidian/family/{firstname}.md` — one file per person, including pets

Template:

```markdown
# {Name}
**Relationship:** {relationship}
**Birthday:** {date}

## Preferences
(none yet)

## Important Dates
- **Birthday:** {date}

## Gift Ideas
(none yet)

## Notes
(none yet)
```

### 5. Area folders

Create area folders from the user's actual mental model.

Each area gets:
- `{area}/{area}.md` — area index with overview, current projects, and existing wiki links
- `{area}/{project}/` — only if the user named a specific active project
  - `{project}.md`
  - `docs/`

Do not scaffold empty project folders just in case. If a project is only vaguely described, note it under `## Potential Projects` in the area index and create the folder only when the project actually starts.

Area index template:

```markdown
---
title: {Area Name}
areas: [{area-slug}]
---

# {Area Name}

## Overview
(what this area covers, current state, context)

## Wiki Knowledge
- (none yet)

## Current Projects
- (none yet)

## Notes
(none yet)
```

If relevant wiki pages or projects already exist, replace `none yet` with real links. Do not invent pages that do not exist.

### 6. `knowledge/` — LLM Wiki

Initialize the full wiki structure inside `~/.hermes/obsidian/knowledge/`:

- `SCHEMA.md`
- `index.md`
- `log.md`
- `raw/articles/`
- `raw/papers/`
- `raw/transcripts/`
- `raw/assets/`
- `entities/`
- `concepts/`
- `comparisons/`
- `queries/`

#### `knowledge/SCHEMA.md`

Write the wiki authority document.

It must include:
- purpose of the wiki
- required frontmatter fields
- tag taxonomy customized to the user's actual areas
- page creation thresholds
- cross-linking rules
- contradiction handling
- split pages over roughly 200 lines into sub-topics with cross-links
- rule that `raw/` sources are immutable

Required frontmatter template:

```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query | summary
tags: [from taxonomy below]
sources: [raw/articles/source-name.md]
areas: [{area-slug}]
---
```

Cross-linking rules:
- every wiki page must link to at least 2 other wiki pages when such pages exist
- entity and concept pages must link back to their owning area in both frontmatter and body

Contradiction handling:
1. newer sources generally supersede older ones
2. if genuinely contradictory, note both with dates and sources
3. mark in frontmatter: `contradictions: [page-name]`
4. flag for user review

#### `knowledge/index.md`

Create a sectioned catalog with headers for:
- Entities
- Concepts
- Comparisons
- Queries

Start empty except for the headers.

#### `knowledge/log.md`

Create the initial entry:

```markdown
## [YYYY-MM-DD] create | llm wiki initialized
- Areas covered: {area1}, {area2}
- Initialized during user onboarding
```

### 7. `brain/` files

Create all six files in `~/.hermes/obsidian/brain/`:

- `North Star.md` — fill from the user's current goals
- `Memories.md` — index of all brain files
- `Key Decisions.md` — placeholder populated from Phase 2 decisions
- `Patterns.md` — lifestyle and work patterns from Phase 1
- `Gotchas.md` — pet peeves and boundaries from Phase 1
- `Skills.md` — placeholder that will grow through problem-solving

### 8. `templates/`

Create `~/.hermes/obsidian/templates/` only if the user actually takes recurring note types.

Common examples:
- `meeting-notes.md`
- `project.md`
- `client.md`
- `research-doc.md`

Do not create daily-note or journal templates unless the user explicitly said they use them.

## Important

- Phase 2 answers directly shape the vault. Build from what the user said, not from generic defaults.
- Write all scaffold files in the same session.
- Use information actually shared. Do not infer or fabricate.
- Use `none yet` for empty sections.
- This vault is always agent-first.
- `AGENTS.md` is the workspace operating manual.
- `knowledge/SCHEMA.md` is the single source of truth for wiki schema and taxonomy.
- Do not scaffold empty project folders.
- Delete `~/.hermes/.onboarding-state.json` only after every required artifact and memory write succeeds.
- After onboarding is complete, future changes happen through direct file maintenance, not by re-running this skill.
