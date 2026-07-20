# Ecommerce Consumer Protection: US and EU pre-purchase disclosure, price transparency, withdrawal, and subscription rules

| Field | Value |
|---|---|
| **Jurisdiction** | US (federal, plus California statute noted) and EU/EEA |
| **Regulator / enforcer** | US: Federal Trade Commission; state attorneys general (California AG and district attorneys under the ARL). EU: national consumer protection authorities coordinated through the CPC Network; national courts |
| **In force since** | Varies by instrument. EU Consumer Rights Directive: applied from 13 June 2014. EU Omnibus measures: applied from 28 May 2022. FTC Merchandise Rule: 1975 (as amended). ROSCA: 2010. California ARL: 2010, materially amended by AB 2863 for contracts entered, amended, or extended on or after 1 July 2025. FTC Rule on Unfair or Deceptive Fees: effective 12 May 2025 |
| **Last amended** | 12 February 2026: the FTC restored the pre-2024 text of the Negative Option Rule (16 CFR Part 425), withdrew the CARS Rule (Part 463), and removed the Non-Compete Rule (Part 910), conforming the CFR to court decisions (91 FR 6507) |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force, with one significant repeal. The FTC "click to cancel" rule is **vacated and gone**. See [Notes](#notes) before building any subscription flow |

This file covers transactional sites: anything that takes money for goods, services, digital content, or subscriptions. Privacy, cookies, and accessibility duties are in the sibling files (`gdpr.md`, `eprivacy-cookies.md`, `ccpa-cpra.md`, `ada-wcag.md`, `eu-accessibility-act.md`) and apply on top of everything here.

## Applies when

Work through these at intake. Each is answerable yes or no.

**EU Consumer Rights Directive (2011/83/EU) and the Omnibus amendments**

- The site concludes distance contracts with **consumers** (natural persons acting outside their trade or profession) resident in an EU or EEA member state. B2B-only sites are outside the consumer regime.
- Trigger is the **customer's location, not the business's**. A US business shipping to or serving EU consumers is caught if it directs activity at that market (language, currency, shipping options, country-specific domain, EU-targeted advertising).
- The withdrawal right attaches to distance and off-premises contracts. It does **not** apply to several categories, including custom or personalised goods, sealed goods unsealed after delivery for health or hygiene reasons, and digital content supplied where the consumer gave prior express consent to immediate performance and acknowledged loss of the withdrawal right (Article 16).
- Omnibus price-reduction rules bite the moment the site displays **any** price reduction claim: a strikethrough, a percentage off, "was/now", "sale".
- Omnibus review rules bite if the site displays consumer reviews or ratings, or states that reviews come from actual purchasers.
- Omnibus ranking rules bite if the site has a search function that returns products ranked by any parameter.

**Digital Services Act trader traceability (Regulation (EU) 2022/2065, Articles 30 to 32)**

- Applicable since **17 February 2024** for all in-scope intermediaries. Some VLOP and VLOSE provisions have applied since 16 November 2022.

- Applies only to an **online platform allowing consumers to conclude distance contracts with traders**. In build terms: a marketplace where third-party sellers transact with buyers.
- A single merchant selling only its own inventory is **not** caught by Articles 30 to 32. Do not bolt marketplace seller-verification onto a normal store.
- Providers that qualify as micro or small enterprises under Commission Recommendation 2003/361/EC are exempt from these obligations, unless designated a Very Large Online Platform.

**FTC Rule on Unfair or Deceptive Fees (16 CFR Part 464)**

- Applies **only** to two categories of covered good or service: (1) live-event tickets, and (2) short-term lodging, defined as "temporary sleeping accommodations at a hotel, motel, inn, short-term rental, vacation rental, or other place of lodging."
- This rule does **not** apply to general retail ecommerce. A clothing store, a SaaS product, or a food delivery site is outside Part 464. Generic FTC Section 5 deception law still applies to their pricing.

**FTC Mail, Internet, or Telephone Order Merchandise Rule (16 CFR Part 435)**

- Applies to any seller shipping physical merchandise ordered by mail, internet, or telephone to US buyers. This is the rule most US stores actually fall under, and most never hear of it.

**ROSCA (15 USC 8401 to 8405) and the Negative Option Rule (16 CFR Part 425)**

- ROSCA applies to any internet sale using a **negative option feature**: free trials converting to paid, auto-renewing subscriptions, continuity plans, and pre-checked upsells.
- The current 16 CFR Part 425 covers only **prenotification plans**: the book-club or record-club model where the seller periodically sends notice of a selection and ships it unless the subscriber declines. Ordinary auto-renewing subscriptions are not covered by Part 425 as it currently stands.

**California Automatic Renewal Law (Bus. & Prof. Code sections 17600 to 17606)**

- Applies to any business making an automatic renewal or continuous service offer to a **consumer in California**. There is no revenue or headcount threshold, and no carve-out for small sellers.
- The AB 2863 amendments apply to contracts "entered into, amended, or extended" on or after **1 July 2025**. A pre-existing subscriber base is on the old rules until the contract is amended or extended.
- Many other US states have their own automatic renewal statutes with differing notice windows. Treat California as the floor for a US-wide build, then check the specific states a client actually sells into.

## What the site must have

| Requirement | What that means in the build |
|---|---|
| **Total price before commitment (EU)** | Article 6(1)(e) CRD: total price inclusive of taxes, plus all delivery and additional charges, shown before the consumer is bound. If charges cannot be reasonably calculated in advance, say so and say how they will be calculated. Practically: show tax-inclusive prices to EU consumers on the product page, not just at checkout |
| **Order button wording (EU)** | Article 8(2) CRD: the button that concludes the order must be labelled "order with obligation to pay" or an equally unambiguous formulation. "Submit", "Continue", "Complete", and "Place order" alone are non-compliant. If the label is wrong, **the consumer is not bound by the contract**. Change the final button string, not just the copy above it |
| **No pre-ticked boxes for extras (EU)** | Article 22 CRD: express consent required for any payment beyond the main obligation. Insurance, expedited shipping, donations, warranties, and gift wrap all ship **unchecked** by default. A pre-ticked box entitles the consumer to reimbursement |
| **Withdrawal information (EU)** | Article 6(1)(h) CRD: before the order, disclose the existence of the 14-day withdrawal right, the conditions, the time limit, and the procedure, and supply the model withdrawal form. Where the right does not apply, say so explicitly (Article 6(1)(k)) |
| **14-day withdrawal right (EU)** | Article 9 CRD. For goods, the period runs from the day the consumer acquires physical possession. For services, from the day the contract is concluded. Build a returns/withdrawal page and an accessible withdrawal route; the consumer may use the model form or "any other unequivocal statement", so an email address must be honoured |
| **Penalty for not disclosing withdrawal (EU)** | Article 10 CRD: if withdrawal information is omitted, the period extends by **12 months**. If the trader supplies the information within that window, the period ends 14 days after the consumer receives it. A missing paragraph converts a 14-day exposure into a 12-month one |
| **Refund on withdrawal (EU)** | Article 13 CRD: reimburse all payments received, including delivery costs, within **14 days**, using the same means of payment the consumer used. Standard delivery cost is refundable; the premium portion of an upgraded shipping option is not. The trader may withhold reimbursement until the goods are back or proof of dispatch is supplied |
| **Return by the consumer (EU)** | Article 14 CRD: the consumer returns the goods within 14 days of notifying withdrawal and bears the direct cost of return **only if the trader informed them of that cost in advance**. If the returns page is silent on who pays, the trader pays |
| **Price reduction claims (EU)** | Article 6a of Directive 98/6/EC as inserted by the Omnibus Directive: any announcement of a price reduction must state the prior price, being the **lowest price applied by the trader during at least the 30 days** before the reduction. The strikethrough number is a computed value from price history, not a marketing input. Store a price history table and derive it |
| **Review authenticity (EU)** | Amended UCPD: stating that reviews come from actual consumers without taking "reasonable and proportionate steps" to check is an unfair practice. Submitting or commissioning fake reviews is banned outright (Annex I). Build verified-purchase checking, or remove any claim that reviews are from real buyers |
| **Ranking transparency (EU)** | Article 7(4a) UCPD: disclose the main parameters determining ranking in a dedicated section directly and easily accessible from the results page. Annex I point 11a: paid placement in search results must be labelled. Ship a "How we rank results" page linked from the results header, and an "Ad" or "Sponsored" badge on paid slots |
| **Trader identity and contact (EU)** | Article 6(1)(b) to (d) CRD: legal name, geographical address, telephone number, and email. Put it on an imprint or legal-notice page linked from the footer, not only in a contact form |
| **Complaints and dispute resolution (EU)** | Article 6(1)(t) CRD: disclose the availability of out-of-court complaint and redress mechanisms the trader is subject to. Note the ODR platform link requirement is no longer live: see [Notes](#notes) |
| **Marketplace trader traceability (EU, platforms only)** | DSA Article 30: before allowing a trader to sell, collect and store name, address, telephone, email, payment account details, identification document or equivalent, trade register entry, and a self-certification of legal compliance. Make best efforts to assess reliability. Retain for the contract duration **plus six months**. Article 31: design the interface so traders can supply the product-safety and identity information consumer law requires. Article 32: if illegal product listings are removed, inform affected buyers |
| **Total price disclosure (US, tickets and lodging only)** | 16 CFR 464.2: disclose the total price clearly and conspicuously in any advertising, and display it **more prominently** than other pricing information. Where the final payment amount is shown, it must be as prominent as or more prominent than the total price. Before the consumer consents to pay, disclose the nature, purpose, and amount of any excluded charge, and the final payment amount. Government charges, shipping, and optional add-ons sit outside "total price" but must still be itemised before payment |
| **Shipping timing (US)** | 16 CFR 435.2: have a reasonable basis to ship within the advertised time, or within **30 days** of a properly completed order if no time is stated (50 days where the buyer applies for credit to pay). If the date will slip, send a delay notice offering consent to the delay or cancellation with a prompt refund |
| **Refund timing (US)** | 16 CFR 435.1: a prompt refund is **7 working days** by cash, check, or money order where the payment was not a credit sale, or **one billing cycle** where the seller is the creditor. Encode these in the refunds runbook and the policy page |
| **Subscription disclosure (US federal)** | ROSCA 15 USC 8403: clearly and conspicuously disclose all material terms **before obtaining billing information**, get express informed consent to the charge, and provide a **simple mechanism** to stop recurring charges. Material terms mean the amount, the billing frequency, the renewal date, and the deadline to cancel before the next charge |
| **Subscription disclosure (California ARL)** | Present the automatic renewal terms clearly and conspicuously in visual proximity to the consent, covering: that the subscription continues until cancelled, how to cancel, the recurring charge amount and that it may change, the renewal term length, and any minimum purchase obligation. Obtain affirmative consent to those terms specifically, and **retain verification of that consent for at least three years, or one year after the contract terminates, whichever is longer** |
| **Post-purchase acknowledgement (California ARL)** | Send an acknowledgement the consumer can retain, containing the renewal terms, the cancellation policy, and cancellation instructions. For a free trial or gift offer, disclose how to cancel before the charge lands |
| **Online cancellation (California ARL)** | Where the consumer signed up online, they must be able to cancel online through "a prominently located direct link or button", or a clearly presented cancellation email route. No retention-offer maze, no phone-only cancellation, no obstruction. Cancellation must be available through the same medium used to sign up |
| **Renewal and price-change notices (California ARL)** | Automatic renewal terms of one year or longer require a reminder **15 to 45 days** before the renewal, stating the product, the charge amount and frequency, and how to cancel. Fee changes require notice **7 to 30 days** before the change takes effect, with cancellation information. Free trials or promotional periods longer than 31 days require notice **3 to 21 days** before expiry |
| **Consent and order records** | Store, per order: the exact terms displayed, timestamp, the consent event, the price shown, the shipping estimate given, and for subscriptions the renewal schedule and every notice sent. These are the evidence in a dispute. The California ARL floor is three years, or one year after the contract terminates, whichever is longer, so a long-lived subscription sets the clock, not the signup date; align with the retention schedule in `gdpr.md` for EU personal data |
| **Policy pages** | At minimum: Terms of Sale, Returns and Refunds (including the EU withdrawal right and the model withdrawal form), Shipping and Delivery, and a legal-notice/imprint block with trader identity. Link all of them from the global footer and from checkout before the pay button |

## How to verify

Run these against a staging build before delivery.

- **Order button string.** Grep the checkout component for the final submit label: `rg -i "place order\|complete order\|submit\|confirm\|continue\|pay now" src/`. For an EU-facing build, the terminal button must read "Order with obligation to pay" or equivalent. Confirm the rendered string in DevTools Elements, not only the source, because a translation layer may override it.
- **Pre-ticked extras.** In DevTools console on the cart and checkout pages, run `document.querySelectorAll('input[type=checkbox]:checked')` and confirm no result adds cost. Repeat after any address or shipping-method change, because some flows re-check on re-render.
- **Tax-inclusive display for EU.** Set a shipping country in the EU, then compare the product-page price against the checkout total. If tax appears only at checkout, the product page is non-compliant for consumer sales.
- **Strikethrough price provenance.** Grep for hardcoded compare-at prices: `rg -n "compareAtPrice\|was_price\|originalPrice\|msrp" src/`. Each must resolve to a stored price-history query, not a static field an admin types. Ask the client to show the 30-day price history for one discounted SKU and reconcile it against the displayed prior price.
- **Withdrawal information reachability.** From the product page, count clicks to reach the 14-day withdrawal text. It must be available before the order is placed. Confirm the model withdrawal form is downloadable or reproduced inline, and that the stated returns email actually delivers.
- **Return cost attribution.** Search the returns page for who pays return postage. If it is silent, flag it: silence means the trader pays under Article 14.
- **Cancellation path depth.** Log in as a test subscriber and count the interactions from account home to confirmed cancellation. One prominent link or button is the target. Any step that requires a phone call, a chat agent, an email to support with no acknowledgement, or more than one retention interstitial is a finding. Record the click path as delivery evidence.
- **Consent logging.** Place a test subscription order, then query the database for that order's consent record. Confirm it stores the rendered terms text or a version hash, plus a timestamp. A boolean `terms_accepted = true` is not sufficient proof of consent.
- **Renewal notice job.** Confirm a scheduled job exists for annual reminders, price-change notices, and trial-expiry notices, and that it is actually enabled in production config rather than defined and dormant. Check the queue dashboard, not the source.
- **Shipping promise.** Grep for delivery estimates in marketing copy: `rg -in "ships in\|delivered in\|arrives in\|business days" src/`. Each claim needs a reasonable basis. Confirm a delay-notification path exists for orders that pass the promised date.
- **Marketplace seller fields (platforms only).** In the seller onboarding schema, confirm fields exist for identification document, trade register number, payment account, and the self-certification. Confirm the retention policy keeps them for the contract term plus six months.
- **Ranking disclosure.** On a search results page, confirm a visible link to the ranking-parameters explanation and that sponsored results carry a label rendered in the DOM rather than painted into an image.

## Penalties

- **EU, widespread infringements.** The Omnibus Directive requires member states to provide maximum fines of **at least 4% of the trader's annual turnover** in the member state or states concerned, or **at least EUR 2 million** where turnover information is unavailable, for widespread infringements handled under the CPC coordinated procedure. Source: Directive (EU) 2019/2161 amending Article 13 of Directive 2005/29/EC. National ceilings vary and can be higher.
- **EU, order button defect.** Article 8(2) CRD, final subparagraph: the consumer "shall not be bound by the contract or order" where the button obligation is breached. The commercial consequence is unwound transactions rather than a fine.
- **EU, missing withdrawal information.** Article 10 CRD: withdrawal period extends by 12 months. The exposure is a year of unconditional returns.
- **US, FTC Act civil penalties.** Violations of a trade regulation rule (including 16 CFR Parts 435 and 464) expose the seller to civil penalties per violation under Section 5(m)(1)(A) of the FTC Act. The last figure confirmed for this file is **USD 53,088 per violation**, the adjustment effective 17 January 2025 (16 CFR 1.98). UNVERIFIED: the adjustment is annual, so a 2026 figure almost certainly supersedes it and could not be retrieved in this session. Check the current 16 CFR 1.98 text before quoting any number to a client.
- **California ARL.** UNVERIFIED: the ARL does not itself set a fixed civil penalty schedule; enforcement generally proceeds through the Unfair Competition Law (Bus. & Prof. Code section 17200) and private class actions, and unlawfully charged amounts are treated as unconditional gifts to the consumer under section 17603. Confirm the current remedy structure with counsel before advising a client on exposure.

## Common ways sites fail this

- Shipping a US-built store into the EU market with "Complete order" on the final button. This one string can void contracts.
- Storing the strikethrough price as an editable field the merchandiser types in, so the "was" price is whatever makes the discount look best.
- Pre-checking shipping insurance or a donation to lift average order value.
- Writing a returns page that describes the US 30-day return policy and never mentions the EU 14-day withdrawal right, which silently extends the right to 12 months.
- Building subscription signup in one click and cancellation through a support ticket.
- Claiming "verified reviews" or "reviews from real customers" with no purchase-matching logic behind it.
- Adding mandatory service fees at the last checkout step, then treating the earlier number as the advertised price.
- Copying marketplace-style seller verification into a single-merchant store because a compliance checklist said "DSA", adding onboarding friction the law never required here.
- Building the annual renewal reminder job, then never enabling it in production.
- Treating the vacated FTC click-to-cancel rule as still binding, or the reverse, assuming its vacatur removed all US subscription duties. ROSCA and state law never went away.
- Quoting delivery estimates in marketing copy that the fulfilment operation cannot meet, with no delay-notice path.

## Sources

Official sources first. All retrieved 2026-07-20.

- [Directive 2011/83/EU on consumer rights (consolidated text, EUR-Lex)](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32011L0083) - retrieved 2026-07-20. Articles 6, 8, 9, 10, 11, 13, 14, 22.
- [Directive (EU) 2019/2161 (Omnibus Directive), EUR-Lex](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32019L2161) - retrieved 2026-07-20. Article 6a of 98/6/EC, UCPD review and ranking amendments, penalties.
- [Regulation (EU) 2022/2065 (Digital Services Act), EUR-Lex](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32022R2065) - retrieved 2026-07-20. Articles 30, 31, 32 and the micro/small enterprise exemption.
- [16 CFR Part 464, Rule on Unfair or Deceptive Fees, section 464.1 definitions](https://www.law.cornell.edu/cfr/text/16/464.1) - retrieved 2026-07-20.
- [16 CFR 464.2, Hidden fees prohibited](https://www.law.cornell.edu/cfr/text/16/464.2) - retrieved 2026-07-20.
- [FTC Trade Regulation Rule on Unfair or Deceptive Fees, 90 FR 2066 (10 January 2025), govinfo](https://www.govinfo.gov/content/pkg/FR-2025-01-10/html/2024-30293.htm) - retrieved 2026-07-20. Effective date 12 May 2025; scope limited to live-event ticketing and short-term lodging.
- [16 CFR 435.1, definitions including "prompt refund"](https://www.law.cornell.edu/cfr/text/16/435.1) - retrieved 2026-07-20.
- [16 CFR 435.2, Mail, Internet, or Telephone Order Merchandise Rule](https://www.law.cornell.edu/cfr/text/16/435.2) - retrieved 2026-07-20.
- [15 USC 8403, ROSCA negative option requirements](https://www.law.cornell.edu/uscode/text/15/8403) - retrieved 2026-07-20.
- [16 CFR Part 425, current text (Use of Prenotification Negative Option Plans)](https://www.law.cornell.edu/cfr/text/16/425.1) - retrieved 2026-07-20.
- [Custom Communications, Inc. v. FTC, Nos. 24-3137, 24-3388, 24-3415, 24-3442 (8th Cir. 8 July 2025), slip opinion](https://ecf.ca8.uscourts.gov/opndir/25/07/243137P.pdf) - retrieved 2026-07-20. URL resolves and returns the slip opinion PDF, but the text layer could not be extracted in this session; the holding is corroborated independently by 91 FR 6507.
- [FTC, "Revision of the Negative Option Rule, Withdrawal of the CARS Rule, Removal of the Non-Compete Rule To Conform These Rules to Federal Court Decisions", final rule, 91 FR 6507 (12 February 2026), effective on publication](https://www.federalregister.gov/documents/2026/02/12/2026-02866/revision-of-the-negative-option-rule-withdrawal-of-the-cars-rule-removal-of-the-non-compete-rule-to) - retrieved 2026-07-20. federalregister.gov blocks automated retrieval; the govinfo mirror at https://www.govinfo.gov/content/pkg/FR-2026-02-12/html/2026-02866.htm serves the same text (91 FR 6507-6510).
- [Regulation (EU) 2024/3228 repealing Regulation (EU) No 524/2013 on online dispute resolution, EUR-Lex](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32024R3228) - retrieved 2026-07-20. Repeal effective 20 July 2025; complaint submission discontinued 20 March 2025.
- [EUR-Lex summary of the Digital Services Act, application dates](https://eur-lex.europa.eu/EN/legal-content/summary/digital-services-act.html) - retrieved 2026-07-20. Applies from 17 February 2024; some VLOP/VLOSE rules from 16 November 2022.
- [California Business and Professions Code sections 17600 to 17606 (Automatic Renewal Law), California Legislative Information](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=BPC&division=7.&title=&part=3.&chapter=1.&article=9.) - retrieved 2026-07-20.
- [California AB 2863 (2023-2024), bill history and text](https://leginfo.legislature.ca.gov/faces/billNavClient.xhtml?bill_id=202320240AB2863) - retrieved 2026-07-20. Approved 24 September 2024; applies to contracts entered into, amended, or extended on or after 1 July 2025.

## Notes

**The FTC click-to-cancel rule is dead. Do not cite it.** The 2024 Rule Concerning Recurring Subscriptions and Other Negative Option Programs was vacated in full by the Eighth Circuit on 8 July 2025. The court held the FTC's rulemaking was procedurally insufficient because it skipped the required preliminary regulatory analysis, and found prejudicial error. UNVERIFIED: the exact concluding sentence previously quoted here ("Accordingly, we grant the petitions for review and vacate the Rule.") and the statements that the court declined party-specific vacatur and overrode the severability clause could not be confirmed against the slip opinion text in this session. The vacatur itself and its procedural ground are confirmed by the FTC's own conforming rule at 91 FR 6507, which describes the Commission's failure to issue a preliminary regulatory analysis as "procedurally insufficient". On 12 February 2026 the FTC conformed the CFR by restoring the pre-2024 Part 425 text, and in the same document withdrew the CARS Rule and removed the Non-Compete Rule. Any client-facing guidance, boilerplate, or checklist in this studio that still references a federal click-to-cancel mandate needs correcting.

**What survived the vacatur.** ROSCA (15 USC 8403) is a statute, untouched by the ruling, and still requires clear pre-billing disclosure, express informed consent, and a simple cancellation mechanism. California's ARL is untouched and is stricter than ROSCA on cancellation UI. In practice the build target for subscriptions barely moves: build the easy online cancellation anyway, because California requires it and the FTC can still bring Section 5 and ROSCA actions.

**Scope discipline on the FTC fees rule.** Part 464 covers live-event tickets and short-term lodging only. Applying it to a general store is a harmless over-delivery, but claiming a general store is legally obliged under Part 464 is wrong and will damage credibility with a client's counsel. General ecommerce pricing deception is handled under FTC Act Section 5 and state UDAP statutes instead.

**The EU ODR platform link is dead too.** Regulation (EU) 2024/3228 of 19 December 2024 repealed Regulation (EU) No 524/2013 with effect from **20 July 2025**. The platform stopped accepting new complaints on **20 March 2025**, and platform case data was to be deleted by 20 July 2025. Do not add the ODR link to new builds, and strip it from existing client sites along with any Terms copy that promises it. The Article 6(1)(t) CRD duty to disclose out-of-court redress mechanisms the trader is actually subject to survives; only the ODR platform link requirement is gone.

**UNVERIFIED items to close before relying on them.**
- Current inflation-adjusted FTC civil penalty maxima per violation. The 17 January 2025 adjustment set USD 53,088; the 2026 adjustment could not be retrieved because federalregister.gov and ecfr.gov both blocked the request. Check 16 CFR 1.98 before quoting.
- The status of the EU **Digital Fairness Act** could not be confirmed. It has been under development to address dark patterns, personalised pricing, addictive design, and influencer marketing, and would land directly on checkout and subscription UX. Confirm whether it has been proposed, agreed, or is in force before advising, and re-check this file when it moves.
- The exact concluding disposition language of the Eighth Circuit opinion, flagged inline above.

**Cross-references and conflicts within this library.**
- `ftc-disclosures.md` covers advertising claims, endorsements, and influencer disclosure. The Omnibus review rules here overlap with it on fake reviews; the EU rule is a strict prohibition plus a verification duty, which is stronger than the US endorsement guides.
- `gdpr.md` governs the consent and order records this file requires you to keep. The California ARL retention floor (three years, or one year post-termination, whichever is longer) must still satisfy GDPR storage limitation for EU customers. Keep the two schedules explicit rather than defaulting to "keep forever".
- `eprivacy-cookies.md` governs analytics on checkout pages. Do not let a conversion-tracking script fire pre-consent inside a checkout flow.
- `ada-wcag.md` and `eu-accessibility-act.md` apply to the checkout and cancellation UI. A cancellation button that only works with a mouse fails both the accessibility rules and the ARL's "without obstruction" standard.

**Watch item: state-by-state US subscription law.** With the federal rule vacated, states are the active front. California is the strictest widely applicable one and is the sensible build floor, but several states have their own notice windows and cancellation rules. For a client selling nationally, confirm the specific states in scope rather than assuming California compliance is sufficient everywhere.
