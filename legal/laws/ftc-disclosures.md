# FTC Disclosures: Federal Trade Commission advertising, endorsement, fee, and negative option rules

| Field | Value |
|---|---|
| **Jurisdiction** | United States, federal. Applies to any business advertising to US consumers, including businesses based outside the US |
| **Regulator / enforcer** | Federal Trade Commission, Bureau of Consumer Protection. State attorneys general enforce parallel state UDAP statutes. Some overlapping state laws carry a private right of action |
| **In force since** | FTC Act Section 5: 1914. Endorsement Guides: 1980. ROSCA: 29 December 2010. Consumer Reviews Rule: 21 October 2024. Unfair or Deceptive Fees Rule: 12 May 2025 |
| **Last amended** | No substantive amendment since the Unfair or Deceptive Fees Rule took effect on 12 May 2025. Most recent development: 13 March 2026, when the FTC published an Advance Notice of Proposed Rulemaking reopening negative option rulemaking after the 2024 rule was vacated (91 FR 12318) |
| **Last reviewed** | 2026-07-20 |
| **Status** | Partly in force. Four components are live and enforceable. The 2024 Negative Option Rule ("click to cancel") was vacated on 8 July 2025 and is not in effect; ROSCA still governs subscriptions and is fully enforceable |

This file covers five separate legal instruments that all bear on marketing sites. They have
different scopes and different teeth. Read the scope of each before assuming it applies.

| Instrument | Citation | Kind | Direct civil penalties? |
|---|---|---|---|
| Endorsement Guides | 16 CFR Part 255 | Interpretive guides, not a rule | No, not on their own |
| Consumer Reviews and Testimonials Rule | 16 CFR Part 465 | Trade regulation rule | Yes |
| Rule on Unfair or Deceptive Fees | 16 CFR Part 464 | Trade regulation rule | Yes |
| ROSCA | 15 U.S.C. 8401-8405 | Statute | Yes |
| Negative Option Rule (2024 amendments) | 16 CFR Part 425 (2024 version) | Vacated | Not in effect |

---

## Applies when

Answer these at intake. Each "yes" pulls in the matching section below.

### Endorsement Guides (16 CFR Part 255)

- The site contains any testimonial, customer quote, case study, star rating, or "what our clients say" block.
- The site contains any affiliate link, referral link, or link carrying a tracking parameter that earns the client money on click or conversion.
- The client pays, gifts, discounts, or otherwise compensates anyone who talks about the product publicly, including influencers, brand ambassadors, and affiliates.
- Employees, founders, contractors, or their family members post reviews or endorsements of the client's product anywhere.
- The site displays a badge, award, seal, or "as seen in" logo whose issuer was paid.
- The site publishes an endorsement generated or edited with AI, or a person's likeness or voice generated with AI.

There is no revenue threshold, no employee threshold, and no minimum audience size. A one-page
site with a single affiliate link is caught.

### Consumer Reviews and Testimonials Rule (16 CFR Part 465)

- The site displays reviews or testimonials of any kind, whether hosted natively, pulled from a third-party widget, or embedded from Google, Trustpilot, Yelp, or similar.
- The client solicits reviews from customers by any mechanism (post-purchase email, in-app prompt, QR code on a receipt).
- The client offers anything of value in exchange for reviews.
- The build includes a review moderation, filtering, gating, or approval feature.
- The client operates a site or entity that presents itself as an independent reviewer of a category that includes the client's own product.
- The client buys followers, likes, views, or subscribers for any social account linked from the site.

Applies to businesses of every size. No threshold.

### Rule on Unfair or Deceptive Fees (16 CFR Part 464)

This rule is narrow, and it is widely misdescribed as a general "junk fees" ban. It is not.

