# ADA / WCAG: Americans with Disabilities Act Titles II and III, as applied to websites and mobile apps in the United States

| Field | Value |
|---|---|
| **Jurisdiction** | United States (federal). Applies to US-facing sites regardless of where the developer sits. |
| **Regulator / enforcer** | US Department of Justice, Civil Rights Division (Titles II and III). Private plaintiffs also sue directly. US Access Board writes the Section 508 standard. HHS Office for Civil Rights enforces the parallel Section 504 rule for its funding recipients. |
| **In force since** | ADA signed July 26, 1990. Title III effective January 26, 1992. DOJ Title II web rule published April 24, 2024 (89 FR 31320), effective June 24, 2024. |
| **Last amended** | April 20, 2026: DOJ interim final rule extending Title II compliance dates by one year (91 FR 20902, doc. 2026-07663), effective April 20, 2026, comments closed June 22, 2026. May 11, 2026: HHS interim final rule extending its Section 504 web dates by one year (91 FR 25496, doc. 2026-09266), effective May 7, 2026. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. The Title II technical standard is in force but its compliance deadlines have not yet arrived (April 26, 2027 and April 26, 2028). Title III is in force now with no technical standard. |

## Applies when

Work through these at intake. More than one branch can fire on the same project.

**Title II branch (has a hard technical standard and a deadline):**

- The client is a state or local government body, or an agency or department of one. This includes cities, counties, school districts, public universities and community colleges, courts, police and fire departments, public libraries, public hospitals, transit agencies, and special purpose districts.
- Also caught: Amtrak and other commuter authorities.
- Population threshold decides the deadline, not whether the rule applies. A public entity (other than a special district government) serving a total population of 50,000 or more has until **April 26, 2027**. A public entity serving a total population under 50,000, and any special district government regardless of population, has until **April 26, 2028**.
- Note the population figure is the entity's total population served, not its employee count and not its budget.
- If you are a private vendor building the site for a public entity, the entity is the regulated party. Your build is what makes them compliant or not, so the standard lands on you contractually.

**Title III branch (no technical standard, but this is where the lawsuits are):**

- The client is a private business that is a "place of public accommodation" under one of the 12 statutory categories: retail stores, restaurants and bars, hotels, theaters and stadiums, doctors' and lawyers' offices, banks, gyms, schools, day care, museums, parks, service establishments, and transportation depots.
- The client has a physical location that customers visit AND a website that supports it (booking, ordering, store locator, menus, accounts, appointment scheduling). This is the strongest trigger and is actionable in every federal circuit.
- The client is online-only with no physical premises: coverage depends on the circuit. See "Notes". Treat this as caught anyway for build purposes; the cost of conforming is far below the cost of defending.
- Employer-facing note: Title I (employment) is separate and can reach careers pages and application portals even for businesses that are not public accommodations. If the site has an apply-for-a-job flow, build it accessible.
- There is **no revenue floor and no employee-count floor** for Title III. A single-location business with one employee is a public accommodation if it is in one of the categories. The "small business" carve-outs people expect do not exist here.

**Section 508 branch (federal procurement):**

- The client is a federal agency, or the site or app is being developed, procured, maintained, or used by a federal agency.
- The client is a contractor delivering information and communication technology (ICT) to a federal agency. Section 508 binds the agency directly; contractors get bound through the contract via FAR part 39.2 and the solicitation language, not by the statute itself.
- Deliverable to expect: an Accessibility Conformance Report (ACR), commonly on the VPAT template.

**Section 504 / HHS branch (often missed):**

- The client receives federal financial assistance from HHS. This sweeps in hospitals and health systems, community health centers and FQHCs, nursing homes participating in Medicare or Medicaid, state Medicaid and human services agencies, and HHS-funded universities and research institutions.
- Deadline is by employee count: 15 or more employees, **May 11, 2027**. Fewer than 15 employees, **May 10, 2028**. Both were extended one year on May 7, 2026.
- Standard is the same as Title II: WCAG 2.1 Level A and AA.

**State law overlay (changes the money, not the build):**

