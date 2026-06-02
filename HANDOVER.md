# HANDOVER.md — Current State

> Snapshot of what is set up, what is verified, what is pending. Update this whenever the system state changes meaningfully.

**Last updated:** 2026-06-02
**Set up by:** Initial bootstrap session
**Smoke tested:** 2026-05-03 against rcarecords.com, curious.co/about, flyhyer.com — **PASS**, with five substrate fixes applied to [`analyzer/extract-prompt.md`](analyzer/extract-prompt.md). Outputs at `C:\tmp\design-system-smoke\` (kept ~1 week as regression baseline; see `SMOKE-TEST-RESULTS.md` there).

---

## ✅ What is set up

### Repo structure (this repo, `C:\dev\Projects\design-system\`)

#### Core methodology
- [x] [`README.md`](README.md) — what the system is and how it is used
- [x] [`CLAUDE.md`](CLAUDE.md) — repo-specific Claude behavior rules
- [x] [`INIT.md`](INIT.md) — fresh-session entry point (read first when opening this repo)
- [x] [`HANDOVER.md`](HANDOVER.md) — this file
- [x] [`OTLC-Brainstorm.MD`](OTLC-Brainstorm.MD) — vision, architecture, decisions, open questions, session log
- [x] [`WORKFLOW.md`](WORKFLOW.md) — inherited from dev-template, kept as-is
- [x] [`PROCESS.md`](PROCESS.md) v1.2 — the 6-step workflow with branch question, hard-enforced post-mortem
- [x] [`ANTI-SLOP.md`](ANTI-SLOP.md) — 26 universal rules (growable)
- [x] [`STACK-DECISIONS.md`](STACK-DECISIONS.md) — plain HTML / Astro / Next / native decision tree
- [x] [`MODE-INTERNAL.md`](MODE-INTERNAL.md) — adaptation for owned/internal work
- [x] [`APP-ADAPTATION.md`](APP-ADAPTATION.md) — adaptation for app/product UI (with customer-app tightening subsection)
- [x] [`devneural.jsonc`](devneural.jsonc) — populated with real metadata
- [x] [`.gitignore`](.gitignore) — extended for Claude/IDE caches and project-template scratch

#### Substrate folders
- [x] [`references/INDEX.md`](references/INDEX.md) — pre-seeded with ~40 curated sites (marketing + app + galleries)
- [x] [`tokens/`](tokens/) — type-scales, color-systems, spacing, motion templates
- [x] [`patterns/`](patterns/) — subdivided into `marketing/` and `app/` (both empty by design; grow from real work)
- [x] [`analyzer/`](analyzer/) — extract-prompt and extraction procedure
- [x] [`project-template/`](project-template/) — vanilla-vite and astro placeholders

#### Owner-brand
- [x] [`owner-brand/source/MichaelCollins_BrandGuide.docx`](owner-brand/source/MichaelCollins_BrandGuide.docx) — source of truth for owner brand
- [x] [`owner-brand/profile.md`](owner-brand/profile.md) — index of brand surfaces
- [x] [`owner-brand/voice.md`](owner-brand/voice.md) — universal voice DOs/DON'Ts
- [x] [`owner-brand/brands/personal-site.md`](owner-brand/brands/personal-site.md) — Solutions Wizard / cyan brand
- [x] [`owner-brand/brands/mhw.md`](owner-brand/brands/mhw.md) — Material Handling Weekly / navy + gold brand
- [x] [`owner-brand/tokens/personal-site.css`](owner-brand/tokens/personal-site.css) — drop-in CSS tokens
- [x] [`owner-brand/tokens/mhw.css`](owner-brand/tokens/mhw.css) — drop-in CSS tokens

### Skill (canonical source: [`skill/SKILL.md`](skill/SKILL.md) in this repo)

- [x] [`skill/SKILL.md`](skill/SKILL.md) — entry point. Asks the 4-way branch question. Reads from this repo as substrate. Hard-enforces post-mortem.
- [x] **Now git-tracked in-repo.** `C:\Users\michael\.claude\skills\OTLC-Design` is a **directory junction** to `skill/` so Claude Code loads it while git versions it. No vendored copy, no drift. Recreate the junction per [`skill/README.md`](skill/README.md).
- [x] Registered as `OTLC-Design` (visible in available-skills list)
- [x] Invoked by `/OTLC-Design`, `/design`, or natural language ("let's build a site for X", "build an app for Y", "internal tool", etc.)

### MCP servers (user scope, available everywhere)

- [x] `chrome-devtools` — installed, connected ✓
- [x] `playwright` — installed, connected ✓
- [x] `context7` — installed, connected ✓

### Git

- [x] Repo initialized (inherited from dev-template clone)
- [x] dev-template origin removed; standalone repo
- [x] All bootstrap work committed in topical commits
- [ ] Remote not yet configured. To add: `gh repo create OTLC-Design --private --source=. --remote=origin --push`

---

## 🔁 The closing loop (this is what makes the system better)

**The point of this entire system is that every project makes the next one start higher.** That only happens if Step 6 post-mortem is actually walked. The skill **hard-enforces** this — you cannot exit a project as complete without writing `POSTMORTEM.md` with substantive answers to all questions.

### How a project closes

1. You signal done with one of: `we're done`, `ship it`, `client approved`, `post-mortem`, `let's wrap up`, `/done`, `/postmortem`
2. The skill enters **post-mortem enforcement mode**
3. The skill walks 5 universal questions (or 6 if internal mode), one at a time
4. For each question, you must give either:
   - **A concrete addition** ("Yes, add rule: never X"; "Yes, lift this hero pattern"; "Yes, add this site to references") — Claude writes the addition AND commits it to this repo with a topical message
   - **An explicit skip with reason** ("Intentionally nothing this round, because [reason]") — logged in the project's `POSTMORTEM.md`
5. Non-answers ("nah", "skip", "we're good", silence) are **rejected**. The skill re-asks. The skill does not advance until satisfied.
6. After all questions answered, the skill writes `[client-project]/POSTMORTEM.md` with the date, every question, every answer, and links to commits made in this repo as a result.
7. Only then is the project marked complete.

### The 5 universal post-mortem questions

1. **New ANTI-SLOP rule?** Did anything ship that felt generic, default, or templated?
2. **New pattern for `patterns/`?** Did we build a structural move you'd reach for again?
3. **New reference for `references/INDEX.md`?** Did we encounter a site worth keeping?
4. **Did `PROCESS.md` drag or lack a step?**
5. **Did the skill itself need refinement?** Wrong tone, wrong order, missing checkpoints?

### Internal-mode 6th question

6. **Did anything from this project deserve to go into your owner-brand profile?** New brand surface? New token? New voice rule? New design rule for the brand guide?

### What gets committed where

| Addition type | Goes to | Commit message convention |
|---------------|---------|---------------------------|
| Anti-slop rule | `ANTI-SLOP.md` | `anti-slop: <short rule summary>` |
| Pattern (marketing) | `patterns/marketing/[name].md` | `patterns: add marketing/<name>` |
| Pattern (app) | `patterns/app/[name].md` | `patterns: add app/<name>` |
| Reference | `references/INDEX.md` (+ optional deep analysis at `references/[slug].md`) | `references: add <domain>` |
| Process change | `PROCESS.md` (bump version) | `process: <what changed>` |
| Skill change | `skill/SKILL.md` (in-repo canonical; `~/.claude/skills/OTLC-Design` junction loads it live) | `skill: <what changed>` |
| Owner-brand change | `owner-brand/source/MichaelCollins_BrandGuide.docx` + derived markdown | `owner-brand: <what changed>` |

### Why hard enforcement matters

Without the gate, post-mortems get skipped when you're tired and the project is shipped. "We're good, nothing came up." Then the system stays static and every project starts from the same baseline. The gate is annoying-on-purpose — it forces the 30 seconds of reflection that grows the system.

---

## ✅ Smoke test — PASSED 2026-05-03

Run against rcarecords.com, curious.co/about, flyhyer.com. All five HANDOVER checks passed:

- Chrome DevTools MCP navigated each URL
- Type system extracted with real computed values (curious.co thin by design — sparse semantic HTML — not a tooling failure)
- Colors converted to OKLCH cleanly via embedded sRGB → linear → OKLab → OKLCH math
- Screenshots captured at 4 breakpoints (375 / 768 / 1280 / 1920) as PNG full-page
- Output written using the `extract-prompt.md` schema (one schema flex on curious.co, now codified as the experience-style rubric)

**Substrate fixes applied to [`analyzer/extract-prompt.md`](analyzer/extract-prompt.md):**

1. Step 2 — call `take_screenshot` without `format`/`quality` args (the `format: "jpeg"` arg overrides `.png` paths)
2. Step 6 — fork into **scrolling-document** vs **experience-style** rubric based on `docHeight > viewport * 1.5`
3. Step 7 — force `prefers-reduced-motion: no-preference` before observing motion (test machines often have reduced-motion on)
4. New **Canonical extractor** section — paste-in JS that returns one JSON blob covering Steps 3-6 + Step 8 programmatic signals; do not reimplement OKLCH math per session
5. Step 8 — programmatic checks (`document.fonts`, `cursor: none`, `::selection`, framework class-name patterns, sub-pixel font sizes) promoted ahead of visual hunting

Smoke-test outputs kept at `C:\tmp\design-system-smoke\` for ~1 week as regression baseline. See `SMOKE-TEST-RESULTS.md` there for full details.

---

## ⏳ What is pending — first real project

Run a real project end-to-end. The first one will surface gaps in:

- `PROCESS.md` step coverage
- `ANTI-SLOP.md` rule completeness
- `analyzer/extract-prompt.md` schema fields
- `tokens/` template usefulness
- `STACK-DECISIONS.md` decision tree edge cases
- `SKILL.md` workflow phrasing
- `MODE-INTERNAL.md` and `APP-ADAPTATION.md` correctness in real use
- `owner-brand/` profile coverage

Capture all gaps in the Step 6 post-mortem. The system's first 5 real projects will dramatically refine it.

### Optional improvements (not blocking)

- [ ] Set up GitHub remote (`gh repo create`)
- [ ] Decide whether `project-template/` should ship with concrete starter scaffolds (currently empty by design)
- [ ] Consider Firecrawl MCP as fallback for JS-heavy reference sites (not currently installed)
- [ ] Build the first 1-2 patterns into `patterns/` once they emerge from real work

---

## 🔧 Verification commands

Run these to confirm setup is intact:

### MCP health

```bash
claude mcp list
```

Expected: `chrome-devtools`, `playwright`, `context7` all show ✓ Connected.

### Skill registration

```powershell
# Confirm the junction resolves to the in-repo canonical source
Get-Item C:\Users\michael\.claude\skills\OTLC-Design | Select-Object LinkType,Target
ls C:\Users\michael\.claude\skills\OTLC-Design\SKILL.md
```

Expected: `LinkType` = `Junction`, `Target` = `C:\dev\Projects\design-system\skill`, and `SKILL.md` resolves through it. If the junction is missing, recreate it per [`skill/README.md`](skill/README.md).

### Repo state

```bash
cd C:\dev\Projects\design-system
git log --oneline
git status
```

Expected: clean working tree, multiple bootstrap commits.

---

## 📝 If something is broken

| Symptom | Fix |
|---------|-----|
| MCP `chrome-devtools` missing | `claude mcp add --scope user chrome-devtools -- npx -y chrome-devtools-mcp@latest` |
| MCP `playwright` missing | `claude mcp add --scope user playwright -- npx -y @playwright/mcp@latest` |
| MCP `context7` missing | `claude mcp add --scope user context7 -- npx -y @upstash/context7-mcp` |
| Skill not triggering | Check the `~/.claude/skills/OTLC-Design` junction resolves to `skill/` (`Get-Item ... \| Select LinkType,Target`); recreate per [`skill/README.md`](skill/README.md) if missing; restart Claude session |
| Repo missing files | This file lists everything that should exist; restore from git history if needed |
| Brand-guide markdown out of sync with .docx | Re-extract from `owner-brand/source/MichaelCollins_BrandGuide.docx` and update derived markdown files |

---

## 📅 How to update this file

Update `Last updated` and the relevant section whenever:

- A new substrate file is added (process step / anti-slop rule additions don't count individually; major file additions do)
- An MCP is added or removed
- A new known issue is identified
- A smoke test or first project completes
- The closing-loop conventions change

Commit with message: `handover: [what changed]`.