- **Caught:** the client sells or resells live-event tickets (concerts, sports, theater, festivals), or short-term lodging (hotels, motels, inns, vacation rentals, short-term rentals). Third-party platforms, resellers, travel agents, and booking intermediaries in those two categories are also caught.
- **Not caught by this rule:** every other industry. A SaaS product, a restaurant, a gym, a contractor, or an online store selling physical goods is outside 16 CFR Part 464.
- Applies whenever price information appears in any advertisement, offer, or display, including the site itself, paid ads, and listings.

If the client is outside those two categories, the federal fee rule does not apply, but state
pricing laws may. See the California entry under Notes.

### ROSCA (15 U.S.C. 8401-8405)

- The site charges a US consumer for anything over the internet using a negative option feature: a subscription, an auto-renewing plan, a free trial that converts to paid, a membership that continues until cancelled, or any arrangement where the customer's silence results in a charge.
- Applies to business-to-consumer transactions. Courts have applied ROSCA where a customer's inaction continues a paid membership.
- No revenue threshold, no subscriber-count threshold.

ROSCA is a statute. The Eighth Circuit's vacatur of the 2024 Negative Option Rule did nothing
to ROSCA. If the site takes recurring payments, ROSCA applies today.

### Negative Option Rule, 2024 amendments

- Does not apply. Vacated in its entirety by the Eighth Circuit on 8 July 2025, before its 14 July 2025 compliance date. *Custom Commc'ns, Inc. v. FTC*, 142 F.4th 1060 (8th Cir. 2025).
- The older 1973 Prenotification Negative Option Rule at 16 CFR Part 425 remains on the books, but it covers prenotification plans of the book-club and record-club type, not ordinary online subscriptions.
- The FTC reopened rulemaking on 13 March 2026. Watch for a Notice of Proposed Rulemaking. Nothing new is enforceable until a new rule is finalized and takes effect.

---

## What the site must have

### Endorsements, affiliate links, and sponsorships

| Requirement | What that means in the build |
|---|---|
| Material connection disclosed at the point of the claim | The disclosure sits next to the endorsement or affiliate link, in the same block, visible without scrolling past the claim. A footer link, an "Affiliate Disclosure" page, or a line at the bottom of a 3,000-word article does not qualify |
| Disclosure is "clear and conspicuous" per 16 CFR 255.0(f) | Difficult to miss and easily understandable by ordinary consumers. In interactive media the FTC's standard is that the disclosure is **unavoidable** |
| Disclosure in the same medium as the claim | A video endorsement gets an on-screen disclosure and a spoken one if the video has sound. Text-only disclosure under a video fails |
| Plain wording | "We earn a commission from purchases made through links on this page." Do not use "sp", "spon", "collab", "thanks", "partner", or a bare "#ambassador". Do not bury the disclosure in a hashtag block |
| Not styled away | Same font size and contrast class as surrounding body text. Not grey-on-grey, not 10px, not collapsed behind a tooltip, disclosure icon, or "read more" toggle |
| Persists across responsive breakpoints | The disclosure has to remain above the fold on a 360px viewport, not only on desktop |
| Typical-results substantiation | If a testimonial reports a result, either the result is what customers generally achieve, or the site clearly discloses the generally expected result. A "results not typical" disclaimer alone does not cure it |
| Endorser actually used the product | Records showing the endorser is a bona fide user, held by the client |
| Written affiliate and influencer terms | Contract requiring disclosure, plus an actual monitoring routine. The advertiser is liable for its endorsers' failures |

### Reviews and testimonials

