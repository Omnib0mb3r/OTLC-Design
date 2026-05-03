# design-system

A repeatable methodology for building **non-slop, professional websites for clients**. The substrate that powers the `design-website` skill.

This repo is not a website. It is the system that produces websites: process, anti-slop rules, reference vault, pattern library, token templates, and analyzer prompts that Claude reads at the start of every client project.

## What lives here

| Path | Purpose |
|------|---------|
| [`PROCESS.md`](PROCESS.md) | The 6-step workflow: Intake → Analyze → Synthesize → Build → Verify → Iterate |
| [`ANTI-SLOP.md`](ANTI-SLOP.md) | Durable rules Claude follows on every project, no reminding required |
| [`STACK-DECISIONS.md`](STACK-DECISIONS.md) | When to use plain HTML / Astro / Next.js. Not "always React". |
| [`references/`](references/) | Curated vault of sites worth studying. Catalog in [`references/INDEX.md`](references/INDEX.md). Grows over time. |
| [`patterns/`](patterns/) | Hand-built layout primitives. Your vocabulary, not shadcn defaults. |
| [`tokens/`](tokens/) | Type scale, color, spacing, motion templates. Synthesized per project, not copied. |
| [`analyzer/`](analyzer/) | The prompts and procedures Claude uses to extract design data from reference URLs via Chrome DevTools MCP. |
| [`project-template/`](project-template/) | Starter scaffolds copied out when a new client project begins. |
| [`INIT.md`](INIT.md) | What a fresh Claude session reads first when this repo is opened. |
| [`HANDOVER.md`](HANDOVER.md) | Live status of the system: what is set up, what is pending. |

## How it is used

You do not work *in* this repo to build client sites. You work in `C:\dev\Projects\[client-name]\`. The `design-website` skill reads from this repo as its knowledge base.

Typical flow:

1. New client project. You run `/design-website` (or just say "let's build a site for X").
2. The skill walks intake, then uses Chrome DevTools MCP to analyze the references you provide.
3. Synthesizes tokens, proposes a stack and structure, gets your sign-off.
4. Builds. Verifies via Playwright MCP. Iterates.
5. Anything genuinely reusable extracted to this repo: a new pattern, a new anti-slop rule, a new reference.

## How it improves

Every client project ends with a 5-minute post-mortem:

- New rule worth adding to `ANTI-SLOP.md`?
- New pattern worth lifting into `patterns/`?
- New reference worth adding to `references/INDEX.md`?
- Did `PROCESS.md` need to change because a step dragged or was missing?

The repo is a flywheel. Each project makes the next one start higher.

## Required tooling

Three Claude Code MCP servers must be installed (user scope):

- **playwright** — multi-browser verification, screenshots, automation
- **chrome-devtools** — reference analysis (computed styles, Lighthouse, perf, network)
- **context7** — current documentation for any library or web spec

See [`HANDOVER.md`](HANDOVER.md) for verification commands.

## Honest scope

This system raises the floor. It does not replace art direction. The last 20% (the part separating "very good" from "Pentagram") still requires your judgment. What this gives you: every project starts at *considered* instead of *Tailwind template*, the slop tells are eliminated systematically, and matching a reference aesthetic gets to ~80% on first pass.
