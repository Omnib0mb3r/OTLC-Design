# Color Systems

> Author colors in **OKLCH**, not hex or HSL. OKLCH is perceptually uniform: equal lightness numbers look equally bright across all hues, which makes building a coherent palette mathematically tractable.

## OKLCH basics

```css
oklch( <Lightness>%  <Chroma>  <Hue>deg )
```

- **Lightness**: 0% (black) to 100% (white). Perceptual.
- **Chroma**: 0 (gray) to ~0.4 (most saturated). Most visible colors live in 0.05-0.25.
- **Hue**: 0-360 degrees. Same hue value = same perceptual hue regardless of lightness.

Browser support: all evergreen browsers since 2023. Safe to use without fallback.

## Building a neutral ramp

Pick a hue (often slightly cool or warm, *never* pure 0). Build 9-12 lightness steps with low chroma.

### Recipe: slightly warm neutral (cream/off-white background)

```css
:root {
  /* Hue: 70deg (warm yellow-ish), Chroma: 0.005-0.015 (near-gray but warm) */
  --neutral-50:  oklch(98% 0.005 70);    /* near-white, warm */
  --neutral-100: oklch(95% 0.008 70);
  --neutral-200: oklch(90% 0.010 70);
  --neutral-300: oklch(82% 0.012 70);
  --neutral-400: oklch(70% 0.015 70);
  --neutral-500: oklch(58% 0.015 70);
  --neutral-600: oklch(45% 0.015 70);
  --neutral-700: oklch(35% 0.015 70);
  --neutral-800: oklch(22% 0.012 70);
  --neutral-900: oklch(15% 0.010 70);    /* near-black, warm */
}
```

### Recipe: slightly cool neutral (modern product feel)

```css
:root {
  /* Hue: 250deg (slightly blue), Chroma: 0.005-0.012 */
  --neutral-50:  oklch(98% 0.005 250);
  --neutral-100: oklch(95% 0.008 250);
  --neutral-200: oklch(90% 0.010 250);
  --neutral-300: oklch(82% 0.012 250);
  --neutral-400: oklch(70% 0.012 250);
  --neutral-500: oklch(58% 0.012 250);
  --neutral-600: oklch(45% 0.012 250);
  --neutral-700: oklch(35% 0.010 250);
  --neutral-800: oklch(22% 0.008 250);
  --neutral-900: oklch(15% 0.005 250);
}
```

### Recipe: true neutral (gray)

```css
:root {
  --neutral-50:  oklch(98% 0 0);
  --neutral-100: oklch(95% 0 0);
  --neutral-200: oklch(90% 0 0);
  --neutral-300: oklch(82% 0 0);
  --neutral-400: oklch(70% 0 0);
  --neutral-500: oklch(58% 0 0);
  --neutral-600: oklch(45% 0 0);
  --neutral-700: oklch(35% 0 0);
  --neutral-800: oklch(22% 0 0);
  --neutral-900: oklch(15% 0 0);
}
```

## Accents

Pick 1-2 accents max. Each accent should have its own ramp at the same lightness steps as neutrals (for hover/active/disabled states).

### Recipe: single accent ramp

```css
:root {
  /* Pick the hue from references. Example: 240deg = blue. */
  --accent-50:  oklch(95% 0.04 240);
  --accent-100: oklch(88% 0.08 240);
  --accent-200: oklch(78% 0.12 240);
  --accent-300: oklch(68% 0.16 240);
  --accent-400: oklch(58% 0.18 240);   /* primary accent */
  --accent-500: oklch(48% 0.18 240);
  --accent-600: oklch(38% 0.16 240);
  --accent-700: oklch(28% 0.12 240);
  --accent-800: oklch(20% 0.08 240);
  --accent-900: oklch(14% 0.05 240);
}
```

The "use this for accents" step is usually 400-500 (most chromatic). 300 for hover-lighten, 600 for hover-darken.

## Semantic tokens

Always layer semantic tokens on top of the raw ramps. This is what components reference.

```css
:root {
  --color-bg:           var(--neutral-50);
  --color-bg-elevated:  var(--neutral-100);
  --color-bg-overlay:   var(--neutral-100);

  --color-fg:           var(--neutral-900);
  --color-fg-muted:     var(--neutral-600);
  --color-fg-subtle:    var(--neutral-500);

  --color-border:       var(--neutral-200);
  --color-border-strong: var(--neutral-300);

  --color-accent:       var(--accent-400);
  --color-accent-fg:    var(--neutral-50);
  --color-accent-hover: var(--accent-500);

  --color-link:         var(--accent-400);
  --color-link-visited: var(--accent-500);
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-bg:           var(--neutral-900);
    --color-bg-elevated:  var(--neutral-800);
    --color-fg:           var(--neutral-50);
    --color-fg-muted:     var(--neutral-400);
    --color-border:       var(--neutral-800);
    /* etc. */
  }
}
```

## Contrast verification

Before shipping:

- **Body text on background**: WCAG AA = 4.5:1 minimum. Aim for AAA = 7:1.
- **Large text on background** (>=18pt or 14pt bold): AA = 3:1, AAA = 4.5:1.
- **UI components and graphics**: AA = 3:1 minimum.

Use any contrast checker. APCA (the future replacement for WCAG contrast) is more accurate but not yet legally required; use as a sanity check.

For OKLCH, the rule of thumb: a lightness difference of ≥40 percentage points on a low-chroma neutral pair gives AA body contrast in most cases. Verify, do not assume.

## Anti-patterns

- Pure white (`oklch(100% 0 0)`) and pure black (`oklch(0% 0 0)`) as defaults: too harsh, signals "unconsidered". Use 98% and 15% instead.
- Tailwind `slate` / `gray` / `zinc` defaults: instantly recognizable as slop.
- More than 2 accent hues: palette becomes incoherent.
- Same lightness across hues: fails for color-blind users; use chroma + lightness together.
- Generic gradients (purple → pink, blue → cyan): see ANTI-SLOP rule 5.

## Tools

- [oklch.com](https://oklch.com): interactive picker, see hue wheel at constant lightness
- [huetone.ardov.me](https://huetone.ardov.me): palette + contrast verification
- [APCA contrast](https://www.myndex.com/APCA/): modern contrast tool
