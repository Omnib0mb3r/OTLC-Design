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
| BUG-007 | RESOLVED | 496 em/en dashes across 37 files cleared; `guides/` verbatim external content explicitly exempt |
| BUG-008 | RESOLVED | All three required MCP servers vanished from user scope; HANDOVER claimed them connected |
| BUG-009 | RESOLVED | Page shipped as ~73% inline JS tripped a carrier reputation filter and blocked the live domain |
| BUG-010 | RESOLVED | Cloudflare migration left dead email-decoder script: emails rendered broken and the 404 tripped scanners |
| BUG-011 | RESOLVED | Emoji used as iconography on omnibomber-site, no brand control and inconsistent cross-platform rendering |
| BUG-012 | RESOLVED | Label text at 8-9.6px on omnibomber-site, below the 12px legibility floor |

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

## BUG-007: Repo-wide em dash violations

**Status:** RESOLVED
**Found:** 2026-05-03
**Fixed:** 2026-07-20
**Area:** all text files across the repo, not markdown only

The global standing rule bans em dashes and en dashes in every produced artifact with no exceptions, explicitly including config files, YAML content, and string literals. A scripted recount at commit `506265f` (2026-07-20) found **496 occurrences across 37 files**: 492 em dashes (U+2014) and 4 en dashes (U+2013). Untracked files carry none.

Split by file type:

- Markdown: 491 across 34 files.
- Non-markdown: 5 across 3 files. `devneural.jsonc` (3, in comments), `owner-brand/tokens/personal-site.css` (1), `owner-brand/tokens/mhw.css` (1). These fall inside the rule because it covers config and string literals, and an earlier framing of this bug as markdown-only wrongly excluded them.

Worst offenders: `references/INDEX.md` (52), `HANDOVER.md` (49), `PROCESS.md` (47), `APP-ADAPTATION.md` (45), `analyzer/extract-prompt.md` (35), `skill/SKILL.md` (32, including the YAML `description` field that Claude Code reads on every session).

The 4 en dashes sit in `ANTI-SLOP.md` (1, inside the rule 22 example), `guides/seo-crawlability.md` (1), and `guides/seo-how-to.md` (2). The two guides files store external material verbatim, so decide explicitly whether re-pulled guides are exempt; otherwise this count drifts upward on every re-pull.

The violation was first identified and partly fixed on 2026-05-03 by commit `89a9b93` ("readme: rewrite for cohesion, surface done signals, kill em dashes"), which took `README.md` from 6 to 0 and left the rest of the repo untouched. It resurfaced during the `anti-ai-writing` skill build, which lists em dash overuse as an AI tell. So this is a partially applied fix, not a fresh discovery. This is the substrate the design system reads from, so the violations propagate into generated work.

**Fix:** RESOLVED 2026-07-20. A per-file remediation pass ran one agent per file, replacing each dash with a context-appropriate colon, comma, parenthesis, or hyphen rather than blind-substituting a hyphen, then a second agent verified each file by codepoint. A scripted recount now reports **0 dashes in every repo-authored file**, down from 496.

**Explicit exemption, decided 2026-07-20:** the seven files under `guides/` are stored verbatim from external authors and carry a "do not edit the bodies, re-pull from the source" header. They keep their 19 dashes. Editing them would break the verbatim contract and the provenance claim, and the dashes are the original authors' punctuation, not ours. The rule governs what this repo *produces*, not what it *quotes*. `guides/INDEX.md`, which is repo-authored, is held to the rule and is clean.

The recount is scripted, not hand-tallied, so the figures cannot drift again:

```bash
python -c "
import io,glob
t=0
for p in glob.glob('**/*.md',recursive=True)+glob.glob('**/*.jsonc',recursive=True)+glob.glob('**/*.css',recursive=True):
    if p.startswith('guides') and not p.endswith('INDEX.md'): continue
    s=io.open(p,encoding='utf-8').read(); n=s.count(chr(0x2014))+s.count(chr(0x2013))
    if n: print(n,p); t+=n
print('TOTAL:',t)"
```

---

## BUG-008: Required MCP servers missing from user scope

**Status:** RESOLVED
**Found:** 2026-07-20
**Fixed:** 2026-07-20
**Area:** environment (user-scope MCP config in `~/.claude.json`), HANDOVER.md accuracy

`claude mcp list` returned none of the three MCPs the system depends on (`chrome-devtools` for Step 2 analysis, `playwright` for Step 5 verification, `context7` for Steps 3-4 docs). `~/.claude.json` user-scope `mcpServers` was empty. HANDOVER.md still claimed all three installed and connected, so a fresh session would have discovered the breakage mid-project at Step 2, not at setup. Cause unknown; likely lost in a config reset or Claude Code update since the 2026-06-02 handover.

