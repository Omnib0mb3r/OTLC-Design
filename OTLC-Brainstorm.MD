# design-system — OTLC-Brainstorm

---

## Vision

A repeatable methodology and skill that lets Michael produce **professional, non-slop client websites** with reference-quality aesthetics, without doing the heavy art-direction lift on every project from scratch.

The system exists because:

- Michael builds websites for other people. Each client has different aesthetic needs. He cannot codify a "personal style."
- AI defaults (Tailwind, shadcn, generic gradients, Lucide bullets, "Elevate your X" copy) produce visually identical output across every project. That output is slop.
- Pointing Claude at reference URLs *every project* is the right idea, but it should be a one-time setup with growing institutional memory, not per-project re-explanation.
- Tooling (browser MCPs, current-docs MCP) does not produce taste. Process, references, and durable rules do.

What success looks like:

- User says "let's build a site for [client]" and provides 1-3 reference URLs.
- Skill executes a 6-step workflow that systematically prevents slop and matches the references' aesthetic vocabulary.
- Output: a site that looks like good studio work (Land-book / Awwwards-honorable quality) on first pass.
- User does art direction on top instead of fighting defaults.
- Each project ends with a 5-minute post-mortem that improves the system: new rule, new pattern, new reference.

## Architecture

```
C:\dev\Projects\design-system\       ← this repo (system + knowledge base)
├── PROCESS.md                       6-step workflow
├── ANTI-SLOP.md                     Durable rules
├── STACK-DECISIONS.md               Plain HTML / Astro / Next decision tree
├── references/                      Curated reference vault (growable)
├── patterns/                        Hand-built layout primitives (growable)
├── tokens/                          Type/color/spacing/motion templates
├── analyzer/                        Prompts for extracting design data
├── project-template/                Starter scaffolds
├── INIT.md, HANDOVER.md             Fresh-session pickup
└── CLAUDE.md, WORKFLOW.md           Repo behavior rules

C:\Users\michael\.claude\skills\OTLC-Design\
└── SKILL.md                         The entry point Claude invokes

C:\dev\Projects\[client-name]\       ← actual client work happens here
                                     Skill reads design-system as knowledge base
```

Three Claude Code MCP servers are required (user scope, available everywhere):

- **chrome-devtools** — reference analysis in Step 2
- **playwright** — verification in Step 5
- **context7** — current documentation throughout

The skill is the entry point. The repo is the substrate. Both are git-versioned and evolve together.

---

## Tools

**Chrome DevTools MCP** — Drives Chrome to navigate reference sites, extract computed styles, type scales, color values, spacing, run Lighthouse, capture screenshots. The reference-analysis engine.

**Playwright MCP** — Drives Chromium/Firefox/WebKit for verifying the user's built site: multi-browser screenshots, accessibility audits, interaction testing.

**Context7 MCP** — Pulls current documentation for any library or web spec on demand. Prevents hallucination of stale APIs (especially relevant for newer CSS like anchor positioning, container queries, view transitions).

**Visual Companion** — Browser-based companion for showing mockups, diagrams, and option comparisons during sessions. Available via the superpowers brainstorming skill.

---

## Feature Workflow

When *modifying the design-system itself* (not building a client site), use the OTLC + superpowers pipeline inherited from the template. See [`CLAUDE.md`](CLAUDE.md) for details.

When *building a project (any of the four modes)*, the user invokes the `OTLC-Design` skill, which reads from this repo and follows [`PROCESS.md`](PROCESS.md).

### PRE — before brainstorming changes to the system

1. Read this file (Vision, Architecture, Decisions Made, Open Questions)
2. Vision check (already defined above; only revise on explicit request)
3. Visual Companion offer for any layout / pattern / token visualization work

### RUN — superpowers pipeline

Standard `superpowers:brainstorming` → `writing-plans` → `subagent-driven-development` → `finishing-a-development-branch`.

### POST — log decisions

- Append to `Decisions Made` below
- Append/resolve `Open Questions` below
- Update `Architecture` if structure changed

### END — close the session

- Append a dated `Session Log` entry below

---

## Decisions Made

### 2026-05-02 — Initial setup

