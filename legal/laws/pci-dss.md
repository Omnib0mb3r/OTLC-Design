# PCI DSS: Payment Card Industry Data Security Standard, version 4.0.1

| Field | Value |
|---|---|
| **Jurisdiction** | Global, and not a law. PCI DSS is a private contractual standard imposed through the card brand rules that flow down from Visa, Mastercard, American Express, Discover, and JCB, through the acquiring bank, into the client's merchant agreement. It binds anyone who accepts branded payment cards anywhere. Breaching it is a contract breach, not a statutory offence, but the money consequences are real and the acquirer can stop the client taking cards. |
| **Regulator / enforcer** | The PCI Security Standards Council writes and publishes the standard. It does **not** enforce it and levies no fines. Enforcement runs through the individual card brands and their compliance programs (Visa, Mastercard Site Data Protection), which act on the acquiring bank, which acts on the merchant. The merchant's practical counterparty is the acquirer or payment facilitator (Stripe, Adyen, Square, a bank). |
| **In force since** | PCI DSS v1.0 published December 2004. Version 4.0 published March 2022. Version 4.0.1 published June 2024 and effective immediately on publication. |
| **Last amended** | v4.0.1 (June 2024) is a limited revision with zero new and zero deleted requirements: typo corrections and clarifications only. The material change since then is at the SAQ level: a revised **SAQ A published January 2025**, effective 31 March 2025. A PCI SSC information supplement for Requirements 6.4.3 and 11.6.1 was published 10 March 2025. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force, fully. v3.2.1 retired 31 March 2024. v4.0 retired 31 December 2024, leaving v4.0.1 as the only active version. The 51 future-dated v4.0 requirements stopped being best practice and became mandatory on **31 March 2025**. As of this review there is no transition period left and no phase-in remaining: every requirement in v4.0.1 is assessable today. |

## Applies when

PCI DSS is not scoped by company size. There is no revenue floor, no employee count, and no record count that exempts anyone. If the client takes card payments, it applies. What size changes is **how the client proves it**, not whether the client owes it.

**Does the standard apply at all**

- [ ] The client accepts, or the site will accept, payment cards branded Visa, Mastercard, American Express, Discover, or JCB. If yes, PCI DSS applies. Stop looking for an exemption.
- [ ] OR the client's systems store, process, or transmit cardholder data (the primary account number, cardholder name, expiry date, service code).
- [ ] OR the client's systems could **affect the security** of the cardholder data environment. This is the clause that catches studio-built marketing sites. A website that hosts the page containing the payment iframe, or the page that redirects to the processor, can affect the security of the payment even though card data never touches it.
- [ ] The site takes donations, deposits, bookings, or subscription payments by card. All of these are card acceptance. "We are a charity" and "it is only a booking deposit" are not carve-outs.

**Who is NOT caught**

- A site that links out to a completely separate domain the client does not control and does not build, where the client has no merchant account (for example, a restaurant page linking to an independent third-party booking brand that is the merchant of record). The client is not a merchant on those transactions.
- A brochure site with no payment path, no card fields, and no payment iframe. Note that this can change silently the moment marketing adds a "Buy now" embed.
- Payment methods that are not card scheme transactions (bank transfer, direct debit, invoice, cash on delivery, and most account-to-account wallets). Watch the wallet case: PayPal, Apple Pay, and Google Pay usually ride card rails, and the merchant is still a merchant.

**Which merchant level the client sits in (this sets the validation burden)**

Levels are set by each card brand independently, counted on annual transaction volume, and assigned by the acquirer. Take the highest level any brand assigns.

Visa, per Visa's published compliance validation criteria:

- [ ] **Level 1**: more than 6 million Visa transactions per year, all channels. Requires an annual Report on Compliance by a QSA plus quarterly ASV scans.
- [ ] **Level 2**: 1 million to 6 million Visa transactions per year, all channels. Annual SAQ plus quarterly ASV scans.
- [ ] **Level 3**: 20,000 to 1 million Visa **e-commerce** transactions per year. Annual SAQ plus quarterly ASV scans.
- [ ] **Level 4**: fewer than 20,000 Visa e-commerce transactions per year, and all other merchants up to 1 million Visa transactions per year. SAQ recommended, with validation requirements set by the acquirer.

