# PROCESS.md — The 6-Step Workflow

> Version 1.3 (2026-07-20)

The methodology the `OTLC-Design` skill enforces on every client project. Each step has explicit inputs, outputs, and a tool dependency. Skipping steps produces slop.

---

## Step 1 — INTAKE

**Goal:** Understand the project well enough that the rest of the workflow has correct constraints.

### 1a. Branch question (always first)

Before any other intake, ask exactly:

> *"What are we building?*
> *1. **Customer site** — marketing/showcase site for an external client*
> *2. **Customer app** — product/app interface for paying customers (B2B SaaS, customer portal, web app)*
> *3. **Internal site** — your own marketing/showcase site (your portfolio, MHW, project landing pages)*
> *4. **Internal app** — your own tools, dashboards, admin panels"*

Based on the answer, load adaptation docs and set context:

| Branch | Adaptations to load | Brand source |
|--------|---------------------|--------------|
| 1. Customer site | (default — none extra) | Discovered from client brief + references |
| 2. Customer app | [`APP-ADAPTATION.md`](APP-ADAPTATION.md) (with customer-app tightening subsection) | Discovered from client brief + references |
| 3. Internal site | [`MODE-INTERNAL.md`](MODE-INTERNAL.md) | Owner-brand profile (ask which: personal-site, MHW, or new) |
| 4. Internal app | [`MODE-INTERNAL.md`](MODE-INTERNAL.md) + [`APP-ADAPTATION.md`](APP-ADAPTATION.md) | Owner-brand profile (ask which) |

State the resolved context in writing before proceeding:

> *"Mode: [internal / external]. Type: [site / app]. Loading: [adaptation docs]. Brand: [source]."*

### 1b. Mode-appropriate intake

Based on the branch answer, ask the appropriate question set:

