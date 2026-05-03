# Reference Extraction Procedure

> Used during PROCESS.md Step 2. For each reference URL provided at intake, follow this procedure with Chrome DevTools MCP. Output to `[client-project]/references/[domain].md` using the schema below.

---

## Procedure

### 1. Navigate

Open the URL in Chrome via Chrome DevTools MCP. Wait for full load (network idle, fonts loaded).

### 2. Capture screenshots

Capture full-page screenshots at four widths:

- **375px** — mobile
- **768px** — tablet
- **1280px** — desktop standard
- **1920px** — large desktop

Save to `[client-project]/references/[domain]/screens/[width].png`.

### 3. Extract type system

Inspect the DOM and computed styles. For at least: `body`, `h1`, `h2`, `h3`, `h4`, `p`, `small`, and any visible display/hero text.

For each:
- Font family (computed)
- Font size in px
- Font weight
- Line height
- Letter spacing
- Color (convert to OKLCH)

Compute the **modular ratio**: divide each step's font-size by the next smaller step. Look for the consistent ratio. Common values: 1.125, 1.2, 1.25, 1.333, 1.414, 1.5, 1.618.

Identify font families used. Note if Google Fonts, Adobe, custom WOFF, or system stack.

### 4. Extract color palette

Sample colors from the rendered page:

- Background (body, sections, cards)
- Primary text
- Secondary text (muted)
- Borders, dividers
- Accent (links, buttons, CTAs)
- Any unusual colors (custom selection, custom highlight, brand splashes)

For each, convert to OKLCH and note: `oklch(L% C H)`.

Note unusual choices: cream instead of white, off-black instead of pure black, low-chroma neutrals warm/cool tilt, etc.

### 5. Extract spacing

Measure (via computed styles):

- Section padding top/bottom
- Section gaps (vertical rhythm)
- Container max-width
- Common element gaps (between paragraphs, between cards, between nav items)

Identify the **base unit** if evident. Marketing sites commonly use 4 or 8 px base.

### 6. Extract grid / layout primitives

For each major section type observed:

- **Hero** — Centered? Left? Asymmetric? Image-led? Type-only? Full-bleed? Overlapping content?
- **"What we do"** — Three-up cards? List? Numbered paragraphs? Interactive? Type-led?
- **"Showcase / Work"** — Grid? List? Carousel? Sticky sidebar with scroll narrative?
- **"About / Team"** — Photos? Type? Story-told?
- **"Contact"** — Form? Inline letter? Email link only?
- **"Footer"** — Utility? Statement? Full-bleed display type? Column-based?

Note column counts (12-col grid? 6-col? bespoke?) and whether breakouts beyond the main column happen.

### 7. Extract motion patterns

Observe the page over 30 seconds with cursor movement and scroll:

- **Hover states** — Subtle? Exaggerated? Color? Translate? Reveal?
- **Scroll motion** — Parallax? Fades? Reveals? Sticky? Scrub? Pin?
- **Page transitions** — Hard load? Cross-fade? View transitions?
- **Cursor effects** — Custom cursor? Magnetic? Trail?
- **Loading state** — Skeleton? Loader? Snap?

Note easing feel (snappy? smooth? mechanical?) — guess at cubic-bezier curve or describe.

### 8. Note unusual / signature choices

Anything that signals deliberate design choice:

- Custom cursor
- Custom selection color
- Marquee text
- Mixed type sizes within a single line
- Unusual border treatments (thick rules, double borders, none at all)
- Asymmetric breakouts beyond the main column
- Inline images with text wrap
- Type set in tables or forms
- Sound effects
- Easter eggs
- Anything else that makes the site feel built by a human

### 9. Run Lighthouse (optional but recommended)

Capture performance baseline of the reference. Often the reference's actual performance is worse than its design suggests; note this so the client doesn't expect both.

---

## Output Schema

Write to `[client-project]/references/[domain].md`:

```markdown
# [Domain]

**URL:** https://...
**Captured:** [date]
**Lighthouse:** Perf X / A11y X / Best X / SEO X

## Aesthetic vocabulary

One paragraph describing the aesthetic in design terms (not vibes). E.g., "Editorial Swiss with brutalist breaks. Restrained warm neutral palette. Heavy display serif paired with clean grotesque body. Asymmetric grid with frequent right-margin breakouts. Subtle smooth-scroll, no parallax, hover states are color-only."

## Type system

| Element | Family | Size | Weight | Line-height | Letter-spacing | Color |
|---------|--------|------|--------|-------------|----------------|-------|
| h1 | ... | 64px | 700 | 1.05 | -0.03em | oklch(15% 0.02 250) |
| h2 | ... | 48px | 600 | 1.1 | -0.02em | oklch(15% 0.02 250) |
| h3 | ... | 32px | 600 | 1.2 | -0.01em | oklch(15% 0.02 250) |
| body | ... | 17px | 400 | 1.6 | 0 | oklch(20% 0.02 250) |
| small | ... | 13px | 400 | 1.5 | 0.02em | oklch(50% 0.02 250) |

**Modular ratio:** 1.333 (perfect fourth)
**Pairing:** [Display family] + [Body family] + [optional mono]
**Notes:** [anything unusual]

## Color palette

**Background:** oklch(98% 0.005 70) — warm cream
**Foreground:** oklch(15% 0.02 250) — near-black, slightly cool
**Muted:** oklch(50% 0.02 250)
**Border:** oklch(85% 0.01 250)
**Accent:** oklch(58% 0.18 240) — saturated blue
**Notes:** [unusual choices, hue stories, etc.]

## Spacing

**Base unit:** 8px
**Section padding (vertical, desktop):** 128px
**Section padding (vertical, mobile):** 64px
**Container max-width:** 1280px
**Element gap (paragraphs):** 24px

## Layout / structural choices

**Hero:** Asymmetric. Headline left-aligned, breaking out 1 column past the main grid. No image. Subhead underneath, half-width. CTA inline with subhead, not below.

**"Work" section:** Sticky left sidebar with project nav. Right side scrolls through deep dives. View Transitions on selection.

**"About":** Long-form essay structure. Type-only. Pull quotes break the column.

**Footer:** Full-bleed display type. Email and social as a single inline sentence.

## Motion

**Hover:** Color shift only, 200ms ease-out.
**Scroll:** Fade-in + 20px translate on section enter, 600ms ease-out-quart. No parallax.
**Page transitions:** View Transitions API, cross-fade.
**Cursor:** Standard.
**Easing voice:** Smooth, not snappy.

## Unusual / signature

- Custom selection color matching accent
- Body copy uses `text-wrap: pretty` for orphan control
- Footer uses `font-feature-settings: "ss01"` for stylistic alternates
- Section dividers are 1px hairlines, not gaps

## Pull-forward candidates

Things this reference does that we should consider lifting (informed by, not copied):

- Asymmetric hero with right breakout
- Sticky sidebar work navigation
- Full-bleed display footer
```

---

## Notes on rigor

- **Always extract computed values, not visual estimates.** "Looks like a 1.25 scale" is not the same as "computed h1=48px / h2=36px / h3=27px / body=18px → ratio 1.333".
- **Always convert colors to OKLCH.** Hex/RGB obscures perceptual relationships.
- **Always note unusual choices.** They are usually what separates the reference from slop.
- **Always identify "pull-forward candidates."** The synthesis step depends on this.
- **Never copy 1:1.** Extract principles, not pixels (ANTI-SLOP rule on references).
