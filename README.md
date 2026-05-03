# design-system

A repeatable methodology for building **non-slop, professional sites and apps** for clients and for owned work, marketing and product. The substrate that powers the `OTLC-Design` skill.

This repo is not a website or app. It is the system that produces them: process, anti-slop rules, reference vault, pattern library, token templates, mode adaptations, owner-brand profile, and analyzer prompts that Claude reads at the start of every project.

---

## Skill invocation

The `OTLC-Design` skill is the entry point. Invoke it from the project directory you're working in.

### Triggers

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
> *3. **Internal site**: your own marketing/showcase site (your portfolio, MHW, project landing pages)*
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

After you signal done, the skill walks **5 universal questions** (or 6 in internal mode), one at a time. Each question requires either:

- **A concrete addition** ("Yes, add rule: never X"; "Yes, lift this hero pattern to patterns/marketing/"; "Yes, add bbb.studio to references"). Claude writes the addition AND commits it to this repo with a topical message.
- **An explicit skip with reason** ("Intentionally nothing this round, because [reason]"). Logged in the project's `POSTMORTEM.md`.

**Non-answers ("nah", "skip", "we're good", silence) are rejected.** The skill re-asks. The skill does not advance until satisfied.

### The 5 universal questions

1. **New ANTI-SLOP rule?** Did anything ship that felt generic, default, or templated? Did you have to tell Claude to stop doing X mid-project?
2. **New pattern for `patterns/`?** Did we build a structural move you'd reach for again on a different project?
3. **New reference for `references/INDEX.md`?** Did we encounter a site worth keeping in the curated vault?
4. **Did `PROCESS.md` drag or lack a step?** Was any step too long, too short, missing, in the wrong order, or asking the wrong questions?
5. **Did the skill itself need refinement?** Wrong tone, wrong order, missing checkpoints, over-asking, under-asking?

### Internal-mode 6th question

6. **Did anything from this project deserve to go into your owner-brand profile?** New brand surface? New token? New voice rule? New design rule for the brand guide?

### What gets committed where

| Addition type | Goes to | Commit message |
|---------------|---------|----------------|
| Anti-slop rule | `ANTI-SLOP.md` | `anti-slop: <short rule summary>` |
| Pattern (marketing) | `patterns/marketing/[name].md` | `patterns: add marketing/<name>` |
| Pattern (app) | `patterns/app/[name].md` | `patterns: add app/<name>` |
| Reference | `references/INDEX.md` (+ optional deep analysis at `references/[slug].md`) | `references: add <domain>` |
| Process change | `PROCESS.md` (bump version) | `process: <what changed>` |
| Skill change | `~/.claude/skills/OTLC-Design/SKILL.md` | `skill: <what changed>` |
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
| [`ANTI-SLOP.md`](ANTI-SLOP.md) | 24 universal durable rules Claude follows on every project. |
| [`STACK-DECISIONS.md`](STACK-DECISIONS.md) | When to use plain HTML / Astro / Next.js / native. |
| [`MODE-INTERNAL.md`](MODE-INTERNAL.md) | Adaptation for internal/owned work. Skips brand discovery, pulls owner-brand profile. |
| [`APP-ADAPTATION.md`](APP-ADAPTATION.md) | Adaptation for app/product UI. Anti-slop inversion, app stack defaults, app verification gates. Includes customer-app tightening subsection. |
| [`owner-brand/`](owner-brand/) | Standing brand profile (personal-site, MHW), voice rules, drop-in tokens, source `.docx`. |
| [`references/`](references/) | Curated vault of sites worth studying. Catalog in [`references/INDEX.md`](references/INDEX.md). |
| [`patterns/`](patterns/) | Hand-built layout primitives. Subdivided into [`marketing/`](patterns/marketing/) and [`app/`](patterns/app/). Empty by design; grow from real work. |
| [`tokens/`](tokens/) | Type scale, color, spacing, motion *templates*. Synthesized per project, not copied from here. |
| [`analyzer/`](analyzer/) | Prompts and procedures Claude uses to extract design data from references via Chrome DevTools MCP. |
| [`project-template/`](project-template/) | Starter scaffolds copied out when a new project begins. |
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

Install commands and verification steps live in [`HANDOVER.md`](HANDOVER.md).

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

## Where to start

If you've just set this up:

1. Verify the three MCPs are connected: `claude mcp list`
2. Open `C:\dev\Projects\design-system\` in a fresh Claude session and run a smoke test (see [`HANDOVER.md`](HANDOVER.md) §"What is pending")
3. After smoke test passes, start a real project in `C:\dev\Projects\[project-name]\` and invoke `/OTLC-Design`

The skill is the entry point. The repo is the substrate. Both are git-versioned and evolve together.
