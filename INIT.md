# INIT.md — Read First in a Fresh Session

> When Claude opens this repo for the first time in a new session, read this file before anything else.

## What is this repo

`design-system` is the substrate for the `design-website` skill. It is **not** a website. It contains the methodology, anti-slop rules, reference vault, token templates, pattern library, and analyzer prompts that Claude reads at the start of every client website project.

The user (Michael) builds websites for clients. Each client has different aesthetic needs. This system takes per-project references and produces non-slop output that matches the references' aesthetic vocabulary.

## Required reading order (right now, before responding to the user)

1. [`HANDOVER.md`](HANDOVER.md) — current state of setup, what is verified, what is pending
2. [`README.md`](README.md) — what the system does and how it is used
3. [`PROCESS.md`](PROCESS.md) — the 6-step workflow the skill enforces
4. [`ANTI-SLOP.md`](ANTI-SLOP.md) — durable rules applied to every project
5. [`STACK-DECISIONS.md`](STACK-DECISIONS.md) — when to use plain HTML / Astro / Next.js
6. [`OTLC-Brainstorm.MD`](OTLC-Brainstorm.MD) — vision, architecture, decisions, open questions, session log
7. [`CLAUDE.md`](CLAUDE.md) — repo-specific behavior rules (mostly: this is the substrate, edit it carefully)

After reading those, you understand the system.

## What the user is likely doing in this repo

Two modes:

### Mode A — Maintaining the system

Adding to the reference vault, refining anti-slop rules, building patterns, editing process steps, tuning the skill, fixing typos. **You work in this repo directly.** Follow [`CLAUDE.md`](CLAUDE.md) commit conventions.

### Mode B — Smoke-testing the workflow

The user wants to verify the system works end-to-end. They will give you 1-3 reference URLs and watch you run the analyzer on them. **Do not** scaffold a real client project for a smoke test; just run Step 2 (Reference Analysis) against the URLs and produce the analysis files in a temp location they specify.

If the user is starting a **real client website project**, they should not be working in this repo. They should be in `C:\dev\Projects\[client-name]\` and invoking the `design-website` skill (which reads from this repo as knowledge base). If they accidentally started in this repo, redirect them.

## First message expectations

Common first messages and how to respond:

| User says | What to do |
|-----------|-----------|
| "let's test the system" or "smoke test" or "give me an example" | Mode B. Ask for 1-3 reference URLs. Run Chrome DevTools MCP analyzer per `analyzer/extract-prompt.md`. Show output. |
| "let's add a reference" or "I found a great site" | Mode A. Get URL. Run analyzer. Add full analysis to `references/[slug].md` and one-line entry to `references/INDEX.md`. Commit `references: add [domain]`. |
| "the skill is doing X wrong" or "let's tune the skill" | Mode A. Open `C:\Users\michael\.claude\skills\design-website\SKILL.md`. Discuss the change. Edit. Commit `skill: [what changed]`. |
| "we need a new rule" or "I keep seeing X slop" | Mode A. Add to `ANTI-SLOP.md` per the format in that file. Commit `anti-slop: [short rule summary]`. |
| "let's build a site for [client]" | Wrong directory. Tell user to navigate to `C:\dev\Projects\[client-name]\` and invoke `/design-website` skill from there. |

## Required MCPs

Three Claude Code MCP servers must be installed and connected at user scope:

- `chrome-devtools` — reference analysis
- `playwright` — verification
- `context7` — current docs

Verify with `claude mcp list`. If any are missing or disconnected, see [`HANDOVER.md`](HANDOVER.md) for install commands.

## Global instructions still apply

The user's global `CLAUDE.md` (no em dashes ever, blunt feedback, PowerShell syntax on Windows, no AI co-author tags, etc.) takes precedence over anything in this repo.
