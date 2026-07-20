# INIT.md: Read First in a Fresh Session

> When Claude opens this repo for the first time in a new session, read this file before anything else.

## What this repo is

`design-system` is the **substrate for two skills**, both loaded live by Windows directory junction from inside this repo: `OTLC-Design` (from [`skill/`](skill/)) and `anti-ai-writing` (from [`skill-writing/`](skill-writing/)). It is **not** a website or app under construction. It contains the methodology, anti-slop rules, reference vault, token templates, pattern library, owner-brand profile, mode adaptations, technical guides, legal requirements, and analyzer prompts that Claude reads at the start of every project.

The operator builds:
- Customer sites (marketing/showcase for external clients)
- Customer apps (B2B SaaS, customer portals for paying customers)
- Internal sites (own portfolio, publications, project landings)
- Internal apps (own tools, dashboards, admin panels)

The OTLC-Design skill takes any of these from "let's build X" through to a non-slop, professional, verified deliverable. It uses a 4-way branch question at intake to set the right rules, brand source, stack defaults, and verification gates.

## Required reading order (right now, before responding substantively)

1. [`HANDOVER.md`](HANDOVER.md): current state of setup, smoke test status, **the closing loop** (how projects close to keep improving the system)
2. [`README.md`](README.md): what the system does and how it is used
3. [`PROCESS.md`](PROCESS.md): the 6-step workflow with branch question and hard-enforced post-mortem
4. [`ANTI-SLOP.md`](ANTI-SLOP.md): 26 universal durable rules (visual slop)
4b. [`skill-writing/SKILL.md`](skill-writing/SKILL.md): the `anti-ai-writing` skill (prose slop). Applies to every word produced anywhere, not only design work
5. [`STACK-DECISIONS.md`](STACK-DECISIONS.md): when to use plain HTML / Astro / Next / native
6. [`MODE-INTERNAL.md`](MODE-INTERNAL.md): adaptation for owned/internal work (loaded by skill when intake branch = internal)
7. [`APP-ADAPTATION.md`](APP-ADAPTATION.md): adaptation for app UI (loaded by skill when intake branch = app, with customer-app tightening subsection)
8. [`owner-brand/profile.md`](owner-brand/profile.md): index of owner brand surfaces
9. [`OTLC-Brainstorm.MD`](OTLC-Brainstorm.MD): vision, architecture, decisions, open questions, session log
10. [`CLAUDE.md`](CLAUDE.md): repo-specific behavior rules

After reading those, you understand the system.

### Substrate you should know exists (read the INDEX, open a file only when the work needs it)

- [`guides/INDEX.md`](guides/INDEX.md): seven verbatim-stored technical guides (SEO crawlability, structured data, how-to markup, AEO, AI-search inspection, GA4, browser-aware design). How-to material for the Build and Verify steps, distinct from the reference vault.
- [`legal/INDEX.md`](legal/INDEX.md): what a site must have to be lawful, with [`legal/CHECKLIST.md`](legal/CHECKLIST.md) as the per-project gate and one file per statute under [`legal/laws/`](legal/laws/).
- [`references/INDEX.md`](references/INDEX.md): 51 catalogued sites worth studying, grouped by aesthetic category.
- [`patterns/`](patterns/): subdivided into [`marketing/`](patterns/marketing/) and [`app/`](patterns/app/). Grown from real work only, never pre-populated.
- [`BUGS.md`](BUGS.md): the persistent bug log. Scan its index block before troubleshooting anything.

## What the user is likely doing in this repo

Two modes:

### Mode A: Maintaining the system

Adding to the reference vault, refining anti-slop rules, building patterns, editing process steps, tuning the skill, fixing typos, evolving owner-brand. **You work in this repo directly.** Follow [`CLAUDE.md`](CLAUDE.md) commit conventions.

### Mode B: Smoke-testing the workflow

The user wants to verify the system works end-to-end. They will give you 1-3 reference URLs and watch you run the analyzer on them. **Do not** scaffold a real project for a smoke test; just run Step 2 (Reference Analysis) against the URLs and produce the analysis files in a temp location.

If the user is starting a **real project** (customer or internal), they should not be working in this repo. They should be in `C:\dev\Projects\[project-name]\` and invoking the OTLC-Design skill (which reads from this repo as knowledge base). If they accidentally started in this repo, redirect them.

## First message expectations

Common first messages and how to respond:

| User says | What to do |
|-----------|-----------|
| "smoke test" / "test the system" / "give me an example" | Mode B. Ask for 1-3 reference URLs. Run Chrome DevTools MCP analyzer per `analyzer/extract-prompt.md`. Show output. |
| "let's add a reference" / "I found a great site" | Mode A. Get URL. Run analyzer. Add full analysis to `references/[slug].md` and one-line entry to `references/INDEX.md`. Commit `references: add [domain]`. |
| "the skill is doing X wrong" / "let's tune the skill" | Mode A. Open the in-repo canonical `skill/SKILL.md` (the `~/.claude/skills/OTLC-Design` junction loads it live). Discuss the change. Edit. Commit `skill: [what changed]`. |
| "we need a new rule" / "I keep seeing X slop" | Mode A. Visual slop goes in `ANTI-SLOP.md`, commit `anti-slop: [summary]`. Prose slop goes in `skill-writing/SKILL.md` plus `skill-writing/references/tells.md`, commit `skill-writing: [summary]`. |
| "this copy sounds like AI" / "de-slop this writing" | Invoke the `anti-ai-writing` skill. Works in this repo or anywhere else. |
| "update the brand" / "I changed the guide" | Mode A. Re-extract from `owner-brand/source/<BrandGuide>.docx`. Update derived markdown. Commit `owner-brand: [what changed]`. |
| "let's build a site/app for [X]" | **Wrong directory.** Tell user to navigate to `C:\dev\Projects\[name]\` and invoke `/OTLC-Design` from there. |

## Required MCPs

Three Claude Code MCP servers must be installed and connected at user scope:

- `chrome-devtools`: reference analysis (Step 2)
- `playwright`: verification (Step 5)
- `context7`: current docs (Steps 3-4)

Verify with `claude mcp list`. If any are missing or disconnected, see [`HANDOVER.md`](HANDOVER.md) for install commands.

## The closing loop (read once, then it shapes everything)

The OTLC-Design skill **hard-enforces** Step 6 post-mortem. Every project must close by walking 6 questions (or 7 in internal mode) one at a time. Each requires either a concrete addition (which gets committed to this repo) or an explicit skip with reason. Non-answers are rejected.

This is the only mechanism that makes the system improve over time. See [`HANDOVER.md`](HANDOVER.md) §"The closing loop" for the full mechanism.

When you're maintaining this repo (Mode A above), you are filling in additions that came from past project post-mortems, or proactively expanding the system between projects. Either way, every change here should be either (a) a post-mortem addition or (b) a deliberate substrate improvement, not random tinkering.

## Global instructions still apply

The user's global `CLAUDE.md` (no em dashes ever, blunt feedback, PowerShell syntax on Windows, no AI co-author tags, etc.) takes precedence over anything in this repo.
