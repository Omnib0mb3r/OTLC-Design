# skill-writing/ - canonical anti-ai-writing skill source

`SKILL.md` here is the **single source of truth** for the `anti-ai-writing` skill.

Claude Code loads skills from `~/.claude/skills/`. To avoid a second drifting copy,
`~/.claude/skills/anti-ai-writing` is a **directory junction** pointing at this folder.
Edits made here are what Claude Code runs; git tracks them.

Same pattern as [`../skill/`](../skill/README.md), which hosts `OTLC-Design`.

## What it is

Prose counterpart to [`../ANTI-SLOP.md`](../ANTI-SLOP.md). `ANTI-SLOP.md` stops a page
from looking AI-generated. This skill stops the words on it from reading AI-generated.

Scope is deliberately wider than design work: it applies to commit messages, docs,
emails, PR bodies, release notes, and UI strings across every project, not only to
sites built through `OTLC-Design`.

## Recreate the junction (fresh machine / after repo move)

PowerShell, no admin needed on Windows 11:

```powershell
Remove-Item -LiteralPath "$env:USERPROFILE\.claude\skills\anti-ai-writing" -Force -Recurse -ErrorAction SilentlyContinue

New-Item -ItemType Junction `
  -Path "$env:USERPROFILE\.claude\skills\anti-ai-writing" `
  -Target "C:\dev\Projects\design-system\skill-writing"
```

Verify:

```powershell
Get-Item "$env:USERPROFILE\.claude\skills\anti-ai-writing" | Select-Object Name,LinkType,Target
# LinkType should read: Junction
```

## Layout

```
skill-writing/
  SKILL.md                        entry point, the rules you apply
  README.md                       this file
  references/
    tells.md                      complete taxonomy, verbatim watch-phrase lists
    false-positives.md            ineffective indicators, detection caveats
    model-artifacts.md            per-model fingerprints, citation failure modes
```

`SKILL.md` is the working subset and loads on trigger. The `references/` files load
only when the full taxonomy is needed, so the always-on context cost stays small.

## Adding a source

The skill is source-extensible. To fold in a new source on AI writing tells:

1. Distil each finding into the repo's rule shape: the ban, `**Why:**`, `**How to apply:**`.
2. Add it to the right section of `SKILL.md` (§1 vocabulary, §2 construction, §3 content, §4 formatting).
3. Add the full detail to `references/tells.md`.
4. Append a row to the provenance table at the bottom of `references/tells.md`.
5. If the source describes something that is **not** a reliable tell, it goes in
   `references/false-positives.md`. That file is as important as the tells list.

## Editing

Edit in this repo. Commit with `skill-writing: <what changed>` per [`../CLAUDE.md`](../CLAUDE.md).
No copy step; the junction means Claude Code picks up the change immediately.
