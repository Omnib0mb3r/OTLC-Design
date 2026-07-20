# MODE-INTERNAL.md: Adaptation for Owned / Internal Work

> Loaded by the `OTLC-Design` skill when the intake branch resolves to **Internal site** or **Internal app**. Adapts intake (skips brand discovery), pulls the owner-brand profile as the brand source, and keeps everything else (anti-slop, verification, post-mortem) in full effect.

## When this applies

- Internal site (your own portfolio, publications, project landing pages, personal experiments)
- Internal app (your own tools, dashboards, admin panels, CLI utilities with UI)

For external client work, this file is **not loaded**. Client work uses the default workflow (full intake, references-driven, no owner-brand override).

## Core premise

You own the brand. The skill should not ask you what colors you want or what your audience prefers. The owner-brand profile already answers those questions. What the skill **should** still ask: project goals, scope, stack preferences, hosting, optional references that scope this specific project's aesthetic deviation from the standing brand.

## Intake adaptation

### Skipped questions

These are answered by the owner-brand profile and should NOT be asked:

- ~~Client name~~ (no client; project is owned)
- ~~Industry / domain context~~ (you know your domain)
- ~~Audience aesthetic preferences~~ (you are the audience, or you know who is)
- ~~Brand voice~~ (read `owner-brand/voice.md`)
- ~~Color preferences~~ (read brand tokens)
- ~~Typography preferences~~ (read brand tokens)
- ~~Existing brand constraints~~ (read brand profile)
- ~~Competitor references the client liked~~ (no client to please)

### Still asked

- **Project name** (becomes folder name at `C:\dev\Projects\[name]\`)
- **Project goals**: what should this thing accomplish?
- **Scope**: one-pager, multi-page, full app, etc.
- **Optional references**: if you want this project to deliberately deviate from the standing brand or lean into a specific aesthetic, give 1-3 refs. Otherwise skip.
- **Hosting / deploy preference**: Vercel, Netlify, Cloudflare, self-host, doesn't matter
- **Stack preference, if any**: defaults from STACK-DECISIONS.md and (for apps) APP-ADAPTATION.md, but you can override

### Brand surface question

After basic intake, ask one disambiguation question:

**Read `owner-brand/profile.md` first and enumerate the surfaces it actually lists.** Do not hardcode them here; the profile is the source of truth and it changes. Then ask:

> *"Which brand surface for this project?*
> *1..N. [each surface from profile.md, with its one-line identity]*
> *N+1. **New brand**: this project earns its own brand identity"*

If `owner-brand/` is empty or missing (it is gitignored and local-only, see `owner-brand/README.md`), say so and fall back to customer-style brand discovery instead of guessing.

For option 3, the project becomes a candidate for a future owner-brand entry. Ask the user to flag it for capture in the post-mortem.

## What still applies in full

Internal work has the same quality bar as customer work. The taste threshold does not drop.

- **All ANTI-SLOP rules** (read `ANTI-SLOP.md`). No relaxation.
- **owner-brand/voice.md** rules (DO/DON'T list, banned phrases, brand-mark conventions).
- **Verification gates** (Step 5): full Lighthouse, full a11y, and the cross-browser bar set by the mode gate table (site or app; see `APP-ADAPTATION.md` for app gates).
- **Post-mortem hard enforcement** (Step 6): all 6 universal questions, plus the internal-mode 7th question about owner-brand evolution.
- **Stack decision tree** (STACK-DECISIONS.md): apps still use Next.js + React, sites still use vanilla or Astro per the same logic.
- **Pattern library** (`patterns/marketing/` and `patterns/app/`): same patterns apply, same growth flywheel.

## What changes

### Token synthesis (Step 3)

Instead of building tokens from references, **start from `owner-brand/tokens/[brand].css`** as the project's `tokens.css`. Override only where the brief explicitly justifies a deviation.

If the user said "new brand" in the brand-surface question, then synthesize from references the way customer work would, but flag the new brand as a post-mortem candidate.

### Reference analysis (Step 2)

Optional, not required. If the user provided references, analyze them per `analyzer/extract-prompt.md` and use them as project-specific aesthetic targets. If not, skip Step 2 and proceed straight to Step 3 with brand tokens as the synthesis basis.

### Project location

`C:\dev\Projects\[name]\`: no client wrapper, no `clients/` subdirectory.

### Voice

Apply `owner-brand/voice.md` as authored. Specific copy, real names, real numbers, real outcomes. Internal projects get the strongest application of voice rules because there's no client to dilute them.

### Post-mortem 7th question (internal-mode addition)

In addition to the 6 universal post-mortem questions in PROCESS.md Step 6:

7. **Did anything from this project deserve to go into your owner-brand profile?** New brand surface? New token convention? New voice rule? New design rule that should be lifted into the brand guide?

Same hard enforcement. Substantive answer required:
- *"Yes, lift X to owner-brand"* → write the addition; commit `owner-brand: add X`
- *"Intentionally nothing, this project stayed within the standing brand"* → log in POSTMORTEM.md
- Non-answer ("nah", "skip") → push back

## What does NOT change

The rest of the system applies identically:

- 6-step PROCESS.md workflow
- ANTI-SLOP.md universal rules
- Done signals
- Hard-enforced post-mortem
- Stack decision tree
- Verification gates appropriate to mode (site vs app)
- Reference vault, pattern library, token system templates
- Skill behavior contract

## Anti-pattern

Do not use internal mode as an excuse to lower the quality bar. "It's just internal" is the trap. The whole point of having a system is that internal work doesn't suck. The only thing internal mode skips is the brand-discovery questions you've already answered. Everything else is held.

If you find yourself wanting to skip verification ("it's just for me"), skip a structural decision ("nobody else will see it"), or skip the post-mortem ("nothing to capture, it was just a quick thing"), you're misusing the mode. Quit and start over with the standard workflow if you need to.
