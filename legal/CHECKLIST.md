# Legal Delivery Checklist

> The Step 5 gate. Run this before any site goes live, alongside Lighthouse and axe.
> Triage and disclaimer live in [`INDEX.md`](INDEX.md). Read that first.

A site fails this gate the same way it fails an accessibility gate: it does not ship
until the failures are fixed or the client accepts them in writing.

---

## 0. Scope, recorded at intake

Copy this block into `BRIEF.md` during Step 1 and fill it in. Everything below depends
on it, and answering it late is how a cookie banner becomes a retrofit.

```
Audience jurisdictions : [ ] US  [ ] California  [ ] EU/EEA  [ ] UK  [ ] Canada  [ ] Quebec  [ ] Brazil  [ ] other:
Personal data collected: [ ] none  [ ] contact form  [ ] accounts  [ ] payments  [ ] health  [ ] financial  [ ] biometric  [ ] location
Minors in audience     : [ ] no  [ ] under 18  [ ] under 13
Third-party tags       : [ ] none  [ ] analytics  [ ] ads/pixels  [ ] embeds (maps, video, fonts)  [ ] chat  [ ] A/B
Commerce               : [ ] none  [ ] one-time sales  [ ] subscriptions/auto-renewal
Email marketing        : [ ] none  [ ] newsletter  [ ] transactional only
Client industry        : [ ] general  [ ] health  [ ] legal  [ ] financial  [ ] other regulated:
Applicable law files   : (from the INDEX triage table)
Compliance reviewed by : [ ] client's counsel  [ ] client accepts no counsel review (recorded, dated)
```

If the last line is blank, the project is not ready to ship. That is the single most
important row in this file.

---

## 1. Documents present and truthful

| Check | Applies when | Pass condition |
|---|---|---|
| Privacy policy exists | Any personal data at all, including a contact form | Reachable from every page. Describes the data the site **actually** collects, verified against the real build, not a template's guesses |
| Privacy link says "Privacy" | California visitors | The literal word appears in the link text ([`caloppa`](laws/caloppa.md)) |
| Cookie policy exists | Any non-essential cookie or tag | Lists each cookie, its purpose, its lifetime, and its owner |
| Terms of service exists | Accounts, purchases, or user content | Includes governing law, liability limits, and a DMCA clause if content is user-submitted |
| Accessibility statement exists | US or EU business | States the conformance target, known gaps, and a contact route ([`ada-wcag`](laws/ada-wcag.md), [`eu-accessibility-act`](laws/eu-accessibility-act.md)) |
| Refund, shipping, cancellation terms | Any sale | Disclosed before the payment step, not only after |
| Disclaimers present | Affiliate links, professional advice, testimonials | Placed with the claim, not buried in a footer page ([`ftc-disclosures`](laws/ftc-disclosures.md)) |
| Copyright notice in footer | Every site | Current year, correct legal entity name |

**The truthfulness test.** For each document, pick three specific claims and verify them
against the build. A policy that says "we do not use third-party analytics" on a site
running GTM is a dated written misstatement, and it is the studio that wrote it.

---

## 2. Consent and tracking behavior

| Check | Applies when | Pass condition |
|---|---|---|
| No non-essential tag fires before consent | EU/EEA/UK visitors | Load with a clean profile, watch the network panel: zero analytics, ads, or embed requests until consent is given |
| Reject is as easy as accept | EU/EEA/UK | Same level, same prominence, one click. No "manage preferences" maze to decline ([`eprivacy-cookies`](laws/eprivacy-cookies.md)) |
| Consent is recorded | EU/EEA/UK, and US state laws | A retrievable record of who consented to what, when, and to which policy version |
| Consent is revocable | Same | A persistent, reachable control, not a one-time banner |
| Global Privacy Control honored | California and several US states | Send a GPC signal, confirm the site treats it as an opt-out ([`ccpa-cpra`](laws/ccpa-cpra.md)) |
| Do Not Sell or Share link | California, if sharing for ads | Present in the footer, working, wired to something real |
| Data subject request route works | GDPR, US state laws | Submit a test request end to end. A form that emails nobody is a failure |
| No dark patterns | Everywhere | No pre-ticked boxes, no confirmshaming, no styling that hides the decline path |