**Fix:** Reinstalled all three per HANDOVER's own "If something is broken" table (`claude mcp add --scope user ...`). Verified: all three report Connected. Lesson: HANDOVER's verification commands are worth actually running at session start; the doc asserting state is not the state.

---

## BUG-009: Inline-JS page tripped a carrier reputation filter and blocked the live domain

**Status:** RESOLVED
**Found:** 2026-07 (live production site)
**Fixed:** commit `86821b0` (codified in STACK-DECISIONS "Shipping hygiene (reputation-safe)")
**Area:** shipping hygiene, delivered page structure

A page shipped as roughly 73% one inline `<script>` blob, a JS engine plus a large dataset inlined into the HTML. A major mobile carrier reputation filter flagged and blocked the whole domain. Google Safe Browsing and Norton stayed clean the entire time, so it was a heuristic category flag rather than a malware detection, which made it hard to diagnose from the usual reputation checkers. A real user was blocked from the live site.

**Fix:** STACK-DECISIONS.md gained a "Shipping hygiene (reputation-safe)" section: keep JS and large data external and content-hash versioned, never inline a large engine or dataset into page HTML (acceptable only for a deliberately offline self-contained artifact), force HTTPS with a loop-safe proxy-aware redirect plus HSTS and the standard security headers, and version data URLs on any shell or data-contract change. A reputation-safe shipping gate plus a returning-user check were added to the skill's Verify step. Durable fix is the rule, not the one page.

---

## BUG-010: Cloudflare migration left a dead email-decoder script

**Status:** RESOLVED
**Found:** 2026-07 (surfaced alongside BUG-009)
**Fixed:** commit `86821b0` (codified in STACK-DECISIONS "Shipping hygiene (reputation-safe)")
**Area:** host migration, delivered page markup

Moving a site off Cloudflare leaves behind `__cf_email__` spans and `/cdn-cgi/l/email-protection#HEX` links whose decoder script is no longer served. Two failures at once: the email addresses render as broken obfuscated text for every visitor, and the 404 on the decoder script trips security scanners, which compounds the reputation problem in BUG-009.

**Fix:** Decode `data-cfemail` back to real `mailto:` links (first hex byte is the XOR key, remaining bytes are XORed with it) and delete the dead `cdn-cgi/.../email-decode.min.js` reference. Recorded as the Cloudflare-migration gotcha in the STACK-DECISIONS shipping hygiene section so any future migration checks for it.

---

## BUG-011: Emoji used as iconography

**Status:** RESOLVED
**Found:** 2026-05-03
**Fixed:** commit `ccf68a1` (codified as ANTI-SLOP rule 21)
**Area:** design output (omnibomber-site analysis)

The omnibomber-site analysis found emoji standing in for icons across `tool-card-icon`, `lc-icon`, `dl-icon`, and `proj-card-vis .emo`. Emoji glyphs render differently on Apple, Google, Windows, and fallback fonts, cannot be brand-controlled, and read as template filler.

**Fix:** ANTI-SLOP rule 21 bans emoji as iconography outright. Use SVG icons (custom, Lucide, Phosphor, or Heroicons per rule 11), typographic glyphs, or no icon at all.

---

## BUG-012: Label text below the 12px legibility floor

**Status:** RESOLVED
**Found:** 2026-05-03
**Fixed:** commit `ccf68a1` (codified as ANTI-SLOP rule 22)
**Area:** design output (omnibomber-site analysis)

The omnibomber-site analysis found labels set at 8 to 9.6px (`0.5rem` to `0.6rem`). Sub-12px text fails legibility on retina at normal viewing distance, and WCAG 1.4.4 expects users to scale to 200% without loss, which breaks well before that target.

**Fix:** ANTI-SLOP rule 22 sets the floors: body content at 14px or above, labels and supporting text at 12px or above. Smaller is acceptable only for ornamental elements that carry no comprehension load. App UI may run 11-13px labels with appropriate weight and contrast per APP-ADAPTATION rule 22.

<!-- DETAILS END -->

## How to use this file

- **New bug:** next `BUG-NNN` id, one Index row plus one detail entry. `Found` = today, absolute date. `Status: OPEN`.
- **Status change:** flip it in **both** the Index row and the detail block. They must always agree.
- **Statuses:** `OPEN` (confirmed, not fixed) → `SMOKE-TESTING` (fix applied, verifying) → `RESOLVED` (fixed and verified). `DEFERRED` for a real bug intentionally parked.
- Never delete rows. History stays.
