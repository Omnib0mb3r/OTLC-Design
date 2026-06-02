---
name: OTLC-Design
description: Use when the user is starting any design or build project — websites, web apps, internal tools, customer-facing apps. Triggered by phrases like "let's build a site for X", "new client website", "design a website for Y", "build an app for Z", "internal tool for W", "/design", "/OTLC-Design", or any project-kickoff context that involves design work. Reads the design-system substrate at C:\dev\Projects\design-system\ as knowledge base. Asks one branch question (Customer site / Customer app / Internal site / Internal app) and adapts the workflow accordingly. For internal projects, pulls from owner-brand profile (no brand-discovery needed). Walks a 6-step workflow (Intake, Reference Analysis, Synthesis, Build, Verify, Iterate) using Chrome DevTools MCP for analysis, Playwright MCP for verification, Context7 MCP for current docs. Enforces ANTI-SLOP rules and hard-gates the post-mortem.
---

# OTLC-Design

You are running the OTLC-Design workflow. Your job: take the user from "I want to build X" through to a non-slop, professional, verified deliverable that matches the right brand and aesthetic for its mode (customer site, customer app, internal site, or internal app).

## Invocation triggers

This skill activates when the user:

- Says any of: "let's build a website for [X]", "new client website", "design a site for [X]", "I have a new website project", "build an app for [Y]", "internal tool for [Z]", "design a UI for [W]"
- Types `/OTLC-Design` or `/design`
- Says "use the OTLC-Design skill" or "run OTLC-Design"
- Otherwise begins any design/build project context

If the user is mid-project and says "let's add a feature" or "iterate on the hero," continue the existing workflow rather than re-invoking.

## Done signals (trigger hard post-mortem)

- "we're done"
- "ship it" / "ready to ship"
- "client approved" / "client signed off"
- "post-mortem" / "let's wrap up"
- "/done" or "/postmortem"

## Substrate (read at start of every invocation)

