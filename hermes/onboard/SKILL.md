---
name: onboard
description: "Use this skill in the initial conversation with your user. Covers personal profile, family, communication preferences, AND how the user thinks and organizes — then generates a personalized Obsidian vault structure. Trigger whenever onboarding a new user, setting up a second brain, or building a user profile for the first time."
---

You're getting to know your human for the first time. Your goal is to build
a rich personal profile AND a vault structure that mirrors how they actually
think — so every future interaction feels personal, useful, and organized.

Run this as a CONVERSATION — not a survey. Ask 2-3 questions at a time,
wait for answers, then ask follow-ups based on what they share. Be genuinely
curious, not clinical. If they give short answers, don't push — you'll learn
more over time.

There are two phases. Phase 1 captures who they are. Phase 2 captures how
they think and organize. Transition naturally between them — don't announce
"Phase 2 starting now."

---

## Phase 1: Personal Profile

What to cover (let it flow naturally, don't force the order):

Identity & Basics
- Name, what they prefer to be called
- Location, timezone
- Phone number (if they want you to have it)

Daily Life
- Typical day — wake time, work hours, evening routine
- Morning ritual
- Currently watching/reading/playing?
- Food relationship — foodie or fuel?

Work & Projects
- What they do, how long they've been doing it
- Current active projects or businesses
- Work style — planner or builder? Deep focus or context-switching?
- Strengths and energy drains

Family & Household
- Who lives in the house? Partner, kids, pets?
- Names, birthdays, relationships
- Notable details — hobbies, schools, schedules
- Extended family worth knowing about

Interests & Hobbies
- What they do for fun
- Music, sports, collections, creative outlets
- Travel preferences
- Hidden passions or guilty pleasures

Communication Preferences
- Brief or detailed info delivery?
- Tone — formal, casual, snarky, warm?
- When to proactively reach out vs. stay quiet
- What annoys them in an AI assistant
- Quiet hours — when to never message
- OPTIONAL: offer to pick an agent name for yourself. Some users love
  this and it becomes a meaningful personalization anchor. If they
  give you naming rights, pick something with intention (meaning
  behind the name) and explain the choice briefly. If they decline
  or seem indifferent, don't push.

Goals & Aspirations
- What they're working toward now
- Long-term dreams or "someday" projects
- What success looks like to them

Pet Peeves & Boundaries
- Things they hate (AI responses, general)
- Off-limits or sensitive topics
- Privacy boundaries for group chats

---

## Phase 2: Mental Model & Vault Scaffolding

This phase captures HOW the user thinks, works, and organizes — so the
vault structure reflects their brain, not a generic template.

Transition naturally from Phase 1. Something like: "Now let's talk about
how you want to organize things — so the vault works like your brain, not
mine."

### Agent-First vs. Human-Browsed Vault (ask early)

Ask the user directly: "Do you plan to open and browse this vault
yourself in Obsidian, or is this primarily the agent's memory store
that you'll rarely touch directly?"

This is THE most consequential design question in the whole skill —
it changes what files to create and how to frame them. Two modes:

**Agent-first (default assumption for most users doing second-brain
with an AI):**
- No Home.md landing page — agent reads VAULT.md + brain/Memories.md
  at session start instead
- No dashboards/ folder — agent greps for `- [ ]` when it needs open
  tasks
- No plugin dependencies (Tasks, Dataview, etc.) — retrieval is
  direct file reading and grep
- Templates exist so the AGENT stays consistent when creating notes,
  not for the user to pick from
- Frontmatter is structured metadata for agent filtering, not for
  plugin queries
- VAULT.md includes a "Primary Consumer: [agent name]" section and a
  "Session Start Protocol" list

**Human-browsed (user opens Obsidian and clicks around):**
- Create Home.md as a landing page with wikilinks to active areas
- Consider dashboards/ with Tasks-plugin queries if they use Tasks
- Templates and frontmatter serve the user's workflow too
- Can lean on Obsidian plugins the user already has installed

**Hybrid (rare — most users are one or the other):**
- Build agent-first, but keep files extra-readable so the occasional
  manual browse isn't painful

Default to **agent-first** if the user is ambiguous or says "mostly
for you." That's the more common case and it degrades gracefully —
an agent-first vault is still perfectly browsable if the user
occasionally opens a file.

What to cover:

Life Categories
- How do they mentally bucket their life? By roles (dad, founder,
  employee), areas (health, career, finances), projects, or something
  more organic?
- Do they think of work and personal as separate worlds or blended?
- Are there categories that feel more important to track than others?

Information Habits
- Do they have an existing system or methodology? (GTD, PARA,
  Zettelkasten, bullet journal, or "it's all in my head")
- Where does stuff currently live? (notes app, scattered docs, browser
  tabs, memory)
- What do they wish they could find but can't?
- When they save something, do they expect to come back to it or is it
  more "just in case"?

Task & Project Flow
- How do they track what they're working on? (app, list, mental queue)
- How do they decide what to work on next? (urgency, energy, deadlines,
  gut feel)
- Do they plan ahead or react in the moment?
- What does their project lifecycle look like — quick sprints or slow
  burns?

What Falls Through the Cracks
- What do they forget or lose track of most often?
- Where do good ideas go to die?
- Is the problem capturing things, organizing them, or retrieving them?

Reference vs. Action
- Do they want a searchable knowledge base, a task-driving system, or
  both?
- How important is archiving finished work vs. clearing the deck?

Note Types
- What kinds of notes do they take most often? (meeting notes, ideas,
  research, journal entries, project plans, checklists)
- This shapes which templates to create — only build templates for things
  they actually do.

---

## Output: Files to Create

After BOTH phases are complete, create all files in the same session.
Don't promise to do it later.

### Hermes-Native Memory (USER.md and MEMORY.md)

CRITICAL: Hermes has a built-in memory layer at
`~/.hermes/memories/USER.md` and `~/.hermes/memories/MEMORY.md`,
managed by the `memory` tool. These files are loaded into every turn
automatically. **Do NOT create USER.md or MEMORY.md inside the
Obsidian vault** — that creates two sources of truth that will drift
apart.

Instead, use the `memory` tool with:
- `target: user` — identity facts, family, work context, communication
  preferences, agent name, quiet hours. Keep each entry compact
  (1–3 sentences). The memory tool has a character limit, so prioritize
  what the agent needs every turn, not everything you learned.
- `target: memory` — durable environment/workflow facts: vault path,
  vault rules, rejected patterns ("no inbox"), naming conventions,
  research-split rule, anything that prevents a future session from
  re-deriving how things work.

Rich context that doesn't fit in the memory tool (detailed daily
rhythm, hobby lists, music taste, extended self-knowledge) goes into
`brain/Patterns.md` under a "Lifestyle Context" section, NOT into a
vault-root USER.md.

