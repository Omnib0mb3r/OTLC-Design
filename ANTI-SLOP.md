# ANTI-SLOP.md: durable rules

> 26 rules and growing. Add to this list every time slop slips through. Never delete a rule without an explicit rationale logged in `OTLC-Brainstorm.MD`.

These rules apply to every client project automatically. The `OTLC-Design` skill reads them at the start of work and enforces them throughout. They override defaults from any framework (Tailwind, shadcn, Next.js templates, etc.).

A rule that says "never X" can be broken if the user **explicitly** opts in for a specific project, with a logged reason. Default behavior is the rule.

---

## Type

### 1. Never use a default modular type scale.

Pick a specific ratio (1.2, 1.25, 1.333, 1.414, 1.5, 1.618, or 2.0) deliberately based on the project's voice. Tailwind's default `text-xs / text-sm / text-base / text-lg / text-xl` is an inconsistent scale that produces flat hierarchy.

**Why:** Modular scales are a 100-year-old typographic principle. Skipping them is the loudest signal of "AI default."
**How to apply:** Synthesize the scale in Step 3 from references. Author tokens. Reference tokens, not arbitrary sizes.

### 2. Never use a single font across the entire site.

Minimum: one display + one body. Optionally add mono for code or numbers. The display can be the same family at a different weight if budget is tight, but variation must be visible.

**Why:** Single-typeface sites read as undesigned unless they're done by a typographer who knows what they're doing. AI defaults are single-Inter.
**How to apply:** Pick pairings from the references. If references use one font, find the *expressive variation* (weight, italic, optical size) that gives texture.

### 3. Never use Inter as the only typeface unless the references demand it.

Inter is the default of defaults. It signals "I used the first option." Plenty of beautiful sites use Inter, but they pair it with something or treat it expressively.

**Why:** Visual sameness across the modern web. Same energy as "I used Bootstrap defaults."
**How to apply:** Look at references. If they use a serif, use a serif. If they use a weirder grotesk (Söhne, Neue Haas, GT America, ABC Diatype), pull a similar one.

---

## Color

### 4. Never use the default Tailwind palette.

`bg-blue-500`, `bg-gray-100`, `text-slate-700` are slop signals. Any designer audits the palette before approving.

**Why:** Tailwind defaults appear in every AI-built site. Instant recognition.
**How to apply:** Author colors in OKLCH. Build a custom 9-step neutral ramp + 1-2 accents per project.

### 5. Never use generic gradients.

Purple-to-pink, blue-to-cyan, the "sunset" gradient. These are 2020 SaaS defaults that aged into slop.

**Why:** A gradient is a strong design statement. Generic gradients are "I want a strong statement but did not pick one."
**How to apply:** If a gradient is right, build a specific one with intent (single hue with lightness shift, complementary, conic, mesh). Or skip gradients.

### 6. Never use pure white (#FFF) and pure black (#000) by default.

Cream, off-white, near-black, dark navy, near-charcoal: choose a specific neutral story. Pure white and pure black are harsh defaults.

**Why:** Real designers tune their neutrals. Pure values look unconsidered.
**How to apply:** Pull background and foreground from references. Convert to OKLCH. Use ~98% L for "white" backgrounds and ~12-18% L for "black" foregrounds unless deliberately contrasty.

---

## Layout

### 7. Never default to centered hero + headline + subhead + two pill buttons.

The single most overused layout in AI-built sites. Looks like a Vercel template every time.

**Why:** Maximum recognizability as slop.
**How to apply:** Look at references. Hero structures vary wildly: left-aligned, asymmetric, image-first, type-only, marquee, full-bleed video, no hero at all. Pick from references.

### 8. Never default to symmetric three-up feature card grids.

"Feature 1 / Feature 2 / Feature 3" cards with a Lucide icon, an h3, and a paragraph. Slop ground zero.

**Why:** Same recognizability problem as #7.
**How to apply:** What is the actual structure of "what we do" in the references? Often it's a list, a table, a numbered set of paragraphs, an interactive showcase, or a dense type-only block.

### 9. Never default to perfect symmetry.

Asymmetric layouts read as designed. Centered-everything reads as templated.

**Why:** Asymmetry signals deliberate composition.
**How to apply:** Use a real grid (12-col or fewer). Break out of it intentionally. Mix wide and narrow content blocks.

### 10. Never use the same border-radius value everywhere.

If everything is `rounded-xl`, the design has no rhythm. Either commit to a specific radius value used surgically, mix sharp and rounded with intent, or use no radius at all.

