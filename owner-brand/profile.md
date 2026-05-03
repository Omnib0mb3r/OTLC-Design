# Owner Brand Profile

> Index of standing brand surfaces. The `OTLC-Design` skill reads this when mode is internal.
>
> **Source of truth:** [`source/MichaelCollins_BrandGuide.docx`](source/MichaelCollins_BrandGuide.docx)
> **Version:** 1.0 (extracted 2026-05-03)

## Owner

- **Full name:** Michael Collins
- **Primary handle:** Michael Collins_ (underscore after, blinking cyan pip in nav)
- **YouTube handle:** @OmniB0mb3r
- **TikTok handle:** @warehouseautomationguy
- **Newsletter brand:** Material Handling Weekly
- **Domain:** onthelevelconcepts.com
- **Positioning:** Solutions Wizard. 27 years in warehouse automation.

## Brand surfaces

The owner has more than one brand. Internal projects must specify which surface applies.

### 1. [Personal Site](brands/personal-site.md)

The Solutions Wizard / Michael Collins_ brand. Dark, engineered, premium aesthetic with cyan as primary accent.

- **Used for:** personal site (onthelevelconcepts.com), all general-purpose Michael Collins assets, internal tools that share the personal aesthetic
- **Tokens:** [`tokens/personal-site.css`](tokens/personal-site.css)
- **Primary colors:** dark navy `#02040A`, cyan `#00DCFF`
- **Type:** Sora + JetBrains Mono

### 2. [Material Handling Weekly](brands/mhw.md)

The MHW newsletter brand. Professional, editorial, industry-publication feel. Navy and gold only.

- **Used for:** Material Handling Weekly properties (materialhandlingweekly.com, MHW emails, MHW social, MHW-specific cards on the personal site)
- **Tokens:** [`tokens/mhw.css`](tokens/mhw.css)
- **Primary colors:** MHW navy `#1A1A2E`, MHW gold `#F0C419`
- **Type:** Archivo + Montserrat (Beehiiv Tradecraft template)

## Voice

Universal across all brand surfaces. See [`voice.md`](voice.md).

## Skill behavior

When `OTLC-Design` skill detects mode = internal:

1. Read this file
2. Ask: *"Personal-site brand, MHW brand, or a new brand for this project?"*
3. If existing brand chosen, load the matching `brands/*.md` and `tokens/*.css`
4. Skip brand-discovery intake questions
5. Still apply [`voice.md`](voice.md) regardless of brand choice
6. Still apply universal [`../ANTI-SLOP.md`](../ANTI-SLOP.md) rules (anti-slop is global, not brand-scoped)

## Adding a new brand

If a new internal project needs a third brand surface:

1. Build it in the project as a one-off
2. If it earns repeated use, lift it here as `brands/[name].md` + `tokens/[name].css`
3. Add an entry to this file under "Brand surfaces"
4. Update `source/MichaelCollins_BrandGuide.docx` to document it
5. Commit: `owner-brand: add [brand-name]`

A brand earns its place by being used on more than one project, just like patterns.
