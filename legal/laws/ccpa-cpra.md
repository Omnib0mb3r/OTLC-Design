# CCPA/CPRA: California Consumer Privacy Act of 2018, as amended by the California Privacy Rights Act of 2020

| Field | Value |
|---|---|
| **Jurisdiction** | California, USA (protects California residents; binds businesses anywhere that do business in California) |
| **Regulator / enforcer** | California Privacy Protection Agency (CPPA, public-facing name "CalPrivacy") and the California Attorney General. Private plaintiffs for breach claims only. |
| **In force since** | 2020-01-01 (CCPA). CPRA amendments operative 2023-01-01. |
| **Last amended** | Statute: AB 566 ("Opt Me Out Act"), signed 2025-10-08. Regulations: CCPA updates plus new cybersecurity audit, risk assessment, and ADMT articles, effective 2026-01-01. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. ADMT obligations take effect 2027-01-01. AB 566 browser duty takes effect 2027-01-01. Cybersecurity audit certifications phase in 2028 to 2030. |

## Applies when

Answer these at intake. All of the first four must be true, plus at least one threshold.

- The entity is **for profit**. Nonprofits and government agencies are outside the definition of "business" in Civ. Code 1798.140(d)(1). A nonprofit controlled by a covered business and sharing common branding can be pulled in under 1798.140(d)(2).
- The entity **does business in California**. There is no physical presence or nexus test in the statute. Selling to Californians over the web is enough in practice.
- The entity **collects personal information about California residents** and **determines the purposes and means** of processing it. A pure service provider or contractor working on another company's behalf has different, lighter obligations.
- The residents in question are **California residents**. Their location at the moment of the visit is not the test; residency is. You cannot geofence your way out by IP address alone.

Then at least one of these three thresholds (Civ. Code 1798.140(d)(1)):

- **Revenue**: annual gross revenue above **$26,625,000**. The statute says $25,000,000; the CPPA raises it for inflation in odd-numbered years under Civ. Code 1798.199.95(d). The $26,625,000 figure took effect 2025-01-01 and is the operative number for the 2026 compliance year. Next adjustment due January 2027. Note: this is total worldwide gross revenue, not California revenue.
- **Volume**: buys, sells, or shares the personal information of **100,000 or more consumers or households** per year. Household counts, so a 100,000-visitor site with tracking pixels can hit this even with modest revenue. Note the verb list excludes plain "collects", so a site that collects but never sells or shares does not trip this one.
- **Data monetization**: derives **50 percent or more** of annual revenue from selling or sharing consumers' personal information.

Two more scoping facts that catch people out:

- **Employee, job applicant, and B2B contact data is in scope.** The exemptions expired 2023-01-01. A careers page or a "contact sales" form on a covered client's site is covered.
- **"Sharing" is broader than most people expect.** Civ. Code 1798.140(ah)(1) defines share as disclosing personal information to a third party **for cross-context behavioral advertising**, with or without money changing hands. Running Meta Pixel, Google Ads remarketing, or TikTok Pixel is almost always "sharing". A site with zero revenue from data can still owe a full opt-out mechanism because of its ad tags.
- **"Selling"** (1798.140(ad)(1)) covers disclosure to a third party for monetary **or other valuable consideration**. Free analytics in exchange for the vendor's own use of the data has been treated as a sale.

## What the site must have

