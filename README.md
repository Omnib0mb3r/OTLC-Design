# design-system (GitHub: OTLC-Design)

A repeatable methodology for building **non-slop, professional sites and apps** for clients and for owned work, marketing and product. The substrate that powers two Claude Code skills:

- **`OTLC-Design`**: the build workflow. Takes any project from "let's build X" through intake, reference analysis, token synthesis, build, verification, and a hard-enforced post-mortem.
- **`anti-ai-writing`**: the prose rules. Roughly 60 documented tells that mark text as LLM-generated, distilled into bans applied to every word produced (site copy, docs, commit messages, UI strings), in any project, not only design work.

The two cover the same defect in different media. `ANTI-SLOP.md` stops a page from *looking* AI-generated; `skill-writing/` stops it from *reading* AI-generated.

This repo is not a website or app. It is the system that produces them: process, anti-slop rules, prose rules, reference vault, pattern library, token templates, mode adaptations, owner-brand profile, and analyzer prompts that Claude reads at the start of every project.

**Scope, before you read further.** This is single-operator personal tooling. Windows 11 only (both skills load through directory junctions), Claude Code only, and built around one person's brand profile in [`owner-brand/`](owner-brand/). It is published as reference, not as a product. To run it yourself you would replace `owner-brand/` wholesale (profile, voice rules, per-brand files, token CSS, source `.docx`), translate the PowerShell junction commands to `ln -s` on macOS or Linux, and rewrite the hardcoded paths in `skill/SKILL.md` and `skill-writing/SKILL.md` if you put the repo anywhere other than the required location.