**Customer site (full intake):**
1. Client name, domain (if known), industry
2. Audience (who visits this site)
3. Project goals — sell something, inform, showcase work, drive contact, convert to signup, etc. Pick 1-2 primary, 0-1 secondary
4. Scope — one-pager, multi-page marketing, blog/content site
5. **1 to 3 reference URLs** the client liked or that match the brief aesthetically
6. Brand constraints — existing logo, mandated colors, mandated fonts, voice/tone
7. Content state — does the client have copy and imagery, or do we generate/source it
8. Deadline / budget signals — affects how aggressive we get
9. Hosting / deploy preference (Vercel, Netlify, Cloudflare, custom, doesn't matter)

**Customer app (extends customer site with app questions per APP-ADAPTATION.md):**
- All of the above, plus the app intake questions in `APP-ADAPTATION.md`
- Plus customer-app tightening questions (mobile required, onboarding model, help architecture, notifications, billing surface, i18n)

**Internal site (per MODE-INTERNAL.md):**
1. Project name (becomes folder name at `C:\dev\Projects\[name]\`)
2. Project goals
3. Scope
4. Optional references (only if you want a deliberate aesthetic deviation from owner-brand)
5. Hosting / deploy preference
6. Brand surface — personal-site, MHW, or new (ask per MODE-INTERNAL.md)

**Internal app (per MODE-INTERNAL.md + APP-ADAPTATION.md):**
- Internal site intake questions, plus the app intake questions

### 1c. Output

`BRIEF.md` in the project root capturing all answers. Include the branch resolution at the top so future-Claude has context.

Project folder location:
- Customer work → `C:\dev\Projects\[client-name]\`
- Internal work → `C:\dev\Projects\[name]\` (no client wrapper)

**Tool:** None. Conversation only.

**Anti-pattern:** Skipping intake because "we have references" or "it's just internal." References define aesthetic; brief defines everything else (structure, copy, scope, hosting). Internal mode skips brand-discovery questions specifically — not the rest of intake.

---

## Step 2 — REFERENCE ANALYSIS

**Goal:** Extract the *aesthetic vocabulary* of each reference site into structured data we can synthesize from.

**Procedure (per reference URL, using Chrome DevTools MCP):**
1. Navigate to the URL.
2. Capture screenshots at 4 breakpoints: 375px, 768px, 1280px, 1920px.
3. Extract the **type system**:
   - Font families used (display, body, mono if present)
   - Computed font-size for h1, h2, h3, body, small
   - Compute the modular ratio (e.g. h1=64, h2=48, h3=36, body=18 → ratio ≈ 1.333)
   - Line heights and letter-spacing
4. Extract the **color palette**:
   - Background, foreground, accent, neutral steps
   - Convert to OKLCH for perceptual reasoning
   - Note any unusual choices (e.g. cream instead of pure white, off-black instead of #000)
5. Extract the **spacing system**:
   - Common gaps between sections, between elements
   - Identify a base unit if one is evident (4, 6, 8, 10, etc.)
6. Extract the **grid / layout primitives**:
   - Max content width
   - Number of columns (if any)
   - Asymmetric or symmetric
   - How the hero is structured (centered? left? full-bleed? overlapping?)
   - How "what we do" sections are structured
7. Extract **motion patterns**:
   - Hover states (subtle? exaggerated?)
   - Scroll-driven (parallax, reveals, sticky, scrub)
   - Page transitions
   - Cursor effects
8. Note **unusual choices** that contribute to non-slop feel:
   - Custom cursor, custom selection color, weird border treatments, marquee text, asymmetric breakouts, mixed type sizes within a line, etc.

**Output:** A markdown file at `[client-project]/references/[domain].md` using the structure documented in [`analyzer/extract-prompt.md`](analyzer/extract-prompt.md).

**Tool:** Chrome DevTools MCP (required).

**Anti-pattern:** Visual inspection only. Always extract computed values. "Looks like a 1.25 scale" is not the same as "computed h1=48, h2=36, h3=27, body=18 → ratio 1.333".

---

## Step 3 — SYNTHESIS

**Goal:** Build a project-specific design token system informed by the references, plus a structural proposal.

**Procedure:**
1. **Type tokens** — pick one display family + one body family + (optionally) one mono. Pick a modular ratio (commonly 1.2 / 1.25 / 1.333 / 1.414 / 1.5 / 1.618 / 2.0). Compute the scale up and down from a base body size.
2. **Color tokens** — author in OKLCH. Build a 9-step neutral ramp, 1-2 accents, semantic tokens (bg, fg, muted, border, accent, accent-fg). Verify WCAG AA contrast (AAA preferred for body).
3. **Spacing tokens** — pick a base unit (commonly 4 or 8). Build a scale.
4. **Radius / shadow / motion tokens** — minimal, opinionated. Sharp + 1 rounded option, or all rounded with one specific value. Motion: 2-3 easing curves and 3-4 duration steps.
5. **Stack pick** — consult [`STACK-DECISIONS.md`](STACK-DECISIONS.md). Default to plain HTML/CSS/JS + Vite for one-pagers, Astro for content sites, Next.js only for genuine apps.
6. **Sitemap** — list the pages (often just one).
7. **Section structure** — for each page, list the sections in order (e.g. "Nav, hero, work selector, single project deep-dive, footer"). Use the structural vocabulary from references, not template defaults.
8. **Operational design** — consume the intake deploy-preference answer (customer Q9 / internal Q5), which is otherwise captured and never used. Decide, before any build, how the thing runs outside the laptop. For **marketing sites** this is a one-line confirmation (static host + any build-time env). For **apps** (customer or internal) this is a real plan per [`APP-ADAPTATION.md`](APP-ADAPTATION.md) §"Operational readiness": where it runs, how config and secrets are provided, how it updates, how it rolls back, and which production failures must be observable. Operational design is part of software design, not an afterthought — deciding it here is the cheapest it will ever be.

**Output:**
- `[client-project]/tokens.css` — CSS custom properties
- `[client-project]/SITEMAP.md` — pages + section structure proposal
- `[client-project]/OPERATIONS.md` (app mode) — deploy target, runtime config + secrets handling, update + rollback path, failure-observability decisions

**Tool:** Context7 MCP for current docs on whatever stack is picked.

**Gate:** **Show this to the user. Do not start building until they confirm.** Synthesis is the cheapest stage to iterate. For apps, the operational plan (`OPERATIONS.md`) is part of what they confirm — a deploy/rollback decision is far cheaper to change now than after the system is built around it.

**Anti-pattern:** Skipping synthesis and going straight from references to coding. Tokens enforce consistency. Without them, the build drifts toward defaults.

---

## Step 4 — BUILD

**Goal:** Implement the site using the synthesized tokens and structure, with [`ANTI-SLOP.md`](ANTI-SLOP.md) enforced automatically.

**Procedure:**
1. Scaffold the project (vanilla Vite, Astro, or Next per Step 3).
2. Wire up `tokens.css` as the foundation. Nothing hardcoded; everything references tokens.
3. Build the structural skeleton (semantic HTML, real grid, no divitis).
4. Write **specific copy** — no lorem, no placeholder. Real names, real numbers, real dates. If client copy is missing, draft it in the client's voice and flag it.
5. Apply type system using the modular scale. No arbitrary sizes.
6. Apply color system using semantic tokens.
7. Implement motion — even subtle. Hover, focus, scroll-into-view at minimum.
8. Add custom touches — at least one element that signals human consideration (custom cursor, custom selection color, unusual layout breakout, mixed-weight inline type, etc.).
9. Cross-check against [`ANTI-SLOP.md`](ANTI-SLOP.md) — for each rule, confirm compliance.

**Output:** Working site in `[client-project]/`.

**Tool:** Context7 MCP throughout for current API references.

**Anti-pattern:** Building first, applying tokens later. Defaults leak in immediately and refactoring them out is harder than starting clean.

---

## Step 5 — VERIFY

**Goal:** Confirm the build meets quality bars before showing the client.

**Procedure (using Playwright MCP and Chrome DevTools MCP):**
1. **Multi-browser screenshots** — Playwright MCP captures the site in Chromium, Firefox, WebKit at 4 breakpoints each.
2. **Lighthouse** — Chrome DevTools MCP runs Lighthouse. Targets:
   - Performance ≥ 90
   - Accessibility ≥ 95
   - Best Practices ≥ 90
   - SEO ≥ 90
3. **Accessibility audit** — axe-core results via Playwright. Zero critical / serious violations.
4. **Token compliance audit** — script (or manual scan) checking that no CSS values exist outside the token system. Hardcoded colors, sizes, spacings → fail.
5. **Reference comparison** — side-by-side the verification screenshots with reference screenshots from Step 2. Does the *aesthetic vocabulary* match? Not pixel match. Vocabulary match: type rhythm, color story, spacing density, motion feel.

**Output:** `[client-project]/VERIFICATION.md` with screenshots, scores, audit results, and a verdict (pass / fail / iterate).

**Tool:** Playwright MCP + Chrome DevTools MCP (both required).

**Gate:** Do not advance to client review without a passing verification report. If failing, iterate within Step 4 until passing.

**Anti-pattern:** "It looks fine" without running the audits. Lighthouse perf <90 means the design *feels* worse than it looks. A11y fails are unprofessional and legally risky.

---

## Step 6 — ITERATE + POST-MORTEM (hard-enforced)

**Goal:** Incorporate user feedback through sign-off, then close the loop with a system-improvement post-mortem. The post-mortem is **hard-enforced** — the project does not complete until all 5 questions have substantive answers.

### Iteration phase

1. Show the user the verification report and a live preview.
2. Capture feedback — be specific (which section, what feeling, what change).
3. Triage feedback:
   - Token-level (font, color, spacing, scale) → edit tokens.css, full-site cascade
   - Structure-level (section order, layout) → edit HTML
   - Copy-level → edit content
   - Motion-level → edit JS / CSS animations
4. Re-run Step 5 verification after each meaningful round of changes.
5. Loop until the user gives a **done signal**.

### Done signals (trigger post-mortem enforcement)

- "we're done"
- "ship it" / "ready to ship"
- "client approved" / "client signed off"
- "post-mortem" / "let's wrap up"
- "/done" or "/postmortem"

When the user gives a done signal, enter **post-mortem enforcement mode**.

### Post-mortem enforcement mode

Walk these 6 questions one at a time. Do not batch them. For each, the user must give either (a) a concrete addition or (b) an explicit "intentionally nothing this round, because [reason]". Non-answers ("nah", "skip", "we're good", silence) get pushed back: *"I need a substantive answer. Either name a concrete addition or give a reason for intentionally skipping. Take 30 seconds."*

1. **New ANTI-SLOP rule?** Did anything ship that felt generic, default, or templated? Did you have to tell Claude to stop doing X mid-project?
2. **New pattern for [`patterns/`](patterns/)?** Did we build a structural move (hero shape, layout primitive, section structure) you would reach for again on a different project?
3. **New reference for [`references/INDEX.md`](references/INDEX.md)?** Did we encounter (or did the user bring) a site worth keeping in the curated vault?
4. **Did `PROCESS.md` drag or lack a step?** Was any step too long, too short, missing, in the wrong order, or asking the wrong questions?
5. **Did the skill itself need refinement?** Was Claude's behavior off — wrong tone, wrong order, missing checkpoints, over-asking, under-asking? Edit the in-repo canonical `skill/SKILL.md` (the `~/.claude/skills/OTLC-Design` junction picks it up live).
6. **New anti-ai-writing rule?** Question 1 covers how the work looked. This one covers how it read. Did any copy ship sounding generated? A phrase you struck, a construction you kept correcting, a tell not yet on the list? Edit [`skill-writing/SKILL.md`](skill-writing/SKILL.md) and [`skill-writing/references/tells.md`](skill-writing/references/tells.md).

### What counts as a substantive answer

| Answer type | Example | What you do |
|-------------|---------|-------------|
| Concrete addition (rule) | "Yes, add: never use scroll-snap on marketing landings unless the design earns it." | Write to [`ANTI-SLOP.md`](ANTI-SLOP.md). Commit `anti-slop: scroll-snap restriction`. Confirm. |
| Concrete addition (pattern) | "Yes, lift the asymmetric hero with right breakout to patterns." | Write `patterns/asymmetric-hero-right-breakout.md`. Commit `patterns: add asymmetric-hero-right-breakout`. Confirm. |
| Concrete addition (reference) | "Yes, add bbb.studio." | Add line to [`references/INDEX.md`](references/INDEX.md). Optionally write full analysis. Commit `references: add bbb.studio`. |
| Concrete addition (process) | "Step 2 should also capture page transition timing." | Edit `PROCESS.md`. Bump version. Commit `process: capture page transition timing in step 2`. |
| Concrete addition (skill) | "You over-asked during intake. Cut question 8." | Edit `SKILL.md`. Commit `skill: trim intake question 8`. |
| Concrete addition (prose rule) | "You kept writing 'purpose-built for'. Ban it." | Add to `skill-writing/SKILL.md` §3 and `references/tells.md`. Commit `skill-writing: ban purpose-built for`. |
| Intentional skip with reason | "Intentionally nothing this round — project was small enough nothing generalized." | Log in client `POSTMORTEM.md`. Move on. |
| Non-answer (REJECT) | "Nah", "skip", silence | Push back. Re-ask. Do not advance. |

### Output — required before completion

Write `[client-project]/POSTMORTEM.md`:

```markdown
# Post-mortem — [client-name]

**Date:** [date]
**Project:** [path to client folder]

## 1. New ANTI-SLOP rule?
[answer]
[link to commit if added]

## 2. New pattern?
[answer]
[link to commit if added]

## 3. New reference?
[answer]
[link to commit if added]

## 4. PROCESS.md change?
[answer]
[link to commit if added]

## 5. Skill change?
[answer]
[link to commit if added]
```

**Tool:** Playwright MCP for ongoing verification during iteration.

**Project complete only when:** `POSTMORTEM.md` exists with substantive answers to all 5 questions, and any improvement commits to the design-system repo are pushed.

**Anti-pattern:** Soft-quitting the post-mortem because the user is tired. The hard gate is the entire point — without it, the system stays static and every project starts from the same baseline.

---

## What this process explicitly does NOT do

- Replace the user's art direction. The system handles structure, prevents slop, accelerates the 80%. The remaining 20% (the difference between "good studio work" and "Pentagram") is the user's judgment.
- Generate brand strategy. If a client lacks a brand, that is upstream work the system does not cover.
- Source photography or illustration. Custom imagery commissioning is out of scope.
- Write long-form copy from nothing. Drafting in the client's voice from a brief is in-scope; full copy strategy is not.
