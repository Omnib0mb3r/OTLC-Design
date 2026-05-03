# design-system — Claude Instructions

> Human-readable workflow lives in [`README.md`](README.md), [`PROCESS.md`](PROCESS.md), and [`WORKFLOW.md`](WORKFLOW.md). The rules below are the machine-readable authority for Claude when this repo is the working directory.

## What this repo is

**This repo is the design-system substrate, not a project under construction.** It powers the `OTLC-Design` skill, which reads from here when building client websites in other directories.

When the user is working **inside this repo**, they are maintaining the system itself: adding references, refining the anti-slop list, building new patterns, editing process steps, tuning the skill, etc.

When the user is working **on a client website**, they are in `C:\dev\Projects\[client]\` (not here). The skill reads this repo automatically.

## Required reading on session start

If the user's first message in this repo is *anything other than a trivial question*, read these in order before responding substantively:

1. [`INIT.md`](INIT.md) — fresh-session entry point, current state
2. [`HANDOVER.md`](HANDOVER.md) — what is set up, what is pending
3. [`PROCESS.md`](PROCESS.md) — the 6-step workflow the skill enforces
4. [`ANTI-SLOP.md`](ANTI-SLOP.md) — durable rules
5. [`STACK-DECISIONS.md`](STACK-DECISIONS.md) — when to use which stack

If the user is starting a client project (not maintaining the system), invoke the `OTLC-Design` skill directly instead.

## Behavior rules in this repo

### Maintenance work

When the user adds or refines content in this repo (new reference, new pattern, new anti-slop rule):

- **References** — write a new file in `references/[slug].md` with the analysis structure documented in [`analyzer/README.md`](analyzer/README.md). Add a one-line entry to [`references/INDEX.md`](references/INDEX.md) under the right aesthetic category.
- **Patterns** — write to `patterns/[pattern-name].md`. Include intent, structural sketch (ASCII or SVG), code reference, and when to use it.
- **Anti-slop rules** — append to `ANTI-SLOP.md` under the right category. Include `**Why:**` and `**How to apply:**`.
- **Process changes** — edit `PROCESS.md` directly. Bump the version line at the top.
- **Skill changes** — edit `C:\Users\michael\.claude\skills\OTLC-Design\SKILL.md`.

### Anti-slop applies even here

When generating examples or sample code in this repo (in patterns, tokens, project-template), follow `ANTI-SLOP.md`. Do not seed slop into the system that exists to prevent it.

### Git hygiene

This repo is a tool used across years and projects. Commits should be small and topical:

- One reference added → one commit, message: `references: add [domain]`
- One pattern added → one commit, message: `patterns: add [pattern-name]`
- Rule added → one commit, message: `anti-slop: [short rule summary]`
- Skill change → one commit, message: `skill: [what changed]`

Never amend. Never force-push.

## Brainstorm workflow (inherited from template)

If the user wants to brainstorm a *change to the system itself* (e.g., reworking the process, adding a major new subsystem), follow the OTLC + superpowers workflow inherited from the dev-template:

1. Read `OTLC-Brainstorm.MD` (Vision, Architecture, prior Decisions, Open Questions)
2. Run `superpowers:brainstorming`
3. Auto-flow into `superpowers:writing-plans` then `superpowers:subagent-driven-development`
4. Update `OTLC-Brainstorm.MD` Decisions Made and Session Log

For everyday content additions (new reference, new pattern, new rule), the brainstorm pipeline is overkill. Just do the work.

## devneural.jsonc

`devneural.jsonc` registers this repo in the DevNeural graph. It is metadata only and does not affect the skill workflow.

## What this repo does NOT do

- Build any client website (those live in `C:\dev\Projects\[client]\`)
- Run any web server or have a deploy target
- Contain client-specific code, copy, or assets
- Replace the user's judgment as the designer of record

## Global instructions still apply

The user's global `CLAUDE.md` (no em dashes ever, blunt feedback, PowerShell syntax on Windows, no co-author tags in commits, etc.) takes precedence over anything written here.