The GitHub repo is named `OTLC-Design` after the skill it was built for. On disk the folder is `design-system`, and that name is load-bearing because both skills resolve their file reads against it. See [Setup](#setup).

---

## Skill invocation

The `OTLC-Design` skill is the entry point for build work. Invoke it from the project directory you're working in.

The `anti-ai-writing` skill invokes on its own triggers ("does this sound like AI", "de-slop this copy", `/anti-ai-writing`) or automatically before substantial prose. It needs no project context.

### Triggers (OTLC-Design)

- `/OTLC-Design` or `/design`
- "let's build a site for [X]"
- "new client website"
- "build an app for [Y]"
- "internal tool for [Z]"
- "design a UI for [W]"
- "use the OTLC-Design skill"
- Any project-kickoff phrase that involves design work

### Done signals (trigger hard-enforced post-mortem)

When you're ready to close a project, say one of:

- `we're done`
- `ship it` / `ready to ship`
- `client approved` / `client signed off`
- `post-mortem` / `let's wrap up`
- `/done` or `/postmortem`

These trigger Step 6 enforcement. The skill will not exit the project as complete until the post-mortem is written with substantive answers to all questions. See [The closing loop](#the-closing-loop) below.

---

## The 4-mode branch

The skill asks one question at intake to set context for the whole workflow:

> *"What are we building?*
> *1. **Customer site**: marketing/showcase site for an external client*
> *2. **Customer app**: product/app interface for paying customers (B2B SaaS, customer portal, web app)*
> *3. **Internal site**: your own marketing/showcase site (portfolio, publications, project landing pages)*
> *4. **Internal app**: your own tools, dashboards, admin panels"*

The answer determines which adaptation docs load, which brand source applies, which stack defaults are used, and which verification gates are enforced.

| Branch | Adaptations loaded | Brand source | Stack default |
|--------|---------------------|--------------|---------------|
| 1. Customer site | (default) | Discovered from client brief + references | Plain HTML/CSS/JS + Vite (or Astro for content) |
| 2. Customer app | [`APP-ADAPTATION.md`](APP-ADAPTATION.md) (with customer-app tightening) | Discovered from client brief + references | Next.js + React + TypeScript + shadcn |
| 3. Internal site | [`MODE-INTERNAL.md`](MODE-INTERNAL.md) | [`owner-brand/`](owner-brand/) profile | Plain HTML/CSS/JS + Vite |
| 4. Internal app | [`MODE-INTERNAL.md`](MODE-INTERNAL.md) + [`APP-ADAPTATION.md`](APP-ADAPTATION.md) | [`owner-brand/`](owner-brand/) profile | Next.js + React (or native per [`STACK-DECISIONS.md`](STACK-DECISIONS.md)) |

---

## Typical flow

1. Start a new project in `C:\dev\Projects\[project-name]\`.
2. Invoke the skill (any trigger above).
3. Skill asks the **branch question**.
4. Skill walks intake (full for customer, light for internal).
5. For projects with references: Chrome DevTools MCP analyzes each.
6. Skill synthesizes tokens (informed by references for customer; pulled from owner-brand for internal). Proposes stack and structure. **Gets your sign-off (synthesis gate).**
7. Skill builds. Verifies via Playwright MCP and Lighthouse. Iterates with you.
8. **You signal done** with one of the done signals above.
9. Skill enters hard-enforced post-mortem. Anything genuinely reusable from this project gets extracted and committed to this repo with a topical message.
10. `POSTMORTEM.md` written in the project folder. Project marked complete.

---

## The closing loop

This is the only mechanism that makes the system improve over time. It is hard-enforced.

### How a project closes

After you signal done, the skill walks **6 universal questions** (or 7 in internal mode), one at a time. Each question requires either:

- **A concrete addition** ("Yes, add rule: never X"; "Yes, lift this hero pattern to patterns/marketing/"; "Yes, add bbb.studio to references"). Claude writes the addition AND commits it to this repo with a topical message.
- **An explicit skip with reason** ("Intentionally nothing this round, because [reason]"). Logged in the project's `POSTMORTEM.md`.

**Non-answers ("nah", "skip", "we're good", silence) are rejected.** The skill re-asks. The skill does not advance until satisfied.

### The 6 universal questions

1. **New ANTI-SLOP rule?** Did anything ship that felt generic, default, or templated? Did you have to tell Claude to stop doing X mid-project?
2. **New pattern for `patterns/`?** Did we build a structural move you'd reach for again on a different project?
3. **New reference for `references/INDEX.md`?** Did we encounter a site worth keeping in the curated vault?
4. **Did `PROCESS.md` drag or lack a step?** Was any step too long, too short, missing, in the wrong order, or asking the wrong questions?
5. **Did the skill itself need refinement?** Wrong tone, wrong order, missing checkpoints, over-asking, under-asking?
6. **New anti-ai-writing rule?** Question 1 covers how it looked; this covers how it read. Any copy that shipped sounding generated, any phrase struck, any construction repeatedly corrected?

### Internal-mode 7th question

7. **Did anything from this project deserve to go into your owner-brand profile?** New brand surface? New token? New voice rule? New design rule for the brand guide?

### What gets committed where

| Addition type | Goes to | Commit message |
|---------------|---------|----------------|
| Anti-slop rule | `ANTI-SLOP.md` | `anti-slop: <short rule summary>` |
| Pattern (marketing) | `patterns/marketing/[name].md` | `patterns: add marketing/<name>` |
| Pattern (app) | `patterns/app/[name].md` | `patterns: add app/<name>` |
| Reference | `references/INDEX.md` (+ optional deep analysis at `references/[slug].md`) | `references: add <domain>` |
| Process change | `PROCESS.md` (bump version) | `process: <what changed>` |
| Skill change (OTLC-Design) | `skill/SKILL.md` (junction loads it live) | `skill: <what changed>` |
| Prose rule (anti-ai-writing) | `skill-writing/SKILL.md` + `skill-writing/references/tells.md` | `skill-writing: <what changed>` |
| Owner-brand change | `owner-brand/source/<BrandGuide>.docx` + derived markdown | `owner-brand: <what changed>` |
| Handover update | `HANDOVER.md` | `handover: <what changed>` |

### Why hard enforcement

Without the gate, post-mortems get skipped when you're tired and the project is shipped. "We're good, nothing came up." Then the system stays static and every project starts from the same baseline. The gate is annoying-on-purpose: it forces the 30 seconds of reflection that grows the system.

The repo is a flywheel. Each project makes the next one start higher.

---

## What lives here

| Path | Purpose |
|------|---------|
| [`PROCESS.md`](PROCESS.md) | The 6-step workflow. Intake (with branch question), Reference Analysis, Synthesis, Build, Verify, Iterate + hard-enforced post-mortem. |
| [`ANTI-SLOP.md`](ANTI-SLOP.md) | 26 universal durable rules Claude follows on every project. Visual slop. |
| [`skill-writing/`](skill-writing/) | Canonical source of the `anti-ai-writing` skill. Prose slop: banned vocabulary, banned constructions, content padding, formatting tells, false-positive guard. `~/.claude/skills/anti-ai-writing` is a junction to here. See [`skill-writing/README.md`](skill-writing/README.md). |
| [`BUGS.md`](BUGS.md) | Persistent bug log. Index block first, detail blocks below. Survives context resets. |
| [`STACK-DECISIONS.md`](STACK-DECISIONS.md) | When to use plain HTML / Astro / Next.js / native. |
| [`MODE-INTERNAL.md`](MODE-INTERNAL.md) | Adaptation for internal/owned work. Skips brand discovery, pulls owner-brand profile. |
| [`APP-ADAPTATION.md`](APP-ADAPTATION.md) | Adaptation for app/product UI. Anti-slop inversion, app stack defaults, app verification gates, operational-readiness rules + gates (config/secrets/deploy/rollback/observability). Includes customer-app tightening subsection. |
| [`owner-brand/`](owner-brand/) | Standing brand profile, voice rules, drop-in tokens. **Local-only and gitignored**: the repo is public, the brand is not. See [`owner-brand/README.md`](owner-brand/README.md) for the shape it expects. |
| [`references/`](references/) | Curated vault of sites worth studying. Catalog in [`references/INDEX.md`](references/INDEX.md). |
| [`patterns/`](patterns/) | Hand-built layout primitives. Subdivided into [`marketing/`](patterns/marketing/) and [`app/`](patterns/app/). Grown from real work only, never pre-populated. |
| [`legal/`](legal/INDEX.md) | Compliance library. One file per law under [`laws/`](legal/laws/), a triage table in [`INDEX.md`](legal/INDEX.md), and a delivery gate in [`CHECKLIST.md`](legal/CHECKLIST.md). Not legal advice. |
| [`tokens/`](tokens/) | Type scale, color, spacing, motion *templates*. Synthesized per project, not copied from here. |
| [`analyzer/`](analyzer/) | Prompts and procedures Claude uses to extract design data from references via Chrome DevTools MCP. |
| [`guides/`](guides/) | Verbatim-stored external guides (SEO, AEO, structured data, GA4, browser-aware design). Provenance headers inline; re-pull from source rather than editing. Not yet wired into PROCESS steps. |
| [`skill/`](skill/) | Canonical source of the `OTLC-Design` skill (`SKILL.md`). `~/.claude/skills/OTLC-Design` is a directory junction to here, so Claude Code loads the git-tracked file. See [`skill/README.md`](skill/README.md). Same junction pattern as `skill-writing/`. |
| [`project-template/`](project-template/) | Placeholders recording which scaffold command the skill runs per stack (`npm create vite@latest`, `npm create astro@latest`). Kept empty on purpose so the repo carries no stale dependencies. |
| [`INIT.md`](INIT.md) | What a fresh Claude session reads first when this repo is opened. |
| [`HANDOVER.md`](HANDOVER.md) | Live status: what is set up, what is pending, the closing loop conventions. |
| [`CLAUDE.md`](CLAUDE.md) | Repo-specific Claude behavior rules. |
| [`OTLC-Brainstorm.MD`](OTLC-Brainstorm.MD) | Vision, architecture, decisions, open questions, session log. |

---

## How it is used

You do not work *in* this repo to build sites or apps. You work in `C:\dev\Projects\[project-name]\`. The OTLC-Design skill reads from this repo as its knowledge base.

To **maintain or extend the system itself** (add a reference, add a rule, refine the skill), open this repo in Claude. See [`INIT.md`](INIT.md) for the maintenance entry point and [`CLAUDE.md`](CLAUDE.md) for commit conventions.

---

## Required tooling

Three Claude Code MCP servers must be installed at user scope:

- **chrome-devtools**: reference analysis (computed styles, Lighthouse, perf, network)
- **playwright**: multi-browser verification, screenshots, automation
- **context7**: current documentation for any library or web spec

Install commands are in [Setup](#setup) below. Troubleshooting steps live in [`HANDOVER.md`](HANDOVER.md).

---

## Honest scope

This system raises the floor. It does not replace art direction. The last 20% (the part separating "very good" from "Pentagram") still requires the owner's judgment.

What this gives:

- Every project starts at *considered* instead of *Tailwind template*
- The slop tells are eliminated systematically
- For customer work, matching a reference aesthetic gets to ~80% on first pass
- For internal work, the owner-brand profile means brand-discovery is one question, not ten
- The hard-enforced post-mortem means the system gets smarter with every project shipped
- Quality bar does not drop for internal work. Same anti-slop, same verification gates appropriate to mode.

What this does NOT do:

- Replace the user's art direction
- Generate brand strategy or commission custom photography
- Write long-form copy from nothing (drafting from a brief is in scope; copy strategy is not)
- Deploy

---

## Setup

### Prerequisites

- Windows 11. Both skills load through directory junctions (`New-Item -ItemType Junction`), which has no drop-in equivalent elsewhere without rewriting the commands as symlinks.
- Claude Code, signed in.
- Node and npm, for the `npx`-based MCP servers in step 3.

### 1. Clone to the required path

```powershell
git clone https://github.com/Omnib0mb3r/OTLC-Design.git C:\dev\Projects\design-system
```

The path is not a preference. `skill/SKILL.md` hardcodes `C:\dev\Projects\design-system\` for every substrate file it reads, because it is loaded through a junction and a relative path would resolve against `~/.claude/skills/` instead of this repo. Clone anywhere else and the skill still loads and still triggers, but reads nothing: no process, no anti-slop rules, no references, no owner-brand. It fails quietly, which makes it worth stating up front. If the repo must live elsewhere, rewrite every `C:\dev\Projects\design-system\` path inside `skill/SKILL.md` and `skill-writing/SKILL.md` to match.

### 2. Create both skill junctions

PowerShell, no admin needed:

```powershell
Remove-Item -LiteralPath "$env:USERPROFILE\.claude\skills\OTLC-Design" -Force -Recurse -ErrorAction SilentlyContinue
New-Item -ItemType Junction `
  -Path "$env:USERPROFILE\.claude\skills\OTLC-Design" `
  -Target "C:\dev\Projects\design-system\skill"

Remove-Item -LiteralPath "$env:USERPROFILE\.claude\skills\anti-ai-writing" -Force -Recurse -ErrorAction SilentlyContinue
New-Item -ItemType Junction `
  -Path "$env:USERPROFILE\.claude\skills\anti-ai-writing" `
  -Target "C:\dev\Projects\design-system\skill-writing"
```

Junctions rather than copies, so each skill has one git-tracked source and no second copy to drift. Detail in [`skill/README.md`](skill/README.md) and [`skill-writing/README.md`](skill-writing/README.md).

### 3. Install the three MCP servers

```powershell
claude mcp add --scope user chrome-devtools -- npx -y chrome-devtools-mcp@latest
claude mcp add --scope user playwright -- npx -y @playwright/mcp@latest
claude mcp add --scope user context7 -- npx -y @upstash/context7-mcp
```

User scope, so every project directory picks them up. What each one is for is in [Required tooling](#required-tooling) above.

---

## Where to start

Once setup is done:

1. Verify the three MCPs are connected: `claude mcp list`
2. Verify both junctions resolve: `Get-Item "$env:USERPROFILE\.claude\skills\OTLC-Design" | Select-Object LinkType,Target` and the same for `anti-ai-writing`. `LinkType` should read `Junction`.
3. Start a real project in `C:\dev\Projects\[project-name]\` and invoke `/OTLC-Design`

The smoke test passed 2026-05-03 (three reference sites; see [`HANDOVER.md`](HANDOVER.md)). Real projects have since run the loop and fed it: the devneural-hub design pass produced `patterns/app/two-band-type-scale.md` and ANTI-SLOP rule 25, and a 2026-07 carrier-block incident produced the shipping-hygiene section in [`STACK-DECISIONS.md`](STACK-DECISIONS.md).

The skills are the entry points. The repo is the substrate. All of it is git-versioned and evolves together through the closing loop.
