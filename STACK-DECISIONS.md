# STACK-DECISIONS.md: when to use which stack

> Stack does not determine if a site is beautiful. Taste does. Pick the simplest stack that gets the job done; complexity is overhead the user pays forever.

## The default decision tree

The OTLC-Design skill's branch question (Customer site / Customer app / Internal site / Internal app) maps to stack defaults:

```
Branch resolves to APP (customer or internal)?
│
├── YES (web app) → Next.js + React + TypeScript + shadcn (see APP-ADAPTATION.md)
├── YES (desktop app) → C# + .NET WPF, Tauri, or Electron (rare, project-driven)
│
└── NO (site) → Is it a content site (5+ pages, blog, case studies, docs)?
         │
         ├── YES → Astro
         │
         └── NO (one-pager, simple multi-page marketing, portfolio, showcase)
              → Plain HTML/CSS/JS + Vite (the owner's preferred default for
                 single-file deployable sites)
```

For desktop / native app contexts (e.g., the stream-deck WPF tray utility), the web stack tree does not apply: pick the appropriate native stack for the platform. The skill's process still applies (intake, anti-slop, verification, post-mortem).

---

## Plain HTML/CSS/JS + Vite

**Use when:**
- One-pager (most landing pages, portfolios, single-purpose marketing sites)
- Simple multi-page where each page is structurally different (3-5 pages, no shared content collection)
- Showcase/portfolio sites
- Microsites for campaigns, events, single products
- Anything where the build is design-led and content rarely changes

**Why this is the default:**
- Zero framework overhead: every choice is yours
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

**Deploy:** Vercel, Netlify, Cloudflare Pages (all work, all free).

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

## Next.js + React (web app default)

**Use when (this is the default for web apps):**
- The branch question resolves to Customer app or Internal app (web)
- Multi-step interactive flows with shared client state
- Real-time features (websockets, server-sent events, live data)
- Authentication / authorization with session-aware UI
- In-browser editor, dashboard, complex form with cross-field validation
- Server actions, server components, edge functions are core to the requirement
- Client has explicitly mandated React

**Why Next is the app default:**
- React's component model + state management ecosystem is right for stateful UIs
- Server components, streaming, and edge runtimes are the modern standard for app-shaped products
- The React ecosystem (TanStack Query, Radix primitives, shadcn/ui) is unmatched for complex interaction
- For app mode, the conventional choice serves users better than the distinctive choice (see APP-ADAPTATION.md)

**Why NOT to use Next for marketing sites:**
- Next adds significant complexity (hydration, RSC concerns, SSR/SSG decisions, larger bundles) for negligible benefit
- The "Next + Tailwind + shadcn" default look is the visual signature of AI slop **for marketing**
- For apps, that same conventional look is *correct* (see APP-ADAPTATION.md anti-slop inversion)

**Stack:**
- Next.js (App Router, current major version)
- React (current major version)
- TypeScript (always for apps)
- Tanstack Query for server state
- Zustand or Jotai for client state (when needed beyond server state)
- shadcn/ui (or Radix primitives + custom) for component layer, appropriate for apps per APP-ADAPTATION rule 12
- Tailwind CSS with project token theme (still custom theme; defaults are lazy)
- NextAuth / Clerk / Auth.js / custom for auth
- Prisma + Postgres typical for ORM/data
- Resend / Postmark / Loops for email (customer apps)

**Deploy:** Vercel (native), or self-host with Node.

---

## Native / Desktop apps

For desktop or platform-native apps (e.g., the stream-deck WPF tray utility), pick the right native stack for the platform; the web stack tree does not apply.

| Platform | Recommended | Examples |
|----------|-------------|----------|
| Windows desktop | **C# + .NET WPF** (or WinUI 3 for newer) | stream-deck |
| Cross-platform desktop | **Tauri** (Rust + web frontend) or Electron (when native size matters less) | most cross-platform tools |
| macOS native | Swift + SwiftUI | Apple-only tools |
| iOS / Android | Native (Swift / Kotlin) or React Native / Flutter | mobile apps |

The OTLC-Design process still applies (intake, anti-slop, verification, post-mortem) regardless of platform. APP-ADAPTATION.md rules apply where relevant (some web-specific rules like Lighthouse don't apply to native; replace with native equivalents).

## What we do NOT use

- **Create React App**: deprecated, replaced by Vite or Next
- **Gatsby**: superseded by Next/Astro for content sites
- **WordPress / Webflow / Squarespace / Wix**: out of scope for code-built sites
- **Framer (no-code)**: out of scope; Framer the React library is fine if needed
- **Generic site builders**: none

## What we conditionally use

- **Tailwind CSS**: fine *if* used with custom token theme (not defaults). Otherwise it leaks slop colors and spacing. Default for design-system: vanilla CSS with cascade layers.
- **shadcn/ui**: only for *applications* where consistency wins, never for marketing. See ANTI-SLOP rule 12.
- **GSAP**: premium animation. Use when motion is significant. Free for non-commercial; commercial license for client work.
- **Motion One / Framer Motion**: lighter animation libraries. Motion One for vanilla, Framer Motion for React.
- **Lenis**: smooth scroll. Add only when the design calls for it; do not impose smooth scroll on every site.
- **Lottie**: for designer-authored animations. Only when an animator delivers Lottie files.

---

## How to override

If a client mandates a stack (corporate WordPress, mandated Webflow, internal React framework), respect the mandate. Document the override in the project's `BRIEF.md`. The anti-slop rules still apply within whatever stack.

If you want to try a new stack experimentally (Solid, Qwik, HTMX), discuss it with the user *before* the project, not during. Stack changes mid-project are expensive.

---

## Shipping hygiene (reputation-safe)

Learned from a live incident (2026-07): a page shipped as ~73% one inline `<script>` blob (a JS engine plus a large dataset inlined into the HTML) got the whole domain flagged and blocked by a major mobile carrier reputation filter. Google Safe Browsing and Norton were clean the entire time, so it was a heuristic/category flag, not malware. A real user was blocked from the live site. Rules for anything that goes live:

- **Keep JS and large data external.** Ship scripts and datasets as separate `.js` files, cache-busted with a content hash (`?v=<hash>`). Never inline a large engine or dataset into the page HTML. A page that is mostly one giant inline script reads like an obfuscated payload to reputation crawlers and is a false-positive magnet. Inlining is acceptable *only* for a deliberately offline, self-contained artifact, never for the hosted site.
- **Force HTTPS + security headers.** Host config (`.htaccess` on Apache/cPanel): 301 HTTP→HTTPS with a proxy-safe double condition so it cannot loop (`RewriteCond %{HTTPS} off` **and** `RewriteCond %{HTTP:X-Forwarded-Proto} !https`), plus HSTS, X-Content-Type-Options, X-Frame-Options, Referrer-Policy. Skip CSP only when the page ships intentional inline script/style (a broken CSP is worse than none).
- **Cache contract.** If `.js`/data cache long (`max-age`) while HTML is `no-cache`, version the data URLs on any shell/data-contract change, or returning browsers run the new shell against day-old cached data (silent breakage).
- **Cloudflare-migration gotcha.** Moving a site off Cloudflare leaves `__cf_email__` / `/cdn-cgi/l/email-protection#HEX` obfuscated emails whose decoder script now 404s: the emails render broken *and* the 404 trips security scanners. Decode `data-cfemail` (first hex byte = XOR key, remaining bytes XORed with it) back to real `mailto:` links and delete the dead `cdn-cgi/.../email-decode.min.js` script.