| Requirement | What that means in the build |
|---|---|
| Privacy policy at a stable URL | A `/privacy` page linked from every page footer. Must state the categories of personal information collected, sources, business purposes, categories of third parties, categories sold or shared, categories disclosed to service providers and contractors, retention period (or the criteria used to set it) per category, and a description of each consumer right with how to exercise it. Civ. Code 1798.130(a)(5). |
| Privacy policy dated and refreshed every 12 months | Put a visible "Last updated: YYYY-MM-DD" line on the page. The statute requires the information be updated at least once every 12 months. Set a calendar reminder at handover; a policy dated 14 months ago is a documented violation. |
| Notice at collection | Delivered **at or before** the point of collection. On the web this can be a link that jumps to the specific anchor in the privacy policy holding the categories, purposes, sale/share status, and retention. Reg. 7012. Linking to the top of the policy and making the user scroll does not satisfy it. In practice: every form gets a link near the submit button pointing to `/privacy#collection`, not just `/privacy`. |
| "Do Not Sell or Share My Personal Information" link | Clear and conspicuous, on the homepage, titled with that exact string. Civ. Code 1798.135(a)(1). In practice put it in the global footer on every page. |
| "Limit the Use of My Sensitive Personal Information" link | Same treatment, exact string. Civ. Code 1798.135(a)(2). Only required if the client uses or discloses sensitive personal information beyond the permitted purposes in 1798.140(e)(2), (4), (5), and (8). Sensitive PI collected or processed **without the purpose of inferring characteristics** is out of scope entirely (1798.121(d)), so a checkout that stores a card number to run the charge does not by itself trigger this link. |
| Or: one combined "Your Privacy Choices" link | Reg. 7015 lets you replace both links with a single link titled "Your Privacy Choices" or "Your California Privacy Choices", with the official opt-out icon adjacent, in the header or footer. The icon is the blue-and-white toggle published by the California AG. Size it like your other footer icons. It must land on a page that describes both rights and carries the working submission form. This is the cleaner build and what most sites should use. |
| Or: skip the links via frictionless signal handling | Civ. Code 1798.135(b) removes the link requirement if the business processes opt-out preference signals in a frictionless manner under Regs. 7025(f) and (g). The privacy policy must then state that the business responds to and abides by opt-out preference signals. Treat this as the advanced path. Getting "frictionless" wrong loses you the safe harbor and leaves you with no link either. Default to shipping the link. |
| Honor Global Privacy Control | **Mandatory, not optional**, for any business that sells or shares. Reg. 7025. Read the `Sec-GPC: 1` request header or `navigator.globalPrivacyControl` in the browser, and treat it as a valid opt-out for that browser or device, for any pseudonymous profile tied to it, and for the logged-in account if the visitor is known to you. A GPC signal must override a conflicting account-level setting that permits sale or sharing. The later absence of a signal is never consent to opt back in. |
| Show the visitor that the signal was honored | New as of 2026-01-01. Reg. 7025(b)(6) was amended from "a business may display" to "a business must display" whether it has processed the opt-out preference signal. The site has to give a California consumer a way to confirm the opt-out was processed. The regulation's own example is the string "Opt-Out Preference Signal Honored" on the site, or a toggle or radio button showing the opted-out state per Reg. 7026(g). Footer or privacy settings panel both work. |
| Block sale/share tags until the opt-out state is resolved | If GPC is present, advertising and cross-context tags must not fire. Build the tag loader so ad and social pixels are gated behind a check of the GPC header plus any stored opt-out cookie, and default to blocked while that check resolves. Strictly necessary and first-party analytics are treated differently, but assume Meta, Google Ads, TikTok, LinkedIn, and any ad-tech SDK are gated. |
| Symmetrical choice, no dark patterns | Opting out must take the same number of steps or fewer than opting in. Accept and reject controls must match in size and visual weight. Closing a banner or navigating away is **not** consent (2026 regulations). A design where "Accept All" is a filled primary button and "Reject All" is grey small text is a documented violation. |
| Two or more request channels | Civ. Code 1798.130(a)(1). A toll-free phone number is required unless the business operates exclusively online and has a direct relationship with the consumer, in which case an email address alone is enough. Most client sites qualify for the online-only carve-out; confirm it rather than assuming it. |
| 12-month lookback on access requests | Disclosures cover the 12 months preceding the request (1798.130(a)(2)). Consumers may request beyond 12 months for personal information collected on or after 2022-01-01, unless it is impossible or would take disproportionate effort. Any request-intake log or data map you build needs at least 12 months of retention to answer this. |
| Response deadline | 45 days from a verifiable consumer request, extendable once by another 45 days with notice inside the first 45. Build the intake so requests are timestamped and routed, not dropped into an unmonitored inbox. |
| Do not over-verify opt-outs | Opt-out of sale/sharing and limit-use requests must **not** require identity verification or an account. Honda and Todd Snyder were both fined partly for this. An opt-out form asking for a driver's license number is a violation. |
| Under-16 opt-in | If the business has actual knowledge a consumer is under 16, sale or sharing requires affirmative opt-in: from the consumer for ages 13 to 15, from a parent or guardian for under 13. Civ. Code 1798.120(c). |
| Consent log | Retain, per visitor: the signal or click received, the timestamp, the scope applied (browser, device, account), and what was suppressed as a result. Regulator enforcement in 2025 and 2026 turned on whether the business could evidence that opt-outs actually propagated. |
| Service provider contracts | Third parties receiving personal information need CCPA-compliant terms limiting use. This is a client legal task, not a build task, but flag it: Tractor Supply was fined in part for disclosing personal information to service providers without the required contract terms. |

