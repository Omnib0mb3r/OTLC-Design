# Spacing

Pick a base unit. Build a scale. Apply consistently. Spacing is what gives a design rhythm; arbitrary spacing is the most common slop signal after color defaults.

## Base unit choices

| Base | Voice | Use when |
|------|-------|----------|
| **4px** | Dense, fine-grained | App UIs, dashboards, dense product pages |
| **6px** | Slightly less dense, uncommon | Specific brand systems, rarely chosen |
| **8px** | Default, balanced | Most marketing sites, general-purpose |
| **10px** | Looser, more editorial | Editorial, type-led, breathing room |
| **12px** | Loose, dramatic | Statement-led brands, luxury |

Default to **8px** unless references suggest otherwise.

## Building a scale

Linear (most common):

```
4, 8, 12, 16, 24, 32, 48, 64, 96, 128, 192
```

Or modular (matches your type scale):

```css
--space-base: 0.5rem;   /* 8px */
--space-ratio: 1.5;

--space-1: var(--space-base);
--space-2: calc(var(--space-base) * var(--space-ratio));         /* 12 */
--space-3: calc(var(--space-2) * var(--space-ratio));            /* 18 */
--space-4: calc(var(--space-3) * var(--space-ratio));            /* 27 */
--space-5: calc(var(--space-4) * var(--space-ratio));            /* 40.5 */
```

Linear is easier to reason about. Modular ties spacing to type rhythm.

## Naming

Either size-named (`--space-4` = 4 base units) or t-shirt-sized (`--space-sm`, `--space-md`, `--space-lg`). Size-named is more flexible (numeric ordering, easy to add new steps). Default to size-named.

## Layout-level spacing

Distinguish between **layout spacing** (between sections) and **component spacing** (within elements).

```css
:root {
  /* component-level (within a card, button, etc.) */
  --space-1: 0.25rem;   /* 4px */
  --space-2: 0.5rem;    /* 8px */
  --space-3: 0.75rem;   /* 12px */
  --space-4: 1rem;      /* 16px */
  --space-6: 1.5rem;    /* 24px */
  --space-8: 2rem;      /* 32px */

  /* layout-level (between sections, between major blocks) */
  --layout-xs: 3rem;    /* 48px */
  --layout-sm: 5rem;    /* 80px */
  --layout-md: 8rem;    /* 128px */
  --layout-lg: 12rem;   /* 192px */
  --layout-xl: 16rem;   /* 256px */
}
```

Marketing sites typically use **80-128px between sections** at desktop, scaling down to 48-64px at mobile.

## Container widths

Pick a max content width. Common choices:

- **Narrow** (~640-720px): long-form reading, editorial
- **Standard** (~1100-1280px): general marketing
- **Wide** (~1440-1600px): image-heavy, showcase
- **Full bleed** (no max): statement design

Use container queries for component-level responsive spacing where helpful, not just media queries.

## Breakpoints

Don't use Tailwind defaults. Common considered set:

```css
/* mobile-first */
@media (min-width: 480px)  { /* small tablet / large phone */ }
@media (min-width: 768px)  { /* tablet */ }
@media (min-width: 1024px) { /* desktop */ }
@media (min-width: 1440px) { /* large desktop */ }
@media (min-width: 1920px) { /* very large */ }
```

Or fewer (and more opinionated):

```css
@media (min-width: 768px)  { /* "tablet+" - most layout shifts happen here */ }
@media (min-width: 1280px) { /* "desktop" */ }
```

## Anti-patterns

- Using arbitrary pixel values (`margin: 23px`, `padding: 17px`) instead of the scale.
- Mixing the spacing scale with arbitrary line-heights.
- Tailwind defaults (`p-4`, `mt-8`) without confirming they map to your scale.
- The same spacing value between *every* section (no rhythm).
- Insufficient layout-level spacing (sections feel cramped). 64-128px between major sections is the floor for marketing sites at desktop.
