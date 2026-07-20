# Technical Guides: INDEX

> Implementation reference for the engineering side of shipping a site: getting
> crawled, getting cited by AI search, measuring what happens, and staying fast.
>
> This is not the [reference vault](../references/INDEX.md), which catalogs sites
> worth studying for their aesthetics. This directory is how-to material for the
> Build and Verify steps of the workflow.
>
> Source: [The Lazy Developer](https://www.thelazydeveloper.org/resources) · retrieved 2026-07-20.
> Stored verbatim. Do not edit the bodies; re-pull from the source instead.

---

## Performance and layout

| Guide | Covers |
|---|---|
| [browser-aware-web-design.md](browser-aware-web-design.md) | Designing for one clear LCP element, preventing layout shift, transform/opacity-only animation, keeping third-party scripts off the critical path, server-rendering meaningful content |

Read this during **Synthesis**, before committing to a layout. Most of its rules are
design decisions, not optimizations you can bolt on afterwards. A hero with three
competing focal points has already lost the LCP argument.

## SEO

| Guide | Covers |
|---|---|
| [seo-how-to.md](seo-how-to.md) | On-page and technical SEO end to end: meta tags, robots.txt, sitemaps, CSP, llms.txt, Core Web Vitals |
| [seo-crawlability.md](seo-crawlability.md) | Fixing client-rendered SPAs so Google can actually see them. Phase 0 diagnosis, then a Vite prerendering branch or a Next.js hygiene branch |
| [seo-structured-data.md](seo-structured-data.md) | JSON-LD for 14 schema types (Organization, WebSite, BreadcrumbList, FAQPage, LocalBusiness, Article, Event, VideoObject, SoftwareApplication, Product, and more), plus `@graph` composition |

`seo-crawlability.md` is the one to reach for when a site built as a client-rendered
SPA is not appearing in search. Run its Phase 0 diagnosis before choosing a fix: the
Vite and Next.js branches are genuinely different work.

## AI search (AEO)

| Guide | Covers |
|---|---|
| [aeo-foundations.md](aeo-foundations.md) | How AI search actually retrieves and cites: training data vs live retrieval, query fan-out, why citation is a probability rather than a ranking |
| [inspect-ai-search.md](inspect-ai-search.md) | A devtools method for seeing the queries ChatGPT and Claude actually run for a given prompt |

Read `aeo-foundations.md` before promising anything about AI visibility. It is
explicit that citation is probabilistic and that platforms disagree with each other,
which is the correct expectation to set with a client.

## Analytics

| Guide | Covers |
|---|---|
| [ga4-analytics.md](ga4-analytics.md) | GA4 for Next.js 16: installation, event tracking, and making a "reject" choice in the consent banner actually stop data collection |

The consent section matters beyond compliance. A banner whose reject button does
nothing is worse than no banner, because it looks like a promise.

## Where these fit in the workflow

[`PROCESS.md`](../PROCESS.md) v1.4 cites these directly, so they are part of the workflow
rather than optional background reading. Step 3 sends you to the layout guide before the
layout locks; Step 4 wires the technical layer from the SEO and analytics guides.

- **Step 3, SYNTHESIS**: `browser-aware-web-design.md` shapes the layout decisions
- **Step 4, BUILD**: `seo-how-to.md`, `seo-structured-data.md`, `ga4-analytics.md`
- **Step 5, VERIFY**: `seo-crawlability.md` Phase 3, `inspect-ai-search.md`

Security, authorization, and input validation are **not** here. Those live in
OTLC Guardian at `C:\dev\Projects\otlc-guardian\guides\`, which has an audit engine
that enforces them.