| Requirement | What that means in the build |
|---|---|
| No fabricated reviews (16 CFR 465.2) | No seeded launch reviews, no AI-generated reviews, no reviews from anyone who never used the product, no purchased reviews, no fake negative reviews of competitors |
| No sentiment-conditioned incentives (16 CFR 465.4) | You may offer an incentive for *a review*. You may not condition it on the review being positive or on a star rating. Kill any "leave us 5 stars and get 10 percent off" copy, coupon flow, or email template |
| Insider reviews disclosed (16 CFR 465.5) | Reviews by officers, managers, employees, agents, or their immediate relatives carry a clear and conspicuous disclosure of the relationship. Officers and managers may not solicit reviews from their immediate relatives without disclosure |
| No deceptive review gating (16 CFR 465.7) | Any moderation must apply neutral criteria. Do not configure a widget to publish 4-5 star reviews and route 1-3 star reviews to a private feedback form. This is the single most common failure in installed review plugins |
| No misrepresenting an owned review site as independent (16 CFR 465.6) | If the client owns the comparison or review property linking to its own product, say so on the property |
| No fake social proof (16 CFR 465.8) | No purchased followers, likes, views, or subscribers on any account the site links to or displays counts from |
| Aggregate ratings reflect all published reviews | The star average and review count on screen match the underlying set. No excluding negatives from the math |
| Retain review provenance | Records of where each displayed review came from, when, and from which verified purchaser. Needed to answer an FTC civil investigative demand |

### Pricing, if the client sells live-event tickets or short-term lodging

| Requirement | What that means in the build |
|---|---|
| Total price displayed upfront (16 CFR 464.2) | Any display of price shows the total of all mandatory fees and charges, including mandatory ancillary goods or services. Resort fees, cleaning fees, service fees, and booking fees go into the number shown first |
| Total price is the most prominent price | Display it more prominently than any other pricing figure, except the final amount due at payment. A large "$99" with a small "+ fees" fails |
| Excludable items | Shipping charges and government charges (such as taxes) may be excluded from the total price |
| Excluded charges disclosed before the customer consents to pay (16 CFR 464.2(c)) | Show the nature, purpose, and amount of every charge excluded from the total price, plus the good or service it is charged for, and the final amount of payment. The trigger is the moment the customer consents to pay, not the end of the transaction |
| No misrepresented fees (16 CFR 464.3) | Do not misstate the purpose, nature, amount, or refundability of any fee, or who requires it. A "resort fee" that funds nothing resort-related is a violation |

### Subscriptions and auto-renewal (ROSCA)

| Requirement | What that means in the build |
|---|---|
| Material terms disclosed before billing information is collected | Price, billing frequency, renewal date, trial length and conversion date, and how to cancel, all rendered on the page *above* the payment fields, not behind a Terms link |
| Express informed consent, separately given | A dedicated, unchecked checkbox or equivalent affirmative action for the recurring charge itself. No pre-ticked boxes. Consent to the subscription cannot be bundled into a general "I agree to the Terms" checkbox |
| Simple cancellation mechanism | ROSCA requires a simple mechanism to stop recurring charges. Build online cancellation reachable from the account area. If the customer signed up in two clicks, cancelling should not require a phone call, a retention chat, or an email to support |
| Consent record retained | Store what the customer saw (policy or offer version), what they consented to, the timestamp, and the IP or session identifier. This is the evidence that answers a complaint |
| Renewal and price-change notices | Not a federal ROSCA requirement in itself, but required by several state laws and by the Amazon settlement's injunctive terms. Build the notification hooks |

---

## How to verify

Run these before delivery. They are all things a developer can do in a browser or a terminal.

**Affiliate and endorsement disclosures**

1. Grep the codebase for affiliate patterns: `rg -i "tag=|affid|/aff/|ref=|utm_medium=affiliate|shareasale|impact\.com|awin|cj\.com|amzn\.to|partnerize"`. Every file that hits needs a disclosure rendered on the same page.
2. For each page with a hit, load it at 360px width and screenshot the first viewport. The disclosure has to be readable in that screenshot, before any scrolling.
3. In devtools, inspect the disclosure element. Check the computed `font-size`, `color`, and `opacity` against the surrounding body text. If it is smaller or lower contrast, fix it.
4. Search the templates for disclosure text hidden behind interaction: `rg -i "details>|aria-expanded|tooltip|read more"` near disclosure strings. Anything requiring a click to reveal fails the "unavoidable" standard.
5. Disable CSS (devtools, uncheck the stylesheet) and reload. Confirm the disclosure still appears near the claim in source order, not appended at the end of the DOM and positioned up with CSS.

