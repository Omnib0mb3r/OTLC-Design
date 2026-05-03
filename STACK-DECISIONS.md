# STACK-DECISIONS.md — When to Use Which Stack

> Stack does not determine if a site is beautiful. Taste does. Pick the simplest stack that gets the job done; complexity is overhead the user pays forever.

## The default decision tree

```
Is it an interactive application (real-time, dashboard, editor, multi-step
state, drag-drop, complex form validation, authenticated session)?

├── YES → Next.js + React (only when actually needed)
│
└── NO → Is it a content site (5+ pages, blog, case studies, docs, dynamic
         routing for content collections)?

         ├── YES → Astro
         │
         └── NO (one-pager, simple multi-page marketing, portfolio, showcase)
              → Plain HTML/CSS/JS + Vite
```

---

## Plain HTML/CSS/JS + Vite

**Use when:**
- One-pager (most landing pages, portfolios, single-purpose marketing sites)
- Simple multi-page where each page is structurally different (3-5 pages, no shared content collection)
- Showcase/portfolio sites
- Microsites for campaigns, events, single products
- Anything where the build is design-led and content rarely changes

**Why this is the default:**
- Zero framework overhead — every choice is yours
- Hardest stack to make slop with (no defaults to inherit)
- Fastest possible runtime
- Trivial to deploy anywhere
- No build complexity to debug

**Stack:**
- HTML (semantic, hand-written)
- CSS (modern: cascade layers, container queries, OKLCH, view transitions, anchor positioning where supported)
- JS (vanilla, ESM, no framework)
- Vite for dev server (HMR, fast builds, optimization)
- Optional: GSAP or Motion One for animation; lenis for smooth scroll

**Deploy:** Vercel, Netlify, Cloudflare Pages — all work, all free.

---

## Astro

**Use when:**
- Content site with 5+ pages
- Blog, case studies, docs, portfolio with many works
- Need content collections (typed markdown/MDX)
- Need a few interactive islands (e.g., a modal, a search input) but the rest is static
- Want to use multiple frameworks selectively (React for one component, Svelte for another) without paying SPA tax

**Why Astro over Next:**
- Ships near-zero JS by default (Lighthouse perf is automatic)
- Content collections are excellent for blog/case-study patterns
- Component model is HTML-first (less impedance than React for design work)
- Islands architecture means you only pay for interactivity where it exists
- Build output is mostly static HTML, deployable anywhere

**Stack:**
- Astro (current major version)
- Astro content collections for any structured content
- Vanilla CSS or Tailwind (your call)
- React/Svelte/Vue islands only where needed
- View Transitions API via Astro's built-in support

**Deploy:** Vercel, Netlify, Cloudflare Pages, anywhere static.

---

## Next.js + React

**Use when:**
- It is an actual application, not a site
- Multi-step interactive flows with shared client state
- Real-time features (websockets, server-sent events, live data)
- Authentication / authorization with session-aware UI
- In-browser editor, dashboard, complex form with cross-field validation
- Server actions, server components, edge functions are core to the requirement
- Client has explicitly mandated React

**Why Next over Astro for apps:**
- React's component model + state management ecosystem is right for stateful UIs
- Server components, streaming, and edge runtimes are the modern standard for app-shaped products
- The React ecosystem (TanStack, Radix primitives, etc.) is unmatched for complex interaction

**Why NOT to use Next:**
- For marketing/showcase sites, Next adds significant complexity (hydration, RSC concerns, SSR/SSG decisions, larger bundles) for negligible benefit
- The "Next + Tailwind + shadcn" default look is the visual signature of AI slop
- Build complexity scales with project; debugging takes longer

**Stack:**
- Next.js (App Router, current major version)
- React (current major version)
- TypeScript (always for apps)
- Tanstack Query for server state
- Radix primitives or hand-built for UI primitives (NOT shadcn defaults — see ANTI-SLOP rule 12)
- Custom CSS architecture (cascade layers + tokens, NOT Tailwind defaults — see ANTI-SLOP rule 4)

**Deploy:** Vercel (native), or self-host with Node.

---

## What we do NOT use

- **Create React App** — deprecated, replaced by Vite or Next
- **Gatsby** — superseded by Next/Astro for content sites
- **WordPress / Webflow / Squarespace / Wix** — out of scope for code-built sites
- **Framer (no-code)** — out of scope; Framer the React library is fine if needed
- **Generic site builders** — none

## What we conditionally use

- **Tailwind CSS** — fine *if* used with custom token theme (not defaults). Otherwise it leaks slop colors and spacing. Default for design-system: vanilla CSS with cascade layers.
- **shadcn/ui** — only for *applications* where consistency wins, never for marketing. See ANTI-SLOP rule 12.
- **GSAP** — premium animation. Use when motion is significant. Free for non-commercial; commercial license for client work.
- **Motion One / Framer Motion** — lighter animation libraries. Motion One for vanilla, Framer Motion for React.
- **Lenis** — smooth scroll. Add only when the design calls for it; do not impose smooth scroll on every site.
- **Lottie** — for designer-authored animations. Only when an animator delivers Lottie files.

---

## How to override

If a client mandates a stack (corporate WordPress, mandated Webflow, internal React framework), respect the mandate. Document the override in the project's `BRIEF.md`. The anti-slop rules still apply within whatever stack.

If you want to try a new stack experimentally (Solid, Qwik, HTMX), discuss it with the user *before* the project, not during. Stack changes mid-project are expensive.