**The clean-profile test is the whole section.** Open a private window, load the site, and
read the network panel before touching the banner. Most consent failures are visible in
the first two seconds and invisible to anyone testing with a primed cache.

---

## 3. Security and payments

| Check | Applies when | Pass condition |
|---|---|---|
| HTTPS forced, HSTS set | Every site | Already required by `STACK-DECISIONS.md` shipping hygiene |
| No secrets in the client bundle | Every site | Grep-verified. See OTLC Guardian |
| Card data never touches our server | Any payments | Hosted fields, Checkout, or redirect. Anything else expands PCI scope hugely ([`pci-dss`](laws/pci-dss.md)) |
| Payment page script integrity | Any payments | Scripts inventoried and integrity-checked per PCI DSS v4 |
| Breach plan written | Any personal data | Who is told, in what order, on what clock, decided before launch not during an incident ([`data-breach-notification`](laws/data-breach-notification.md)) |
| Retention and deletion defined | Any personal data | How long each data type is kept, and what deletes it |

---

## 4. Asset provenance

Every project. This is the check most often skipped and it is the one most likely to
produce a real invoice from a real rights-holder.

| Check | Pass condition |
|---|---|
| Fonts licensed for web use, at this traffic level | Desktop licenses do not cover web serving. Pageview caps are real and are enforced ([`content-licensing-attribution`](laws/content-licensing-attribution.md)) |
| Self-hosted rather than hotlinked, where the license or privacy law requires it | Applies to Google Fonts for EU visitors |
| Images and video licensed, editorial-only restrictions respected | No editorial-licensed asset on a commercial page |
| Model and property releases held where people or private property appear | Client holds them, and says so in writing |
| Icons licensed, attribution rendered where required | |
| Code and library licenses compatible | No AGPL or GPL dependency in a proprietary client deliverable unless the client agreed |
| No copied policy text from another site | Policies are themselves copyrighted. Copying one is both infringement and inaccuracy |
| Image metadata not stripped | Removing copyright management information carries its own liability ([`dmca-copyright`](laws/dmca-copyright.md)) |

Record the provenance list in the project. When someone asks in two years where a photo
came from, the answer needs to exist.

---

## 5. Industry overlays

Only if the client is in one of these. Each is a reason to insist on counsel review
rather than a reason to proceed carefully.

| Industry | Non-negotiables |
|---|---|
| Health | BAA signed before any patient data touches anything we built. No ad pixels or analytics on patient-facing pages. See [`hipaa`](laws/hipaa.md) |
| Legal | No specialization claims without certification, no outcome promises, disclaimers on every page carrying results or testimonials. See [`legal-industry-aba`](laws/legal-industry-aba.md) |
| Financial | Safeguards Rule controls, retention and approval workflow for public-facing copy. See [`financial-glba-sec`](laws/financial-glba-sec.md) |
| Children | If under-13 users are plausible, COPPA changes the whole architecture. Decide at intake, never later. See [`coppa`](laws/coppa.md) |

---

## 6. Sign-off

The gate is passed when all three are true:

- [ ] Every applicable row above passes, or the failure is written down with the client's acceptance
- [ ] The compliance-review line in `BRIEF.md` is filled in and dated
- [ ] `VERIFICATION.md` records this checklist's result next to the Lighthouse and axe scores

Then record honestly in `VERIFICATION.md`:

```
Legal gate: PASS / PASS WITH ACCEPTED EXCEPTIONS / FAIL
Law files applied: ...
Exceptions accepted by client (dated): ...
Counsel review: yes (firm, date) / no (client accepted, date)
```

"Probably fine" is not a value for that field.