**Reviews**

6. Open the review widget's admin configuration. Look for any setting named "minimum rating to publish", "auto-approve above", "feedback threshold", "sentiment routing", or similar. Screenshot the setting. If low-rated reviews go anywhere other than the same public list, that is a 16 CFR 465.7 problem and it is a configuration change, not a copy change.
7. Count the published reviews and recompute the average. Compare against the displayed aggregate. They must match.
8. Grep the site copy and all transactional email templates for sentiment-conditioned incentives: `rg -i "5 star|five star|positive review|good review|leave us a review and|in exchange for a review"`.
9. Ask the client, in writing, where the launch reviews came from. Record the answer in the project. If any were written by staff, founders, or friends, they either carry a disclosure or come down.

**Pricing (ticketing and lodging clients only)**

10. Walk the full booking flow from the first price the site displays to the payment confirmation screen. Record every number at every step. The first number shown must already include every mandatory fee. If the total climbs at checkout for any reason other than shipping or taxes, the build fails.
11. Compare the font size and visual weight of the total price against every other price on the page. The total has to win.

**Subscriptions**

12. Sign up for the subscription as a real user in a clean profile. Count the clicks from landing page to charged. Then cancel. Count the clicks. Screenshot both paths. If cancelling takes materially more work than signing up, or leaves the site, flag it.
13. On the checkout page, confirm the recurring-charge consent control is unchecked on load and is separate from the terms-acceptance control. Check the DOM for `checked` attributes: `rg -i "checked.*(subscri|renew|trial|recurring)"`.
14. Confirm the renewal terms render as visible page text above the card fields. View source and confirm they are not only inside a linked Terms document.
15. Trigger a test signup and confirm a consent record lands in the database with a timestamp and an offer or policy version.

---

## Penalties

| Instrument | Maximum civil penalty | Notes |
|---|---|---|
| Consumer Reviews Rule (Part 465) | **$53,088 per violation** | Adjusted figure in effect since 17 January 2025 (up from $51,744). OMB Memorandum M-26-11, issued 17 April 2026, cancelled the 2026 inflation adjustment because the shutdown stopped BLS producing October 2025 CPI-U data, so agencies continue using 2025 levels |
| Unfair or Deceptive Fees Rule (Part 464) | **$53,088 per violation** | Same basis. Applicable since the rule took effect 12 May 2025 |
| ROSCA | **$53,088 per violation** | 15 U.S.C. 8404 treats a ROSCA violation as a violation of a rule under Section 18 of the FTC Act, which routes it to the Section 5(m)(1)(A) penalty |
| Endorsement Guides (Part 255) | No civil penalty on their own | The Guides are interpretive. A violation is evidence of a deceptive practice under Section 5. Penalties attach only where the party is already under an FTC order, or where the FTC has served that party a Notice of Penalty Offenses covering the conduct |

"Per violation" is the number that matters. The FTC has treated each affected consumer or each
day of a continuing violation as a separate violation, which is how these figures reach the
scale below.

**Real enforcement figures:**

- Amazon settled FTC ROSCA claims over Prime enrollment and cancellation on 25 September 2025 for up to **$2.5 billion**: a **$1 billion civil penalty** (half due within 14 days, the rest within 18 months) and **up to $1.5 billion** in consumer redress. The FTC described the civil penalty as the largest it has ever obtained for a rule violation. The settlement also required a clear and conspicuous option to decline Prime and a cancellation method matching the enrollment method.
- On 22 December 2025 FTC staff sent warning letters to 10 companies over possible Consumer Reviews Rule violations. The FTC said the letters were based on consumer complaints and information from the companies, and its business blog described the conduct as using fake reviews or providing incentives for 5-star reviews. The announcement cited the $53,088 per-violation figure. This marked the shift from education to enforcement on Part 465.