- The client does business in California. The Unruh Civil Rights Act treats an ADA violation as an automatic Unruh violation and carries a statutory minimum of $4,000 per violation plus attorney fees. Federal ADA Title III gives private plaintiffs no damages at all, so California is where the damages come from.
- The client does business in New York. New York state and city human rights laws are routinely pleaded alongside ADA claims in state court. UNVERIFIED: the specific damages available under NYSHRL and NYCHRL for web accessibility claims were not confirmed for this file.

## What the site must have

| Requirement | What that means in the build |
|---|---|
| **Conform to WCAG 2.1 Level AA (Title II, Section 504)** | All Level A and Level AA success criteria. This is a regulatory requirement with a date attached, not a recommendation. Build to it now even if the deadline is 2027 or 2028; retrofitting a finished site costs more. |
| **Conform to WCAG 2.1 Level AA (Title III, as the practical target)** | DOJ has no Title III web regulation. WCAG 2.1 AA is the de facto standard in settlements, consent decrees, and DOJ's own Title III guidance, which names WCAG and the Section 508 standards as "helpful guidance". Write WCAG 2.1 AA into the client contract as the acceptance criterion so both sides have a defined finish line. |
| **Conform to WCAG 2.0 Level AA (Section 508)** | The Revised 508 Standards (36 CFR part 1194, appendices A and C) incorporate WCAG 2.0 Level A and AA by reference. WCAG 2.0 is a subset of 2.1, so a site that meets 2.1 AA also meets 2.0 AA. Build to 2.1 AA and you cover both. |
| **Mobile apps** | The Title II rule covers mobile apps on the same standard, the same deadlines, and the same exceptions as web content. If the project includes a native app, it is in scope. |
| **Keyboard operability** | Every interactive control reachable and operable with keyboard alone. No keyboard traps. Visible focus indicator on every focusable element. Logical focus order. Custom components (dropdowns, modals, carousels, tabs, date pickers) need explicit key handling; a `div` with an `onclick` is the single most common failure. |
| **Text alternatives** | Meaningful `alt` on informative images. Empty `alt=""` on decorative images so screen readers skip them. Text alternatives for icons used as controls. Captions for prerecorded video, and audio description or a transcript where visual content carries information. |
| **Contrast** | 4.5:1 for normal text, 3:1 for large text (18pt, or 14pt bold) and for UI component boundaries and graphical objects that convey meaning. This is the criterion most often broken by a designer-chosen brand palette on light grey. |
| **Forms** | Every input has a programmatically associated `<label>`. Errors identified in text, not by color alone. Error messages describe the fix. Required fields marked in text. Grouped controls in `<fieldset>` with `<legend>`. |
| **Structure and semantics** | Correct heading hierarchy with a single `h1` and no skipped levels used for styling. Landmark regions (`header`, `nav`, `main`, `footer`). Lists marked up as lists. Tables with `<th>` and scope. Skip-to-content link as the first focusable element. |
| **Page essentials** | `lang` attribute on `<html>`. Unique, descriptive `<title>` per page. Link text that makes sense out of context (not "click here" or "read more" repeated 12 times). |
| **Motion and timing** | Respect `prefers-reduced-motion`. No content that flashes more than three times per second. Any auto-advancing carousel or auto-playing media needs a pause control. Session timeouts need a warning and an extend option. |
| **Zoom and reflow** | Usable at 200% text zoom and at 320 CSS pixels wide without horizontal scrolling. Do not set `user-scalable=no` or `maximum-scale=1` in the viewport meta tag. |
| **Accessibility statement page** | Publish at a stable URL such as `/accessibility`. See the content list below. |
| **Footer link** | Link the accessibility statement from the global footer on every page, alongside privacy and terms. |
| **Feedback channel** | A monitored email address or form specifically for accessibility problems, named in the statement, with a stated response time the client can actually meet. |
| **Records** | Keep the audit reports, the remediation log with dates, and any third-party ACR/VPAT for components you did not build. This is the evidence of good-faith effort that shapes settlement posture. |

**What the accessibility statement should say.** Keep it honest and specific; a boilerplate statement claiming full conformance on a site that does not conform is worse than no statement, because it is a written admission the plaintiff will quote back.