Deeper self-knowledge insights (work style, core drives, decision
patterns) go into `brain/Patterns.md` — the brain file is the right
home for "how this person operates" observations.

### family/README.md

Household overview table with names, relationships, birthdays, ages.
Include an "Upcoming Dates" section for the current year listing
birthdays and anniversaries chronologically.

### family/{firstname}.md (one per family member)

Use this template for each person mentioned:

  # {Name}
  **Relationship:** {relationship to user}
  **Birthday:** {date}
  ---
  ## Preferences
  (none yet)
  ## Important Dates
  - **Birthday:** {date}
  ## Gift Ideas
  (none yet)
  ## Notes
  (none yet)

Include pets too (simpler format — name, breed/species, any quirks).

### Vault Structure Files

Generate a personalized vault structure based on Phase 2 answers. This is
the most important part — the structure should feel like it came from the
user, not from a template.

Guiding principles:
- Lightweight over comprehensive. Lean toward 3-5 top-level folders,
  but honor the user's actual mental model if they clearly bucket
  their life into more categories. Don't force a fake simplification
  to hit an arbitrary number.
- Folders map to how the user THINKS, not an ideal system.
- Don't create empty folders "just in case" — only build what maps to
  something the user actually talked about.
- The structure will evolve over time. Get the bones right; the daily
  cron and ongoing conversations will fill in the rest.

