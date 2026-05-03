# APP-ADAPTATION.md — Adaptation for Apps (vs Marketing Sites)

> Loaded by the `OTLC-Design` skill when the intake branch resolves to **Customer app** or **Internal app**. Adapts intake, anti-slop rules, stack defaults, and verification gates to the app context (where users do tasks, not read content).
>
> A subsection at the bottom — **Customer-app tightening** — applies additional rules when the app is for paying customers (vs internal employees).

## When this applies

- Customer app (B2B SaaS dashboard, customer portal, end-user web app, customer-facing web tool)
- Internal app (your own tools, admin panel, dashboard, ops utility)

For marketing/showcase sites, this file is **not loaded**.

## Core premise

Apps have different design priorities than marketing sites:

| Marketing site | App |
|----------------|-----|
| Distinctiveness wins (you should remember this site) | Consistency wins (you should remember the function, not the chrome) |
| Visitors *read* content | Users *do* tasks |
| Aesthetic is the product | Function is the product; aesthetic supports it |
| Defaults look templated | Defaults look *correct* |
| Rules push against templates | Rules embrace templates where they're appropriate |

Most marketing anti-slop rules **invert** for apps. The full inversion table is in §3 below.

## Intake additions

Adds these questions to the relevant intake:

1. **Primary user role(s) and usage frequency** — daily power user, weekly viewer, occasional admin?
2. **Core workflows / tasks supported** — top 3 verbs the app enables (create, configure, monitor, etc.)
3. **Data volume / scale** — 10 records or 10 million? Affects table design, pagination, search.
4. **Auth model** — none / password / magic link / SSO / OAuth?
5. **Permissions model** — single user / RBAC / per-org / per-resource?
6. **Required states** — loading, empty, error, partial-data, offline. Each must be designed.
7. **Browser/device targets** — desktop-only fine, mobile required, specific OS?
8. **Existing system consistency** — does it sit alongside other internal tools? Match a design system?

## Intake removals / relaxations

These become optional or irrelevant:

- "References client liked aesthetically" → optional, often irrelevant
- "Brand voice" → becomes "tone of system messages" (clear, helpful, functional)
- "Audience" → becomes "user roles" (people who do things, not visitors)

## ANTI-SLOP rule adaptation table

The big one. Most marketing rules invert because apps need *consistency and learnability*, not distinctiveness:

| # | Marketing rule | App version |
|---|---|---|
| 1 | Never use default modular type scale | **Still applies** — type hierarchy still matters in app UI |
| 2 | Never single typeface | **Relaxed** — single sans-serif (Inter / Geist) is fine for apps |
| 3 | Never Inter as only typeface | **Relaxed** — Inter is the right default for app UI |
| 4 | Never default Tailwind palette | **Inverted** — Tailwind/shadcn defaults are fine; consistency > distinction |
| 5 | Never generic gradients | **Still applies** — no decorative gradients in apps |
| 6 | Never pure white/black | **Relaxed** — system whites/blacks are fine |
| 7 | Never centered hero + 2 pill buttons | **Irrelevant** — no marketing hero |
| 8 | Never symmetric 3-up cards | **Inverted** — dense grids/cards are correct for dashboards |
| 9 | Never perfect symmetry | **Inverted** — predictability matters |
| 10 | Never same radius everywhere | **Relaxed** — single consistent radius is fine |
| 11 | Never Lucide bullets | **Inverted** — Lucide/Heroicons are correct for app affordances |
| 12 | Never shadcn/ui | **Inverted** — shadcn is the right default for internal/B2B apps |
| 13 | Never generic FAQ/pricing | **Irrelevant** for apps |
| 14 | Never icon-only nav | **Still applies** — apps need labels too, especially for new users |
| 15 | Never zero motion | **Functional motion only** — state transitions, loading, success/error feedback. Decorative motion is bad in apps. |
| 16 | Never generic easing | **Relaxed** — system defaults are fine |
| 17 | Never glassmorphism | **Still applies** |
| 18 | Never generic AI copy | **Still applies** — but means "clear and helpful" not "expressive" |
| 19 | Never lorem in delivered | **Stronger** — use realistic data fixtures, not "test test" or "Lorem ipsum" |
| 20 | Never ship without verification | **Still applies, gates change** (see §5) |
| 21 | No emoji as iconography | **Still applies** |
| 22 | No sub-12px label text | **Relaxed** — app UI commonly uses 11-13px labels with appropriate weight/contrast |
| 23 | No personal-aesthetic chrome on client work | **Still applies** |
| 24 | Custom cursor only when deliberate | **Stronger** — apps almost never benefit from custom cursors; default OS cursor wins |

## App-specific anti-slop rules (added)

Apply only in app mode:

- **Never ship a list/table without a documented empty state.** "No items yet" with a call-to-action to create one.
- **Never ship without explicit loading and error states for every async operation.** Skeleton or spinner; error message that's recoverable.
- **Never trap focus or skip keyboard navigation on any flow.** Tab, Shift-Tab, Enter, Escape must work everywhere.
- **Never use color alone to convey state.** Always icon + color, or text + color. Colorblind users exist.
- **Never ship undocumented permissions behavior.** What does a viewer see vs an admin? Document and verify both.
- **Never use `alert()` or browser-native confirm dialogs.** Build inline confirmations or modal patterns. Native dialogs feel cheap.
- **Never expose technical errors to end users.** "500 Internal Server Error" → "Something went wrong on our end. Try again or contact support."

## Stack defaults (app)

Stack defaults flip vs marketing:

