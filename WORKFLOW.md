# WORKFLOW.md: maintaining the design-system repo

This is the human-readable guide to working *on* this repo. It is not the client-project workflow: that lives in [`PROCESS.md`](PROCESS.md), which is canonical for the 6 build steps. [`CLAUDE.md`](CLAUDE.md) is the machine-readable authority when this repo is the working directory. Where this file and CLAUDE.md ever disagree, CLAUDE.md wins.

## Two ways this repo gets used

| You are | Working directory | What happens |
|---------|-------------------|--------------|
| Maintaining the system | `C:\dev\Projects\design-system\` | You add references, patterns, rules, guides, or process changes. This file applies. |
| Building a client site or app | `C:\dev\Projects\[client]\` | You invoke the `OTLC-Design` skill. It reads this repo as its knowledge base. [`PROCESS.md`](PROCESS.md) applies. |

You do not build client work in this repo. Nothing here deploys or runs a server.

## Session start

If the first message is anything more than a trivial question, read in order:

1. [`INIT.md`](INIT.md) for the fresh-session entry point
2. [`HANDOVER.md`](HANDOVER.md) for what is set up and what is pending
3. [`PROCESS.md`](PROCESS.md) for the 6-step workflow the skill enforces
4. [`ANTI-SLOP.md`](ANTI-SLOP.md) for the durable visual rules
5. [`STACK-DECISIONS.md`](STACK-DECISIONS.md) for stack selection

Then scan the index block in [`BUGS.md`](BUGS.md) for OPEN or SMOKE-TESTING entries touching whatever you are about to change.

## The two skills

Both skills are sourced from inside this repo and loaded through a Windows directory junction, so the git-tracked file is the one Claude Code reads:

| Skill | Source in repo | Junction |
|-------|----------------|----------|
| `OTLC-Design` | [`skill/`](skill/) | `~/.claude/skills/OTLC-Design` |
| `anti-ai-writing` | [`skill-writing/`](skill-writing/) | `~/.claude/skills/anti-ai-writing` |

Because both `SKILL.md` files resolve relative paths against `~/.claude/skills/`, every repo file they reference must be written as an absolute path starting `C:\dev\Projects\design-system\`. Relative links inside the other repo docs are fine.

## The maintenance loop

The repo grows from finished projects, not from speculation. Step 6 of [`PROCESS.md`](PROCESS.md) hard-gates every project on a post-mortem: 6 universal questions, plus a 7th about the owner-brand profile on internal-mode work only. Whatever those answers produce gets committed back here.

| Addition type | Goes to | Commit message |
|---------------|---------|----------------|
| Anti-slop rule | `ANTI-SLOP.md` | `anti-slop: <short rule summary>` |
| Pattern (marketing) | `patterns/marketing/[name].md` | `patterns: add marketing/<name>` |
| Pattern (app) | `patterns/app/[name].md` | `patterns: add app/<name>` |
| Reference | `references/INDEX.md` (+ optional deep analysis at `references/[slug].md`) | `references: add <domain>` |
| Process change | `PROCESS.md` (bump the version line) | `process: <what changed>` |
| Stack decision | `STACK-DECISIONS.md` | `stack: <what changed>` |
| Skill change (OTLC-Design) | `skill/SKILL.md` | `skill: <what changed>` |
| Prose rule (anti-ai-writing) | `skill-writing/SKILL.md` + `skill-writing/references/tells.md` | `skill-writing: <what changed>` |
| Owner-brand change | `owner-brand/source/<BrandGuide>.docx` + derived markdown | `owner-brand: <what changed>` |
| Handover update | `HANDOVER.md` | `handover: <what changed>` |

Commits stay small and topical: one addition, one commit. Never amend, never force-push. The remote is `https://github.com/Omnib0mb3r/OTLC-Design` (private); push after each work session.

`patterns/` is subdivided into `marketing/` and `app/`. Patterns land only after a real project earns them: `app/` currently holds one (`two-band-type-scale.md`), `marketing/` is still empty.

## Anti-slop applies here too

Sample code, token examples, and pattern sketches written in this repo follow [`ANTI-SLOP.md`](ANTI-SLOP.md). Prose written here follows the `anti-ai-writing` skill. Do not seed slop into the system built to prevent it.

## Changing the system itself

For a structural change (reworking the process, adding a subsystem), run the brainstorm pipeline:

1. Read [`OTLC-Brainstorm.MD`](OTLC-Brainstorm.MD) for Vision, Architecture, prior Decisions, Open Questions
2. Run `superpowers:brainstorming`
3. Flow into `superpowers:writing-plans`, then `superpowers:subagent-driven-development`
4. Append to Decisions Made and the Session Log in `OTLC-Brainstorm.MD`

For routine additions (a reference, a pattern, a rule), skip the pipeline and just do the work.

## devneural.jsonc

[`devneural.jsonc`](devneural.jsonc) registers this repo in the DevNeural graph. It is metadata only and has no effect on the skill workflow or on anything in this file.