Later-dated obligations to note in the handover, not in this build:

- **ADMT (automated decisionmaking technology), compliance from 2027-01-01.** Applies where ADMT replaces or substantially replaces human decisionmaking for a "significant decision", defined as one resulting in the provision or denial of financial or lending services, housing, education enrollment or opportunities, employment or independent contracting opportunities or compensation, or health care services. Brings disclosure duties folded into the notice at collection, an opt-out right with exceptions, and a right to access the logic and factors behind the output. Relevant if you are building an application screener, a lending or eligibility flow, or an admissions tool.
- **Risk assessments, compliance from 2026-01-01, first submission to the CPPA due 2028-04-01.** Triggered by selling or sharing personal information, processing sensitive personal information, using ADMT for a significant decision, and certain profiling. Submission timing is Reg. 7157(a)(1): assessments conducted in 2026 and 2027 are reported by 2028-04-01, then annually by April 1. Processing that was already underway before 2026-01-01 and continues past it must have a documented risk assessment by **2027-12-31** (Reg. 7155(b)). Assessments must be reviewed at least every three years, and updated within 45 days of any material change. Retention under Reg. 7155(c) is for as long as the processing continues, or five years after the assessment is completed, whichever is later. This is a client governance task; your build feeds it by documenting what data the site collects and where it goes.
- **Cybersecurity audits, phased.** Reg. 7120(b) applies where processing presents significant risk, which is any one of three triggers: the business derives 50 percent or more of revenue from selling or sharing (7120(b)(1), via Civ. Code 1798.140(d)(1)(C)); or it meets the revenue threshold (1798.140(d)(1)(A)) **and** processed the personal information of 250,000 or more consumers or households in the prior calendar year (7120(b)(2)(A)); or it meets the revenue threshold **and** processed the sensitive personal information of 50,000 or more consumers in the prior calendar year (7120(b)(2)(B)). Audit report deadlines are set by Reg. 7121(a): 2028-04-01 (2026 revenue over $100M), 2029-04-01 (2027 revenue $50M to $100M), 2030-04-01 (2028 revenue under $50M).

## How to verify

Run all of this before delivery, on a production-like build with real tag IDs.

1. **Footer link.** Load the homepage. Confirm a footer link reading exactly "Your Privacy Choices" (with the AG opt-out icon next to it) or exactly "Do Not Sell or Share My Personal Information". Check it is present on every template, not only the homepage. Grep the built output: `rg -i "your privacy choices|do not sell or share"` should hit the shared layout component, not one page.
2. **Opt-out page works.** Click the link. Confirm it lands on a page describing both the opt-out and limit-use rights and containing a working form. Submit it while logged out. It must not ask for identity verification or account creation.
3. **GPC is actually read.** In Chrome DevTools, Network panel, reload with a GPC-enabled browser or extension and inspect the document request headers for `Sec-GPC: 1`. Then in the Console run `navigator.globalPrivacyControl` and confirm it returns `true`. Confirm the server or client code branches on it: grep the codebase for `Sec-GPC` and `globalPrivacyControl` and confirm at least one hit outside of comments.
4. **Tags are blocked under GPC.** With GPC on, hard-reload and filter the Network panel for `facebook.com`, `connect.facebook.net`, `googleadservices`, `google-analytics`, `doubleclick`, `analytics.tiktok`, `snap.licdn`. No ad or cross-context requests should fire. Repeat with GPC off to confirm the tags do fire, otherwise you have proven nothing about the gate.
5. **Persistence and scope.** Opt out, then navigate to three other pages and reload. Confirm no ad tags reappear. Log in and confirm the opt-out still applies to the account, not only the browser. Disney's 2026 settlement turned on opt-outs that applied to only one device or one property.
6. **Confirmation state.** Confirm the site shows the visitor that the signal was honored, either in the footer or in the privacy settings panel.
7. **Banner symmetry.** Screenshot the consent banner. Measure the accept and reject controls. Same size, same visual weight, same number of clicks. Press Escape and click outside the banner: neither may set a consent cookie. Check `document.cookie` and localStorage after each to prove nothing was written.
8. **Notice at collection.** For every form on the site, confirm a link near the point of collection that deep-links into the privacy policy section holding categories, purposes, sale/share status, and retention. Confirm the anchor actually scrolls to that section.
9. **Policy freshness.** Confirm the "Last updated" date on `/privacy` is inside 12 months, and that retention periods or the criteria for setting them are stated per category.
10. **Request routing.** Send a test access request through each published channel. Confirm it arrives somewhere a human monitors and that a timestamp is recorded.

