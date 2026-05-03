# tokens/

> Templates and procedures for building project-specific design tokens. **Tokens are synthesized per project from references — never copied from here as defaults.** This folder holds the *systems* (modular type scales, OKLCH palette construction, spacing scales), not the values.

When the `design-website` skill runs Step 3 (Synthesis), it reads these files to choose which scale to apply, then computes specific token values for the project at hand and writes them to `[client-project]/tokens.css`.

## Files

| File | Purpose |
|------|---------|
| [`type-scales.md`](type-scales.md) | Catalog of modular ratios and which projects suit each |
| [`color-systems.md`](color-systems.md) | OKLCH palette construction, neutral ramp recipes, contrast verification |
| [`spacing.md`](spacing.md) | Base units (4 / 8) and how to build spacing scales |
| [`motion.md`](motion.md) | Easing curves, durations, motion vocabulary |

## What gets written to a client project

A `tokens.css` file in the client project root, structured roughly:

```css
@layer tokens {
  :root {
    /* type */
    --font-display: '...', system-ui, sans-serif;
    --font-body: '...', system-ui, sans-serif;
    --font-mono: '...', ui-monospace, monospace;

    --type-scale-ratio: 1.333;
    --type-base: 1.0625rem;       /* 17px */
    --type-xs: calc(var(--type-base) / var(--type-scale-ratio));
    --type-sm: var(--type-base);
    --type-md: calc(var(--type-base) * var(--type-scale-ratio));
    --type-lg: calc(var(--type-base) * pow(var(--type-scale-ratio), 2));
    /* etc. */

    /* color (OKLCH) */
    --color-bg: oklch(98% 0.01 95);
    --color-fg: oklch(15% 0.02 270);
    --color-accent: oklch(60% 0.18 240);
    --color-muted: oklch(60% 0.02 270);
    --color-border: oklch(85% 0.01 270);

    /* spacing (8px base) */
    --space-1: 0.25rem;   /* 4 */
    --space-2: 0.5rem;    /* 8 */
    --space-3: 0.75rem;   /* 12 */
    --space-4: 1rem;      /* 16 */
    --space-5: 1.5rem;    /* 24 */
    --space-6: 2rem;      /* 32 */
    --space-8: 4rem;      /* 64 */
    --space-12: 8rem;     /* 128 */

    /* motion */
    --ease-out-quart: cubic-bezier(0.25, 1, 0.5, 1);
    --ease-in-out-expo: cubic-bezier(0.87, 0, 0.13, 1);
    --duration-fast: 150ms;
    --duration-base: 280ms;
    --duration-slow: 600ms;

    /* radius — opinionated, single value */
    --radius: 4px;
  }
}
```

The skill picks specific values informed by the references (Step 2 output), the system templates here, and any brand constraints from intake.

## Anti-pattern

Do not author tokens once and reuse across all projects. Every project should have its own `tokens.css` derived from its own references and brief. The shared layer is the *system* (how to build a scale, how to author OKLCH), not the *values*.