**Why:** Indiscriminate radius is a default. Considered radius is a choice.
**How to apply:** Audit references. Most professional sites use 0-2 radius values applied to specific element types, not all elements.

---

## Components

### 11. Never use Lucide / Heroicons / FontAwesome icons next to feature bullets.

Generic icon-next-to-text bullets are the most-recognized slop component on the modern web.

**Why:** Same problem as feature cards: every AI site has them.
**How to apply:** Either no icons (type-only feature lists), custom illustrative marks, or numbers/letters used typographically. If an icon set is required, use one with character (Phosphor "Duotone" weight, custom SVGs, or sourced glyphs).

### 12. Never use shadcn/ui or other off-the-shelf component kits for marketing/showcase sites.

Component kits are right for *applications*, where consistency is the goal. They are wrong for *marketing sites*, where distinctiveness is the goal.

**Why:** Every shadcn marketing site looks the same.
**How to apply:** Hand-build components for the project. They are usually 5-10 components, not a library.

### 13. Never use generic FAQ accordion / pricing tier cards / testimonial slider templates without earning them.

These exist in every template. They get reached for as filler. If a section is added because "every site has one," it is slop.

**Why:** Section presence should be driven by the brief, not the template.
**How to apply:** Each section must answer: does the audience need this? Is it the strongest way to answer? If no, cut.

### 14. Never use mystery-meat icon-only navigation on marketing sites.

Hamburger-only on desktop, icon-only nav without labels: these are app patterns, not marketing patterns.

**Why:** Marketing sites need labels for SEO and clarity.
**How to apply:** Text labels for primary nav. Icons can supplement, never replace.

---

## Motion

### 15. Never ship a marketing site with zero motion.

Even subtle motion (hover, focus, scroll-into-view fades, button press feedback) signals craft. Motion-less sites read as static templates.

**Why:** Motion is humanity. Its absence is uncanny.
**How to apply:** Minimum: hover transitions on interactive elements, scroll-reveal on hero/sections, focus rings that animate. Better: scroll-driven parallax, custom cursor, page transitions.

### 16. Never use easing curves that are not custom.

`ease-in-out` and Tailwind's transition defaults feel generic. Use cubic-bezier curves that match the brand voice (sharp/snappy vs. soft/heavy).

**Why:** Easing is the personality of motion.
**How to apply:** Pick 2-3 cubic-beziers in the tokens. Use them everywhere. Never `transition: all 200ms`.

---

## Glass / Effects

### 17. Never use glassmorphism by default.

`backdrop-filter: blur(...)` on every card was a 2021 trend. It now signals "AI built this in 2024." Use only if a reference deliberately calls for it and you can execute it well.

**Why:** Aesthetic peaked and declined. Now reads as cliché.
**How to apply:** Glass effects belong in deliberate moments (a hero overlay, a modal). Never as the base aesthetic.

---

## Copy

> Rules 18 and 19 are the short form. The full prose-slop system is the `anti-ai-writing` skill
> at [`skill-writing/SKILL.md`](skill-writing/SKILL.md): roughly 60 documented LLM tells covering
> vocabulary, sentence construction, content padding, and formatting, plus a false-positive guard.
> Invoke it whenever writing or reviewing any user-facing copy.

### 18. Never use generic AI-flavored copy.

Banned phrases: "Elevate your X", "Built for modern teams", "The future of Y", "Streamline your workflow", "Powered by intelligence", "Unlock the power of", "Take your X to the next level", "Reimagine your Z", anything with "seamlessly".

**Why:** These phrases are ChatGPT defaults. They mark a site as auto-generated immediately.
**How to apply:** Write specific copy. Use the client's actual offering, named features, real numbers, real names, specific benefits. If you don't know the specifics, ask.

### 19. Never ship lorem ipsum, placeholder copy, or filler in delivered work.

Real copy with names, dates, prices, jokes, locations. Placeholder text is for the build phase only.

**Why:** Placeholder copy is a "looks like a template" signal even if visuals are good.
**How to apply:** If the client has not provided copy, draft it from the brief. Mark drafts clearly. Never deliver with filler still in.

---

## Verification

### 20. Never deliver without verification gates passing.

Lighthouse Performance ≥ 90, Accessibility ≥ 95, Best Practices ≥ 90, SEO ≥ 90. Zero critical/serious axe violations. WCAG AA contrast minimum on body text (AAA preferred).

**Why:** Bad performance and a11y *feel* worse than they audit. Slow sites read as cheap. Inaccessible sites are unprofessional and legally risky.
**How to apply:** Step 5 of `PROCESS.md` is non-optional. Run the audits. Fix the failures. Then deliver. App-mode gates differ; see `APP-ADAPTATION.md` §5.

