# BUGS.md: Persistent Bug Log

> Survives across sessions so a fresh-context agent knows what is already known-broken.
> Read the Index block first. Only open a detail block when you need that specific bug.

<!-- INDEX START -->

| ID | Status | Summary |
|----|--------|---------|
| BUG-001 | RESOLVED | Analyzer `take_screenshot` `format: "jpeg"` arg silently overrode `.png` output paths |
| BUG-002 | RESOLVED | Motion observation invalid on machines with `prefers-reduced-motion: reduce` set |
| BUG-003 | RESOLVED | Experience-style sites scored against scrolling-document rubric, producing wrong analysis |
| BUG-004 | RESOLVED | `devneural.jsonc` `localPath` stale after repo move to `C:\dev\Projects\design-system` |
| BUG-005 | RESOLVED | Muted-text token lifted from reference failed WCAG 4.5:1 on dark app canvas |
| BUG-006 | RESOLVED | Node `child_process` calls without `windowsHide: true` flashed console windows on Windows |
| BUG-007 | OPEN | 444 em/en dashes across 29 markdown files violate the standing no-em-dash rule |

<!-- INDEX END -->

<!-- DETAILS START -->

## BUG-001: Analyzer screenshot format arg overrides path extension

**Status:** RESOLVED
**Found:** 2026-05-03
**Fixed:** 2026-05-03
**Area:** `analyzer/extract-prompt.md` Step 2

Chrome DevTools MCP `take_screenshot` was called with `format: "jpeg"` and a `quality` arg. The format arg overrides the file extension in the output path, so files written to `*.png` paths were actually JPEG data. Surfaced during the 2026-05-03 smoke test against rcarecords.com / curious.co / flyhyer.com.

**Fix:** Step 2 now calls `take_screenshot` with no `format` or `quality` args. Landed in commit `f4c9d6f`.

---

## BUG-002: Motion analysis invalid under reduced-motion

**Status:** RESOLVED
**Found:** 2026-05-03
**Fixed:** 2026-05-03
**Area:** `analyzer/extract-prompt.md` Step 7

Test machines commonly have `prefers-reduced-motion: reduce` set at the OS level. Reference sites that respect the media query then present as having zero motion, and the analyzer recorded "no motion" for sites that animate heavily. Silent wrong answer, not an error.

**Fix:** Step 7 now forces `prefers-reduced-motion: no-preference` before observing motion. Landed in commit `f4c9d6f`.

---

## BUG-003: Wrong rubric applied to experience-style sites

**Status:** RESOLVED
**Found:** 2026-05-03
**Fixed:** 2026-05-03
**Area:** `analyzer/extract-prompt.md` Step 6

curious.co/about is a sparse, non-scrolling experience page. Scored against the scrolling-document rubric it read as "thin" and looked like a tooling failure, when it was correct output for a different page archetype.

**Fix:** Step 6 forks into **scrolling-document** vs **experience-style** rubric based on `docHeight > viewport * 1.5`. Landed in commit `f4c9d6f`.

---

## BUG-004: Stale devneural localPath after repo move

**Status:** RESOLVED
**Found:** 2026 (bootstrap era)
**Fixed:** commit `df06188`
**Area:** `devneural.jsonc`

`localPath` still pointed at the pre-move location after the repo was relocated to `C:\dev\Projects\design-system`, so the DevNeural graph resolved this node to a nonexistent directory.

**Fix:** Corrected `localPath`. Metadata only, no workflow impact.

---

## BUG-005: Muted-text token failed contrast gate on dark canvas

**Status:** RESOLVED
**Found:** 2026-05-03
**Fixed:** 2026-05-03
**Area:** design output (DevNeural Hub p3.4 design pass), codified as ANTI-SLOP rule 25

Linear's `oklch(62% 0.012 258)` muted color was lifted 1:1 into an app shell. Lighthouse caught four `text-txt3` instances at 3.1-3.2:1 against `oklch(11.5%)` background, below the 4.5:1 WCAG AA floor. The reference reads fine because marketing sites do not gate on WCAG and use larger body text; the app shell does gate and uses 11-13px labels.

**Fix:** Token bumped to `oklch(70% 0.014 258)`. Codified as ANTI-SLOP rule 25 with explicit lightness floors. Caught only because the gate ran, so the durable fix is the rule, not the token.

---

## BUG-006: Console window flashes from unhidden child processes

**Status:** RESOLVED
**Found:** 2026 (DevNeural dashboard)
**Fixed:** commit `2215ae3` (codified as ANTI-SLOP rule 26)
**Area:** runtime hygiene, Node `child_process` on Windows

DevNeural dashboard polling spawned `powershell -NoProfile ...` every 4 seconds (`system-metrics.ts` drive enumeration) and `execSync` per monitored service every 8 seconds (`services.ts`), neither passing `windowsHide: true`. With the dashboard tab open the user saw roughly 15 PowerShell window flashes per minute while idle. Took multiple wrong diagnoses (blamed unrelated plugins) before the real cause was found.

**Fix:** ANTI-SLOP rule 26 requires `windowsHide: true` on every `spawn` / `spawnSync` / `execSync` / `exec` call, plus `-WindowStyle Hidden -NonInteractive` for scheduled tasks and a `wscript.exe` + VBS shim where a parent harness controls the spawn.

---

## BUG-007 - Repo-wide em dash violations

**Status:** OPEN
**Found:** 2026-07-20
**Area:** 29 markdown files across the repo

The global standing rule bans em dashes and en dashes in every produced artifact with no exceptions, explicitly including config files, YAML content, and string literals. A sweep found **444 occurrences across 29 files**.

Worst offenders: `references/INDEX.md` (52), `PROCESS.md` (47), `APP-ADAPTATION.md` (44), `HANDOVER.md` (43), `analyzer/extract-prompt.md` (34), `skill/SKILL.md` (31, including the YAML `description` field that Claude Code reads on every session).

Found during the `anti-ai-writing` skill build, which lists em dash overuse as an AI tell. This is the substrate the design system reads from, so the violations propagate into generated work.

**Fix:** not yet applied. Needs a mechanical pass replacing each with a context-appropriate colon, comma, parenthesis, or hyphen. Blind replacement to hyphen is safe but degrades some headings; a per-file pass reads better. Deferred from the skill-build commit so the diff stays reviewable.

<!-- DETAILS END -->

## How to use this file

- **New bug:** next `BUG-NNN` id, one Index row plus one detail entry. `Found` = today, absolute date. `Status: OPEN`.
- **Status change:** flip it in **both** the Index row and the detail block. They must always agree.
- **Statuses:** `OPEN` (confirmed, not fixed) → `SMOKE-TESTING` (fix applied, verifying) → `RESOLVED` (fixed and verified). `DEFERRED` for a real bug intentionally parked.
- Never delete rows. History stays.