## Penalties

| Type | Amount | Source |
|---|---|---|
| Administrative fine, CPPA | Up to **$2,663 per violation** | Civ. Code 1798.155(a), CPI-adjusted amount effective 2025-01-01 |
| Administrative fine, intentional violation or violation involving a consumer known to be under 16 | Up to **$7,988 per violation** | Civ. Code 1798.155(a), CPI-adjusted |
| Civil penalty, Attorney General action | Up to **$2,663** per violation, **$7,988** intentional | Civ. Code 1798.199.90(a), CPI-adjusted |
| Private right of action, breach only | **$107 to $799 per consumer per incident**, or actual damages, whichever is greater | Civ. Code 1798.150(a)(1)(A), CPI-adjusted |

"Per violation" is counted per consumer affected in practice, which is what turns small mistakes into seven-figure fines.

There is **no mandatory cure period** for regulator enforcement. The CPRA removed it; Civ. Code 1798.155 contains no grace period.

The **private right of action is narrow**. It reaches only unencrypted and unredacted personal information exposed by a failure to maintain reasonable security, using the narrower breach definition in Civ. Code 1798.81.5(d)(1)(A): first name or initial plus last name in combination with a Social Security number, driver's license or state ID number, account or card number with an access code, medical information, health insurance information, or unique biometric data. Also covered: an email address plus a password or security question answer that would permit account access. A consumer must give 30 days' written notice before suing for statutory damages, and a cured violation blocks statutory damages. No notice is needed for actual pecuniary damages.

Actual enforcement outcomes to quote to a nervous client:

| Action | Amount | Date | What went wrong |
|---|---|---|---|
| GM / OnStar (AG, four DAs, and the CPPA) | $12,750,000 | 2026-05-08 | Retained driving and location data past its purpose and sold it to data brokers. First data-minimization enforcement. |
| Disney (AG) | $2,750,000 | 2026-02-11 | Opt-out toggle applied only to one service and one device; GPC honored only on the device used to make the request. |
| Healthline Media (AG) | $1,550,000 | 2025-07-01 | Ad tracking and opt-out failures on a health content publisher. |
| Tractor Supply (CPPA) | $1,350,000 | 2025-09-30 | No effective opt-out mechanism; failure to notify consumers and job applicants of rights; service provider contracts missing required terms. |
| American Honda (CPPA) | $632,500 | 2025-03-12 | Required excessive personal detail to process opt-outs; did not apply GPC opt-outs to known account holders. |
| Todd Snyder (CPPA) | $345,178 | 2025-05-06 | Misconfigured privacy portal silently dropped opt-out requests for 40 days; demanded identity verification for opt-outs. |

## Common ways sites fail this

- Shipping a GDPR cookie banner and calling it CCPA compliance. The banner is not the requirement. The footer link and the GPC handling are.
- Reading GPC but only applying it to the current browser, so a logged-in user who opted out on desktop is still tracked on mobile. This is exactly what Disney paid for.
- Requiring identity verification, an account, or a driver's license to opt out. Two of the six enforcement actions above include this.
- A privacy portal that appears to work but silently fails to fire the downstream suppression call. Todd Snyder's portal was broken for 40 days and nobody noticed. Test the whole chain, not the success message.
- Reject button smaller, greyer, or one click further away than accept. Straightforward dark-pattern finding.
- Treating banner dismissal or scroll as consent. Explicitly invalid since 2026-01-01.
- A privacy policy last updated two years ago. It is a standalone violation and the easiest one for a regulator to spot from outside.
- Missing retention periods in the notice at collection. Almost every generated policy template omits per-category retention.
- Assuming a small client is exempt because revenue is low, while the site runs enough ad tags to hit the 100,000 consumers-or-households sharing threshold.
- Building the link text as "Do Not Sell My Personal Information". The word "Share" has been required since 2023.