Beyond FTC penalties, expect exposure from state attorneys general under state UDAP statutes,
and from private class actions under state consumer protection laws, which is often the larger
practical risk for a small client.

---

## Common ways sites fail this

1. **The affiliate disclosure is a footer link.** A page-level "Affiliate Disclosure" in the footer nav, or a line at the very bottom of a long review post, while the affiliate buttons sit in the first screen. The disclosure has to be with the link.
2. **The review widget is filtering by default.** Installed review plugins commonly ship with a gating feature that routes low ratings to a private feedback form. Nobody turns it on deliberately, and nobody turns it off either. This is now a rule violation with civil penalties, not a grey area.
3. **Seeded launch reviews.** A new site with 40 five-star reviews on day one. Founders write them, agencies write them, and since October 2024 both are squarely prohibited.
4. **"Leave a 5-star review for 10 percent off."** Still pasted into post-purchase email templates constantly. Offering an incentive for a review is fine. Conditioning it on the rating is not.
5. **Auto-renewal terms only inside the linked Terms of Service.** ROSCA requires the material terms in text before billing information is collected. A hyperlink is not the disclosure.
6. **Consent to the subscription bundled into the terms checkbox.** One checkbox covering both the Terms and the recurring charge is not express informed consent to the charge.
7. **Sign up online, cancel by phone.** Even with the 2024 rule vacated, this pattern drove the Amazon case and remains directly actionable under ROSCA, and it is separately illegal in California and other states.
8. **Assuming the federal fee rule is a general junk-fee ban.** It covers live-event tickets and short-term lodging only. Studios both over-apply it to clients it does not touch and miss that state pricing laws do reach those clients.
9. **Disclosure that vanishes on mobile.** Written and checked at desktop width, pushed below the fold at 360px.
10. **The client's employees reviewing the client's product on Google.** Nobody thinks of this as advertising. 16 CFR 465.5 does.
11. **AI-generated testimonials or AI faces on a "happy customers" section.** A testimonial from a person who does not exist is a fabricated review under 16 CFR 465.2.

---

## Sources

Official sources first. All retrieved 2026-07-20.

**Endorsement Guides**