- The conformance target by name and version: "We aim to conform to WCAG 2.1 Level AA."
- The current conformance status in W3C terms: fully conformant, partially conformant, or not conformant. Use "partially conformant" unless an audit says otherwise.
- Known limitations, listed plainly, with what you are doing about each and a rough timeframe. Example: third-party booking widget on `/book` is not fully keyboard operable; vendor has committed to a fix.
- Which assistive technology and browser combinations you tested.
- The date of the last audit or review.
- A feedback route: email address, phone if the client has one, and expected response time.
- For Title II entities, the ADA coordinator's contact details and the grievance procedure.
- No claim of "fully ADA compliant". There is no such certification for Title III, and the phrase is a liability.

**Third-party content.** Embedded maps, chat widgets, booking engines, payment iframes, review widgets, and video players are the usual sources of failure and you often cannot fix them. Request an ACR from each vendor before you commit to it. If a vendor cannot produce one, treat that as a reason to pick a different vendor, and tell the client in writing.

## How to verify

Automated tools catch roughly a third of issues. The manual passes below are not optional.

**Automated sweep (fast, catches the obvious):**

- Run axe DevTools or Lighthouse in Chrome DevTools on every page template, not just the home page. Lighthouse lives in the Lighthouse panel; choose the Accessibility category.
- Run a crawler across the whole site (Pa11y CI, axe-core CLI, or IBM Equal Access) so you catch the pages nobody remembers, like the 404, the search results page, and the post-checkout confirmation.
- Wire `axe-core` into the CI test run so regressions fail the build rather than surfacing after launch.
- Grep the codebase for the known offenders: `<img` without `alt`, `onclick` on non-interactive elements, `tabindex="` with a positive number, `user-scalable=no`, `maximum-scale=`, `role="button"` without a keydown handler, `<div class="btn"`, and any `outline: none` or `outline: 0` that is not paired with a replacement focus style.

**Manual keyboard pass (do this on every template):**

- Unplug the mouse. Tab from the top of the page to the bottom.
- Confirm a visible focus ring on every stop. Confirm the focus order matches the visual order.
- Open every modal by keyboard, confirm focus moves into it, confirm Escape closes it, confirm focus returns to the element that opened it.
- Confirm you can reach and operate the nav, the search, the cookie banner, the carousel controls, and every form. Confirm you never get stuck (keyboard trap) inside a widget or an embedded iframe.
- Confirm the skip link appears on first Tab and actually moves focus to `main`.

**Screen reader pass (at least one desktop and one mobile):**

- NVDA on Windows with Firefox or Chrome, or VoiceOver on macOS with Safari. VoiceOver on iOS for mobile.
- Navigate by heading (H in NVDA, rotor in VoiceOver) and confirm the heading outline describes the page.
- Navigate by landmark and by form field. Confirm every field announces its label and its required/error state.
- Submit a form with deliberate errors and confirm the errors are announced, not just shown in red.

**Visual and reflow pass:**

- Chrome DevTools, Elements panel, Styles pane: hover any color value to see the contrast ratio and the AA/AAA badges. Use the Inspect tooltip, which reports contrast for the hovered element.
- Chrome DevTools, Rendering panel: emulate `prefers-reduced-motion: reduce` and confirm animation stops. Also emulate vision deficiencies there to check anything encoded by color alone.
- Set browser zoom to 200% and then resize to 320 CSS pixels wide. Nothing should clip and nothing should scroll horizontally.
- Chrome DevTools, Elements panel, Accessibility pane: check the computed accessible name and role for every custom control. A control with an empty accessible name is a defect.

**Network and third-party pass:**

- Open the Network panel and list every third-party script and iframe on the page. For each one, run the keyboard pass inside it. Vendor widgets are the most common uncaught failure.

**Documentation pass before delivery:**

- Confirm `/accessibility` exists, is linked from the footer of every page, states WCAG 2.1 AA as the target, lists real known limitations, and gives a working contact address. Send a test message to that address and confirm someone receives it.

## Penalties

**Title III, private plaintiff suits.** The ADA gives private plaintiffs injunctive relief and attorney fees, not damages (42 U.S.C. 12188). The financial exposure is the plaintiff's fees plus your own defense costs plus the remediation you were going to have to do anyway. Typical resolution is a quick settlement; the fee award is what drives the filing volume.

