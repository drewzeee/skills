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
"Phase 2 starting now." When the personal profile feels solid, shift with
something like "Now let's talk about how you want to organize things."

---

## Phase 1: Personal Profile

What to cover (let it flow naturally, don't force the order):

Identity & Basics
- Name, what they prefer to be called, pronouns
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

### Personal Profile Files

USER.md
Compile everything from Phase 1 into a clean, scannable format with
sections and bullet points. Include subsections for Daily Life, Interests,
Family, Work, etc. This is the primary reference file the agent reads every
session.

family/README.md
Household overview table with names, relationships, birthdays, ages. Include
an "Upcoming Dates" section for the current year listing birthdays and
anniversaries chronologically.

family/{firstname}.md (one per family member)
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

MEMORY.md
Start a long-term memory file. Add a "Self-Knowledge" section capturing
work style, core drives, decision-making patterns — the deeper personality
insights that emerged from the conversation. This file grows over time.

### Vault Structure Files

Generate a personalized vault structure based on Phase 2 answers. This is
the most important part — the structure should feel like it came from the
user, not from a template.

Guiding principles:
- Lightweight over comprehensive. 3-5 top-level folders max to start.
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

Always create these regardless of structure choice:
- inbox/README.md — "Drop anything here. Process later." A universal
  capture point for quick thoughts, links, ideas that don't have a home
  yet.
- templates/ — Starter templates based on the note types the user
  actually described. Only create 2-3 templates for things they said they
  do. Common ones: meeting-notes.md, project.md, daily-note.md — but
  only if relevant to what they shared.

Every folder gets a brief README.md (2-3 lines) explaining what goes
there. This helps both the user and the AI understand the system.

VAULT.md (root level)
This is the system's "owner's manual" — the file the agent reads to
understand how the vault is organized and why. Include:
- Overview of the folder structure and the reasoning behind it
- What goes where (decision rules, not just descriptions)
- Naming conventions (use the user's preference if stated, otherwise
  suggest lowercase-kebab-case for files, Title Case for folders)
- Tagging strategy if the user wants tags, or a note that tags aren't
  in use yet
- A "System Principles" section capturing the user's stated preferences
  about organization (e.g., "action over archive", "keep it flat",
  "everything is a project", "separate work and personal")
- A note that this structure is a starting point and will evolve

### Daily Question Cron

After writing all files, set up a daily question cron job:
- Schedule: Once per day at 9:00 AM in the user's timezone
- Each morning, check if the user answered yesterday's question. If so,
  extract the key facts and update the appropriate file (USER.md, family
  files, MEMORY.md, or vault structure files). Then read existing files,
  find a gap, and ask ONE new thoughtful question. Not a survey —
  something genuine.
- The daily question can also explore vault organization preferences over
  time — things like "I noticed you haven't used the inbox/ folder much.
  Is quick capture something you actually need, or should we rethink
  that?"

---

## Ongoing File Maintenance

The vault is a living system, not a snapshot. Every conversation is an
opportunity to keep the files accurate and current. The agent should treat
file updates as a background responsibility — not something the user has
to ask for.

### When to Update What

**USER.md** — Update when the user shares:
- A new job, role change, or shift in responsibilities
- Changed daily routines, work hours, or habits
- New goals, dropped goals, or reprioritized goals
- Updated communication preferences or pet peeves
- Any personal fact that contradicts or extends what's already there

**MEMORY.md** — Update when you observe or the user reveals:
- A new pattern in how they work or make decisions
- A self-insight ("I've realized I always...")
- An evolving preference that goes deeper than surface-level facts
- Something worth remembering that doesn't fit neatly into USER.md

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

**Folder README.md files** — Update when:
- The purpose or scope of a folder changes
- New subfolders are added that need explaining
- The original description no longer matches how the folder is used

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


# System Instructions

After the onboarding process has completed, create concise but thorough
system instructions for the user to paste into their 'CLAUDE.md' file and
guide the user to copy+paste into the cowork system instructions (found
in the Cowork panel in app settings).

The system instructions MUST include a "File Maintenance" section that
reminds the agent to keep vault files updated. At minimum, include:

1. A rule to read USER.md, MEMORY.md, and VAULT.md at session start for
   orientation.
2. A rule to update USER.md when new personal facts or preference changes
   surface in conversation.
3. A rule to update MEMORY.md when deeper patterns or self-insights
   emerge.
4. A rule to update VAULT.md when the vault structure or organizational
   conventions change.
5. A rule to update family files and folder READMEs when relevant new
   information comes up.
6. A reminder that most updates should just happen silently — don't ask
   permission for routine maintenance.