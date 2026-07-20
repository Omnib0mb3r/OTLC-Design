# Reference Extraction Procedure

> Used during PROCESS.md Step 2. For each reference URL provided at intake, follow this procedure with Chrome DevTools MCP. Output to `[client-project]/references/[domain].md` using the schema below.

---

## Procedure

### 1. Navigate

Open the URL in Chrome via Chrome DevTools MCP. Wait for full load (network idle, fonts loaded).

### 2. Capture screenshots

Capture full-page screenshots at four widths:

- **375px**: mobile
- **768px**: tablet
- **1280px**: desktop standard
- **1920px**: large desktop

Save to `[client-project]/references/[domain]/screens/[width].png`.

**Tooling note (Chrome DevTools MCP):** Call `take_screenshot` with `fullPage: true` and a `filePath` ending in `.png`. Do **not** pass the `format` or `quality` arguments. Passing `format: "jpeg"` overrides the file extension and writes a `.jpeg` even when the path says `.png`. Default behavior is PNG full-page; trust it.

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

**Pick the rubric first.** Compare `document.documentElement.scrollHeight` to `window.innerHeight`:

- If `docHeight > viewport * 1.5` → **scrolling-document** rubric (default: use the section list below).
- If `docHeight ≈ viewport` → **experience-style** rubric (page is a fixed stage, not a scrolling doc; use the experience-style block below instead).

#### Scrolling-document rubric

For each major section type observed:

- **Hero**: Centered? Left? Asymmetric? Image-led? Type-only? Full-bleed? Overlapping content?
- **"What we do"**: Three-up cards? List? Numbered paragraphs? Interactive? Type-led?
- **"Showcase / Work"**: Grid? List? Carousel? Sticky sidebar with scroll narrative?
- **"About / Team"**: Photos? Type? Story-told?
- **"Contact"**: Form? Inline letter? Email link only?
- **"Footer"**: Utility? Statement? Full-bleed display type? Column-based?

Note column counts (12-col grid? 6-col? bespoke?) and whether breakouts beyond the main column happen.

#### Experience-style rubric

When the page is a fixed-viewport interactive (e.g. a Svelte/Three.js stage with no scroll), the section-by-section model does not apply. Capture instead:

- **Page model**: Fixed stage? Pannable canvas? Click-to-progress scenes? Multi-route experience?
- **Navigation model**: Implicit (hitzones / proximity) or explicit (menu overlay / keyboard)? Look for class names like `hitzone`, `MENU`, `wrapper`, `overAll`.
- **Scene / act progression**: Does the page reveal more content over time or interaction? Cross-reference with Font Loading API status (Step 8); lazy-loaded faces often correspond to later scenes.
- **Stage anatomy**: Foreground actors (custom cursor, moon, jet, etc.), middle layer (interactive hitzones), background (canvas/WebGL/video).
- **Aspect handling**: How does the experience adapt across the 4 breakpoints? Does it letterbox, recompose, or break?
- **Sound / motion / haptics**: Site may explicitly opt in or out (e.g. "experience without sound"). Note the choice.

Skip the conventional Hero/About/Contact/Footer section walk; it does not apply.

### 7. Extract motion patterns