**Title III, DOJ enforcement suits.** DOJ can seek civil penalties in cases it brings. Under 28 CFR 36.504(a)(3) as adjusted by 28 CFR 85.5, for penalties assessed after July 3, 2025 (90 FR 29447): a maximum of **$118,225** for a first violation and **$236,451** for a subsequent violation. DOJ announced on July 15, 2026 that its civil monetary penalty amounts do not increase for 2026 and the 2025 levels continue, so these figures are current as of this review date. These maximums apply only to DOJ-initiated actions, not to private suits.

**California Unruh Act.** A statutory minimum of **$4,000 per violation**, actual damages recoverable up to a maximum of three times actual damage, plus attorney fees (Cal. Civ. Code 52(a)). An ADA violation is a per se Unruh violation (Cal. Civ. Code 51(f)), which is why California claims carry real money where the federal claim alone does not.

**Title II.** DOJ enforcement plus private suits for injunctive relief and compensatory damages. Loss of federal funding is available under Section 504 for funding recipients. UNVERIFIED: no fixed civil penalty schedule for Title II web violations was confirmed for this file.

**Accessibility overlay marketing.** In January 2025 the FTC ordered accessiBe to pay **$1 million** over claims that its automated widget could make any website WCAG compliant; the final order was approved in April 2025. This is a warning about what the studio itself says in writing. Do not tell a client a plugin makes them compliant.

## Common ways sites fail this

- Shipping an accessibility overlay or widget and calling it done. Overlays do not fix the underlying code, plaintiffs' firms specifically target sites that use them, and the FTC has already fined the largest vendor over compliance claims.
- Publishing a boilerplate accessibility statement that claims full compliance. It is a written admission when the site fails an audit.
- Running Lighthouse on the home page only. Checkout, search results, account pages, PDFs, and the 404 page are where the failures live.
- Custom controls built from `div` and `span` with click handlers and no keyboard support, no role, and no accessible name.
- `outline: none` in a CSS reset with nothing put back, which removes the focus indicator sitewide.
- Brand palette that fails 4.5:1, usually light grey body text or a mid-tone brand color on white for links and buttons.
- Placeholder text used instead of a `<label>`. The label disappears the moment the user types.
- Third-party booking, chat, or payment widgets that are unreachable by keyboard. The client is liable for them even though the studio did not write them.
- Video with auto-generated captions treated as sufficient. Auto captions routinely fail on names, numbers, and technical terms.
- PDF menus, forms, and reports posted untagged. A PDF is web content and counts.
- Assuming a small business is exempt. Title III has no size threshold.
- For Title II projects, treating the 2027 or 2028 date as the start of the work rather than the finish.
- Carousels and modals that trap focus or that steal focus on page load.

## Sources

Official sources first. All retrieved 2026-07-20.

