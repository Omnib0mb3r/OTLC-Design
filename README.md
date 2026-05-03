# design-system

A repeatable methodology for building **non-slop, professional sites and apps** — for clients and for owned work, marketing and product. The substrate that powers the `OTLC-Design` skill.

This repo is not a website or app. It is the system that produces them: process, anti-slop rules, reference vault, pattern library, token templates, mode adaptations, owner-brand profile, and analyzer prompts that Claude reads at the start of every project.

## What lives here

| Path | Purpose |
|------|---------|
| [`PROCESS.md`](PROCESS.md) | The 6-step workflow (Intake with branch question → Analyze → Synthesize → Build → Verify → Iterate + hard-enforced post-mortem) |
| [`ANTI-SLOP.md`](ANTI-SLOP.md) | 24 universal durable rules Claude follows on every project |
| [`STACK-DECISIONS.md`](STACK-DECISIONS.md) | When to use plain HTML / Astro / Next.js / native |
| [`MODE-INTERNAL.md`](MODE-INTERNAL.md) | Adaptation for internal/owned work (skips brand discovery, pulls owner-brand profile) |
| [`APP-ADAPTATION.md`](APP-ADAPTATION.md) | Adaptation for app/product UI (anti-slop inversion, app stack defaults, app verification gates) — with customer-app tightening subsection |
| [`owner-brand/`](owner-brand/) | Standing brand profile (personal-site, MHW), voice rules, drop-in tokens, source `.docx` |
| [`references/`](references/) | Curated vault of sites worth studying. Catalog in [`references/INDEX.md`](references/INDEX.md) |
| [`patterns/`](patterns/) | Hand-built layout primitives, subdivided into [`marketing/`](patterns/marketing/) and [`app/`](patterns/app/) |
| [`tokens/`](tokens/) | Type scale, color, spacing, motion *templates* (synthesized per project, not copied) |
| [`analyzer/`](analyzer/) | Prompts and procedures Claude uses to extract design data from references via Chrome DevTools MCP |
| [`project-template/`](project-template/) | Starter scaffolds copied out when a new project begins |
| [`INIT.md`](INIT.md) | What a fresh Claude session reads first when this repo is opened |
| [`HANDOVER.md`](HANDOVER.md) | Live status: what is set up, what is pending, **the closing loop** |
| [`CLAUDE.md`](CLAUDE.md) | Repo-specific Claude behavior rules |
| [`OTLC-Brainstorm.MD`](OTLC-Brainstorm.MD) | Vision, architecture, decisions, open questions, session log |

## How it is used

You do not work *in* this repo to build sites or apps. You work in `C:\dev\Projects\[project-name]\`. The OTLC-Design skill reads from this repo as its knowledge base.

### Typical flow

1. Start a new project. Invoke `/OTLC-Design` (or say "let's build a site for X" / "build an app for Y").
2. Skill asks the **branch question**: Customer site / Customer app / Internal site / Internal app.
3. Skill walks intake (full for customer, light for internal).
4. For projects with references: Chrome DevTools MCP analyzes each.
5. Synthesizes tokens (informed by references for customer; pulled from owner-brand for internal). Proposes stack and structure. Gets your sign-off.
6. Builds. Verifies via Playwright MCP and Lighthouse. Iterates.
7. **You signal done.** Skill enters hard-enforced post-mortem. Anything genuinely reusable from this project gets extracted and committed to this repo.

### How the system improves

Every project ends with a hard-enforced post-mortem (Step 6). 5 questions (6 in internal mode), one at a time. Each requires either a concrete addition or an explicit skip with reason. Non-answers are rejected.

| Question | If yes, what gets committed where |
|----------|-----------------------------------|
| New ANTI-SLOP rule? | `ANTI-SLOP.md` → commit `anti-slop: ...` |
| New pattern? | `patterns/marketing/[name].md` or `patterns/app/[name].md` → commit `patterns: add ...` |
| New reference? | `references/INDEX.md` → commit `references: add ...` |
| `PROCESS.md` change? | `PROCESS.md` (bump version) → commit `process: ...` |
| Skill change? | `~/.claude/skills/OTLC-Design/SKILL.md` → commit `skill: ...` |
| (Internal only) Owner-brand change? | `owner-brand/source/MichaelCollins_BrandGuide.docx` + derived markdown → commit `owner-brand: ...` |

The repo is a flywheel. Each project makes the next one start higher. See [`HANDOVER.md`](HANDOVER.md) §"The closing loop" for the full mechanism.

## Required tooling

Three Claude Code MCP servers must be installed (user scope):

- **playwright** — multi-browser verification, screenshots, automation
- **chrome-devtools** — reference analysis (computed styles, Lighthouse, perf, network)
- **context7** — current documentation for any library or web spec

See [`HANDOVER.md`](HANDOVER.md) for verification commands.

## Honest scope

This system raises the floor. It does not replace art direction. The last 20% (the part separating "very good" from "Pentagram") still requires the owner's judgment. What this gives:

- Every project starts at *considered* instead of *Tailwind template*
- The slop tells are eliminated systematically
- For customer work, matching a reference aesthetic gets to ~80% on first pass
- For internal work, the owner-brand profile means brand-discovery is one question, not ten
- The hard-enforced post-mortem means the system gets smarter with every project shipped
- Quality bar does not drop for internal work — same anti-slop, same verification gates appropriate to mode

What this does NOT do:

- Replace the user's art direction
- Generate brand strategy or commission custom photography
- Write long-form copy from nothing (drafting from a brief is in scope; copy strategy is not)
- Deploy

## Skill invocation

The OTLC-Design skill triggers on:
- `/OTLC-Design` or `/design`
- "let's build a site for [X]"
- "new client website"
- "build an app for [Y]"
- "internal tool for [Z]"
- "design a UI for [W]"
- Any project-kickoff phrase that involves design work

The skill is the entry point. The repo is the substrate. Both are git-versioned and evolve together.
