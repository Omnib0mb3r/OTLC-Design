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

C:\Users\michael\.claude\skills\design-website\
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

When *building a client site*, the user invokes the `design-website` skill, which reads from this repo and follows [`PROCESS.md`](PROCESS.md).

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
- **Skill location**: `C:\Users\michael\.claude\skills\design-website\SKILL.md`. Skill is the entry point; repo is the substrate.
- **Stack policy**: Multi-stack per project (plain HTML/CSS/JS for one-pagers, Astro for content sites, React/Next.js only for genuine apps). Documented in [`STACK-DECISIONS.md`](STACK-DECISIONS.md).
- **MCPs**: chrome-devtools, playwright, context7. User scope. Documented in [`HANDOVER.md`](HANDOVER.md).
- **Process steps**: 6 (Intake, Reference Analysis, Synthesis, Build, Verify, Iterate). Documented in [`PROCESS.md`](PROCESS.md).
- **Anti-slop rules**: 20 initial rules covering type, color, layout, copy, motion, components. See [`ANTI-SLOP.md`](ANTI-SLOP.md).
- **Reference vault**: Pre-seeded with ~25 curated studio and product sites organized by aesthetic. See [`references/INDEX.md`](references/INDEX.md).
- **Template origin detached**: This repo is no longer connected to `dev-template` remote. User can `gh repo create` to add a new origin when ready.
- **Reasoning**: User builds websites for clients (no personal style to codify). System needs to take 1-3 reference URLs per project and produce non-slop output that matches the aesthetic. Improvement over time via post-mortem additions to references / patterns / anti-slop.

---

## Open Questions

- [ ] Should `project-template/` ship with concrete starter scaffolds (vanilla-vite, astro), or leave empty and use `npm create vite@latest` / `npm create astro@latest` on demand? Currently scaffolded as empty placeholders.
- [ ] Does the user want a remote origin set up now, or wait until first client project ships?
- [ ] Add a `clients/` directory here for client-specific design preferences as they accumulate, or keep client data isolated to each client's own project repo?
- [ ] How aggressive should the verification gate be in Step 5? Hard-fail on Lighthouse perf <90, or warn?
- [ ] When a reference site is JavaScript-heavy and Chrome DevTools MCP can not extract clean tokens, fallback to Firecrawl MCP? (not currently installed)

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
- First real client project test
- Iterate on rules / patterns / process based on what surfaces
