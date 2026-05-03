# Type Scales

A modular type scale picks one ratio and derives all sizes from a base. Pick the ratio deliberately based on the project's voice.

## Ratios

| Ratio | Name | Voice | Example sites |
|-------|------|-------|---------------|
| **1.067** | Minor second | Very tight, near-flat hierarchy | Editorial dense layouts |
| **1.125** | Major second | Tight, calm | Most documentation, app UI |
| **1.2** | Minor third | Calm, restrained | Quiet product marketing |
| **1.25** | Major third | Balanced, default-feeling | Most general-purpose marketing |
| **1.333** | Perfect fourth | Confident, classic | Editorial, agency work |
| **1.414** | Augmented fourth (√2) | Slightly dramatic | Fashion, lifestyle |
| **1.5** | Perfect fifth | Bold, expressive | Music, entertainment, bold brands |
| **1.618** | Golden ratio | Elegant, expressive | Luxury, refined |
| **2.0** | Octave | Very dramatic | Brutalist, statement-led |

## Base size

Body text base is typically `1rem = 16px` (browser default) but consider:

- **17-18px base** — better long-form readability, subtly more "considered"
- **15-16px base** — denser, more "app-like" or "modern SaaS"
- **20px+ base** — editorial, statement-led, high-contrast brands

Author as `rem` so user font-size preferences cascade.

## Example scales

### 1.25 ratio, 16px base

| Step | Size (px) | Use |
|------|-----------|-----|
| -1 | 12.8 | small print, captions |
| 0 (base) | 16 | body |
| +1 | 20 | lead, blockquote |
| +2 | 25 | h4, eyebrow |
| +3 | 31 | h3 |
| +4 | 39 | h2 |
| +5 | 49 | h1 (small) |
| +6 | 61 | h1 (large), display |
| +7 | 76 | hero display |

### 1.333 ratio, 17px base

| Step | Size (px) | Use |
|------|-----------|-----|
| -1 | 12.75 | small |
| 0 | 17 | body |
| +1 | 22.66 | lead |
| +2 | 30.20 | h4 |
| +3 | 40.25 | h3 |
| +4 | 53.65 | h2 |
| +5 | 71.51 | h1 |
| +6 | 95.32 | display |

### 1.5 ratio, 18px base

| Step | Size (px) | Use |
|------|-----------|-----|
| -1 | 12 | small |
| 0 | 18 | body |
| +1 | 27 | lead |
| +2 | 40.5 | h3 |
| +3 | 60.75 | h2 |
| +4 | 91.13 | h1 |
| +5 | 136.69 | display |

## CSS implementation

Modern approach with CSS custom properties:

```css
:root {
  --type-base: 1.0625rem;          /* 17px */
  --type-ratio: 1.333;

  --type--1: calc(var(--type-base) / var(--type-ratio));
  --type-0:  var(--type-base);
  --type-1:  calc(var(--type-base) * var(--type-ratio));
  --type-2:  calc(var(--type-1) * var(--type-ratio));
  --type-3:  calc(var(--type-2) * var(--type-ratio));
  --type-4:  calc(var(--type-3) * var(--type-ratio));
  --type-5:  calc(var(--type-4) * var(--type-ratio));
  --type-6:  calc(var(--type-5) * var(--type-ratio));
}
```

Or fluid responsive sizing with `clamp()`:

```css
:root {
  --type-h1: clamp(2.5rem, 6vw + 1rem, 5rem);
  --type-h2: clamp(2rem, 4vw + 1rem, 3.5rem);
}
```

Fluid is generally better for hero/display sizes; fixed steps better for body and UI.

## Line height

Inverse relationship to size:

- Body text (16-20px): `line-height: 1.5` to `1.7`
- Small text (12-14px): `line-height: 1.4` to `1.5`
- Headings (24-48px): `line-height: 1.15` to `1.3`
- Display (60px+): `line-height: 0.95` to `1.1`

## Letter spacing

- Body text: 0 (default)
- Small caps / labels: `letter-spacing: 0.05em` to `0.1em`
- Display headlines: `letter-spacing: -0.02em` to `-0.04em` (tighten)
- Mono / code: 0

## Font pairings (starting ideas)

These are *starting ideas only*. Always pull from the references at intake.

| Display | Body | Mono | Voice |
|---------|------|------|-------|
| Söhne (or Inter Display) | Inter | JetBrains Mono | Modern product |
| GT America | GT America | JetBrains Mono | Studio standard |
| Tiempos / Fraunces | Inter | IBM Plex Mono | Editorial / classic |
| Neue Haas Grotesk Display | Neue Haas Grotesk Text | Berkeley Mono | Swiss / serious |
| Editorial New | Inter | JetBrains Mono | Editorial / luxury |
| Migra / Tobias | Inter | Berkeley Mono | Fashion / lifestyle |
| Druk Wide | GT America | JetBrains Mono | Bold / brutalist |
| Adelle / Source Serif | Inter | JetBrains Mono | Long-form readable |

Free / open-source equivalents (via Fontshare, Google Fonts, Fontsource):

- Söhne → **Switzer** (Fontshare)
- GT America → **Satoshi** (Fontshare)  
- Tiempos → **Fraunces** (Google) or **Source Serif Pro**
- Editorial New → **PP Editorial New** (Pangram, free for personal)
- Migra → **Cormorant Garamond** (Google) — close enough
- Neue Haas Grotesk → **Inter** or **Geist** (Vercel)
- Druk Wide → **Bricolage Grotesque** (Google) — wide variants
