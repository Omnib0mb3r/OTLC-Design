# patterns/

> Hand-built layout primitives. **The vocabulary of how *this practice* solves recurring layout problems.** Not a component library to install. A growing collection of structural ideas worth reusing.

This folder starts empty (or near-empty). It fills as you build real client projects and identify structures worth lifting.

## What goes in here

When you build something — a hero, a project showcase, a contact section, a navigation pattern — that you'd reach for again on a different project, extract it.

A pattern is **structural**, not visual. The styling will differ per project (different tokens, different copy). The *structure* is what gets captured.

## What does NOT go in here

- One-off components specific to a single client (those stay in the client project)
- Generic patterns (Hero, FeatureCard, FAQ accordion) — see ANTI-SLOP.md, those are slop
- Components from third-party libraries
- Components that are just shadcn primitives renamed

## File structure per pattern

Create a markdown file: `patterns/[pattern-name].md`. Use this structure:

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

- [client-project-1] — link or note
- [reference-site-from-vault] — note

## Code reference

Path to a clean implementation in a real project, or inline minimal HTML/CSS showing the bones.

## Notes

Lessons, anti-patterns to avoid within this pattern.
```

Commit message when adding: `patterns: add [pattern-name]`.

## Examples of patterns worth capturing (when you build them)

These don't exist yet, but here are the kinds of things that earn a place in this folder:

- **Type-led hero with no image** — for editorial/agency sites where the headline IS the hero
- **Asymmetric two-column with breakout** — narrower text on left, wide image breaking the right margin
- **Project deep-dive single-page** — agency case study format with intent, process, outcome, gallery
- **Marquee + dense info row** — moving headline above tightly-set client list
- **Sticky sidebar with scroll-narrative content** — long-form essay layout with persistent nav
- **Contact-as-form-letter** — form styled as letter with inline blanks instead of stacked fields
- **Footer-as-statement** — full-bleed footer with massive type instead of utility links

When you build one and like it, lift it here.

## Anti-pattern

Do not pre-populate this folder with hypothetical patterns. Patterns earn their place by being *used and proven* in real projects first. An empty folder that grows with real work is more valuable than a full folder of templates that nobody reaches for.