Decision logic for top-level structure:

If the user thinks in AREAS OF LIFE:
  → Top-level folders like career/, health/, finances/, relationships/
  → Projects nest inside the relevant area

If the user thinks in ROLES:
  → Top-level folders like founder/, employee/, parent/
  → Each role contains its own projects and reference material

If the user thinks in PROJECTS:
  → A projects/ folder with active/ and archive/ subfolders
  → A reference/ folder for non-project knowledge

If HYBRID (most common):
  → Combine approaches. Areas or roles at top level, projects nested
    inside, with a cross-cutting index if needed.

If the user has a KNOWN METHODOLOGY (GTD, PARA, etc.):
  → Respect it. Build the structure around their existing mental model.
    Don't fight their system — augment it.

Per-area structure conversations (IMPORTANT):
Once you know the top-level shape, DO NOT assume every area should be
structured the same way. Ask about each meaningful area individually —
the user often has different mental models for different parts of
their life. Examples from real onboardings:
  - Day job might be organized by initiative
  - Consultancy might be organized by client
  - Health might be organized by condition/initiative (sleep apnea,
    fitness)
  - Side projects might be ad-hoc, with structure decided per-project
    when each one is born
Walking through each area one-by-one is the key unlock for a vault
that actually feels bespoke instead of templated. Don't batch-build
areas with identical structure unless the user explicitly says
that's what they want.

Always create these regardless of structure choice:
- templates/ — Starter templates based on the note types the user
  actually described. In agent-first mode, these exist so the agent
  stays consistent when creating notes — not for the user to pick
  from manually. Only create 2-3 templates for things they said they
  do. Common ones: meeting-notes.md, project.md, client.md,
  research-doc.md. No daily-note or journal templates unless the
  user explicitly does those.

Propose but don't force:
- inbox/ — A universal capture point for quick thoughts, links, ideas
  that don't have a home yet. Ask the user first — some people rely on
  inboxes, others find them a graveyard of unsorted junk. If the user
  says no, respect it and design a different ingestion path later.
- knowledge/ — Evergreen reusable atomic notes (one concept per file,
  heavily wikilinked). Use this when the user wants a "connected brain"
  with reference material that transcends any single project. Pair
  with the research-split rule below.
- dashboards/ — ONLY create this if the user is in human-browsed mode
  AND explicitly wants cross-project visibility powered by the Tasks
  plugin or Dataview. In agent-first mode (the default), DO NOT create
  dashboards/ — the agent finds open tasks by grepping for `- [ ]`
  directly. This folder is an anti-pattern for agent-first vaults.

Research-split pattern (propose this when the user asks about
research/docs or has projects that generate reference material):
  - Project-specific research → `project-folder/docs/`
  - Evergreen reusable knowledge → top-level `knowledge/` as atomic
    notes, wikilinked from projects
  - The rule: "If you'd want this info again for a different project,
    it's knowledge. If it only matters for this one thing, it's docs.
    When in doubt, start it in the project folder and promote it
    later."
  This pattern solves the #1 Obsidian rot failure mode (research
  buried inside one project, never found again).

Do NOT create README.md files in each folder just to describe what
the folder is — VAULT.md covers that, and folder-level READMEs create
maintenance burden and drift.

Exceptions (README.md is OK when it holds operational instructions or
actual data, not just a folder description):
- `family/README.md` — household overview table and upcoming dates.
  This one holds real data, always create it.
- `knowledge/README.md` — only useful in human-browsed mode where the
  user might open the folder and need the research-split rule inline.
  In agent-first mode, skip it — the rule lives in VAULT.md and the
  agent reads VAULT.md at session start.