---

## Iconography

### 21. Never use emoji as iconography.

Emoji glyphs in feature lists, palette icons, button labels, or as primary affordances. They render inconsistently across platforms (Apple vs. Google vs. Windows vs. fallback fonts), drift from the brand's visual language, and read as filler.

**Why:** Inconsistent rendering, no brand control, looks like template padding. The omnibomber-site analysis surfaced this: emoji used as `tool-card-icon`, `lc-icon`, `dl-icon`, `proj-card-vis .emo`. Cannot be brand-controlled and reads as default.
**How to apply:** Use SVG icons (custom, Lucide, Phosphor, Heroicons depending on context per ANTI-SLOP rule 11). Use typographic glyphs (numbers, letters, mono characters). Use no icon at all. Never emoji.

---

## Legibility

### 22. Never set body or label content below 12px.

Sub-12px text in body content fails legibility on retina at normal viewing distance and is an accessibility risk. The omnibomber-site analysis surfaced this: labels at 8-9.6px (`0.5rem` to `0.6rem`).

**Why:** Below the legibility floor for body text. WCAG 1.4.4 expects users to scale to 200% without loss; sub-12px breaks before that target.
**How to apply:** Body content: ≥ 14px. Labels and supporting text: ≥ 12px. Smaller is acceptable only for ornamental display elements that are not load-bearing for comprehension (e.g., a tiny version number in a footer corner). App UI may use 11-13px labels with appropriate weight/contrast; see APP-ADAPTATION rule 22.

---

## Personal-aesthetic chrome on client work

### 23. Never import the owner's personal-aesthetic chrome into client work.

Personal-brand decorative chrome (cyberpunk telemetry panels, custom cursor with `cursor: none`, glitch effects, terminal/operator panels, animated bars labeled CPU/MEM, etc.) belongs on the owner's projects only. Importing it into a client project means delivering the wrong brand.

**Why:** A client paid for *their* brand. Decorative chrome from the developer's personal aesthetic is the developer leaking through.
**How to apply:** When in customer mode, do not pull patterns from the owner-brand profile. Owner-brand may inform the developer's instincts (font pairing, anti-slop reflexes) but never overrides client direction. If a client deliberately wants an aesthetic that overlaps with the owner's personal brand, they get a derivative, not a copy.

---

## Custom cursor

### 24. Never replace the OS cursor as a default.

`cursor: none` plus a custom cursor (dot + lagging ring, etc.) is a deliberate use only, never a default. It breaks accessibility (resize handles, text caret, link cues), increases motion load, and is the most common "designer portfolio template" trick of the last few years.

**Why:** Breaks OS expectations and accessibility affordances. Reads as template-default when overused.
**How to apply:** Custom cursor is allowed when the project's voice genuinely calls for it (the owner's personal site qualifies; it's a brand signature). Never on customer work unless explicitly briefed. Never on apps. When using, always preserve native cursor functionality on inputs and resize handles.

---

## Contrast on dark surfaces

### 25. Never copy a reference's muted-text lightness without checking it clears 4.5:1 for app body text.

