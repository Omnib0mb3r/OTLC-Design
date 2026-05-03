# patterns/

> Hand-built layout primitives. **The vocabulary of how *this practice* solves recurring layout problems.** Not a component library to install. A growing collection of structural ideas worth reusing.

This folder starts empty (or near-empty). It fills as you build real projects and identify structures worth lifting.

## Subdivision

Patterns split by mode:

- [`marketing/`](marketing/) — patterns for marketing/showcase sites (heroes, type-led sections, scroll narratives, footer statements, navigation patterns)
- [`app/`](app/) — patterns for app/product UI (data tables, command palettes, multi-step forms, empty states, settings layouts, side nav)

A pattern lives in one folder. If a pattern genuinely applies to both modes (rare), put it in the more-applicable folder and cross-reference from the other.

## What goes in here

When you build something that you'd reach for again on a different project, extract it.

A pattern is **structural**, not visual. The styling will differ per project (different tokens, different copy). The *structure* is what gets captured.

## What does NOT go in here

- One-off components specific to a single project
- Generic patterns (Hero, FeatureCard, FAQ accordion) — see ANTI-SLOP.md
- Components from third-party libraries
- Components that are just shadcn primitives renamed

## File structure per pattern

Create a markdown file: `patterns/[mode]/[pattern-name].md`. Use this structure:

```markdown
# [Pattern Name]

## Intent

What problem does this structure solve? When would you reach for it?

## When to use

- Bullet of project type
- Bullet of context

## When NOT to use

- Things this pattern is wrong for

## Structural sketch

ASCII or SVG showing the layout primitives. Not pixel-accurate; just structure.

## Variations

How the same structure can be styled differently across projects.

## Reference uses

- [project-1] — link or note
- [reference-site-from-vault] — note

## Code reference

Path to a clean implementation in a real project, or inline minimal HTML/CSS showing the bones.

## Notes

Lessons, anti-patterns to avoid within this pattern.
```

Commit message when adding: `patterns: add [mode]/[pattern-name]`.

## Examples of patterns worth capturing (when you build them)

### Marketing patterns
- **Type-led hero with no image** — when the headline IS the hero
- **Asymmetric two-column with breakout** — narrower text left, wide image breaking right margin
- **Sticky sidebar with scroll-narrative content** — long-form essay layout
- **Project deep-dive single-page** — case study format
- **Marquee + dense info row** — motion above a tight client list
- **Footer-as-statement** — full-bleed display type instead of utility links
- **Contact-as-form-letter** — inline-blank form letter, not stacked label/input

### App patterns
- **Command palette** (Cmd-K)
- **Data table with filtering / sorting / pagination**
- **Multi-step form with validation**
- **Empty state composition** (with primary CTA to create)
- **Permission-gated content with explanatory tooltips**
- **Side nav with collapse / pinned items**
- **Bulk action bar** (selection count + actions)
- **Inline edit with optimistic update**
- **Settings sidebar + content**
- **Notification / toast pattern**

When you build one and like it, lift it here.

## Anti-pattern

Do not pre-populate this folder with hypothetical patterns. Patterns earn their place by being *used and proven* in real projects first. An empty folder that grows with real work is more valuable than a full folder of templates that nobody reaches for.
