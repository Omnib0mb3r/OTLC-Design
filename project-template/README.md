# project-template/

> Documentation only. No scaffold is stored here. Each subfolder records the canonical scaffold command the `OTLC-Design` skill runs on demand for that stack.

Nothing in this folder is copied into a client project. Keeping the scaffolds out of the repo avoids carrying stale dependencies, and `npm create ...` always produces the current version. Whether this folder should ever ship concrete starter scaffolds is still an open question in `OTLC-Brainstorm.MD`.

## Variants

| Folder | Stack | Scaffold command | When to use |
|--------|-------|------------------|-------------|
| [`vanilla-vite/`](vanilla-vite/) | Plain HTML/CSS/JS + Vite | `npm create vite@latest -- --template vanilla` (or `vanilla-ts`) | Default for one-pagers and simple multi-page marketing |
| [`astro/`](astro/) | Astro | `npm create astro@latest` | Content sites with 5+ pages, blogs, case studies |

Stack picking guide: [`../STACK-DECISIONS.md`](../STACK-DECISIONS.md)

## Usage

When the `OTLC-Design` skill creates a new client project at `C:\dev\Projects\[client-name]\`:

1. Skill picks stack per `STACK-DECISIONS.md` (PROCESS.md Step 3, item 5)
2. Skill runs the canonical `npm create ...` command for that stack
3. Writes `BRIEF.md`, `tokens.css` (from Step 3 synthesis), `references/` folder
4. Begins build per Step 4

The skill does not read this folder at runtime. It exists so the scaffold command for each stack is written down in one place and stays reviewable.

## What does NOT go in here

- Client-specific code (lives in `C:\dev\Projects\[client]\`)
- Tokens (synthesized per project, not templated)
- Reference analyses (also per-project)
- Anything stack-specific that varies by major version (let the official scaffolders handle freshness)

## Maintenance

The only upkeep is checking that the scaffold commands in the table above are still the ones the official tools publish. If a concrete scaffold ever does land here, keep it at "blank canvas with token wiring", not "feature-complete starter". The system's value is in the methodology and references, not in heavy boilerplate.