- [16 CFR Part 255, Guides Concerning Use of Endorsements and Testimonials in Advertising (eCFR)](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-B/part-255) (retrieved 2026-07-20)
- [16 CFR 255.0, Purpose and definitions, including the "clear and conspicuous" definition at 255.0(f)](https://www.law.cornell.edu/cfr/text/16/255.0) (retrieved 2026-07-20)
- [Guides Concerning the Use of Endorsements and Testimonials in Advertising, 88 FR 48092 (26 July 2023)](https://www.federalregister.gov/documents/2023/07/26/2023-14795/guides-concerning-the-use-of-endorsements-and-testimonials-in-advertising) (retrieved 2026-07-20)
- [FTC press release, updated advertising guides (29 June 2023)](https://www.ftc.gov/news-events/news/press-releases/2023/06/federal-trade-commission-announces-updated-advertising-guides-combat-deceptive-reviews-endorsements) (retrieved 2026-07-20)
- [FTC, The FTC's Endorsement Guides: What People Are Asking](https://www.ftc.gov/business-guidance/resources/ftcs-endorsement-guides-what-people-are-asking) (retrieved 2026-07-20)
- [FTC, Disclosures 101 for Social Media Influencers](https://www.ftc.gov/business-guidance/resources/disclosures-101-social-media-influencers) (retrieved 2026-07-20)
- [FTC, .com Disclosures: How to Make Effective Disclosures in Digital Advertising (March 2013, PDF)](https://www.ftc.gov/system/files/documents/plain-language/bus41-dot-com-disclosures-information-about-online-advertising.pdf) (retrieved 2026-07-20)
- [FTC, Notices of Penalty Offenses](https://www.ftc.gov/enforcement/penalty-offenses) (retrieved 2026-07-20)

**Consumer Reviews and Testimonials Rule**

- [16 CFR Part 465, Rule on the Use of Consumer Reviews and Testimonials (eCFR)](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-D/part-465) (retrieved 2026-07-20)
- [Trade Regulation Rule on the Use of Consumer Reviews and Testimonials, 89 FR 68034 (22 August 2024), effective 21 October 2024](https://www.federalregister.gov/documents/2024/08/22/2024-18519/trade-regulation-rule-on-the-use-of-consumer-reviews-and-testimonials) (retrieved 2026-07-20)
- [Final rule text, govinfo](https://www.govinfo.gov/content/pkg/FR-2024-08-22/html/2024-18519.htm) (retrieved 2026-07-20)
- [FTC, The Consumer Reviews and Testimonials Rule: Questions and Answers](https://www.ftc.gov/business-guidance/resources/consumer-reviews-testimonials-rule-questions-answers) (retrieved 2026-07-20)
- [FTC press release, FTC Warns 10 Companies About Possible Violations of the Consumer Review Rule (December 2025)](https://www.ftc.gov/news-events/news/press-releases/2025/12/ftc-warns-10-companies-about-possible-violations-agencys-new-consumer-review-rule) (retrieved 2026-07-20)
- [FTC business blog, A warning letter (or ten): comply with the FTC's Consumer Review Rule](https://www.ftc.gov/business-guidance/blog/2025/12/warning-letter-or-ten-businesses-comply-ftcs-consumer-review-rule) (retrieved 2026-07-20)

**Unfair or Deceptive Fees Rule**

- [16 CFR Part 464, Rule on Unfair or Deceptive Fees (eCFR)](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-D/part-464) (retrieved 2026-07-20)
- [Trade Regulation Rule on Unfair or Deceptive Fees, 90 FR 2066 (10 January 2025)](https://www.federalregister.gov/documents/2025/01/10/2024-30293/trade-regulation-rule-on-unfair-or-deceptive-fees) (retrieved 2026-07-20)
- [FTC press release, Rule on Unfair or Deceptive Fees to Take Effect on May 12, 2025](https://www.ftc.gov/news-events/news/press-releases/2025/05/ftc-rule-unfair-or-deceptive-fees-take-effect-may-12-2025) (retrieved 2026-07-20)
- [FTC, The Rule on Unfair or Deceptive Fees: Frequently Asked Questions](https://www.ftc.gov/business-guidance/resources/rule-unfair-or-deceptive-fees-frequently-asked-questions) (retrieved 2026-07-20)
- [FTC press release, Bipartisan Rule Banning Junk Ticket and Hotel Fees (December 2024)](https://www.ftc.gov/news-events/news/press-releases/2024/12/federal-trade-commission-announces-bipartisan-rule-banning-junk-ticket-hotel-fees) (retrieved 2026-07-20)

**ROSCA and negative option**

- [Restore Online Shoppers' Confidence Act, Public Law 111-345 (29 December 2010, PDF)](https://www.congress.gov/111/plaws/publ345/PLAW-111publ345.pdf) (retrieved 2026-07-20)
- [15 U.S.C. Chapter 110, Online Shopper Protection (US House, current)](https://uscode.house.gov/view.xhtml?path=%2Fprelim%40title15%2Fchapter110&edition=prelim) (retrieved 2026-07-20)
- [15 U.S.C. 8404, Enforcement by Federal Trade Commission](https://www.law.cornell.edu/uscode/text/15/8404) (retrieved 2026-07-20)
- [FTC legal library, Restore Online Shoppers' Confidence Act](https://www.ftc.gov/legal-library/browse/statutes/restore-online-shoppers-confidence-act) (retrieved 2026-07-20)
- [Rule Concerning the Use of Prenotification Negative Option Plans, ANPRM, 91 FR 12318 (13 March 2026), comments due 13 April 2026](https://www.federalregister.gov/documents/2026/03/13/2026-04952/rule-concerning-the-use-of-prenotification-negative-option-plans) (retrieved 2026-07-20)
- [FTC press release, FTC Seeks Public Comment in Response to ANPRM Regarding Negative Option Marketing Practices (March 2026)](https://www.ftc.gov/news-events/news/press-releases/2026/03/ftc-seeks-public-comment-response-advance-notice-proposed-rulemaking-regarding-negative-option) (retrieved 2026-07-20)
- [FTC press release, FTC Submits Draft ANPRM Related to Negative Option Plans to OMB (January 2026)](https://www.ftc.gov/news-events/news/press-releases/2026/01/ftc-submits-draft-anprm-related-negative-option-plans-omb-review) (retrieved 2026-07-20)

**Penalties**

- [16 CFR 1.98, Adjustment of civil monetary penalty amounts](https://www.law.cornell.edu/cfr/text/16/1.98) (retrieved 2026-07-20)
- [Adjustments to Civil Penalty Amounts, 90 FR 5580 (17 January 2025)](https://www.federalregister.gov/documents/2025/01/17/2025-01361/adjustments-to-civil-penalty-amounts) (retrieved 2026-07-20)
- [Federal Register text of the 2025 adjustment, govinfo (PDF)](https://www.govinfo.gov/content/pkg/FR-2025-01-17/pdf/2025-01361.pdf) (retrieved 2026-07-20)
- [FTC press release, FTC Publishes Inflation-Adjusted Civil Penalty Amounts for 2025](https://www.ftc.gov/news-events/news/press-releases/2025/02/ftc-publishes-inflation-adjusted-civil-penalty-amounts-2025) (retrieved 2026-07-20)
- [OMB Memorandum M-26-11, Cancellation of Penalty Inflation Adjustments for 2026 (April 2026, PDF)](https://www.whitehouse.gov/wp-content/uploads/2026/04/M-26-11-Cancellation-of-Penalty-Inflation-Adjustments-for-2026-Regarding-the-Federal-Civil-Penalties-Inflation-Adjustment-Act-Improvements-Act-of-2015.pdf) (retrieved 2026-07-20)

**Overlapping state law**

- [California SB 478, Honest Pricing Law (bill text)](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202320240SB478) (retrieved 2026-07-20)
- [California Attorney General, SB 478 Hidden Fees resource page](https://oag.ca.gov/hiddenfees) (retrieved 2026-07-20)
- [California Attorney General, SB 478 FAQ (PDF)](https://oag.ca.gov/system/files/attachments/press-docs/SB%20478%20FAQ%20(B).pdf) (retrieved 2026-07-20)
- [California AB 2863, Automatic renewal and continuous service offers (bill text)](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202320240AB2863) (retrieved 2026-07-20)

**Secondary, used for case status and cross-checking only**

- [Sidley, U.S. FTC Click-to-Cancel Rule Struck Down (July 2025)](https://www.sidley.com/en/insights/newsupdates/2025/07/us-ftc-click-to-cancel-rule-struck-down) (retrieved 2026-07-20)
- [Gibson Dunn, FTC Restarts Negative Option Rulemaking After Eighth Circuit Vacatur](https://www.gibsondunn.com/ftc-restarts-negative-option-rulemaking-after-eighth-circuit-vacatur-enforcement-under-rosca-continues/) (retrieved 2026-07-20)
- [Alston & Bird, FTC Reaches Record $2.5 Billion Settlement with Amazon over Prime Subscription Practices](https://www.alston.com/en/insights/publications/2025/10/ftc-settlement-prime-subscription-practices) (retrieved 2026-07-20)
- [Covington, FTC Launches New Rulemaking on the Negative Option Rule (March 2026)](https://www.cov.com/en/news-and-insights/insights/2026/03/ftc-launches-new-rulemaking-on-the-negative-option-rule) (retrieved 2026-07-20)

---

## Notes

**Watch: the negative option rulemaking.** The FTC published its ANPRM on 13 March 2026 with
comments due 13 April 2026. The Commission may issue a Notice of Proposed Rulemaking, propose
narrower amendments, or drop it. Commentary suggests the same four themes will return (clear
and conspicuous disclosure of material terms, affirmative express consent, a simple cancellation
mechanism, and a bar on misrepresentations). Building subscription flows to those four standards
now is the low-cost path, and it is close to what ROSCA and California already demand. Re-check
this file's status line before any subscription build.

**The vacatur was procedural, not substantive.** The Eighth Circuit vacated the 2024 rule
because the FTC skipped a preliminary regulatory analysis after an ALJ found the economic impact
would exceed $100 million, not because the requirements were unlawful. The court held the failure
was not harmless because it deprived petitioners of an opportunity to dissuade the FTC. Do not
read the vacatur as approval of hard-to-cancel flows. The Amazon settlement landed on
25 September 2025, eleven weeks after the vacatur.

**State law is stricter than federal law on both fees and cancellation.** Two examples that
catch clients the federal rules miss:

- California SB 478 (in force since 1 July 2024) requires that any advertised or displayed price include all mandatory fees, for essentially all goods and services, with carve-outs, at Civil Code 1770(a)(29)(A), for government taxes and for postage or carriage reasonably and actually incurred to ship a physical good. A separate exemption at Civil Code 1770(a)(29)(D), added by later 2024 legislation, covers mandatory fees on individual food or beverage items sold by a restaurant, bar, food concession, grocery store, or grocery delivery service, but that exemption does not reach third-party food delivery platforms. Further sector carve-outs exist (the bill text names vehicle rentals, leases, dealer sales, and broadband among others), so check the statute for the client's sector rather than relying on this summary. This reaches clients that 16 CFR Part 464 does not.
- California AB 2863 amended the state Automatic Renewal Law with requirements applying to contracts entered into, amended, or extended on or after 1 July 2025, covering same-medium cancellation, express affirmative consent, free trials, annual renewal reminders, and advance notice of fee changes. The bill text sets the fee-change notice window at no less than 7 and no more than 30 days before the change takes effect.

If the client sells to California residents and takes recurring payments, build to the
California standard and the federal position resolves itself.

**Overlap with other files in this library.** Auto-renewal, price transparency, and refund terms
also appear in [`ecommerce-consumer-protection.md`](ecommerce-consumer-protection.md); treat that
file as the checkout-flow view and this one as the advertising-claims view. Review and
testimonial handling for regulated clients is stricter than this file: see
[`legal-industry-aba.md`](legal-industry-aba.md), where testimonials are restricted or barred
outright in some states, and [`financial-glba-sec.md`](financial-glba-sec.md), where the SEC
marketing rule governs adviser testimonials separately. Where the two conflict, the industry
rule wins.

**Unverified or unresolved.**

- UNVERIFIED: whether the FTC has served a Notice of Penalty Offenses concerning endorsements on any specific client. This determines whether Endorsement Guides violations carry civil penalties for that client. Check the FTC's penalty offenses recipient lists per client rather than assuming.
- UNVERIFIED: civil penalty amounts available under California SB 478 and the CLRA. The California AG page confirms enforcement and private remedies exist; this file does not state a figure because none was confirmed from an official source.
- 16 CFR 465.3 is reserved. The proposed "review hijacking" provision (reusing a review from one product on a substantially different product) was not finalized, because the FTC could not resolve how to define "substantially different product". The conduct can still be challenged as deception under Section 5, and the FTC noted it may revisit the provision. Do not repurpose reviews across products.