| | Marketing default | **App default** |
|---|---|---|
| Primary | Plain HTML/CSS/JS + Vite | **Next.js + React + TypeScript** |
| Content-heavy | Astro | n/a |
| Component layer | Hand-built, no kits | **shadcn/ui** (or Radix primitives + custom) |
| Styling | Custom CSS, OKLCH tokens | **Tailwind + CSS vars** (still tokenized; less aggressive about avoiding utility defaults) |
| State | Minimal vanilla JS | **Tanstack Query** + Zustand/Jotai for client state |
| Auth | Often none | NextAuth, Clerk, Auth.js, custom |
| ORM/data | n/a | Prisma + Postgres typical |
| Testing | Playwright | **Playwright + Vitest** for component tests |

For **internal apps**, the stack is more permissive — desktop-native (.NET WPF as in stream-deck) is fine if it serves the use case better than web. The branch question's resolution determines the platform; this section is about web app defaults specifically.

## Verification gate adjustments (app)

| Gate | Marketing | App (internal) | App (customer — see tightening below) |
|------|-----------|----------------|----------------------------------------|
| Lighthouse Performance | ≥ 90 | ≥ 80 | ≥ 90 |
| Lighthouse Accessibility | ≥ 95 | **= 100** | = 100 |
| Lighthouse Best Practices | ≥ 90 | ≥ 90 | ≥ 90 |
| Lighthouse SEO | ≥ 90 | **Skip** (auth-walled) | Skip |
| axe critical/serious | 0 | 0 | 0 |
| Keyboard navigation verified | nav only | **every flow** | every flow |
| Screen reader pass | spot check | **critical flows required** | critical flows required |
| Empty/error/loading states | n/a | **documented + tested** | documented + tested |
| Real data fixtures | realistic copy | **realistic data volume** (1, 10, 1000 records) | realistic data volume |
| Mobile responsive | required | optional | **required** |
| Cross-browser | Chrome enough | Chrome enough | **Chrome + Safari iOS + Firefox** |

## Patterns folder

App patterns live in `patterns/app/`. Different vocabulary than marketing patterns. Examples that earn their place over time (none built yet — start empty, grow from real work):

- Command palette
- Data table with filtering / sorting / pagination
- Multi-step form with validation
- Empty state composition
- Permission-gated content with explanatory tooltips
- Side nav with collapse / pinned items
- Bulk action bar
- Inline edit with optimistic update
- Settings layout (sidebar + content)
- Notification / toast pattern

## Reference vault

App references live under "App / Product UI" in `references/INDEX.md`. Different sites than marketing references. Linear (the actual app, not marketing), Stripe Dashboard, Notion (in-app), Vercel Dashboard, Retool, Pitch (in-app), Plausible, Cal.com.

---

## Customer-app tightening (subsection)

> Loaded **additionally** when the intake branch is specifically **Customer app** (not Internal app). Tightens gates because end users are paying customers and have higher expectations than internal users.

### Additional intake questions

- **Mobile required?** (almost always yes for customer apps)
- **Onboarding model** — first-run experience, empty product state, sample data?
- **Help architecture** — in-app docs, tooltips, chat support, knowledge base?
- **Notification model** — email, in-app, push?
- **Subscription/billing exposed in UI?** (Stripe customer portal pattern)
- **i18n requirements** — single locale or multi?

### Additional anti-slop rules

- **Never leave dead-end error states.** Always offer a next action ("retry", "contact support", "go back").
- **Never use system fonts only.** Customer apps still need brand presence — pick a brand-consistent type pairing even if the body font is system-ish.
- **Never use stock-feeling empty state illustrations.** Custom or none.
- **Never ship without an onboarding decision documented.** Even "no onboarding needed" with rationale.
- **Never assume desktop.** Mobile-first verification on customer apps.
- **Never use generic "Welcome to [App]!" greetings.** Customer apps' first impression should be the value, not the greeting.

### Additional verification gates

| Gate | Internal app | **Customer app** |
|------|--------------|------------------|
| Lighthouse Performance | ≥ 80 | **≥ 90** (back to marketing-strict; mobile users on bad networks pay the cost) |
| Mobile responsive | optional (desktop assumed) | **required at 375 / 768 / 1024** |
| Touch target sizing | n/a | **≥ 44×44px on every interactive** |
| First-run / empty product state | documented | **designed and verified** |
| Onboarding flow | n/a | **designed and verified** |
| Error recovery | functional | **user-friendly + recoverable** (no dead ends) |
| Cross-browser | Chrome/Edge enough | **Chrome + Safari iOS + Firefox** at minimum |
| Loading skeleton on all routes | optional | **required** (no blank-page-then-pop) |

### Stack tweaks for customer apps

- **Email layer** becomes important (Resend, Postmark, Loops)
- **Auth becomes more sophisticated** — multi-factor, password reset, magic link, social
- **Analytics integration** — Plausible, PostHog, custom
- **Support tooling** — Crisp, Intercom, Plain
- **Billing** — Stripe Checkout / Customer Portal if subscription
- **i18n** if international users likely

---

## Anti-pattern

Do not apply marketing-site anti-slop rules to apps without translation. "Don't use shadcn" is right for marketing, wrong for apps. Always check this file's table first when working in app mode.

Do not apply customer-app tightening to internal apps. Internal apps don't need mobile, don't need onboarding flows, don't need cross-browser. Tightening is for customer apps specifically.

Do not skip verification gates because "it's just internal." Internal apps still hit the internal app gates. The relaxation is from customer-app strict to internal-app practical, not from "verified" to "vibes."
