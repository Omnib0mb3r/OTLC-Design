# design-system: OTLC-Brainstorm

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
├── PROCESS.md                       6-step workflow (v1.3)
├── ANTI-SLOP.md                     Durable visual rules (26, growable)
├── STACK-DECISIONS.md               Plain HTML / Astro / Next decision tree
├── MODE-INTERNAL.md                 Adaptation for owned work
├── APP-ADAPTATION.md                Adaptation for app/product UI
├── BUGS.md                          Persistent bug log
├── skill/                           CANONICAL OTLC-Design skill source
├── skill-writing/                   CANONICAL anti-ai-writing skill source
├── legal/                           Per-law compliance library + delivery gate
├── guides/                          Technical build guides (perf, SEO, AEO, GA4)
├── owner-brand/                     Standing brand profile, voice, tokens
├── references/                      Curated reference vault (growable)
├── patterns/                        Hand-built layout primitives (growable)
├── tokens/                          Type/color/spacing/motion templates
├── analyzer/                        Prompts for extracting design data
├── project-template/                Starter scaffolds
├── INIT.md, HANDOVER.md             Fresh-session pickup
└── CLAUDE.md, WORKFLOW.md           Repo behavior rules

C:\Users\michael\.claude\skills\
├── OTLC-Design       → junction to design-system\skill\
└── anti-ai-writing   → junction to design-system\skill-writing\
                       Junctions, not copies: Claude Code runs the git-tracked file

C:\dev\Projects\[client-name]\       ← actual client work happens here
                                     Skill reads design-system as knowledge base
