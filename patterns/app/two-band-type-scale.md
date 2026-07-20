# Two-band type scale

## Intent

Replace a single continuous modular ratio with two distinct ratios: a tight body band (1.143-1.222) and a separate display band that uses dramatic jumps (1.4-1.6× from h2 to h1). The body band stays uniform for label/caption/body density; the display band creates impact moments for empty states, daily-brief headlines, and hero panels without inflating the whole hierarchy.

Solves the "everything-flat" problem of one-ratio scales (which give either flat hierarchy or oversized body text) and the "showy-everywhere" problem of theatrical scales (which look like marketing voices stuffed into an app).

## When to use

- Information-dense application shells where body density matters (dashboards, ops consoles, file browsers, command surfaces)
- Apps with explicit "brief", "headline", or empty-state moments where one or two large surfaces need to dominate, but the rest of the chrome stays uniform
- Internal apps where you want some narrative texture (a "Good morning, [name]" moment) without the whole UI shouting
- Any place where a single continuous ratio would either bloat the body or flatten the display

## When NOT to use

- Pure data tools where every cell needs the same density (use a single tight ratio instead, OpenStatus-style)
- Marketing sites (the display band's job is already done by hero+section structure; one continuous ratio plus structural rhythm carries it)
- Customer-app surfaces where consistency is the goal and individual moments shouldn't stand out (use a single ratio with weight/color carrying hierarchy)

## Structural sketch

```
body band, ratio ~1.143-1.222 (tight):

  --fs-11 ─┐
  --fs-12  │  consistent rhythm
  --fs-13  │  hover ≈ +1px
  --fs-14  │  body baseline
  --fs-16  │
  --fs-18 ─┘

display band, custom jumps (no continuous ratio):

  --fs-22  ┐ h3 panel heading        (1.222× from 18)
  --fs-28  │ h2 section heading      (1.273× from 22)
  --fs-40  │ h1 page / brief headline (1.429× from 28)  ← display jump starts here
  --fs-56  ┘ display / hero only     (1.4×    from 40)
```

Letter-spacing scales with size:
- body band: `--ls-soft (-0.011em)` or normal
- display band 22-28: `--ls-snug (-0.022em)`
- display band 40-56: `--ls-tight (-0.04em)`

## Variations

- **Three-band variant:** for apps with both "panel chrome density" and "data density" (spreadsheet inside a panel), insert a sub-body band of `--fs-9 / --fs-10 / --fs-11` for cell text. Keep the rule that body band is internally consistent.
- **Mono inside body band:** mono characters at the same px size as their sans neighbors look ~1px smaller because of optical character width. Bump mono `font-size` by ~1px relative to body to optically match (e.g., body 14 + mono 15 with same baseline). Or use a tabular sans (Inter `tnum`) and skip the optical correction.
- **Display band weight discipline:** keep display weight in a narrow range (e.g., 510-680). A continuous weight scale across both bands is what makes a "two-band" feel intentional rather than scrappy. Linear uses 510 across the display band; Vercel uses 600. Pick one stance.

## Reference uses

- [linear.app](https://linear.app): body band ~1.143 (13/15/20), display jump 40 → 64. Weight 510 across.
- [DevNeural Hub](../../): body band 11/12/13/14/16/18 (~1.143 average), display band 22/28/40/56 with custom jumps. Weight 560 (between Linear's 510 and Vercel's 600).
- [vercel.com/docs](https://vercel.com/docs): wider variant (1.5 ratio) but same two-band structure: 14 body / 24 h2 / 40 h1.

## Code reference

`C:\dev\Projects\DevNeural\08-dashboard\mockup\tokens.css` (the `--fs-*` block and the tailwind `fontSize` mapping in `08-dashboard/mockup/index.html`).

Minimal token shape:

```css
:root {
  /* body band */
  --fs-11: 11px;
  --fs-12: 12px;
  --fs-13: 13px;
  --fs-14: 14px;
  --fs-16: 16px;
  --fs-18: 18px;
  /* display band */
  --fs-22: 22px;
  --fs-28: 28px;
  --fs-40: 40px;
  --fs-56: 56px;
  /* letter-spacing scales with band */
  --ls-soft:  -0.011em;
  --ls-snug:  -0.022em;
  --ls-tight: -0.04em;
}
```

## Notes

- Anti-pattern: extending the display band into 64/72/96 inside an app shell. Above 56px the display starts feeling marketing-like rather than app-internal. Cap at 56px for app surfaces; reserve 64+ for the rare empty-state-as-art moment.
- Anti-pattern: using the body band's ratio inside the display band. If h1 is 1.143× of h2, the hierarchy collapses. Display band exists specifically to break the body band's rhythm.
- The two-band approach works because body density and display impact are *different problems*. A single ratio assumes they aren't. They are.