Mastercard, per the Site Data Protection program:

- [ ] **Level 1**: more than 6 million Mastercard and Maestro transactions per year. Annual assessment producing a ROC and AOC signed by a QSA, a PCI SSC certified ISA, or (unless prohibited by law) an executive officer of the merchant.
- [ ] **Level 2**: more than 1 million and up to and including 6 million per year. (Mastercard's published wording is "greater than one million but less than or equal to six million"; a merchant at exactly 6 million is Level 2, not Level 1.) Annual SAQ. A Level 2 merchant completing SAQ A, SAQ A-EP, or SAQ D must additionally engage a QSA or ISA for validation. This surprises clients: an SAQ does not always mean self-service.

Every client a small studio builds for is almost certainly Level 4, occasionally Level 3. That means the acquirer decides what evidence it wants, and the acquirer usually wants an SAQ plus a passing quarterly ASV scan.

**Any-level override**

- [ ] A merchant that suffers an account data compromise can be escalated to Level 1 by the brand regardless of volume. Build as if this could happen.

**Which SAQ the site will use (decide this at intake, before design)**

This is the single most consequential question in the project, because SAQ A is roughly a dozen pages of controls and SAQ A-EP is several times that with a mandatory penetration test.

- [ ] **SAQ A**: card-not-present only (e-commerce or mail/telephone order), with **all** processing of account data outsourced to a PCI DSS compliant third-party service provider or payment processor. The merchant stores, processes, and transmits no account data electronically. This is the target. See the eligibility criteria below, which tightened on 31 March 2025.
- [ ] **SAQ A-EP**: e-commerce only. The merchant's site does not receive account data, but it **controls how the customer or the account data is redirected** to the compliant processor, or it delivers elements of the payment page itself. Direct post, JavaScript that composes the payment form, and merchant-controlled tokenization flows land here.
- [ ] **SAQ D (Merchant)**: everything that fits nothing else, including anything that touches or stores a PAN. If a project drifts here, the compliance cost stops being a line item and starts being a project.
- [ ] Other SAQs exist for card-present and telephone environments: **B** (imprint or standalone dial-out terminals), **B-IP** (standalone IP terminals), **C** (payment application connected to the internet), **C-VT** (virtual terminal, manual single-transaction keying), **P2PE** (validated point-to-point encryption terminals), and **SPoC** (PCI-listed software-based PIN entry on COTS). A web studio will rarely own these, but a client may be completing one for its in-store estate at the same time.

**The SAQ A eligibility criteria that changed on 31 March 2025**

The January 2025 SAQ A **removed Requirements 6.4.3 and 11.6.1 from the questionnaire**, and removed the Requirement 12.3.1 targeted risk analysis tied to 11.6.1. It did not make the underlying risk go away. It converted the obligation into an **eligibility criterion**, in these terms:

> "The merchant has confirmed that their site is not susceptible to attacks from scripts that could affect the merchant's e-commerce system(s)."

Per **PCI SSC FAQ 1588**, a merchant meets that criterion one of two ways:

1. Implement the techniques described in Requirements 6.4.3 and 11.6.1 to protect the page from script attacks, directly or through a third party, or
2. Obtain confirmation from the compliant TPSP or payment processor providing the embedded payment page or form that, when implemented per the provider's instructions, the provider's solution includes techniques that protect the merchant's payment page from script attacks.

FAQ 1588 states this criterion applies **only to e-commerce merchants with embedded payment pages or forms (iframes)**. It does not apply to merchants that redirect the customer away, or that fully outsource the payment function. Read that carefully at intake, because it is the strongest argument in this file for choosing a redirect over an embed on a small build.

**The ASV scan trap in SAQ A**

SAQ A under v4.x is not scan-free. PCI SSC added external vulnerability scanning by an Approved Scanning Vendor (Requirement 11.3.2) to SAQ A, and it applies to the merchant system that hosts the webpage that either redirects payment transactions to a compliant TPSP or embeds the TPSP's payment page or form. In build terms: **the marketing site the studio ships is in ASV scan scope**, at least quarterly and after significant change, even on the lightest SAQ. Budget for it and tell the client before launch, not after.

## What the site must have

The table below is scoped to what a studio-built site actually controls. It assumes the target is SAQ A with a hosted or redirect integration, and flags where SAQ A-EP adds work.

| Requirement | What that means in the build |
|---|---|
| **Zero card fields on the merchant origin** | No `<input>` collecting a PAN, CVV, expiry, or cardholder name that posts to the client's own server. The card fields must live inside the processor's iframe, or on the processor's own page after a redirect. Grep the built output for `card`, `cardnumber`, `cvc`, `cvv`, `expiry`, and `autocomplete="cc-number"` on any form whose `action` points at the merchant domain. Any hit means the project is SAQ A-EP or worse. |
| **Prefer redirect or a full processor-hosted page** | Stripe Checkout, a hosted payment page, or a server-side 302 to the processor takes the payment form off the merchant origin entirely. This is what makes SAQ A available and, per FAQ 1588, sidesteps the script-susceptibility eligibility criterion altogether. Redirect via a server-side redirect or a plain link rather than client-side JavaScript, so that no merchant script sits in the payment path. |
| **If an iframe embed is used (Stripe Elements, hosted fields)** | Card fields render in a cross-origin iframe served by the processor. The merchant page never reads keystrokes. This keeps card data off the merchant's servers, but the **containing page** is now in scope for the script-susceptibility criterion, so either implement 6.4.3 and 11.6.1 controls on that page or get the processor's written confirmation per FAQ 1588. Keep that confirmation in the project file. |
| **Do not use processor JS that composes the form yourself** | Building your own card inputs and calling a tokenization JS API on them puts the merchant's own script in contact with the PAN in the browser. That is SAQ A-EP territory: full 6.4.3 and 11.6.1, plus penetration testing under Requirement 11.4, plus a much longer questionnaire. |
| **Requirement 6.4.3, script authorization and integrity** (mandatory since 31 March 2025; in scope for SAQ A-EP and SAQ D, and for SAQ A merchants meeting eligibility via route 1) | Three separate things, all required: (a) a method that confirms **each script on the payment page is authorized**, (b) a method that **assures the integrity of each script**, and (c) an **inventory of all scripts** with a written business or technical justification for why each is necessary. In practice: a documented script allowlist, Subresource Integrity hashes or an equivalent integrity mechanism on every third-party script, and a maintained inventory file that a human signed off. On CSP: the PCI SSC information supplement says CSP "can be quite effective for script authorization and, to some extent, script integrity", and that hash- or nonce-based directives "can further enforce integrity". A source-allowlist CSP on its own is authorization control, not integrity assurance; pair it with SRI hashes or nonce/hash-based CSP, and note that neither substitutes for the inventory and justification element. |
| **Requirement 11.6.1, change and tamper detection** (same applicability) | A mechanism that alerts personnel to unauthorized modification, including indicators of compromise, changes, additions, and deletions, to the **security-impacting HTTP headers and the script contents of payment pages as received by the consumer browser**. Two words carry the weight: "as received by the consumer browser." Server-side file integrity monitoring does not satisfy this, because it cannot see a CDN, a tag manager, or a compromised third party injecting downstream. The mechanism must run at least once every seven days, or at a frequency justified by a documented targeted risk analysis under Requirement 12.3.1. Client-side monitoring vendors exist for this; a synthetic browser check that diffs headers and script hashes is the buildable minimum. |
| **Strip everything else off the payment page** | Remove analytics, session replay, chat widgets, A/B testing, heatmaps, ad pixels, and tag managers from the payment page and from any page that hosts the payment iframe. Every one of them is a script you would otherwise have to authorize, hash, inventory, justify, and monitor. Session replay (Hotjar, FullStory, Clarity) is the worst case: it can capture form field contents and quietly pull the client into card data storage. |
| **Requirement 4.2.1, strong cryptography in transit** | PAN must be protected with strong cryptography and security protocols whenever it crosses open, public networks. PCI DSS deliberately does **not** name a TLS version. It rules out SSL (all versions) and early TLS (1.0 and 1.1) as not strong cryptography, and points to industry references such as the current NIST SP 800-52 for configuration. Build to TLS 1.2 as the floor and TLS 1.3 as the default, with weak ciphers and renegotiation disabled. Certificates must be valid and unexpired, with revocation checked. Keep an inventory of the certificates and keys used to protect PAN in transit. |
| **HTTPS everywhere, not just checkout** | Serve the whole site over TLS with HSTS. A plain-HTTP page that links or redirects to the payment page is an injection point for the redirect itself, which is the exact Magecart pattern the 2025 SAQ A changes were written against. |
| **Requirement 12.8, third-party service provider management** | The client must maintain a list of every TPSP with which account data is shared or that can affect the security of the cardholder data environment, hold written agreements that acknowledge the TPSP's responsibility for the data, run due diligence before engaging one, and monitor each TPSP's PCI DSS compliance status at least once every 12 months. Practical deliverable: a table in the handover file naming the processor, the CDN, the hosting provider, and the studio, with each party's AOC or compliance page linked and a responsibility split written down. |
| **The studio itself may be a TPSP** | A studio that hosts, maintains, or deploys code to the page containing the payment iframe can affect the security of the CDE. Expect clients (or their acquirers) to ask for the studio's own attestation or a written responsibility matrix. Decide the studio's position on this before a client asks. |
| **Never store sensitive authentication data** | CVV, full track data, and PIN blocks must never be stored after authorization, encrypted or not. This kills a whole class of "helpful" features: no logging of POST bodies on payment endpoints, no storing the card number for a later "quick reorder", no emailing card details to the client's inbox, no card fields in a CRM note or a contact form. |
| **Records to keep** | The script inventory with justifications, the 11.6.1 alert log and its targeted risk analysis, quarterly passing ASV scan reports, the annual SAQ and signed Attestation of Compliance, the TPSP list with compliance evidence, and the processor's written confirmation under FAQ 1588 if that route was used. PCI DSS requires audit log history to be retained for at least 12 months with the most recent 3 months immediately available. |

## How to verify

Run these before delivery, on the production build, not on a local dev server.

1. **Find the card fields.** Open the checkout, then DevTools Elements panel. Confirm every card input is inside an `<iframe>` whose `src` origin belongs to the processor, or that the browser has left the merchant domain entirely. Then run `document.querySelectorAll('input')` in the console on the top document and confirm no card-shaped field is returned. A field in the top document is a scope failure.
2. **Grep the source.** Search the built output for `cc-number`, `cardnumber`, `card_number`, `cvv`, `cvc`, `expiry`, `exp_month`, `exp_year`. Then search the server routes for any handler that accepts those names. Any handler that receives a PAN moves the project to SAQ D.
3. **Watch the network on submit.** DevTools Network panel, preserve log on, submit a test card. Every request carrying card data must go to the processor's domain. Filter to the merchant's own domain and confirm no request body contains card digits. Check XHR, fetch, beacons, and WebSocket frames, not just document loads.
4. **Count the scripts on the payment page.** In the Network panel, filter to JS, and list every distinct origin loading script on the payment page and on the page containing the payment iframe. If the list is longer than the processor plus your own bundle, cut it. Then check the same list against the script inventory document. Anything on the page that is not in the inventory is a 6.4.3 finding.
5. **Check integrity attributes.** Grep the payment page HTML for `<script src` and confirm every third-party entry carries an `integrity=` hash and `crossorigin=`. A script loaded from a tag manager or injected at runtime will not appear in the HTML, which is exactly why tag managers do not belong on this page.
6. **Check the response headers.** `curl -sI https://client.example/checkout` and read `Content-Security-Policy`, `Strict-Transport-Security`, `X-Frame-Options` or CSP `frame-ancestors`, and `Referrer-Policy`. Record the header set: 11.6.1 monitoring is a diff against a known good baseline, so the baseline has to exist.
7. **Hunt session replay and analytics.** With an ad blocker disabled, load the payment page and check the Network panel for calls to replay or analytics vendors. Then open the vendor's own dashboard and confirm the checkout path is excluded and input masking is on. Do not take the vendor's default on trust; look at a recorded session.
8. **Test the TLS configuration.** Run the site through an external TLS test (Qualys SSL Labs or `nmap --script ssl-enum-ciphers -p 443`), and confirm TLS 1.0 and 1.1 are refused, the certificate chain is valid and unexpired, and no weak or export cipher suites are offered. Test the API and any subdomain that serves the payment page, not only the apex.
9. **Force HTTP.** Request `http://client.example/checkout` and confirm a 301 to HTTPS plus an HSTS header on the response. Then confirm every internal link into the payment flow is already HTTPS, so no user is redirected mid-flow.
10. **Test the redirect path.** If the integration is a redirect, confirm it is issued server-side (a 3xx with a `Location` header) rather than by client-side JavaScript. Disable JavaScript and confirm the payment path still works. A JS-only redirect puts merchant script into the payment path.
11. **Confirm the ASV scan is booked.** Ask who the client's ASV is and when the scan runs. The scan applies to the host serving the redirect or embed page. If nobody has booked one, the client will fail its first validation regardless of how clean the build is. Flag it in the handover document.
12. **Get the processor's confirmation in writing.** For iframe integrations, capture the processor's statement that its solution protects the payment page from script attacks when implemented per instructions, and save it in the project file. It is the evidence for SAQ A eligibility under FAQ 1588.
13. **Re-read the SAQ eligibility criteria as published.** Do not rely on this file's summary for the final answer. Download the current SAQ from the PCI SSC document library, read the eligibility section, and confirm the built integration matches it point by point.

## Penalties

There is no statutory fine, because this is not a statute. The money moves through the contract chain.

- **The PCI SSC levies no fines at all.** It publishes the standard and runs the assessor programs. Any claim that "the PCI Council fined a business" is wrong on its face.
- Card brands assess non-compliance amounts against the **acquiring bank**, which passes them to the merchant under the merchant agreement. The brands do not publish a public fine schedule, and the amounts are set in confidential brand operating rules.
- **UNVERIFIED:** the widely repeated figures of roughly $5,000 to $10,000 per month for early non-compliance, rising to $50,000 to $100,000 per month after several months, appear consistently across compliance vendor and consultancy publications but were **not** traced to any published Visa or Mastercard rule during this review. Cite them to a client as "commonly reported industry figures, not published rates". Do not present them as a schedule.
- **UNVERIFIED:** per-compromised-card recovery amounts (often quoted at roughly $50 to $90 per card) were likewise not traced to a published brand rule. These flow through brand account data compromise recovery programs, whose amounts are not public.
- Consequences that are **not** in doubt and are worth telling a client plainly: the acquirer can raise the merchant's transaction rates, can require a forensic investigation by a PCI Forensic Investigator at the merchant's cost after a suspected compromise, can escalate the merchant to Level 1 validation, and can terminate the merchant account. Losing card acceptance is usually the outcome that actually hurts.
- A "PCI non-compliance fee" charged monthly by the processor or acquirer (commonly tens of dollars per month) is a separate, contractual, and openly disclosed line item, not a brand fine. Many small merchants pay it for years because nobody ever completed the SAQ.
- Separately, a card data breach triggers the ordinary breach notification statutes and privacy regulators that other files in this library cover. PCI exposure and statutory exposure stack.

## Common ways sites fail this

- Assuming that using Stripe, Square, or PayPal makes the client compliant. The processor's compliance covers the processor. The merchant still owes an SAQ, still owes the ASV scan on the page that hosts the redirect or embed, and still owns everything on its own origin.
- Loading Google Tag Manager, an analytics snippet, or a chat widget on the checkout page, so a page that could have carried one script now carries a dozen that must each be authorized, hashed, inventoried, justified, and monitored.
- Session replay recording the checkout with masking off or misconfigured, which captures card data into a third-party vendor and drags the client toward SAQ D.
- Building custom card inputs on top of a tokenization JS library because the processor's default styling looked wrong, then filing the project as SAQ A. That is SAQ A-EP.
- Doing the redirect in client-side JavaScript rather than server-side, so merchant script sits in the payment path.
- Treating the January 2025 removal of 6.4.3 and 11.6.1 from SAQ A as a cancellation. It moved the obligation into an eligibility criterion. A merchant that neither implements the controls nor holds the processor's confirmation is not eligible for SAQ A and should be completing SAQ A-EP.
- Interpreting 11.6.1 as server-side file integrity monitoring. The requirement is explicitly about content **as received by the consumer browser**, which is downstream of the server.
- Never running an ASV scan, because "SAQ A does not need scans." That was true under v3.2.1. It is not true under v4.x.
- Logging full request bodies on payment endpoints, so PANs and CVVs land in application logs, error trackers, and log aggregation vendors.
- Emailing card details, or letting staff take a card number over the phone and type it into a CRM note or a support ticket. This is the most common way a low-scope merchant becomes a high-scope merchant.
- Letting the TLS configuration rot after launch: an expired certificate, TLS 1.0 left enabled on an API subdomain, or a legacy cipher suite kept for one old integration.
- Shipping a compliant checkout and then letting the client's marketing team add a tag to it three months later, with no monitoring in place to notice.
- Nobody owning quarterly re-validation, so the SAQ is completed once at launch and never again.

## Sources

Official sources first. All retrieved 2026-07-20.

- [PCI Security Standards Council, Document Library (current PCI DSS v4.0.1, SAQs, AOCs, and information supplements; access requires accepting the licence agreement)](https://www.pcisecuritystandards.org/document_library/) (retrieved 2026-07-20)
- [PCI SSC Blog, Just Published: PCI DSS v4.0.1](https://blog.pcisecuritystandards.org/just-published-pci-dss-v4-0-1) (retrieved 2026-07-20)
- [PCI SSC Blog, Now is the Time for Organizations to Adopt the Future-Dated Requirements of PCI DSS v4.x](https://blog.pcisecuritystandards.org/now-is-the-time-for-organizations-to-adopt-the-future-dated-requirements-of-pci-dss-v4-x) (retrieved 2026-07-20)
- [PCI SSC Blog, Important Updates Announced for Merchants Validating to Self-Assessment Questionnaire A](https://blog.pcisecuritystandards.org/important-updates-announced-for-merchants-validating-to-self-assessment-questionnaire-a) (retrieved 2026-07-20)
- [PCI SSC Blog, FAQ Clarifies New SAQ A Eligibility Criteria for E-Commerce Merchants](https://blog.pcisecuritystandards.org/faq-clarifies-new-saq-a-eligibility-criteria-for-e-commerce-merchants) (retrieved 2026-07-20)
- [PCI SSC FAQ 1588, How does an e-commerce merchant meet the SAQ A eligibility criteria for scripts?](https://www.pcisecuritystandards.org/faqs/1588) (retrieved 2026-07-20)
- [PCI SSC FAQ 1491, Does PCI DSS define which versions of TLS must be used?](https://www.pcisecuritystandards.org/faqs/1491) (retrieved 2026-07-20)
- [PCI SSC Blog, PCI DSS v4: What's New with Self-Assessment Questionnaires (confirms ASV scanning added to SAQ A)](https://blog.pcisecuritystandards.org/pci-dss-v4-whats-new-with-self-assessment-questionnaires) (retrieved 2026-07-20)
- [PCI SSC Blog, New Information Supplement: Payment Page Security and Preventing E-Skimming](https://blog.pcisecuritystandards.org/new-information-supplement-payment-page-security-and-preventing-e-skimming) (retrieved 2026-07-20)
- [PCI SSC Blog, Coffee with the Council Podcast: Guidance for PCI DSS E-commerce Requirements Effective After 31 March 2025](https://blog.pcisecuritystandards.org/coffee-with-the-council-podcast-guidance-for-pci-dss-e-commerce-requirements-effective-after-31-march-2025) (retrieved 2026-07-20)
- [PCI SSC Blog, Resource Guide: Vulnerability Scans and Approved Scanning Vendors](https://blog.pcisecuritystandards.org/resource-guide-vulnerability-scans-and-approved-scanning-vendors) (retrieved 2026-07-20)
- [PCI SSC Bulletin, SAQs for PCI DSS v4.0.1 Now Available (PDF, October 2024)](https://www.pcisecuritystandards.org/wp-content/uploads/2024/10/SAQs_for_PCI_DSS_v4.0.1_Bulletin.pdf) (retrieved 2026-07-20)
- [PCI DSS v4.0 SAQ A (PDF, superseded by the v4.0.1 and January 2025 versions; useful for the eligibility section wording)](https://listings.pcisecuritystandards.org/documents/PCI-DSS-v4-0-SAQ-A.pdf) (retrieved 2026-07-20)
- [PCI DSS v4.0 SAQ A-EP (PDF)](https://listings.pcisecuritystandards.org/documents/PCI-DSS-v4-0-SAQ-A-EP.pdf) (retrieved 2026-07-20)
- [PCI SSC Information Supplement, Payment Page Security and Preventing E-Skimming: Guidance for PCI DSS Requirements 6.4.3 and 11.6.1 (PDF, March 2025; this link is a third-party mirror, prefer the Document Library copy)](https://scotthelme.co.uk/content/files/2025/03/Guidance-for-PCI-DSS-Requirements-6_4_3-and-11_6_1.pdf) (retrieved 2026-07-20)
- [Visa, Validation of Compliance (merchant levels 1 to 4 and validation requirements)](https://caribbean.visa.com/run-your-business/small-business/information-security/compliance-validation.html) (retrieved 2026-07-20)
- [Visa Corporate, Security and Compliance (merchant level determined by 12-month Visa transaction volume)](https://corporate.visa.com/en/resources/security-compliance.html) (retrieved 2026-07-20)
- [Mastercard, Site Data Protection (SDP) Program and PCI](https://www.mastercard.com/global/en/business/cybersecurity-fraud-prevention/site-data-protection-pci.html) (retrieved 2026-07-20)
- [Mastercard, Revised PCI DSS Compliance Requirements for Level 2 Merchants (PDF)](https://www.mastercard.com/content/dam/public/mastercardcom/globalrisk/pdf/Revised_PCI_DSS_Compliance_Requirements_for_L2_Merchants.pdf) (retrieved 2026-07-20)
- [Mastercard, Site Data Protection Program Frequently Asked Questions (PDF, 1 June 2024)](https://www.mastercard.com/content/dam/public/mastercardcom/globalrisk/pdf/Site%20Data%20Protection%20Program%20FAQs%20(1%20June%202024).pdf) (retrieved 2026-07-20)
- [Mastercard, Security Rules and Procedures, Merchant Edition (PDF; **UNVERIFIED:** the 3 February 2026 revision date could not be confirmed, this is a rolling "latest version" URL and Mastercard returned 403 to automated retrieval)](https://www.mastercard.com/content/dam/mccom/shared/business/support/rules-pdfs/SPME-Manual.pdf) (link not machine-verifiable 2026-07-20)
- [Stripe, What is PCI DSS compliance? (vendor guidance on SAQ A versus SAQ A-EP by integration type)](https://stripe.com/guides/pci-compliance) (retrieved 2026-07-20)
- [Chad M. Barr, Visa's Recent Changes to Merchant Levels: Combining Levels 3 and 4 (June 2025, unofficial, see Notes)](https://chadmbarr.com/visa-combining-levels-3-and-4/) (retrieved 2026-07-20)

## Notes

### Verification gaps in this review

- The PCI SSC Document Library gates the current PDFs (SAQ A r1 for v4.0.1, SAQ A-EP, and the March 2025 information supplement) behind a licence acceptance step, and direct links returned 403 or 404 during this review. The requirement text, dates, and eligibility wording in this file come from PCI SSC blog posts and PCI SSC FAQ pages, which are official but secondary to the documents themselves. **Before relying on this file for a real client attestation, download the current SAQ from the Document Library and read the eligibility section directly.**
- Requirement wording for 6.4.3 and 11.6.1 in this file is a close paraphrase reconciled across several sources, not a verbatim quotation from the standard. It matches on every operative element (authorize, integrity, inventory with justification; alert on unauthorized modification to security-impacting HTTP headers and script contents of payment pages as received by the consumer browser). Quote from the standard itself, not from here, if exact wording matters.
- **Confirmed 2026-07-20.** The 11.6.1 cadence is verified against the PCI SSC information supplement, which states: "Requirement 11.6.1 specifies that the mechanism's functions occur at least weekly. Alternatively, an entity may choose to define a targeted risk analysis (TRA) according to PCI DSS Requirement 12.3.1 to determine an alternative frequency." Weekly is the default; a documented TRA is the only route to a different interval.
- **UNVERIFIED:** a report from June 2025 says Visa is consolidating merchant Levels 3 and 4 into a single Level 3. The source was re-read during this review and it cites no Visa announcement, no policy document, and no effective date, only a generic link to Visa's compliance resources page. Visa's own published pages still list four levels at the thresholds given above, and say nothing about consolidation. Treat the claim as unsupported and confirm the client's level with the acquirer.
- **Resolved 2026-07-20.** No PCI DSS version newer than v4.0.1 has been published. The PCI SSC Document Library still lists v4.0.1 as current, and no SAQ revision has been announced since the January 2025 SAQ A. The Request for Comments flagged in the previous review is real and is now confirmed: PCI SSC opened an RFC on PCI DSS v4.0.1 running **3 June to 20 July 2026**, which closes today. The next version is in drafting, so nothing in this file changes yet, but **re-check the bulletins page before the next client delivery** because a v4.1 or v5.0 announcement is the likely next event.
- Mastercard's own pages and PDFs (the SDP program page, the Level 2 requirements PDF, the SDP FAQs, and the SPME manual) all returned HTTP 403 to automated retrieval during this review. The Mastercard level thresholds and the Level 2 QSA/ISA validation rule in this file therefore rest on Mastercard's long-standing published wording rather than a fresh fetch. Confirm against the current SPME manual before quoting them to a client.
- The card brands do not publish fine schedules. Every dollar figure circulating for PCI non-compliance comes from consultancies and vendors, and none was traced to a primary source. This file states that plainly rather than repeating the numbers as fact.

### Design consequences worth raising at intake

The choice between a redirect and an embedded iframe is a compliance decision disguised as a UX decision, and it is usually made in the first design conversation by someone who does not know that.

- **Redirect or fully hosted page**: lowest scope. SAQ A available, and the script-susceptibility eligibility criterion does not apply per FAQ 1588. Cost: the customer leaves the client's domain, and the checkout carries the processor's branding within whatever customization the processor allows.
- **Embedded iframe (hosted fields)**: still SAQ A eligible, but only if the client either implements 6.4.3 and 11.6.1 style controls on the containing page or holds the processor's written confirmation. Cost: on-brand checkout, plus a piece of ongoing evidence to maintain.
- **Custom form with a tokenization API**: SAQ A-EP, with the full 6.4.3 and 11.6.1 obligations, penetration testing under Requirement 11.4, and a materially larger annual validation effort. Only defensible when the client has the budget and staff to sustain it.

Price these differently, and say so in the proposal. A client who wants a fully custom checkout on a Level 4 volume is buying an annual compliance program alongside a website.

### Interaction with other laws in this library

- PCI DSS restricts what may be stored, but breach **notification** duties come from statute, not from this standard. A card data breach usually triggers both.
- Consent banners and cookie rules from privacy law point in the same direction as PCI does here: keep third-party scripts off the payment page. A consent-mode implementation that lets an analytics tag fire on checkout after consent still creates a 6.4.3 and 11.6.1 obligation. Consent does not remove the PCI duty.
- The data minimization instinct in privacy law and the "do not store SAD" rule in PCI DSS agree. Where they conflict, PCI wins on card data specifically, because the client can lose card acceptance over it.

### Watch items

- Client-side security monitoring is now a recurring cost for any merchant on SAQ A-EP or SAQ D. Decide whether the studio resells one, recommends one, or hands the problem to the client, and put the answer in the standard handover document.
- E-skimming (Magecart) attacks are the reason these requirements exist and they target exactly the kind of small merchant site a studio builds. The attack does not need the merchant's server: a compromised CDN, plugin, or tag manager is enough.
- Any project that adds a plugin marketplace, a page builder, or a client-editable script field to a site with a payment page has created a way for the client to break its own compliance after handover. Lock the payment template.
