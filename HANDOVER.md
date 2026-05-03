# HANDOVER.md — Current State

> Snapshot of what is set up, what is verified, what is pending. Update this whenever the system state changes meaningfully.

**Last updated:** 2026-05-02
**Set up by:** Initial bootstrap session

---

## ✅ What is set up

### Repo structure (this repo, `C:\dev\design-system\`)

- [x] `README.md` — explains what the system is
- [x] `CLAUDE.md` — repo-specific Claude behavior rules
- [x] `INIT.md` — fresh-session entry point (you should have already read this)
- [x] `HANDOVER.md` — this file
- [x] `OTLC-Brainstorm.MD` — vision, architecture, decisions, open questions, session log
- [x] `WORKFLOW.md` — inherited from dev-template, kept as-is
- [x] `PROCESS.md` — the 6-step workflow (1.0)
- [x] `ANTI-SLOP.md` — 20 starting rules (growable)
- [x] `STACK-DECISIONS.md` — plain HTML / Astro / Next decision tree
- [x] `devneural.jsonc` — populated with real metadata
- [x] `.gitignore` — extended for Claude/IDE caches and project-template scratch
- [x] `references/INDEX.md` — pre-seeded with ~30 curated studio/product/gallery sites
- [x] `tokens/README.md` + `type-scales.md` + `color-systems.md` + `spacing.md` + `motion.md`
- [x] `patterns/README.md` — empty intentionally; grows from real project work
- [x] `analyzer/README.md` + `extract-prompt.md` — reference extraction procedure
- [x] `project-template/README.md` + `vanilla-vite/` + `astro/` placeholders

### Skill (`C:\Users\michael\.claude\skills\design-website\`)

- [x] `SKILL.md` — the entry point Claude invokes; reads from this repo as substrate

### MCP servers (user scope, available everywhere)

- [x] `chrome-devtools` — installed, connected ✓
- [x] `playwright` — installed, connected ✓
- [x] `context7` — installed, connected ✓

### Memory

- [x] User role saved (web designer for clients)
- [x] design-system repo + skill location saved as reference
- [x] Anti-slop rule summary saved as feedback memory

### Git

- [x] Repo initialized (inherited from dev-template clone)
- [x] dev-template origin removed; this is now a fresh standalone repo
- [x] Initial commit created
- [ ] Remote not yet configured. To add: `gh repo create design-system --private --source=. --remote=origin --push`

---

## ⏳ What is pending

### Smoke test (do this in the next session, before any real client work)

In a fresh Claude session opened in `C:\dev\design-system\`, the user will provide 1-3 reference URLs (e.g. linear.app, stripe.com, manual.is). Run the analyzer per `analyzer/extract-prompt.md` against each. Verify:

- Chrome DevTools MCP successfully navigates each URL
- Type system extracted with real computed values
- Colors converted to OKLCH correctly
- Screenshots captured at 4 breakpoints
- Output written using the schema in `extract-prompt.md`

If any of these fail, the workflow needs fixing before a real client project.

### First real client project

After smoke test passes, run a real `design-website` workflow end-to-end on a real client brief. The first project will surface gaps in:

- `PROCESS.md` step coverage
- `ANTI-SLOP.md` rule completeness
- `analyzer/extract-prompt.md` schema fields
- `tokens/` template usefulness
- `STACK-DECISIONS.md` decision tree edge cases
- `SKILL.md` workflow phrasing

Capture findings in the post-mortem (Step 6).

### Optional improvements (not blocking)

- [ ] Set up GitHub remote (`gh repo create`)
- [ ] Decide whether `project-template/` should ship with concrete starter scaffolds or stay empty (currently empty by design)
- [ ] Add `clients/` directory if client-specific design preferences accumulate
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
ls C:\Users\michael\.claude\skills\design-website\SKILL.md
```

Expected: file exists.

### Repo state

```bash
cd C:\dev\design-system
git log --oneline
git status
```

Expected: at least one commit, clean working tree.

---

## 📝 If something is broken

| Symptom | Fix |
|---------|-----|
| MCP `chrome-devtools` missing | `claude mcp add --scope user chrome-devtools -- npx -y chrome-devtools-mcp@latest` |
| MCP `playwright` missing | `claude mcp add --scope user playwright -- npx -y @playwright/mcp@latest` |
| MCP `context7` missing | `claude mcp add --scope user context7 -- npx -y @upstash/context7-mcp` |
| Skill not triggering | Check `C:\Users\michael\.claude\skills\design-website\SKILL.md` exists; restart Claude session |
| Repo missing files | This file lists everything that should exist; restore from git history if needed |

---

## 📅 How to update this file

Update `Last updated` and the relevant section whenever:

- A new substrate file is added (PROCESS step, anti-slop rule additions don't count individually; major file additions do)
- An MCP is added or removed
- Memory entries change
- A new known issue is identified
- A smoke test or first project completes

Commit with message: `handover: [what changed]`.
