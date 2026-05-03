# owner-brand/

> **The owner's standing brand system.** Read by the `OTLC-Design` skill when mode is internal (your own work, not external client work). Provides defaults so the skill doesn't ask brand-discovery questions you've already answered.

## Source of truth

The canonical brand document is the original `.docx`:

- [`source/MichaelCollins_BrandGuide.docx`](source/MichaelCollins_BrandGuide.docx)

Edit the `.docx` when the brand changes. Then re-extract to markdown (see *Updating* below). The markdown copies are derived working copies — Claude reads them, but the `.docx` is authoritative.

## Files

| Path | Purpose |
|------|---------|
| [`profile.md`](profile.md) | Index of all your brand surfaces; entry point for the skill |
| [`voice.md`](voice.md) | Voice DOs and DON'Ts; universal across all your brand surfaces |
| [`brands/personal-site.md`](brands/personal-site.md) | Solutions Wizard / cyan personal-site brand (the dark/cyan/glass aesthetic) |
| [`brands/mhw.md`](brands/mhw.md) | Material Handling Weekly / navy + gold editorial brand |
| [`tokens/personal-site.css`](tokens/personal-site.css) | Drop-in CSS custom properties for personal-site brand |
| [`tokens/mhw.css`](tokens/mhw.css) | Drop-in CSS custom properties for MHW brand |
| [`source/MichaelCollins_BrandGuide.docx`](source/MichaelCollins_BrandGuide.docx) | Original brand guide (source of truth) |

## How the skill uses this

When the intake branch resolves to **internal site** or **internal app**, the skill:

1. Reads [`profile.md`](profile.md) to enumerate available brand surfaces
2. Asks one disambiguation question if needed: *"Personal-site brand, MHW brand, or a new brand for this project?"*
3. Loads the matching brand file and tokens CSS
4. Skips the brand-discovery intake questions (colors, type, voice — already known)
5. Still asks project-specific questions (goals, scope, optional refs, hosting)

For **external client work**, this folder is **not loaded**. Client work starts brand-discovery from scratch using the client's references and brief. The owner-brand profile may *inform* the developer's defaults (e.g., font pairing instincts) but never overrides client direction.

## Updating

When the brand evolves (new color, retired pattern, etc.):

1. Edit `source/MichaelCollins_BrandGuide.docx` in Word
2. Re-extract to markdown — manually update `profile.md`, `voice.md`, `brands/*.md`, and `tokens/*.css` to match
3. Bump the version line at the top of `profile.md`
4. Commit: `owner-brand: <what changed>`

If the .docx and markdown drift (the .docx is updated but markdown isn't), Claude should flag this at start of internal-mode work and ask you to reconcile.

## Anti-pattern

Do not let `voice.md`, brand files, or token CSS evolve in ways that contradict the source `.docx`. The `.docx` is the single source of truth. The markdown copies must always be derivable from it.

If a rule "feels right" while building a project but is not in the brand guide, it is a candidate for the next brand guide update — not a silent drift in the markdown copy.
