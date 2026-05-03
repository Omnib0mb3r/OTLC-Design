# project-template/

> Starter scaffolds for new client projects. Copied out (not built in place) when starting a new client website.

This folder contains minimal placeholder scaffolds. The current decision (logged in `OTLC-Brainstorm.MD` Open Questions) is to keep these light and prefer running `npm create vite@latest` / `npm create astro@latest` on demand for the freshest scaffolding.

## Variants

| Folder | Stack | When to use |
|--------|-------|-------------|
| [`vanilla-vite/`](vanilla-vite/) | Plain HTML/CSS/JS + Vite | Default for one-pagers and simple multi-page marketing |
| [`astro/`](astro/) | Astro | Content sites with 5+ pages, blogs, case studies |

Stack picking guide: [`../STACK-DECISIONS.md`](../STACK-DECISIONS.md)

## Usage

When the `design-website` skill creates a new client project at `C:\dev\Projects\[client-name]\`:

1. Skill picks stack per `STACK-DECISIONS.md`
2. Skill either:
   - Copies the matching variant from this folder (fast, deterministic), or
   - Runs the canonical `npm create ...` command (latest scaffolding)
3. Writes `BRIEF.md`, `tokens.css` (from Step 3 synthesis), `references/` folder
4. Begins build per Step 4

## What does NOT go in here

- Client-specific code (lives in `C:\dev\Projects\[client]\`)
- Tokens (synthesized per project, not templated)
- Reference analyses (also per-project)
- Anything stack-specific that varies by major version (let the official scaffolders handle freshness)

## Maintenance

These scaffolds are intentionally minimal. Keep them at "blank canvas with token wiring", not "feature-complete starter". The system's value is in the methodology and references, not in heavy boilerplate.