- **Repo location**: `C:\dev\Projects\design-system\` (sibling to other client projects in `C:\dev\Projects\`).
- **Skill location**: `C:\Users\michael\.claude\skills\OTLC-Design\SKILL.md`. Skill is the entry point; repo is the substrate. (Originally named `design-website` — renamed to `OTLC-Design` in session 2 when scope expanded beyond websites.)
- **Stack policy**: Multi-stack per project (plain HTML/CSS/JS for one-pagers, Astro for content sites, React/Next.js only for genuine apps). Documented in [`STACK-DECISIONS.md`](STACK-DECISIONS.md).
- **MCPs**: chrome-devtools, playwright, context7. User scope. Documented in [`HANDOVER.md`](HANDOVER.md).
- **Process steps**: 6 (Intake, Reference Analysis, Synthesis, Build, Verify, Iterate). Documented in [`PROCESS.md`](PROCESS.md).
- **Anti-slop rules**: 20 initial rules covering type, color, layout, copy, motion, components. See [`ANTI-SLOP.md`](ANTI-SLOP.md).
- **Reference vault**: Pre-seeded with ~25 curated studio and product sites organized by aesthetic. See [`references/INDEX.md`](references/INDEX.md).
- **Template origin detached**: This repo is no longer connected to `dev-template` remote. User can `gh repo create` to add a new origin when ready.
- **Reasoning**: User builds websites for clients (no personal style to codify). System needs to take 1-3 reference URLs per project and produce non-slop output that matches the aesthetic. Improvement over time via post-mortem additions to references / patterns / anti-slop.

### 2026-05-03 — Session 2 decisions

- **Scope**: Expanded from "websites for clients" to "any design/build project". 4 modes via single branch question at intake.
- **Mode model**: Customer site / Customer app / Internal site / Internal app. One branch question routes to the right adaptation docs and brand source.
- **Skill rename**: `design-website` → `OTLC-Design`. Reflects broader scope (sites + apps + internal + customer). Folder at `~/.claude/skills/OTLC-Design/`.
- **Owner-brand profile**: Built from user's existing `<BrandGuide>.docx`. Two brand surfaces (personal-site, MHW). Source `.docx` lives in `owner-brand/source/`; markdown copies are derived working copies.
- **Internal mode quality bar**: Same as customer work. Internal mode skips brand-discovery questions only. ANTI-SLOP, verification, post-mortem all apply identically.
- **App adaptation**: Most marketing anti-slop rules invert for apps (shadcn fine, Lucide fine, Tailwind defaults fine, dense grids fine). Customer-app tightening adds onboarding/mobile/perf/cross-browser gates.
- **Hard-enforced post-mortem**: Step 6 cannot be skipped. Each of 5 (or 6 in internal mode) questions requires substantive answer. Project not complete until POSTMORTEM.md exists.
- **Closing-loop conventions**: Topical commit messages (`anti-slop:`, `patterns:`, `references:`, `process:`, `skill:`, `owner-brand:`, `handover:`).
- **Brand-rule softenings**: User flagged his own guide as too rigid in places. Softened: dark backgrounds default-not-required, motion ambient default-not-required, eyebrows available-not-required, blue beta-only scoped to personal-site brand only.
- **Reasoning**: System must serve all the owner's design work, not just websites. Internal work was being underserved by a client-only model that asked brand-discovery questions every time. App work was being malformed by marketing anti-slop rules that don't apply.

### 2026-06-02 — Operational-readiness + skill versioning

- **Operational-readiness pass (app mode)**: Added 5 rules + a gates table to [`APP-ADAPTATION.md`](APP-ADAPTATION.md) (documented runtime config, no secrets in repo/client bundle, deploy decided at synthesis, no deploy without rollback, no invisible async failures). Sourced from the "DevOps for vibe coders" article; scoped to apps because the marketing default branch (static sites) does not deploy infra. `PROCESS.md` bumped to v1.2: Step 3 synthesis gains an Operational-design item that consumes the previously dead-end intake deploy-preference answer and writes `OPERATIONS.md`.
- **Deliberately NOT added**: CI/CD, IaC, monitoring stacks, backup automation. Those are client-project concerns; this repo is substrate and explicitly has no deploy target (per `CLAUDE.md` "What this repo does NOT do").
- **Skill now versioned in-repo**: Canonical `SKILL.md` moved from the unversioned `~/.claude/skills/OTLC-Design/` into the repo at `skill/SKILL.md`. `~/.claude/skills/OTLC-Design` is now a **directory junction** to `skill/`, so Claude Code loads the same physical file git tracks. Chosen over a vendored copy (drift-prone) and a separate git init (fragments history). The skill already hardcodes this repo's path at runtime, so the junction adds no new coupling. Recreation documented in [`skill/README.md`](skill/README.md).
- **Reasoning**: The repo's own `CLAUDE.md` promises "skill changes get committed", but the skill lived outside any repo, so the convention could not hold and edits drifted. Versioning it in-repo closes that gap.

---

## Open Questions

- [ ] Should `project-template/` ship with concrete starter scaffolds (vanilla-vite, astro, next), or leave empty and use `npm create ...` on demand? Currently scaffolded as empty placeholders.
- [ ] Does the user want a remote origin set up now? GitHub repo name suggestion: `OTLC-Design` (matching the skill name) or `design-system` (matching the substrate name).
- [ ] How does the brand-guide `.docx` stay in sync with derived markdown? Currently manual re-extraction. Worth a tiny PowerShell script or skip until it bites?
- [ ] Add Firecrawl MCP as fallback for JS-heavy reference sites? (Not installed.)
- [ ] First app project — which one? Could exercise MODE-INTERNAL + APP-ADAPTATION + owner-brand pull all at once and surface real gaps.
- [ ] Should owner-brand grow a third surface for OTLC-domain customer work (i.e., "OTLC consulting" brand for client-facing materials), or keep client-facing materials per-project?

---

## Session Log

### 2026-05-02 — Session 1: Initial system bootstrap

**Participants:** the operator

**What happened:**
Discussed the slop problem (AI-generated websites all look the same), worked through MCP options (Magic vs Figma vs Playwright vs Chrome DevTools), arrived at: tool stack matters less than process + references + durable rules. Reframed the goal from "personal design system" to "process system that takes per-project references and produces non-slop output." Cloned `dev-template` as starting point, detached origin, built out the design-system structure.

**What was built:**
- Repo structure at `C:\dev\Projects\design-system\` initialized from `dev-template`
- Foundational docs: README, CLAUDE.md (rewritten for this repo's purpose), OTLC-Brainstorm.MD (this file), PROCESS.md, ANTI-SLOP.md, STACK-DECISIONS.md, INIT.md, HANDOVER.md
- Subdirectories with content: references/INDEX.md (pre-seeded with ~25 studio/product sites), patterns/README.md, tokens/ (type-scales, color-systems, spacing, motion), analyzer/ (extract-prompt + README), project-template/ (vanilla-vite + astro placeholders)
- Skill at `C:\Users\michael\.claude\skills\design-website\SKILL.md`
- MCPs installed at user scope: chrome-devtools, playwright, context7
- devneural.jsonc populated with real metadata
- Initial git commit

**Next:**
- User opens `C:\dev\Projects\design-system\` in a fresh Claude session
- Fresh Claude reads INIT.md and HANDOVER.md
- Smoke test: user provides 1-3 reference URLs, Claude runs the analyzer, prove the workflow works
- First real project test
- Iterate on rules / patterns / process based on what surfaces

---

### 2026-05-03 — Session 2: Scope expansion + branch model + owner-brand integration

**Participants:** the operator

**What happened:**
Scope grew from "build websites for clients" to "build any project — sites and apps, internal and external — with the right rules per mode." Worked through:

1. **Mode dimension**: external client (unknown brand) vs internal/owned (known brand). Internal mode skips brand-discovery questions; reads from owner-brand profile.
2. **Type dimension**: marketing/showcase site vs product/app interface. Apps invert most marketing anti-slop rules (shadcn fine, Lucide bullets fine, default Tailwind palette fine, etc.).
3. **App-user dimension** (only when type=app): internal employees vs paying customers. Customer apps tighten gates (mobile required, onboarding designed, perf back to 90, cross-browser including Safari iOS).

Simplified to **4-way branch question** at intake: Customer site / Customer app / Internal site / Internal app. Adaptation docs (MODE-INTERNAL.md, APP-ADAPTATION.md with customer-app tightening subsection) load per branch.

Analyzed user's existing 4 projects (omnibomber-site, Landmark40, stream-deck, conveyor-designer) to extract real house style. Then user provided his actual brand guide (`<BrandGuide>.docx`) — moved into repo as `owner-brand/source/` and converted to markdown working copies.

User pushed back on a few of his own brand rules being too rigid; softened: dark backgrounds default-not-required, motion ambient default-not-required, eyebrows available-not-required, blue beta-only on personal-site brand only.

Renamed skill from `design-website` to `OTLC-Design` reflecting the broader scope (OTLC = On The Level Concepts, the owner's domain).

**What was built:**
- `MODE-INTERNAL.md` — adaptation for internal/owned work
- `APP-ADAPTATION.md` — adaptation for app/product UI with customer-app tightening subsection
- `owner-brand/` — full structure: README, profile (index), voice (universal DOs/DON'Ts), brands/personal-site.md, brands/mhw.md, tokens/personal-site.css, tokens/mhw.css, source/<BrandGuide>.docx
- `patterns/` subdivided into `marketing/` and `app/` with READMEs
- `references/INDEX.md` extended with App / Product UI category (12 app references seeded)
- `STACK-DECISIONS.md` updated for app stack defaults (Next.js + React + shadcn for apps, native section added for desktop)
- `ANTI-SLOP.md` extended with 4 new rules (no emoji icons, sub-12px legibility floor, no personal-aesthetic chrome on client work, custom cursor deliberate-only)
- `PROCESS.md` Step 1 updated with branch question and mode-appropriate intake
- `SKILL.md` renamed to OTLC-Design, fully rewritten for new scope and branch handling
- `HANDOVER.md`, `INIT.md`, `README.md` rewritten for new scope and new closing-loop emphasis
- All cross-references updated (15 files swept for design-website → OTLC-Design)

**Decisions logged below**

**Next:**
- Smoke test in fresh Claude session opened in this repo
- First real project (likely an internal one, to exercise MODE-INTERNAL + owner-brand pull)
- Capture all gaps surfaced through Step 6 hard-enforced post-mortem
- Set up GitHub remote when ready (`gh repo create`)