```

Three Claude Code MCP servers are required (user scope, available everywhere):

- **chrome-devtools**: reference analysis in Step 2
- **playwright**: verification in Step 5
- **context7**: current documentation throughout

The skill is the entry point. The repo is the substrate. Both are git-versioned and evolve together.

---

## Tools

**Chrome DevTools MCP**: drives Chrome to navigate reference sites, extract computed styles, type scales, color values, spacing, run Lighthouse, capture screenshots. The reference-analysis engine.

**Playwright MCP**: drives Chromium/Firefox/WebKit for verifying the user's built site: multi-browser screenshots, accessibility audits, interaction testing.

**Context7 MCP**: pulls current documentation for any library or web spec on demand. Prevents hallucination of stale APIs (especially relevant for newer CSS like anchor positioning, container queries, view transitions).

**Visual Companion**: browser-based companion for showing mockups, diagrams, and option comparisons during sessions. Available via the superpowers brainstorming skill.

---

## Feature Workflow

When *modifying the design-system itself* (not building a client site), use the OTLC + superpowers pipeline inherited from the template. See [`CLAUDE.md`](CLAUDE.md) for details.

When *building a project (any of the four modes)*, the user invokes the `OTLC-Design` skill, which reads from this repo and follows [`PROCESS.md`](PROCESS.md).

### PRE: before brainstorming changes to the system

1. Read this file (Vision, Architecture, Decisions Made, Open Questions)
2. Vision check (already defined above; only revise on explicit request)
3. Visual Companion offer for any layout / pattern / token visualization work

### RUN: superpowers pipeline

Standard `superpowers:brainstorming` → `writing-plans` → `subagent-driven-development` → `finishing-a-development-branch`.

### POST: log decisions

- Append to `Decisions Made` below
- Append/resolve `Open Questions` below
- Update `Architecture` if structure changed

### END: close the session

- Append a dated `Session Log` entry below

---

## Decisions Made

### 2026-05-02: Initial setup

- **Repo location**: `C:\dev\Projects\design-system\` (sibling to other client projects in `C:\dev\Projects\`).
- **Skill location**: `C:\Users\michael\.claude\skills\OTLC-Design\SKILL.md`. Skill is the entry point; repo is the substrate. (Originally named `design-website`, renamed to `OTLC-Design` in session 2 when scope expanded beyond websites.)
- **Stack policy**: Multi-stack per project (plain HTML/CSS/JS for one-pagers, Astro for content sites, React/Next.js only for genuine apps). Documented in [`STACK-DECISIONS.md`](STACK-DECISIONS.md).
- **MCPs**: chrome-devtools, playwright, context7. User scope. Documented in [`HANDOVER.md`](HANDOVER.md).
- **Process steps**: 6 (Intake, Reference Analysis, Synthesis, Build, Verify, Iterate). Documented in [`PROCESS.md`](PROCESS.md).
- **Anti-slop rules**: 20 initial rules covering type, color, layout, copy, motion, components. See [`ANTI-SLOP.md`](ANTI-SLOP.md).
- **Reference vault**: Pre-seeded with ~25 curated studio and product sites organized by aesthetic. See [`references/INDEX.md`](references/INDEX.md).
- **Template origin detached**: This repo is no longer connected to `dev-template` remote. User can `gh repo create` to add a new origin when ready.
- **Reasoning**: User builds websites for clients (no personal style to codify). System needs to take 1-3 reference URLs per project and produce non-slop output that matches the aesthetic. Improvement over time via post-mortem additions to references / patterns / anti-slop.

### 2026-05-03: Session 2 decisions

- **Scope**: Expanded from "websites for clients" to "any design/build project". 4 modes via single branch question at intake.
- **Mode model**: Customer site / Customer app / Internal site / Internal app. One branch question routes to the right adaptation docs and brand source.
- **Skill rename**: `design-website` → `OTLC-Design`. Reflects broader scope (sites + apps + internal + customer). Folder at `~/.claude/skills/OTLC-Design/`.
- **Owner-brand profile**: Built from user's existing `<BrandGuide>.docx`. Two brand surfaces. Source `.docx` lives in `owner-brand/source/`; markdown copies are derived working copies.
- **Internal mode quality bar**: Same as customer work. Internal mode skips brand-discovery questions only. ANTI-SLOP, verification, post-mortem all apply identically.
- **App adaptation**: Most marketing anti-slop rules invert for apps (shadcn fine, Lucide fine, Tailwind defaults fine, dense grids fine). Customer-app tightening adds onboarding/mobile/perf/cross-browser gates.
- **Hard-enforced post-mortem**: Step 6 cannot be skipped. Each of 5 (or 6 in internal mode) questions requires substantive answer. Project not complete until POSTMORTEM.md exists.
- **Closing-loop conventions**: Topical commit messages (`anti-slop:`, `patterns:`, `references:`, `process:`, `skill:`, `owner-brand:`, `handover:`).
- **Brand-rule softenings**: User flagged his own guide as too rigid in places. Softened: dark backgrounds default-not-required, motion ambient default-not-required, eyebrows available-not-required, blue beta-only scoped to personal-site brand only.
- **Reasoning**: System must serve all the owner's design work, not just websites. Internal work was being underserved by a client-only model that asked brand-discovery questions every time. App work was being malformed by marketing anti-slop rules that don't apply.

### 2026-06-02: Operational-readiness + skill versioning

- **Operational-readiness pass (app mode)**: Added 5 rules + a gates table to [`APP-ADAPTATION.md`](APP-ADAPTATION.md) (documented runtime config, no secrets in repo/client bundle, deploy decided at synthesis, no deploy without rollback, no invisible async failures). Sourced from the "DevOps for vibe coders" article; scoped to apps because the marketing default branch (static sites) does not deploy infra. `PROCESS.md` bumped to v1.2: Step 3 synthesis gains an Operational-design item that consumes the previously dead-end intake deploy-preference answer and writes `OPERATIONS.md`.
- **Deliberately NOT added**: CI/CD, IaC, monitoring stacks, backup automation. Those are client-project concerns; this repo is substrate and explicitly has no deploy target (per `CLAUDE.md` "What this repo does NOT do").
- **Skill now versioned in-repo**: Canonical `SKILL.md` moved from the unversioned `~/.claude/skills/OTLC-Design/` into the repo at `skill/SKILL.md`. `~/.claude/skills/OTLC-Design` is now a **directory junction** to `skill/`, so Claude Code loads the same physical file git tracks. Chosen over a vendored copy (drift-prone) and a separate git init (fragments history). The skill already hardcodes this repo's path at runtime, so the junction adds no new coupling. Recreation documented in [`skill/README.md`](skill/README.md).
- **Reasoning**: The repo's own `CLAUDE.md` promises "skill changes get committed", but the skill lived outside any repo, so the convention could not hold and edits drifted. Versioning it in-repo closes that gap.

### 2026-07-20: anti-ai-writing skill (prose slop subsystem)

- **Second skill added, hosted in this repo**: `anti-ai-writing`, canonical source at `skill-writing/`, junctioned to `~/.claude/skills/anti-ai-writing` (same pattern as `skill/`). Distilled from Wikipedia:Signs of AI writing, fetched section-by-section via the MediaWiki API for verbatim watch-phrase lists.
- **Hybrid placement over alternatives**: Considered a standalone repo, a design-system-only doc, and an unversioned skills-dir copy. Chose: deep skill here + thin pointer in global `~/.claude/CLAUDE.md` + wiring into the OTLC workflow. Reasoning: the rule set applies to all prose everywhere (so it cannot live only behind the OTLC-Design trigger), but the repo already owns the anti-slop closing loop, and a second junctioned skill reuses proven infrastructure.
- **Post-mortem grew to 6 universal questions** (7 internal): new question 6 asks for prose-slop rules, mirroring question 1's visual-slop ask. `PROCESS.md` bumped to v1.3. Without a closing-loop hook, the skill would be static; with it, every project can grow the tells list.
- **False-positive guard is load-bearing**: the skill ships `references/false-positives.md` (ineffective indicators, chance-level human detection, unreliable detectors) and mandates density judgements, never authorship verdicts. A tells catalogue without this becomes a witch-hunt tool.
- **BUGS.md created** (global-instructions requirement): 7-bug consolidation sweep from git history and ANTI-SLOP provenance. BUG-007 logged OPEN: 444 em/en dashes across 29 repo markdown files, awaiting a cleanup pass decision.
- **GitHub remote confirmed live**: `Omnib0mb3r/OTLC-Design` (private). HANDOVER's "remote not yet configured" was stale and is fixed.

---

## Open Questions

- [ ] Should `project-template/` ship with concrete starter scaffolds (vanilla-vite, astro, next), or leave empty and use `npm create ...` on demand? Currently scaffolded as empty placeholders.
- [x] ~~Does the user want a remote origin set up now?~~ Resolved: `github.com/Omnib0mb3r/OTLC-Design` (private) is live as origin.
- [ ] How does the brand-guide `.docx` stay in sync with derived markdown? Currently manual re-extraction. Worth a tiny PowerShell script or skip until it bites?
- [ ] Add Firecrawl MCP as fallback for JS-heavy reference sites? (Not installed.)
- [ ] First app project: which one? Could exercise MODE-INTERNAL + APP-ADAPTATION + owner-brand pull all at once and surface real gaps.
- [ ] Should owner-brand grow a third surface for OTLC-domain customer work (i.e., "OTLC consulting" brand for client-facing materials), or keep client-facing materials per-project?
- [ ] `guides/` (added 2026-07-20: SEO/AEO track, structured data, GA4, browser-aware design) is stored but not wired into the workflow. Candidates: PROCESS Step 4 build checklist (crawlability, JSON-LD), Step 5 gates (AEO/SEO verification), or a new delivery-checklist doc. Decide after the first real project shows where they bite.

---

## Session Log

### 2026-05-02: Session 1: Initial system bootstrap

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

### 2026-05-03: Session 2: Scope expansion + branch model + owner-brand integration

**Participants:** the operator

**What happened:**
Scope grew from "build websites for clients" to "build any project (sites and apps, internal and external) with the right rules per mode." Worked through:

1. **Mode dimension**: external client (unknown brand) vs internal/owned (known brand). Internal mode skips brand-discovery questions; reads from owner-brand profile.
2. **Type dimension**: marketing/showcase site vs product/app interface. Apps invert most marketing anti-slop rules (shadcn fine, Lucide bullets fine, default Tailwind palette fine, etc.).
3. **App-user dimension** (only when type=app): internal employees vs paying customers. Customer apps tighten gates (mobile required, onboarding designed, perf back to 90, cross-browser including Safari iOS).

Simplified to **4-way branch question** at intake: Customer site / Customer app / Internal site / Internal app. Adaptation docs (MODE-INTERNAL.md, APP-ADAPTATION.md with customer-app tightening subsection) load per branch.

Analyzed user's existing 4 projects (omnibomber-site, Landmark40, stream-deck, conveyor-designer) to extract real house style. Then user provided his actual brand guide (`<BrandGuide>.docx`), moved into repo as `owner-brand/source/` and converted to markdown working copies.

User pushed back on a few of his own brand rules being too rigid; softened: dark backgrounds default-not-required, motion ambient default-not-required, eyebrows available-not-required, blue beta-only on personal-site brand only.

Renamed skill from `design-website` to `OTLC-Design` reflecting the broader scope (OTLC = On The Level Concepts, the owner's domain).

**What was built:**
- `MODE-INTERNAL.md`: adaptation for internal/owned work
- `APP-ADAPTATION.md`: adaptation for app/product UI with customer-app tightening subsection
- `owner-brand/`: full structure: README, profile (index), voice (universal DOs/DON'Ts), brands/personal-site.md, brands/mhw.md, tokens/personal-site.css, tokens/mhw.css, source/<BrandGuide>.docx
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

### 2026-06-02: Session 3: Operational readiness + skill versioning

**What happened:** Added the operational-readiness rules and gates to `APP-ADAPTATION.md`, bumped `PROCESS.md` to v1.2 so Step 3 consumes the intake deploy-preference answer, and moved the skill's canonical `SKILL.md` into the repo at `skill/` behind a directory junction. Decisions logged above.

**Next:** first real project.

### 2026-07-20: Session 4: anti-ai-writing, legal library, full audit

**Participants:** the operator

**What happened:**

1. **Second skill built.** `anti-ai-writing` at `skill-writing/`, distilled from Wikipedia:Signs of AI writing, junctioned to `~/.claude/skills/anti-ai-writing`. Prose counterpart to `ANTI-SLOP.md`. Post-mortem grew to 6 universal questions and `PROCESS.md` went to v1.3.
2. **BUGS.md created** with a 7-bug consolidation sweep. Later grew to cover the missing MCPs and the repo-wide em dash violations.
3. **MCP servers were gone.** `claude mcp list` returned none of the three the system depends on, while `HANDOVER.md` claimed all three connected. Reinstalled and verified. Logged as BUG-008. This is the clearest evidence so far that HANDOVER's verification commands need running rather than trusting.
4. **`guides/` added** (seven technical guides plus an INDEX) covering performance, SEO, structured data, AEO, and GA4.
5. **`legal/` added.** Per-law compliance library with a triage table, a delivery checklist wired into Step 5, and one file per statute so laws can be amended independently. Explicitly not legal advice, and the checklist forces the counsel-review question to be answered at intake rather than after launch.
6. **Full repo audit run** across nine dimensions (claim accuracy, link integrity, cross-doc consistency, self-compliance with the repo's own prose rules, README quality, skill integrity, orphans, BUGS accuracy, functional verification), with every finding adversarially verified before being accepted. 98 findings raised, 67 confirmed, 31 refuted. Link integrity came back clean.

**What the audit caught that mattered most:** the `POSTMORTEM.md` template in `PROCESS.md` still had five sections after the workflow moved to six questions, so an agent following the template verbatim would have shipped a post-mortem that failed the step's own gate, and the dropped question was the one feeding the new writing skill. The closing loop had a hole in it from the moment it was widened.

**Standing lesson:** documentation asserting a state is not the state. Two of the highest-severity findings this session (the MCPs, the post-mortem template) were places where a doc confidently described something that was not true. The audit dimension worth repeating is "verify every claim against reality", not "read for typos".

**Session 4 continued: legal library, full audit, and the public-repo scrub.**

7. **`legal/` built.** 22 law files, each researched against primary sources and then fact-checked by a separate pass that verified every date, threshold, penalty figure, and citation URL. The fact-checkers corrected real defects (a miscited EDPB example, an unsupported claim that a Council file had been adopted, an unconfirmable court stay) and marked what they could not confirm as `UNVERIFIED:` rather than guessing. That convention is now the standard for this directory: an honest gap beats a confident invention, because these files get used to make compliance decisions.

8. **The repo was public, and nobody had noticed.** `gh repo view` reported PUBLIC. It contained the owner's brand guide `.docx`, brand identity files, the operator's name, and a named production incident stating that a specific site's domain had been blocked by a named carrier. No credentials, but plenty that did not belong on the open internet. Decision: stay public, scrub hard.
   - `owner-brand/` is now gitignored except its README, and was removed from git history entirely along with the source `.docx`.
   - The carrier-block incident is anonymized in the files, in every historical blob, and in the commit message that named it. The engineering rules it produced are untouched; only the attribution went.
   - Workflow docs no longer hardcode brand surface names. `MODE-INTERNAL.md` reads them from `owner-brand/profile.md` at runtime, which is better architecture regardless of privacy.
   - `LICENSE` added (MIT) with explicit carve-outs for the verbatim third-party material in `guides/`, for brand identity, and a not-legal-advice notice for `legal/`.
   - History was rewritten with `git-filter-repo` and force-pushed. A full backup bundle sits at `C:	mp\design-system-pre-scrub-backup.bundle` and the pre-scrub tip is on the `backup-pre-scrub` branch.

**Standing lesson from the scrub:** check repo visibility before writing anything into a repo, not after. Every incident write-up, client name, and brand asset that went in was written on the assumption of privacy that was never verified. The habit worth keeping is that the *first* question about any repo is who can read it.

**Residual exposure the owner should know about:** the git author email appears in every commit and cannot be removed without rewriting authorship on all 43 commits. It is the same address attached to the public GitHub account, so it is already public. Left alone deliberately. Separately, the brand guide was publicly readable from May to July 2026, so anything already cloned or indexed in that window is outside this repo's control.

**Next:**
- First real project end to end, exercising the legal gate for the first time
- Six-month review cadence on `legal/laws/`, with `us-state-privacy-laws.md` the fastest to go stale
- Resolve the `UNVERIFIED:` markers in the legal files as sources become confirmable