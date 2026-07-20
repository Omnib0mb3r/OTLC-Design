# skill/ (canonical OTLC-Design skill source)

`SKILL.md` here is the **single source of truth** for the OTLC-Design skill.

Claude Code loads skills from `~/.claude/skills/`. To avoid a second drifting
copy, `~/.claude/skills/OTLC-Design` is a **directory junction** pointing at
this folder. Edits made here are what Claude Code runs; git tracks them.

## Why a junction (not a copy)

The skill already hardcodes `C:\dev\Projects\design-system\` paths (it reads the
substrate from there at runtime). So the skill is already meaningless without
this repo present. A junction adds no new coupling and removes the manual
copy-after-edit step that a vendored copy would require, eliminating drift.

## Recreate the junction (fresh machine / after repo move)

PowerShell, no admin needed on Windows 11:

```powershell
# Remove any existing dir/copy first if present
Remove-Item -LiteralPath "$env:USERPROFILE\.claude\skills\OTLC-Design" -Force -Recurse -ErrorAction SilentlyContinue

New-Item -ItemType Junction `
  -Path "$env:USERPROFILE\.claude\skills\OTLC-Design" `
  -Target "C:\dev\Projects\design-system\skill"
```

Verify:

```powershell
Get-Item "$env:USERPROFILE\.claude\skills\OTLC-Design" | Select-Object Name,LinkType,Target
# LinkType should read: Junction
```

## Editing

Edit `skill/SKILL.md` in this repo. Commit with `skill: <what changed>` per
[`../CLAUDE.md`](../CLAUDE.md). No copy step. The junction means Claude Code
picks up the change immediately.
