# Motion

Motion is personality. Default `ease-in-out 200ms` reads as "I didn't tune this." A small motion vocabulary — 2-3 easings + 3-4 durations — applied consistently, signals craft.

## Easing curves

The easing communicates the brand voice. Pick 2-3 cubic-beziers per project.

### General-purpose (good defaults)

```css
:root {
  --ease-out-quart:    cubic-bezier(0.25, 1, 0.5, 1);
  --ease-out-expo:     cubic-bezier(0.19, 1, 0.22, 1);
  --ease-in-out-expo:  cubic-bezier(0.87, 0, 0.13, 1);
  --ease-in-out-quart: cubic-bezier(0.83, 0, 0.17, 1);
}
```

### Snappy / sharp brands (Linear, Stripe energy)

```css
--ease-snappy:    cubic-bezier(0.34, 1.56, 0.64, 1);    /* slight overshoot */
--ease-out-back:  cubic-bezier(0.34, 1.56, 0.64, 1);
--ease-tight:     cubic-bezier(0.25, 0.1, 0.25, 1);
```

### Smooth / luxury brands (Apple, Arc energy)

```css
--ease-smooth:    cubic-bezier(0.32, 0, 0.67, 0);
--ease-velvet:    cubic-bezier(0.6, 0, 0.4, 1);
--ease-glide:     cubic-bezier(0.16, 1, 0.3, 1);
```

### Mechanical / brutalist brands

```css
--ease-step-out:  steps(8, end);
--ease-mechanical: cubic-bezier(0.4, 0, 0.6, 1);
--ease-instant:    cubic-bezier(1, 0, 0, 1);
```

## Durations

Pick 3-4 steps. Use semantically.

```css
:root {
  --duration-instant:  100ms;   /* hover state, focus, micro-interactions */
  --duration-fast:     200ms;   /* button press, dropdown open */
  --duration-base:     320ms;   /* most state transitions, modal open */
  --duration-slow:     560ms;   /* page-level reveals, hero animations */
  --duration-deliberate: 900ms; /* big statement moments */
}
```

## Motion vocabulary

A site's motion vocabulary is the *kinds of movement* it uses. Pick from:

### Hover / interactive

- **Color shift** — fg/bg/border state change, fast (200-300ms)
- **Translate** — element shifts up/down on hover (`translateY(-2px)`), fast
- **Underline draw** — text-decoration animates in, fast
- **Reveal** — secondary content appears on hover, base
- **Scale** — element grows slightly (`scale(1.02)`), fast

### Scroll-driven

- **Fade-in on enter viewport** — base duration, ease-out
- **Slide-in from below** (`translateY(40px) → 0`) — base duration
- **Parallax** — background or hero moves slower than scroll (subtle, 0.3-0.5x)
- **Sticky reveal** — section sticks while content scrolls underneath
- **Scrub** — animation tied directly to scroll position
- **Pin** — element pins, animation plays, then unpins (GSAP ScrollTrigger)

### Page transitions

- **View Transitions API** — modern, native, works in Chrome/Edge/Safari (in progress in Firefox)
- **Astro built-in** — `<ViewTransitions />` component
- **Cross-fade** — opacity transition between page states
- **Shared element** — element morphs between pages

### Cursor

- **Custom cursor** — replaces native cursor with styled element
- **Cursor follow** — element trails cursor with delay
- **Cursor magnetic** — cursor pulled toward interactive elements

## Reduced motion

**Always respect `prefers-reduced-motion`.** Failing to is an accessibility violation.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

Or more granular: keep functional motion (state changes), kill decorative motion (parallax, reveals).

## Tools / libraries

| Tool | When |
|------|------|
| **CSS transitions/animations** | Default for hover, focus, simple state |
| **View Transitions API** | Page-to-page transitions in modern browsers |
| **Motion One** | Vanilla JS, lightweight, modern API |
| **GSAP** | Complex sequences, ScrollTrigger, premium polish (commercial license for client work) |
| **Framer Motion** | React-only, declarative, ergonomic for React projects |
| **Lenis** | Smooth scroll (use sparingly — not every site needs it) |
| **Lottie** | Designer-authored animations |

## Anti-patterns

- `transition: all 200ms ease-in-out` — generic, no brand voice
- Same duration for every transition — no rhythm
- Motion on everything (over-animated reads as juvenile)
- No motion at all (reads as static template)
- Smooth scroll forced on every page (annoys users with scroll-heavy reading)
- Animations that block interaction (e.g., 1s page transition where user can't click)
- Ignoring `prefers-reduced-motion`