- `dashboards/README.md` — only exists if dashboards/ exists, which
  only happens in human-browsed mode.

Rule of thumb: if the README would just repeat what VAULT.md says,
don't create it. If it explains how to *use* the folder or holds data
that belongs with the folder, it's fine.

VAULT.md (root level)
This is the vault's single source of truth for structure and
organization. Everything about "how the vault works" lives here — the
agent should never need to look anywhere else to understand the system.
Include:
- **Primary Consumer section (agent-first mode):** State explicitly
  that the vault is agent-facing, the agent's name, and the design
  implications (no landing pages, no plugin dependencies, optimize
  for retrieval not browsing). Skip this section in human-browsed
  mode.
- **Session Start Protocol:** In agent-first mode, list the exact
  order of files the agent should read at session start (VAULT.md,
  brain/North Star.md, brain/Memories.md, brain/Open Threads.md, then
  relevant files). Gives the agent an unambiguous boot sequence.
- Overview of the folder structure and the reasoning behind it
- What goes where (decision rules, not just descriptions)
- File creation rules: frontmatter template, naming conventions, inbox
  fallback rule, template usage, and any cleanup expectations
- Naming conventions (use the user's preference if stated, otherwise
  suggest lowercase-kebab-case for files and folders)
- Tagging strategy if the user wants tags, or a note that tags aren't
  in use yet
- A "System Principles" section capturing the user's stated preferences
  about organization (e.g., "action over archive", "keep it flat",
  "everything is a project", "separate work and personal"). In
  agent-first mode, include "no plugin dependencies" as a principle.
- A note that this structure is a starting point and will evolve

IMPORTANT: VAULT.md is the single source of truth for vault structure.
Do NOT duplicate the folder tree, file creation rules, or naming
conventions in brain/ files or other system instructions — just point to
VAULT.md. This avoids drift between two files that describe the same
thing.

### Home.md (conditional — human-browsed mode only)

**Agent-first mode (default):** Do NOT create Home.md. The agent
doesn't open the vault in Obsidian and doesn't need a landing page.
The session start protocol in VAULT.md tells the agent exactly which
files to read first.

**Human-browsed mode:** Create `~/.hermes/obsidian/Home.md` as a
simple landing page that wikilinks to VAULT.md, brain/North Star.md,
brain/Memories.md, each active area file, and the key people. This
is the file the user opens first when they launch the vault in
Obsidian. Keep it short — it's an index, not a dashboard. Do NOT
wikilink to USER.md or MEMORY.md — those live in
`~/.hermes/memories/` outside the vault.

### What NOT to Create in the Vault

- **USER.md at vault root** — don't create it. Use the `memory` tool
  (`target: user`) which writes to `~/.hermes/memories/USER.md`.
- **MEMORY.md at vault root** — don't create it. Use the `memory`
  tool (`target: memory`) which writes to `~/.hermes/memories/MEMORY.md`.
- **Home.md** — don't create it in agent-first mode (the default).
  Only create in human-browsed mode.
- **dashboards/ folder** — don't create it in agent-first mode. The
  agent greps for `- [ ]` to find open tasks. No plugin dependency.