## Sources

Official:

- [Civil Code 1798.140 (definitions, business thresholds, sell, share, sensitive personal information)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=1798.140.&lawCode=CIV) (retrieved 2026-07-20)
- [Civil Code 1798.135 (opt-out links, alternative link, preference signals)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=1798.135.&lawCode=CIV) (retrieved 2026-07-20)
- [Civil Code 1798.130 (12-month lookback, 45-day response, annual policy update, request channels)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=1798.130.&lawCode=CIV) (retrieved 2026-07-20)
- [Civil Code 1798.150 (private right of action)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=1798.150.&lawCode=CIV) (retrieved 2026-07-20)
- [Civil Code 1798.155 (administrative fines, no cure period)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=1798.155.&lawCode=CIV) (retrieved 2026-07-20)
- [Civil Code 1798.121 (right to limit sensitive personal information)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=1798.121.&lawCode=CIV) (retrieved 2026-07-20)
- [Civil Code 1798.120 (opt-out of sale or sharing, under-16 opt-in)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=1798.120.&lawCode=CIV) (retrieved 2026-07-20)
- [CPPA, Updated Monetary Thresholds in CCPA (CPI adjustment, effective 2025-01-01)](https://cppa.ca.gov/regulations/cpi_adjustment.html) (retrieved 2026-07-20)
- [CPPA, CCPA Updates, Cybersecurity Audits, Risk Assessments, ADMT and Insurance Regulations](https://cppa.ca.gov/regulations/ccpa_updates.html) (retrieved 2026-07-20)
- [CPPA, California Finalizes Regulations to Strengthen Consumers' Privacy (2025-09-23, compliance dates)](https://cppa.ca.gov/announcements/2025/20250923.html) (retrieved 2026-07-20)
- [CPPA, approved regulations text (PDF)](https://cppa.ca.gov/regulations/pdf/ccpa_updates_cyber_risk_admt_appr_text.pdf) (retrieved 2026-07-20)
- [CCPA statute text effective 2026-01-01 (PDF)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf) (retrieved 2026-07-20)
- [California AG, CCPA opt-out icon download](https://oag.ca.gov/privacy/ccpa/icons-download) (retrieved 2026-07-20)
- [California AG, $12.75M General Motors privacy settlement (2026-05-08)](https://oag.ca.gov/news/press-releases/when-it-comes-data-privacy-consumers-must-be-driver%E2%80%99s-seat-attorney-general) (retrieved 2026-07-20)
- [California AG, $2.75M Disney settlement](https://oag.ca.gov/news/press-releases/california-wont-let-it-go-attorney-general-bonta-announces-275-million) (retrieved 2026-07-20)
- [California AG, $1.55M Healthline.com settlement](https://oag.ca.gov/news/press-releases/attorney-general-bonta-announces-largest-ccpa-settlement-date-secures-155) (retrieved 2026-07-20)
- [CPPA, $1.35M Tractor Supply settlement (2025-09-30)](https://privacy.ca.gov/2025/09/nations-largest-rural-lifestyle-retailer-to-pay-1-35m-over-ccpa-violations/) (retrieved 2026-07-20)
- [CPPA, Honda settlement (2025-03-12)](https://cppa.ca.gov/announcements/2025/20250312.html) (retrieved 2026-07-20)
- [CPPA, Todd Snyder order (2025-05-06)](https://cppa.ca.gov/announcements/2025/20250506.html) (retrieved 2026-07-20)
- [CPPA, joint CA/CO/CT investigative sweep on opt-out preference signals (2025-09-09)](https://cppa.ca.gov/announcements/2025/20250909.html) (retrieved 2026-07-20)
- [CPPA, AB 566 announcement (2025-10-08)](https://cppa.ca.gov/announcements/2025/20251008_2.html) (retrieved 2026-07-20)
- [California Privacy, the Opt Me Out Act explained](https://privacy.ca.gov/2026/01/californias-opt-me-out-act-your-privacy-just-got-easier/) (retrieved 2026-07-20)

Secondary, used for reading the regulation text:

- [Cal. Code Regs. tit. 11, section 7025 (opt-out preference signals), Cornell LII](https://www.law.cornell.edu/regulations/california/11-CCR-7025) (retrieved 2026-07-20)
- [Cal. Code Regs. tit. 11, section 7015 (alternative opt-out link), Cornell LII](https://www.law.cornell.edu/regulations/california/11-CCR-7015) (retrieved 2026-07-20)
- [Cal. Code Regs. tit. 11, section 7012 (notice at collection), Cornell LII](https://www.law.cornell.edu/regulations/california/11-CCR-7012) (retrieved 2026-07-20)
- [Greenberg Traurig, revised CCPA regulations effective 2026-01-01, action items](https://www.gtlaw.com/en/insights/2025/9/revised-and-new-ccpa-regulations-set-to-take-effect-on-jan-1-2026-summary-of-near-term-action-items) (retrieved 2026-07-20)
- [Skadden, California risk assessment and cybersecurity audit certification requirements (June 2026)](https://www.skadden.com/insights/publications/2026/06/californias-mandatory-risk-assessment-and-cybersecurity-audit-certification-requirements) (retrieved 2026-07-20)
- [Troutman, courts expand the CCPA private right of action (June 2026)](https://www.troutmanprivacy.com/2026/06/courts-expand-ccpas-private-right-of-action/) (retrieved 2026-07-20)
- [IAPP, California governor signs in-browser opt-out preference signal law](https://iapp.org/news/a/california-governor-signs-new-law-requiring-in-browser-opt-out-preference-signal) (retrieved 2026-07-20)

## Notes

- **AB 566 changes the browser side, not the site side, on 2027-01-01.** From that date, browsers distributed in California must ship a user-configurable opt-out preference signal. The practical effect on client sites is volume: GPC goes from a niche extension signal to a default-available browser setting, so the share of traffic arriving with `Sec-GPC: 1` will jump. Any site whose ad revenue model quietly depends on nobody sending the signal should be told now.
- **The private right of action is being stretched by federal courts in California.** Through mid-2026, several Northern District of California decisions have let CCPA breach claims survive dismissal based on third-party website trackers (Google Analytics, Meta Pixel) rather than a classic breach, reasoning that the statute covers unauthorized disclosure regardless of intent. No court has yet ruled on whether tracker data meets the narrow 1798.81.5(d)(1)(A) definition. Treat unnecessary third-party tags on a client site as litigation exposure, not only regulatory exposure.
- **Data minimization is now an enforcement theory.** The GM settlement was the AG's first action on minimization and purpose limitation. Collecting a field "in case we need it later" is now an enforceable defect. Push back on intake forms that collect data with no stated use.
- **The revenue threshold moves in January 2027.** Re-check the CPPA CPI page before any January 2027 intake. A client sitting just under the line this year may be over it next year.
- **Conflicts and overlaps with other laws in this library.** California's own DELETE Act and data broker registration sit alongside the CCPA and are enforced by the same agency; a client that sells audience data may owe registration on top of everything here. The CCPA opt-out model is opt-out by default, which is the opposite of GDPR's opt-in for the same ad tags, so a site serving both audiences needs region-aware consent logic rather than one global banner. Other US state privacy laws recognize universal opt-out signals with their own lists of approved mechanisms; building on GPC covers most of them, but confirm per state.
- **The link text is exact-match.** Do not let a copywriter improve "Do Not Sell or Share My Personal Information" or "Your Privacy Choices" into something friendlier. The strings are prescribed.
- **Cybersecurity audit applicability has three triggers, not two.** Confirmed against the approved regulation text, Article 9, Reg. 7120(b)(2)(B): a business over the revenue threshold that processed the sensitive personal information of 50,000 or more consumers in the prior calendar year is in scope, even if it never hits the 250,000 consumers-or-households count. Several secondary summaries list only the 50 percent revenue and 250,000 triggers and miss this one. A client processing health, precise geolocation, or government-ID data at modest volume can be caught by it.