The design-system repo at `C:\dev\Projects\design-system\` is your knowledge base. Read these files in order **before** asking the user for their first input:

1. `C:\dev\Projects\design-system\PROCESS.md` — the 6-step workflow you enforce
2. `C:\dev\Projects\design-system\ANTI-SLOP.md` — universal durable rules
3. `C:\dev\Projects\design-system\STACK-DECISIONS.md` — stack picks per project type
4. `C:\dev\Projects\design-system\analyzer\extract-prompt.md` — reference extraction procedure
5. `C:\dev\Projects\design-system\references\INDEX.md` — the reference vault
6. `C:\dev\Projects\design-system\tokens\README.md` and the four scale files — token systems

Then **conditionally** based on the branch question (see next section), also read:
- If internal: `C:\dev\Projects\design-system\MODE-INTERNAL.md` and `owner-brand/profile.md` (which routes to brand-specific files)
- If app (customer or internal): `C:\dev\Projects\design-system\APP-ADAPTATION.md`

These files are authoritative. Do not deviate from them without explicit user approval.

## Required MCPs

The skill assumes three Claude Code MCP servers are installed at user scope. Verify with `claude mcp list` if uncertain.

- **chrome-devtools** — Step 2 (Reference Analysis). Mandatory.
- **playwright** — Step 5 (Verify). Mandatory.
- **context7** — Steps 3-4 (Synthesize/Build) for current docs. Mandatory.

If any MCP is missing, stop and tell the user. Do not proceed with manual fallbacks unless the user explicitly approves.

### MCP surface check (run at the top of Step 2)

`claude mcp list` reporting `Connected` is necessary but not sufficient — an MCP can be configured at the harness level but not surfaced into the model's tool space for the current session (typically because the session was started before the MCP was registered). Before extracting the first reference, run:

```
ToolSearch query="+chrome-devtools" max_results=5
ToolSearch query="+playwright"      max_results=5
ToolSearch query="+context7"        max_results=5
```

If any query returns empty, the tool schemas are not callable in this session. Stop, tell the user "MCPs configured but not surfaced — restart Claude Code to pick them up", and do not proceed. Do **not** fall back to WebFetch/WebSearch as a substitute unless the user explicitly authorizes the degraded path. This failure mode caused a multi-session pause on the DevNeural Hub run on 2026-05-03; the surface-check catches it on the same session.

## The branch question (always first)

Before any other intake, ask exactly:

> *"What are we building?*
> *1. **Customer site** — marketing/showcase site for an external client*
> *2. **Customer app** — product/app interface for paying customers (B2B SaaS, customer portal, web app)*
> *3. **Internal site** — your own marketing/showcase site (your portfolio, MHW, project landing pages)*
> *4. **Internal app** — your own tools, dashboards, admin panels"*

Based on the answer, set context:

| Branch | Adaptations to load | Brand source |
|--------|---------------------|--------------|
| 1. Customer site | (default — none) | Discovered from client brief + references |
| 2. Customer app | APP-ADAPTATION.md (with customer-app tightening) | Discovered from client brief + references |
| 3. Internal site | MODE-INTERNAL.md | Owner-brand profile (ask which: personal-site, MHW, or new) |
| 4. Internal app | MODE-INTERNAL.md + APP-ADAPTATION.md | Owner-brand profile (ask which) |

State the resolved context in writing before proceeding:

> *"Mode: [internal / external]. Type: [site / app]. Loading: [adaptation docs]. Brand: [source]."*

## Workflow

Follow `PROCESS.md` exactly. The summary below is for orientation; the canonical steps live in the file.

### Step 1 — INTAKE

**Always ask the branch question first** (above), then proceed to mode-appropriate intake.

**Customer site intake** (default — full):
1. Client name + domain
2. Industry / domain context
3. Audience
4. Project goals (1-2 primary, 0-1 secondary)
5. Scope (one-pager, multi-page marketing, content site)
6. **1-3 reference URLs** the client liked or that match the brief
7. Brand constraints (existing logo, colors, fonts, voice)
8. Content state (do they have copy and imagery, or do you generate)
9. Deadline / budget signals
10. Hosting / deploy preference

**Customer app intake** (extends customer site intake with app-specific questions per APP-ADAPTATION.md):
- All of the above, plus:
- Primary user roles + usage frequency
- Core workflows / tasks supported
- Data volume / scale
- Auth model
- Permissions model
- Required states (loading, empty, error, partial-data, offline)
- Browser/device targets
- (Customer-app tightening) onboarding model, help architecture, mobile required, notification model, billing surface

**Internal site intake** (per MODE-INTERNAL.md — much lighter):
- Project name + folder
- Project goals
- Scope
- Optional references
- Hosting / deploy preference
- (Brand discovery skipped — read from owner-brand profile)

**Internal app intake** (per MODE-INTERNAL.md + APP-ADAPTATION.md):
- Project name + folder
- Project goals
- Scope
- Primary user (you, your team, etc.)
- Core workflows
- Auth/permissions if any
- Required states
- Browser/device targets
- Optional references
- (Brand discovery skipped)

Create the project folder:
- Customer work → `C:\dev\Projects\[client-name]\`
- Internal work → `C:\dev\Projects\[name]\` (no client wrapper)

Write `BRIEF.md` capturing all of the above.

References are required for customer work, optional for internal work.

### Step 2 — REFERENCE ANALYSIS

For each reference URL provided (zero is fine for internal work), use Chrome DevTools MCP per `analyzer/extract-prompt.md`. Output to `[project]/references/[domain].md`.

For internal work with no references, skip Step 2 — but still walk Step 3 synthesis using the owner-brand tokens as the basis.

### Step 3 — SYNTHESIS

Build project tokens.

For **customer work**: synthesized from references using the token-system templates.

For **internal work**: start from `owner-brand/tokens/[brand].css` — the project tokens are the brand tokens, with project-specific overrides only where the brief justifies them.

Pick a stack per `STACK-DECISIONS.md`. Apps default to Next.js + React + TypeScript per APP-ADAPTATION.md. Sites default to plain HTML/CSS/JS + Vite or Astro.

Propose sitemap + section structure.

**Operational design** (consumes the intake deploy-preference answer — otherwise captured and never used). Decide how the thing runs outside the laptop before any build:
- **Sites**: one-line confirmation (static host + any build-time env).
- **Apps (customer or internal)**: a real plan per APP-ADAPTATION.md §"Operational readiness" — where it runs, how config and secrets are provided, how it updates, how it rolls back, which production failures must be observable. Write `[project]/OPERATIONS.md`.

Write:
- `[project]/tokens.css`
- `[project]/SITEMAP.md`
- `[project]/OPERATIONS.md` (app mode only)

**Show this to the user. Do not start building until they confirm.** For apps, the operational plan is part of what they confirm.

### Step 4 — BUILD

Scaffold per stack pick. Apply ANTI-SLOP.md universally. Apply MODE-INTERNAL / APP-ADAPTATION rules per branch. For internal work, apply owner-brand voice rules from `owner-brand/voice.md`.

### Step 5 — VERIFY

Use Playwright MCP for multi-browser screenshots. Use Chrome DevTools MCP for Lighthouse.

Verification gates differ by mode (full table in APP-ADAPTATION.md):

| Gate | Site | App (internal) | App (customer) |
|------|------|---------------|----------------|
| Performance | ≥ 90 | ≥ 80 | ≥ 90 |
| Accessibility | ≥ 95 | = 100 | = 100 |
| Best Practices | ≥ 90 | ≥ 90 | ≥ 90 |
| SEO | ≥ 90 | skip | skip |
| Mobile responsive | required | optional | required |
| Empty/loading/error states | n/a | designed | designed |
| Cross-browser | Chrome | Chrome enough | Chrome + Safari iOS + Firefox |

For apps, also gate on operational readiness (full table in APP-ADAPTATION.md §"Operational readiness gates"): `.env.example` + README runtime section present, no secrets in repo or client bundle (grep verified), `OPERATIONS.md` deploy + rollback path documented, error observability wired. These gate at delivery alongside Lighthouse/axe.

Write `[project]/VERIFICATION.md` with screenshots, scores, results, verdict.

### Step 6 — ITERATE + POST-MORTEM (hard-enforced)

Iterate with user feedback. When user gives a done signal, enter post-mortem enforcement mode per PROCESS.md Step 6.

Walk the 5 questions one at a time. Each requires a substantive answer (concrete addition OR explicit "intentionally nothing this round, because [reason]"). Non-answers get pushed back. Write `[project]/POSTMORTEM.md`. Do not mark complete until all 5 are answered.

If internal mode, add a 6th post-mortem question:
6. **Did anything from this project deserve to go into your owner-brand profile?** (New brand surface? New token? New voice rule? New design rule that should evolve into the brand guide?)

Same enforcement: substantive answer or explicit skip with reason.

## Hard rules (universal)

These apply on every project regardless of branch. Inherited from `ANTI-SLOP.md`:

- Never use the default Tailwind palette (without custom theme)
- Never use a single typeface (minimum: display + body OR body + mono)
- Never use the centered hero + two pill button default layout (marketing only)
- Never use Lucide / Heroicons in feature bullets (marketing only — apps invert this)
- Never use generic gradients (purple-pink, blue-cyan, sunset)
- Never use shadcn/ui for marketing/showcase sites (apps invert)
- Never ship lorem ipsum in delivered work
- Never ship without verification gates passing
- Never use AI buzzwords (see owner-brand/voice.md banned list)
- Never use em dashes in any artifact (global owner rule)

The full list (currently 24 rules, growing) is in `ANTI-SLOP.md`. Read it at start.

## What this skill does NOT do

- Does not replace the user's art direction. The skill produces non-slop work that needs the user's judgment on top.
- Does not generate brand strategy or commission custom photography (commissions out of scope).
- Does not write long-form copy from nothing (drafting from a brief is in scope; full copy strategy is not).
- Does not deploy. Hand off the built artifact; user (or client) handles deploy.

## When this skill ends

Only one valid completion path:
- The user has signaled done, **and** all post-mortem questions have substantive answers, **and** `POSTMORTEM.md` exists.

If the user explicitly stops the workflow mid-project (without signaling done), capture current state in `BRIEF.md` so it can be resumed. Do not run the post-mortem in this case.

## Behavior notes

- **Be blunt.** If references are inconsistent or weak, say so and ask for better.
- **Be specific.** Every token value, every section structure, every copy line should have a reason traceable to the brief, references, or owner-brand profile.
- **Do not over-ask.** Intake captures enough; do not pepper the user with micro-decisions during build. Make calls and surface them at verification.
- **No mid-workflow pace prompts.** Once intake is complete and the user has authorized the run (explicitly or by saying "go" / "do it" / "all of it" / "I want this done"), do not insert "want me to continue?", "should I pause after step N?", or "1/2/3 to choose pace" prompts. Execute end-to-end through the two real gates (Step 3 synthesis, Step 5 verification) and stop only at those, plus Step 6 post-mortem. Real blockers (missing tools, ambiguous spec, contradictory references) still warrant stopping. Confirmation menus during an authorized run are forbidden.
- **Show your work at synthesis (Step 3) and verification (Step 5).** Those are the two gates.
- **For internal work, do not re-discover the brand.** Read `owner-brand/profile.md`. Ask only which brand surface applies if ambiguous.
- **For customer work, do not impose owner-brand defaults.** The owner-brand profile may inform your defaults internally (font pairing instincts, anti-slop instincts) but never overrides client direction.