**Force motion on first.** If the analyzer host has `prefers-reduced-motion: reduce` set (system accessibility setting on the developer's machine), most well-built sites will short-circuit their motion and render a static fallback. To get truthful motion data, override the media feature before observing:

```js
// Verify first
matchMedia('(prefers-reduced-motion: reduce)').matches
```

If `true`, use Chrome DevTools MCP `emulate` to override CSS media features and set `prefers-reduced-motion` to `no-preference`, then re-check. Only proceed once `matchMedia('(prefers-reduced-motion: reduce)').matches === false`. If the override fails, **flag this in the analysis output as reduced confidence on motion** rather than reporting a static-fallback observation as if it were the real design.

Then observe the page over 30 seconds with cursor movement and scroll:

- **Hover states**: Subtle? Exaggerated? Color? Translate? Reveal?
- **Scroll motion**: Parallax? Fades? Reveals? Sticky? Scrub? Pin?
- **Page transitions**: Hard load? Cross-fade? View transitions?
- **Cursor effects**: Custom cursor? Magnetic? Trail?
- **Loading state**: Skeleton? Loader? Snap?

Note easing feel (snappy? smooth? mechanical?). Guess at a cubic-bezier curve or describe it.

### 8. Note unusual / signature choices

**Run the programmatic checks first** (these are cheap and consistently high-signal; promote them ahead of visual hunting):

- **Font Loading API**: `Array.from(document.fonts).map(f => ({ family: f.family, weight: f.weight, style: f.style, status: f.status }))`. Mixed `loaded` / `unloaded` faces imply a multi-act type system where new faces appear as the user progresses. Self-hosted custom WOFFs (vs Google/Adobe) is itself a signal of taste.
- **Custom cursor**: `getComputedStyle(document.body).cursor === 'none'`. If true, the site is hiding the system cursor and rendering its own (look for a `.cursor` element or class).
- **Custom selection**: Stylesheet rule scan for `::selection`. Presence indicates the site brand-matches the highlight color.
- **Stack signal**: Class-name patterns on top-level wrappers reveal the framework cheaply: `lazyblock-*` / `wp-block-*` (WordPress + Lazy Blocks), `svelte-[hash]` (Svelte), `Component_name__[hash]` (Next.js CSS modules), `_a1b2c3` (CSS-in-JS like styled-components / Emotion). Capture once and note.
- **Fluid sizing**: Any sub-pixel computed font sizes (e.g. `53.4275px`) almost always indicate `clamp()` / `vw` fluid type. Look at h1/h2 sizes; if they are not whole pixels, the system is fluid.

Then visually scan for anything that signals deliberate design choice:

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

## Canonical extractor

Paste the script below verbatim into Chrome DevTools MCP `evaluate_script` after navigating + resizing to 1280×900. It returns one JSON blob covering Steps 3, 4, 5, 6 (page model), and 8 (programmatic checks). Steps 7 (motion) and 9 (Lighthouse) still require their own observation. **Do not reimplement the OKLCH math per session**: keep the canonical version below as the source of truth.

```js
() => {
  // sRGB → linear → OKLab → OKLCH (Björn Ottosson, https://bottosson.github.io/posts/oklab/)
  const parseColor = (str) => {
    if (!str) return null;
    const m = str.match(/rgba?\(([^)]+)\)/);
    if (!m) return null;
    const parts = m[1].split(/[\s,/]+/).filter(Boolean).map(Number);
    if (parts.length < 3) return null;
    const [r, g, b, a = 1] = parts;
    return { r: r/255, g: g/255, b: b/255, a };
  };
  const srgbToLinear = (c) => c <= 0.04045 ? c/12.92 : Math.pow((c+0.055)/1.055, 2.4);
  const cbrt = Math.cbrt;
  const rgbToOklch = (rgb) => {
    if (!rgb) return null;
    const r = srgbToLinear(rgb.r), g = srgbToLinear(rgb.g), b = srgbToLinear(rgb.b);
    const l = 0.4122214708*r + 0.5363325363*g + 0.0514459929*b;
    const m = 0.2119034982*r + 0.6806995451*g + 0.1073969566*b;
    const s = 0.0883024619*r + 0.2817188376*g + 0.6299787005*b;
    const l_ = cbrt(l), m_ = cbrt(m), s_ = cbrt(s);
    const L = 0.2104542553*l_ + 0.7936177850*m_ - 0.0040720468*s_;
    const A = 1.9779984951*l_ - 2.4285922050*m_ + 0.4505937099*s_;
    const B = 0.0259040371*l_ + 0.7827717662*m_ - 0.8086757660*s_;
    const C = Math.sqrt(A*A + B*B);
    let H = Math.atan2(B, A) * 180 / Math.PI; if (H < 0) H += 360;
    return `oklch(${(L*100).toFixed(1)}% ${C.toFixed(3)} ${H.toFixed(1)})`;
  };
  const fmtColor = (str) => {
    const rgb = parseColor(str);
    if (!rgb) return str;
    if (rgb.a < 1) return `${rgbToOklch(rgb)} / a=${rgb.a.toFixed(2)}`;
    return rgbToOklch(rgb);
  };

  // Type system
  const sampleSelectors = ['body','h1','h2','h3','h4','h5','p','a','small','blockquote','figcaption','li','button'];
  const seen = new Set();
  const typeRows = [];
  for (const sel of sampleSelectors) {
    for (const el of document.querySelectorAll(sel)) {
      if (!el.offsetParent && sel !== 'body') continue;
      const txt = (el.innerText || '').trim();
      if (sel !== 'body' && !txt) continue;
      const cs = getComputedStyle(el);
      const key = `${sel}|${cs.fontFamily}|${cs.fontSize}|${cs.fontWeight}`;
      if (seen.has(key)) continue;
      seen.add(key);
      typeRows.push({
        tag: sel, sample: txt.slice(0, 60),
        family: cs.fontFamily, size: cs.fontSize, weight: cs.fontWeight,
        lineHeight: cs.lineHeight, letterSpacing: cs.letterSpacing,
        color: cs.color, colorOklch: fmtColor(cs.color),
        textTransform: cs.textTransform,
      });
      if (typeRows.filter(r => r.tag === sel).length >= 2) break;
    }
  }

  // Color palette
  const bodyCs = getComputedStyle(document.body);
  const htmlCs = getComputedStyle(document.documentElement);
  const colors = {
    htmlBg:   { raw: htmlCs.backgroundColor, oklch: fmtColor(htmlCs.backgroundColor) },
    bodyBg:   { raw: bodyCs.backgroundColor, oklch: fmtColor(bodyCs.backgroundColor) },
    bodyText: { raw: bodyCs.color,           oklch: fmtColor(bodyCs.color) },
  };
  const link = document.querySelector('a[href]');
  if (link) { const cs = getComputedStyle(link); colors.link = { raw: cs.color, oklch: fmtColor(cs.color) }; }
  const button = document.querySelector('button, [class*="button" i], [class*="btn" i], a.cta, [class*="cta" i]');
  if (button) {
    const cs = getComputedStyle(button);
    colors.button = {
      bg:     { raw: cs.backgroundColor, oklch: fmtColor(cs.backgroundColor) },
      color:  { raw: cs.color,            oklch: fmtColor(cs.color) },
      border: cs.borderColor ? { raw: cs.borderColor, oklch: fmtColor(cs.borderColor) } : null,
    };
  }
  const sectionBgs = new Map();
  for (const tag of ['section','main','header','footer','article','aside','nav']) {
    document.querySelectorAll(tag).forEach(el => {
      if (!el.offsetParent) return;
      const bg = getComputedStyle(el).backgroundColor;
      if (bg && bg !== 'rgba(0, 0, 0, 0)') {
        if (!sectionBgs.has(bg)) sectionBgs.set(bg, { tag, oklch: fmtColor(bg), count: 0 });
        sectionBgs.get(bg).count++;
      }
    });
  }
  colors.sectionBackgrounds = Array.from(sectionBgs.entries()).map(([raw, v]) => ({ raw, ...v })).slice(0, 8);

  // Spacing samples
  const spacingSamples = [];
  for (const s of Array.from(document.querySelectorAll('section, main > div, main > article, body > div')).slice(0, 12)) {
    if (!s.offsetParent) continue;
    const cs = getComputedStyle(s);
    const r = s.getBoundingClientRect();
    spacingSamples.push({
      tag: s.tagName.toLowerCase(),
      cls: (s.className || '').toString().slice(0, 50),
      paddingTop: cs.paddingTop, paddingBottom: cs.paddingBottom, paddingLeft: cs.paddingLeft,
      width: Math.round(r.width), height: Math.round(r.height),
    });
  }
  const containers = Array.from(document.querySelectorAll('main, [class*="container" i], [class*="wrapper" i], [class*="content" i]'))
    .filter(el => el.offsetParent).slice(0, 6).map(el => {
      const cs = getComputedStyle(el);
      return { tag: el.tagName.toLowerCase(), cls: (el.className||'').toString().slice(0, 40),
               maxWidth: cs.maxWidth, width: Math.round(el.getBoundingClientRect().width), padding: cs.padding };
    });

  // Headings (helps narrate IA)
  const headings = Array.from(document.querySelectorAll('h1, h2, h3'))
    .filter(el => el.offsetParent).slice(0, 12)
    .map(el => ({ tag: el.tagName.toLowerCase(), text: (el.innerText||'').trim().slice(0, 80) }));

  // Programmatic signals (Step 8)
  const fontsLoaded = [];
  if (document.fonts) document.fonts.forEach(f => fontsLoaded.push({ family: f.family, weight: f.weight, style: f.style, status: f.status }));
  const customCursor = getComputedStyle(document.body).cursor;
  const hasSelectionRule = !!Array.from(document.styleSheets).some(ss => {
    try { return Array.from(ss.cssRules || []).some(r => r.selectorText && r.selectorText.includes('::selection')); } catch { return false; }
  });

  // Page model (Step 6 fork)
  const meta = {
    title: document.title, lang: document.documentElement.lang,
    viewport: { w: window.innerWidth, h: window.innerHeight, dpr: window.devicePixelRatio },
    docHeight: document.documentElement.scrollHeight,
  };
  const pageModel = meta.docHeight > meta.viewport.h * 1.5 ? 'scrolling-document' : 'experience-style';

  return {
    meta, pageModel, typeRows, colors, spacingSamples, containers, headings,
    fontsLoaded: fontsLoaded.slice(0, 30),
    motion: {
      bodyCursor: customCursor,
      hasSelectionRule,
      prefersReducedMotionMedia: matchMedia('(prefers-reduced-motion: reduce)').matches,
    },
  };
}
```

The output JSON drives the markdown schema below. Use `pageModel` to pick which Step 6 rubric you write up.

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

**Background:** oklch(98% 0.005 70), warm cream
**Foreground:** oklch(15% 0.02 250), near-black and slightly cool
**Muted:** oklch(50% 0.02 250)
**Border:** oklch(85% 0.01 250)
**Accent:** oklch(58% 0.18 240), saturated blue
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
- **Use the canonical extractor.** Do not reimplement the OKLCH math or the type/color/fonts probes per session. Paste the script in `## Canonical extractor` and use its JSON output.
- **Be honest about reduced confidence.** If `prefers-reduced-motion` could not be overridden, or if the page blocked extraction (login, geo, JS-heavy SPA needing waits), say so in the analysis. A flagged gap is worth more than a confident-sounding guess.