- [ADA.gov: Fact Sheet, New Rule on the Accessibility of Web Content and Mobile Apps Provided by State and Local Governments](https://www.ada.gov/resources/2024-03-08-web-rule/) (retrieved 2026-07-20)
- [Federal Register: Extension of Compliance Dates for Nondiscrimination on the Basis of Disability; Accessibility of Web Information and Services of State and Local Government Entities, interim final rule, published and effective April 20, 2026, comments closed June 22, 2026](https://www.federalregister.gov/documents/2026/04/20/2026-07663/extension-of-compliance-dates-for-nondiscrimination-on-the-basis-of-disability-accessibility-of-web) (retrieved 2026-07-20)
- [Federal Register / GovInfo: Nondiscrimination on the Basis of Disability; Accessibility of Web Information and Services of State and Local Government Entities, final rule, 89 FR 31320, April 24, 2024](https://www.govinfo.gov/content/pkg/FR-2024-04-24/html/2024-07758.htm) (retrieved 2026-07-20)
- [ADA.gov: Guidance on Web Accessibility and the ADA, March 18, 2022](https://www.ada.gov/resources/web-guidance/) (retrieved 2026-07-20)
- [Federal Register: Extension of Compliance Dates, HHS Section 504 web content and mobile applications, interim final rule, 91 FR 25496, published May 11, 2026, effective May 7, 2026](https://www.federalregister.gov/documents/2026/05/11/2026-09266/extension-of-compliance-dates-for-nondiscrimination-on-the-basis-of-disability-accessibility-of-web) (retrieved 2026-07-20)
- UNVERIFIED: [HHS press release: HHS Office for Civil Rights Extends Web and Mobile Accessibility Compliance Deadline](https://www.hhs.gov/press-room/hhs-extends-mobile-and-web-accessibility-deadline.html). This URL could not be confirmed on 2026-07-20 because hhs.gov returns HTTP 403 to all automated requests, including its own homepage, so the page may or may not exist at this path. The Federal Register entry above (91 FR 25496) is the authoritative support for the HHS extension and does not depend on this link.
- [US Access Board: Revised 508 Standards and 255 Guidelines](https://www.access-board.gov/ict/) (retrieved 2026-07-20)
- [eCFR: 36 CFR part 1194, Information and Communication Technology Standards and Guidelines](https://www.ecfr.gov/current/title-36/chapter-XI/part-1194) (retrieved 2026-07-20)
- [Section508.gov: IT Accessibility Laws and Policies](https://www.section508.gov/manage/laws-and-policies/) (retrieved 2026-07-20)
- [28 CFR 85.5, Adjustments to penalties for violations occurring after November 2, 2015 (Cornell LII mirror of eCFR)](https://www.law.cornell.edu/cfr/text/28/85.5) (retrieved 2026-07-20)
- [eCFR: 28 CFR 36.504, Relief](https://www.ecfr.gov/current/title-28/chapter-I/part-36/subpart-E/section-36.504) (retrieved 2026-07-20)
- [Federal Register: Civil Monetary Penalties Inflation Adjustments for 2026, notice published July 15, 2026, no increase for 2026](https://www.federalregister.gov/documents/2026/07/15/2026-14236/civil-monetary-penalties-inflation-adjustments-for-2026) (retrieved 2026-07-20)
- [42 U.S.C. 12188, Enforcement (Title III remedies)](https://www.law.cornell.edu/uscode/text/42/12188) (retrieved 2026-07-20)
- [W3C: Web Content Accessibility Guidelines (WCAG) 2.2, W3C Recommendation, latest version dated December 12, 2024](https://www.w3.org/TR/WCAG22/) (retrieved 2026-07-20)
- [W3C: Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/) (retrieved 2026-07-20)
- [FTC: Order Requires Online Marketer to Pay $1 Million for Deceptive Claims that its AI Product Could Make Websites Compliant with Accessibility Guidelines, January 2025](https://www.ftc.gov/news-events/news/press-releases/2025/01/ftc-order-requires-online-marketer-pay-1-million-deceptive-claims-its-ai-product-could-make-websites) (retrieved 2026-07-20)
- [FTC: Approves Final Order Requiring accessiBe to Pay $1 Million, April 2025](https://www.ftc.gov/news-events/news/press-releases/2025/04/ftc-approves-final-order-requiring-accessibe-pay-1-million) (retrieved 2026-07-20)
- [California Civil Code section 52(a), statutory minimum of $4,000 per offense, up to three times actual damages, plus attorney's fees](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=CIV&sectionNum=52) (retrieved 2026-07-20)
- [California Civil Code section 51(f), an ADA violation is also an Unruh Act violation](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=CIV&sectionNum=51) (retrieved 2026-07-20)
- [California Department of Rehabilitation: Unruh Civil Rights Act](https://www.dor.ca.gov/Home/UnruhCivilRightsAct) (retrieved 2026-07-20). General overview only; this page does not state the damages figures, so the two statutory sections above are the support for them.
- [Seyfarth Shaw, ADA Title III blog: Federal Court Website Accessibility Lawsuit Filings Bounce Back in 2025, published March 25, 2026](https://www.adatitleiii.com/2026/03/federal-court-website-accessibility-lawsuit-filings-bounce-back-in-2025/) (retrieved 2026-07-20)
- [Seyfarth Shaw, ADA Title III blog: ADA Title III Federal Lawsuit Filings Fall Slightly to 8,667 in 2025](https://www.adatitleiii.com/2026/02/ada-title-iii-federal-lawsuit-filings-fall-slightly-to-8667-in-2025/) (retrieved 2026-07-20)

## Notes

**The Title II deadlines moved, and a lot of published advice is now stale.** DOJ extended both compliance dates by one year on April 20, 2026. The large-entity date moved from April 24, 2026 to April 26, 2027, and the small-entity date from April 26, 2027 to April 26, 2028. Any article, vendor page, or checklist citing April 24, 2026 as the large-entity deadline, or April 26, 2027 as the small-entity deadline, is out of date. Current dates are April 26, 2027 (population 50,000 or more) and April 26, 2028 (population under 50,000, and all special district governments). DOJ issued this as an interim final rule with comments closing June 22, 2026, so a further revision is possible. Re-check before relying on the dates in a client contract.

**HHS moved in the same direction.** The Section 504 web deadlines went from May 11, 2026 to May 11, 2027 (15 or more employees) and from May 10, 2027 to May 10, 2028 (fewer than 15). Healthcare clients who were told "May 2026" in early 2026 now have another year, but the obligation itself did not change.

**Litigation volume is the real Title III driver.** Federal website accessibility filings rose to 3,117 in 2025 from 2,452 in 2024, a 27% increase, and made up 36% of all federal ADA Title III filings. Top jurisdictions in 2025 were New York (1,021), Florida (961), and Illinois (585). California had only 4 federal filings because plaintiffs there use state court and the Unruh Act instead, so state court volume is not in these numbers. Demand letters, which are never counted, outnumber filings.

**The circuit split matters for online-only clients.** The First, Second, and Seventh Circuits read Title III to reach websites within the statutory categories without requiring a physical place. The Third, Sixth, Ninth, and Eleventh Circuits apply a "nexus" test requiring a connection to a physical location, which leaves purely online businesses arguably outside Title III there. Robles v. Domino's Pizza (9th Cir. 2019) is the leading nexus case. Gil v. Winn-Dixie in the Eleventh Circuit was vacated as moot, so it is not binding precedent. The Supreme Court has not resolved this. Practical read: the split affects whether a plaintiff can win, not whether they can file, and defending is more expensive than conforming.

**WCAG 2.2 versus 2.1.** WCAG 2.2 is a W3C Recommendation (latest version December 12, 2024) and adds nine success criteria, four of them at Level AA: 2.4.11 Focus Not Obscured (Minimum), 2.5.7 Dragging Movements, 2.5.8 Target Size (Minimum), and 3.3.8 Accessible Authentication (Minimum). It also removes 4.1.1 Parsing as obsolete. No US regulation adopts 2.2. WCAG 2.1 Level AA remains the legally cited target for Title II and Section 504, and WCAG 2.0 Level AA for Section 508. Content conforming to 2.2 also conforms to 2.1 and 2.0, so building to 2.2 AA is the safer default and costs little extra: target sizes of at least 24 by 24 CSS pixels, no drag-only interactions, no focus rings hidden behind sticky headers, and no authentication that requires transcribing a code or solving a puzzle without a paste-friendly alternative. State WCAG 2.1 AA in the contract as the obligation and treat 2.2 as house style.

**Watch for a Section 508 refresh.** The Revised 508 Standards still point at WCAG 2.0, which is from 2008. A refresh to a newer WCAG version would be the obvious next move by the Access Board. UNVERIFIED: no active rulemaking to update 36 CFR part 1194 to WCAG 2.1 or 2.2 was confirmed as of this review date.

**Conflicts and overlaps with other files in this library.** Cookie consent banners are a frequent accessibility failure: a banner that traps focus, that cannot be dismissed by keyboard, or whose "reject" control has an inaccessible name will fail WCAG while the consent logic itself satisfies privacy law. Build the banner to the same standard as the rest of the site. The European Accessibility Act imposes a separate obligation on businesses selling into the EU and is not covered by this file; check whether a separate EAA file exists in this library before advising a client with EU customers.

**Never certify.** There is no government accessibility certification for private websites. The studio should describe its work as "built to WCAG 2.1 Level AA" and back it with an audit report, never as "ADA compliant" or "ADA certified". The FTC action against accessiBe is the marker for how compliance claims are being policed.
