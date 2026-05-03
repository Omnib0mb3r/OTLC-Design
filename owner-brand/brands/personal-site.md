# Personal Site Brand

> The Solutions Wizard / Michael Collins_ brand. Dark, engineered, premium. Cyan is the primary accent.
>
> **Source:** [`../source/MichaelCollins_BrandGuide.docx`](../source/MichaelCollins_BrandGuide.docx)
> **Drop-in tokens:** [`../tokens/personal-site.css`](../tokens/personal-site.css)

## When to use this brand

- onthelevelconcepts.com and any general-purpose Michael Collins surface
- Internal tools that share the personal aesthetic
- Side projects under the Michael Collins / Solutions Wizard umbrella
- Personal portfolio / showcase work

**Do not use for:** Material Handling Weekly properties (use [`mhw.md`](mhw.md)), client work (use client's brand), or projects that genuinely need a different visual identity.

## Color system

Dark, engineered, premium. Cyan is the primary accent. Gold is reserved for MHW elements only. Violet is reserved for experimental / instructor tier elements only.

| Swatch | Name | Role | Usage |
|--------|------|------|-------|
| `#02040A` | Site Background | `--bg` / Primary BG | Deepest black-navy. Page background. |
| `#060A14` | Surface 1 | `--bg1` / Cards | Slightly lighter. Section backgrounds. |
| `#08101E` | Surface 2 | `--bg2` / Overlays | Gradient fade target on cards. |
| `#00DCFF` | Cyan | `--cyan` / Primary Accent | Buttons, borders, highlights, pip, links. Primary brand color. |
| `rgba(10,15,35,0.6)` | Glass | `--glass` | Card background. Semi-transparent. |
| `#F0C419` | Gold | `--gold` / MHW Accent | **MHW elements only.** Never on personal site outside of MHW cards. |
| `#7B5CF5` | Violet | `--violet` / Experimental | **Experimental / instructor tier only.** Never as a general accent. |
| `#3A8EF0` | Blue | `--blue` / Beta | Beta badge color, mid-level accents. |
| `#E8EEFF` | Text Primary | `--t1` | Main body text on dark backgrounds. |
| `#C8D7FF ~55% opacity` | Text Secondary | `--t2` | Supporting text, descriptions, card body. |

### Semantic color rules (strict)

- **Cyan** is the primary brand accent. Default for CTA, links, highlights.
- **Gold** is **MHW only**. Never as a general accent on the personal site.
- **Violet** is **experimental / instructor tier only**. Never as a general accent.
- **Blue** is **beta tier on the personal site brand specifically**. On other internal-brand projects (one-offs that earn their own brand), blue is available as a general accent.

The first three are strict semantic rules — status colors carry meaning across owner properties. Blue's restriction applies to the personal-site brand only, not to every internal project.

## Typography

| Font | Role | Usage |
|------|------|-------|
| Sora | Display + Body — `--ff` | Headlines, paragraphs, navigation labels, all general text. Google Font. Weights: 200/300/400/500/600/700/800. |
| JetBrains Mono | Mono — `--fm` | Badges, eyebrow labels, kicker text, terminal readouts, code, version numbers, data. Google Font. Weights: 300/400/500/700. |

### Type scale

| Use | Size | Notes |
|-----|------|-------|
| Hero headline (h1) | `clamp(4.5rem, 9.5vw, 9.5rem)` | 800 weight, -0.04em letter-spacing, 0.92 line-height |
| Page headline (h1) | `clamp(3.5rem, 7vw, 7rem)` | 800 weight, tight letter-spacing |
| Section title (h2) | `clamp(2rem, 4vw, 3.2rem)` | 700 weight, -0.03em letter-spacing |
| Card title (h3) | `1rem` | 600 weight |
| Body text | `1rem` / `0.95rem` | 300 weight, 1.75-1.85 line-height |
| Card body | `0.82rem` | 300 weight, 1.65 line-height |
| Eyebrow label | `0.62rem` | JetBrains Mono, 0.2em letter-spacing, uppercase, preceded by `//` |
| Badge text | `0.58rem` | JetBrains Mono, 0.1em letter-spacing, uppercase |
| Button text | `0.68rem` | JetBrains Mono, 0.1em letter-spacing, uppercase, 500 weight |

### Google Fonts import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@200;300;400;500;600;700;800&family=JetBrains+Mono:wght@300;400;500;700&display=swap" rel="stylesheet">
```

## UI Elements

### Buttons

| Type | CSS Class | When to use |
|------|-----------|-------------|
| Primary | `btn btn-primary` | Main CTA. Cyan background, black text. **One per section max.** |
| Ghost | `btn btn-ghost` | Secondary action. Transparent with border. |
| Gold (MHW only) | `btn-gold` | Subscribe Free button. Gold background, black text. MHW elements only. |
| Violet | `btn btn-violet` | Instructor access tier only. Violet tinted background. |
| Small | `btn btn-sm` | Modifier on any button to reduce padding. |

### Status badges

| Badge | Class | Meaning |
|-------|-------|---------|
| LIVE | `badge-live` | Finished, deployed, stable. Cyan text, gold-tinted background. |
| BETA | `badge-beta` | Working but being refined. Blue text. |
| ALPHA | `badge-alpha` | Early build, rough edges. Amber/orange text. |
| EXP | `badge-exp` | Experimental, may break. Violet text. |

### Cards

| Property | Value |
|----------|-------|
| Background | `rgba(10,15,35,0.6)` semi-transparent glass |
| Border | `1px solid rgba(60,130,255,0.15)` default; `rgba(0,220,255,0.28)` on hover |
| Border radius | `14px` (`--r`) |
| Backdrop filter | `blur(12px)` (frosted glass) |
| Hover lift | `translateY(-4px) scale(1.005)` |
| Shadow | `0 4px 16px rgba(0,0,0,0.25)` default; `0 16px 40px rgba(0,0,0,0.4)` on hover |
| Top highlight | `::before` pseudo with linear-gradient cyan strip on featured cards |

## Design rules

| Rule | Details |
|------|---------|
| Dark default, light is deliberate | Default to dark backgrounds. A light variant is allowed but requires documented rationale (the project genuinely benefits from light, not just because it could). |
| One primary CTA per section | Never more than one `btn-primary` per section. Everything else is ghost or secondary. |
| Gold is MHW only | Never use gold (`#F0C419`) on the personal site outside of Material Handling Weekly-specific elements. |
| Violet is experimental only | Never use violet outside of the Lab experiments section or instructor tier. |
| Eyebrows are available, not required | The `//` JetBrains Mono eyebrow above section titles is an available pattern. Use it when it serves the section, not by reflex on every heading. Consistent rhythm is good; formulaic application is slop. |
| Underscores as brand punctuation | `Michael Collins_` / `Solutions Wizard_` / `Builder_`. Underscore closes brand phrases. |
| No em dashes anywhere | Zero em dashes. Locked. Non-negotiable. |
| Glow not harsh shadows | Default to radial-gradient glow effects rather than hard drop shadows. Subtle is better. Hard shadows allowed when a project's voice calls for them (e.g., brutalist deliberate). |
| Directional light implied | Top-left light source implied across the site. Highlights bias toward top-left on cards. |
| Motion default is ambient | Default motion is slow, subtle, atmospheric. Punchier motion is allowed when it serves the project (launch announcement, kinetic data viz, deliberate kinetic statement) — but it requires a reason, not a vibe. |
| Custom cursor | Custom cyan dot with lagging ring on the personal site (deliberate use; not on every internal project). |
| Border radius | `14px` (`--r`) for cards, `8px` (`--rs`) for smaller elements, `100px` for pill buttons. |
| Photo circular crop | Profile photo always circular with cyan border glow. `object-position: center top`. |

## Voice

Universal voice rules in [`../voice.md`](../voice.md). Personal-site brand carries voice as authored — direct, witty, confident, specific. No corporate hedge.