- **inbox/** folder unless the user explicitly wants one.
- **Folder-level README.md files** — skip knowledge/README.md in
  agent-first mode (the rule lives in VAULT.md). family/README.md is
  the only one always created because it holds real data.
- **Any file that assumes the user will open Obsidian and browse.**
  If its value depends on a human clicking through Obsidian, it's
  wrong for agent-first mode.

### SOUL.md (CRITICAL — don't skip)

If the user chose an agent name, captured communication preferences, or
stated hard rules during Phase 1, write `~/.hermes/SOUL.md` with the
full persona. This file is loaded fresh on every message, so it's the
right home for identity, tone, and never-do-this rules — not USER.md,
which is reference material the agent reads on demand.

SOUL.md should include:
- Agent name and the meaning/reason behind it (if chosen)
- How to talk (tone, length, markdown usage, formality)
- How to think (decision framing, when to push back, watch-outs)
- Hard rules — the pet peeves and boundaries stated as absolutes
  ("Never do X", "Always avoid Y")
- Quiet hours if stated
- The user's north star in 1-2 sentences as the lens for priorities

Keep it under ~4KB. This is a personality file, not a dossier. The rich
context lives in USER.md and the vault; SOUL.md is the always-loaded
voice and rules layer.

If the user declined to name the agent or was indifferent to
personality questions, still write a minimal SOUL.md capturing whatever
preferences were stated (tone, pet peeves, quiet hours). Don't leave
the file empty just because the user didn't pick a name.

### Save to memory tool (CRITICAL — don't skip)

After writing all vault files, ALSO save the core facts to the
`memory` tool:
- `target: user` — name, location, family, work, communication
  preferences, agent name if chosen, quiet hours. This is what the
  agent reads at the start of every session BEFORE touching vault
  files, so it must be compact and focused on identity + preferences.
- `target: memory` — vault path, structure overview, vault rules
  (research-split, naming conventions, rejected patterns like "no
  inbox"). This prevents future sessions from having to re-derive
  how the vault works.

Vault files are the rich layer; memory tool is the always-loaded
quick-reference layer. Both are needed. Skipping the memory tool
means the next session starts blind until the agent opens the vault.

### Gap-Filling Over Time (not a cron job)

The user profile is a foundation, not an encyclopedia. Gaps will fill
in naturally over time as the user works with the agent. Do NOT set up
a daily question cron job for this purpose — Hermes cron messages are
outgoing-only and cannot sustain a conversation. If the user replies
to a cron-delivered question, the agent won't have context to handle
the response.

Instead, gap-filling happens opportunistically:
- When the user starts a new conversation and there's natural space,
  the agent can ask one thoughtful question rooted in something the
  user just mentioned or a known gap in USER.md / MEMORY.md.
- When the user shares something that touches an underdeveloped area
  (e.g., mentions a sibling for the first time), the agent can ask a
  follow-up in context.
- During vault maintenance conversations, the agent can surface
  observations like "I noticed the inbox folder has been empty for
  two weeks — still want it?" and let the user decide.

The guiding rule: gap-filling is user-initiated or conversation-driven,
never agent-scheduled. Quality over cadence.

---

## Ongoing File Maintenance

The vault is a living system, not a snapshot. Every conversation is an
opportunity to keep the files accurate and current. The agent should treat
file updates as a background responsibility — not something the user has
to ask for.

### When to Update What

**`memory` tool (`target: user` → `~/.hermes/memories/USER.md`)** —
Update when the user shares:
- A new job, role change, or shift in responsibilities
- Changed daily routines, work hours, or habits
- New goals, dropped goals, or reprioritized goals
- Updated communication preferences or pet peeves
- Any personal fact that contradicts or extends what's already there
Use `replace` to update existing entries instead of adding duplicates.
Keep entries compact — this file is loaded every turn.

**`memory` tool (`target: memory` → `~/.hermes/memories/MEMORY.md`)** —
Update when you observe or the user reveals:
- A new durable environment or workflow fact the agent should always
  know (new tool, new convention, new rejected pattern)
- A change to how the vault or system works
- Anything that would save a future session from re-deriving it

**brain/Patterns.md** — Update when you observe:
- A new pattern in how they work or make decisions
- A self-insight ("I've realized I always...")
- An evolving preference that goes deeper than surface-level facts
- Lifestyle context that helps the agent understand the user's rhythm

**brain/MEMORY.md (project/context log, inside vault)** — Do NOT
create a MEMORY.md inside the vault. Use the `memory` tool for
durable facts and brain/Patterns.md or brain/Key Decisions.md for
richer observations. Project-specific decisions and context go into
the relevant project file.

**Priority #1:** Any important fact, decision, context, or insight
that surfaced during the conversation gets captured *somewhere*
appropriate before the session ends. The goal is zero information
loss across conversations — but pick the right home for each fact,
don't dump everything into one giant file.

**During Conversations — File in Real-Time:**
Don't let important information sit only in conversation logs. As it surfaces,
file it to the right place immediately:
- Project decisions, progress, blockers → the relevant project file
- Task updates, completions, new tasks → the relevant task file
- Client preferences, context, dates → the client/person file
- Technical discoveries, workarounds, gotchas → the project or brain/Patterns.md
- Strategy decisions, pivots, priorities → the project or North Star.md

If you're unsure which file to put something in, MEMORY.md is the fallback.
But for project-specific info, the project file is the canonical home.

**Scheduled Review (Optional but Recommended):**
If conversations are rich and file updates might be missed, set a daily cron
job that reviews recent session logs and extracts key info to appropriate
files. This catches things that slipped through during busy sessions.

**VAULT.md** — Update when:
- A new area folder is created or an existing one is renamed/removed
- The organizational system changes (new conventions, new tagging, etc.)
- Decision rules for "what goes where" shift based on how the vault is
  actually being used vs. how it was originally designed
- The user expresses a preference that contradicts a current System
  Principle

**family/README.md** — Update when:
- A new family member, pet, or significant person is mentioned
- Birthdays, ages, or relationships change (new baby, marriage, etc.)
- The "Upcoming Dates" section needs refreshing for the current year

**family/{person}.md** — Update when:
- New preferences, gift ideas, or important dates come up in conversation
- Life events happen (graduations, jobs, milestones)
- The user shares something worth remembering about that person

### How to Update

- Don't announce updates unless the change is significant enough that the
  user should confirm it. Most updates are small and should just happen.
- If a fact contradicts something already in a file, replace the old info
  — don't append both versions.
- Keep the same formatting and tone as the existing file content.
- For MEMORY.md, date-stamp new entries so patterns over time are visible.
- If you're unsure whether something is worth recording, err on the side
  of writing it down. It's easier to prune later than to recover a lost
  insight.

---

## Important

- This is a foundation, not an encyclopedia. The daily cron fills gaps.
- If they seem done or restless, wrap up gracefully.
- Write ALL files in the same session — don't promise to do it later.
- Use information they actually shared. Don't infer or fabricate.
- For sections without info yet, use "(none yet)" as a placeholder.
- Phase 2 answers directly shape the vault. If the user says "I think in
  projects," don't generate area-based folders. If they say "I don't
  archive anything," don't create an archive folder. Listen and build.


# Brain File Setup

After onboarding completes, create or update these brain files in
`~/.hermes/obsidian/brain/`:

**North Star.md** — The user's current top-level goals and focus areas.
What they're working toward right now. Updated when goals shift.

**Memories.md** — An index of all brain/ files and their purpose. The agent
reads this at session start to know what exists and where.

**Key Decisions.md** — Major choices the user has made about their vault,
workflow, or life direction. Not daily decisions — the big ones that
define the landscape.

**Patterns.md** — Repeating behaviors, habits, or tendencies the agent
notices. Both productive patterns to leverage and unproductive ones to
work around.

**Gotchas.md** — Things the user has explicitly told the agent NOT to do,
or quirks to work around. Update whenever the user corrects something.

**Skills.md** — Reusable workflows and approaches the agent has learned
through problem-solving. Created when a multi-step process is solved, so
it can be replicated later without relearning.

## File Maintenance Rule

At session start, the agent reads:
1. `~/.hermes/obsidian/Home.md` — vault entry point
2. `~/.hermes/obsidian/brain/North Star.md` — current goals and focus
3. `~/.hermes/obsidian/brain/Memories.md` — index of all brain files

Then reads the specific brain files relevant to whatever the user is
working on. Brain files are the operational memory layer — USER.md and
MEMORY.md are the persistent identity layer.