A marketing site's muted body color (Linear's `oklch(62%)` on near-black, for example) reads as designed because the marketing site is not gating on WCAG and its body text is at 14-16px. An app shell IS gating on WCAG (per ANTI-SLOP rule 20 + APP-ADAPTATION's a11y=100 gate) and contains 11-13px labels. Copying the reference's L value 1:1 will silently fail the a11y gate.

**Why:** The DevNeural Hub design pass on 2026-05-03 lifted Linear's `oklch(62% 0.012 258)` muted directly. Lighthouse caught four `text-txt3` instances at 3.1-3.2:1 against `oklch(11.5%)` bg. Token bumped to `oklch(70% 0.014 258)` to clear 4.5:1. Caught only because the gate ran; could have shipped.

**How to apply:**
- Floor for muted text on dark canvas (oklch L < 20%): `--c-fg-muted` ≥ oklch(70%).
- Floor for muted text on light canvas (oklch L > 90%): `--c-fg-muted` ≤ oklch(40%).
- Always run the contrast check **before** authoring the token, not as a post-hoc fix. The reference's L is a starting point, not a target.
- If a reference's restraint genuinely depends on a sub-floor muted (e.g., decorative ornament), put it on a separate token (`--c-fg-ornament` or similar) and never use it for body or label text.

---

## Runtime hygiene

Rules about how the running app behaves on the user's machine, not how it looks. Slop here is invisible during demos and very visible during actual use.

### 26. Never spawn a child process on Windows without `windowsHide: true`.

Every Node `child_process.spawn` / `spawnSync` / `execSync` / `exec` call on Windows MUST pass `windowsHide: true`. Without it, CreateProcess allocates a visible console window for each subprocess, which flashes onto the user's desktop.

**Why:** DevNeural dashboard polling spawned `powershell -NoProfile ...` every 4 seconds (drive enumeration in `system-metrics.ts`) and `execSync` per monitored service every 8 seconds (`services.ts`), both without `windowsHide`. With the dashboard tab open, the user saw roughly **15 powershell window flashes per minute** while sitting idle. Took multiple wrong diagnoses (blamed unrelated plugins) before the user pushed back hard enough to find the actual cause. The symptom was subtle (windows opened and closed faster than the user could see what they were) and dismissed as someone else's problem.

**How to apply:**
- Every `child_process.spawn(...)`, `spawnSync(...)`, `execSync(...)`, `exec(...)` call site: include `windowsHide: true` in the options object. There are no exceptions for "but it's just one call"; call counts compound (4s polling × 15min/dashboard-session × 5 sessions/day = thousands).
- Long-running detached processes: combine `windowsHide: true` + `detached: true` + redirected `stdio`. `detached: true` alone allocates a fresh console; `windowsHide` is what hides it.
- Scheduled tasks (Windows Task Scheduler): action args must include `-WindowStyle Hidden` AND `-NonInteractive` for PowerShell scripts. Without `-WindowStyle Hidden`, the task host briefly shows the console.
- Hooks where a parent harness controls spawn (e.g., Claude Code hooks): wrap the command in a `wscript.exe` + VBS shim. `WshShell.Run cmd, 0, False` reliably hides whatever the parent passes through. Defense in depth is appropriate here because the parent's spawn behavior is not under your control.
- Audit-before-merge: `grep -rn 'spawn\|execSync\|spawnSync' src/` and verify every result has the flag. Add a lint rule if the project has eslint.
- Cross-platform code: the option is ignored on POSIX, so always include it; never gate behind `if (process.platform === 'win32')`.

### 27. Always give a multi-page site real, separate pages, never one long scroll behind an inline-script blob.

**Why:** onthelevelconcepts.com originally shipped as a single ~91KB HTML file with the entire site behavior inlined as one giant `<script>`. Reputation/AV crawlers (Microsoft SmartScreen / Edge) flagged the live domain as malware because a mostly-inline-JS page reads like an obfuscated payload. It also made the "back button" non-functional (fake in-page nav). The fix was a full Astro rebuild into real routes (`/projects`, `/lab`, `/media`, `/about`, `/contact`, `/privacy`, `/training`) with all behavior in an external, content-hashed `/scripts/site.js` and a CSP of `script-src 'self'` (zero inline script). After that: A11y 100, Perf ~99, SEO 100, and the malware flag cause removed.

**How to apply:**
- For any site with more than one section of content, build real pages (separate routes), not one long single-file scroll.
- Use a static multi-page generator (Astro is the owner default) with View Transitions for the SPA feel without faking navigation.
- Every script and dataset lives in an external file, content-hash versioned, referenced with a normal `<script src>`.
- Target zero inline `<script>` and zero inline `on*` handlers so the page can ship a strict CSP (`script-src 'self'`).
- One clear concern per page.
- Real browser history (real `<a href>` to real routes) so Back/Forward work natively.
- This is the professional structure a site developer ships; a single inline-JS blob is both a slop signal and a reputation-filter false-positive magnet. Cross-reference `STACK-DECISIONS.md` "Shipping hygiene (reputation-safe)".

---

## Accessibility structure

Rules about the document's semantic outline, not its visuals. Invisible on screen, loud to a screen reader and to Lighthouse/axe.

### 28. Never skip a heading level; ship a sequential heading outline on every page.

One `<h1>` per page, then `h2`, then `h3`, never jumping `h1` straight to `h3` or `h2` to `h4`. The visual size of a heading is a CSS decision; the tag is a structure decision, and they are set independently.

**Why:** the onthelevelconcepts.com rebuild styled section labels and card titles by eye, so several pages jumped `h1` to `h3` (and the training page `h2` to `h4`). Lighthouse/axe `heading-order` failed and mobile accessibility dropped to 98 on those routes. A screen-reader user navigating by heading hits a gap where a level vanishes. The home page, which happened to nest correctly, scored 100; the difference was purely the outline.

**How to apply:**
- Exactly one `h1` per page (the page title).
- The first content heading after the `h1` is an `h2`. Descend one level at a time.
- A card grid with no visible section title still needs a heading in the tree: add a visually hidden one (`.sr-only { position:absolute; width:1px; height:1px; clip:rect(0 0 0 0); ... }`) so the outline is complete without changing the design.
- Decouple size from level: if an `h2` must look small, set its `font-size` in CSS. Do not down-tag it to `h4` to make it small.
- Verify against the BUILT HTML: extract the `<h1>`..`<h6>` sequence per page and confirm no level is skipped. Do this per route, not just the home page.

## Assets and performance

### 29. Never ship an image whose intrinsic size dwarfs its display size, and always declare `width`/`height` matching the true aspect ratio.

The file's real pixels should be about the display size (at most ~2x for retina), and the `width`/`height` attributes must describe the image's actual proportions.

**Why:** the onthelevelconcepts.com hero shipped `michael-collins.jpg` at **8179 x 6336 (9 MB)** to fill a 420px-wide slot, with `width="440" height="520"` attributes that did not match the real 1.29 ratio. Lighthouse flagged `image-aspect-ratio` (distortion / layout-shift risk) and it was a multi-megabyte download for a thumbnail. Re-encoding to 880 x 682 (~86 KB) with correct attributes cleared the flag and cut the transfer by 99%.

**How to apply:**
- Resize the source to roughly 2x the largest CSS display width, then compress (progressive JPEG or WebP/AVIF, quality ~80). A 400px slot does not need an 8000px file.
- Set `width` and `height` attributes to the encoded image's true pixel ratio, and let CSS scale with `height: auto`. Correct attributes reserve the right box and prevent CLS.
- Never let mismatched legacy attributes (a portrait `440x520` on a landscape file) survive a redesign.
- Verify: Lighthouse `image-aspect-ratio` passes and no single image dominates the transfer size.

### 30. Never let the bundler inline fonts (or other assets) as `data:` URIs under a strict CSP.

Build tools inline small assets as `data:` URIs by default. A `data:font/woff2` violates a strict `font-src 'self'`, and the browser silently drops that font subset.

**Why:** on onthelevelconcepts.com, Vite inlined a small `@fontsource` woff2 subset (under its 4 KB limit) as a `data:font/woff2` into one page's CSS. The site's CSP was `font-src 'self'`, so the browser blocked it and that subset never loaded, logging a console error that also dinged Best Practices. The fix was forcing every woff2 to stay an external, content-hashed file.

**How to apply:**
- Set the bundler's inline threshold to exclude fonts (Vite: `build.assetsInlineLimit` as a function returning `false` for `.woff2`/`.woff`), so fonts are always external and cacheable.
- Keep the CSP strict (`font-src 'self'`) rather than widening it to `data:` to paper over inlining; external fonts are better for caching anyway.
- If a `data:` asset is genuinely intended, the CSP must explicitly allow that scheme for that directive, decided deliberately, not by bundler default.
- Verify: no `data:font` in the built output, and no CSP font/console errors on load.

### 31. Always ship link-preview metadata with a composed OG card on every live site.

Every site that goes live gets Open Graph tags AND a purpose-composed preview image, not a raw photo or a missing card. Links get shared in text threads and group chats before anyone sees the site; the preview card IS the first impression.

**Why:** the John Simms family deck (2026-07-23) shipped first with a raw hero photo as og:image. A composed 1200x630 card (hero image + scrim + display-type title + eyebrow + "Prepared by" byline, matching the site's tokens) reads as designed in the chat thread instead of accidental. Client-facing links live or die in iMessage/WhatsApp previews.

**How to apply:**
- Required tags: `og:title`, `og:description`, `og:type`, `og:url`, absolute-URL `og:image`, `og:image:width`/`og:image:height`/`og:image:alt`, `twitter:card: summary_large_image`, `twitter:image`.
- Compose the card as a small HTML page using the project's own tokens and fonts (hero image, scrim, title, eyebrow, byline), screenshot it at 1200x630 (or proportional), ship the capture as a static asset. Do not ship the template page.
- The og:image URL must be absolute, so it is set after the production URL exists; add it to the deploy checklist, not the build checklist.
- Preview caches are sticky per chat thread: verify in a fresh thread or with a fresh recipient after changing the card.

---

## How to add to this file

When a slop pattern slips through (you noticed it in delivered work, or the user flagged it):

1. Find the right category above.
2. Append a new numbered rule. Title it as "Never X" or "Always Y".
3. Include `**Why:**` (the reason, typically a specific incident or aesthetic principle).
4. Include `**How to apply:**` (the tactical implementation).
5. Commit with message `anti-slop: <short rule summary>`.

The list keeps growing. That's the point.
