# EAA: Directive (EU) 2019/882 on the accessibility requirements for products and services (European Accessibility Act)

| Field | Value |
|---|---|
| **Jurisdiction** | European Union (all 27 member states), applied through national transposing laws. Text is marked "EEA relevance". Catches providers established outside the EU who offer covered services to consumers in the EU. |
| **Regulator / enforcer** | No single EU regulator. Each member state designates market surveillance authorities for products and separate compliance authorities for services (Articles 19 and 23). Examples: Ireland uses the CCPC for products plus five other sectoral authorities; Germany uses the Marktüberwachungsstelle der Länder für die Barrierefreiheit von Produkten und Dienstleistungen (MLBF) in Magdeburg. |
| **In force since** | Entered into force 27 June 2019. Transposition deadline 28 June 2022. Applies to products placed on the market and services provided to consumers from **28 June 2025**. |
| **Last amended** | UNVERIFIED: no amending act was found in the sources checked. Treat the 2019 text as current and re-check the EUR-Lex ELI record before relying on this. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force and applicable. Transitional periods still running until 28 June 2030 (and up to 20 years for some self-service terminals). |

## Applies when

Work through these at intake. The EAA does **not** cover every website. It covers a closed list of products and services.

**Service scope (Article 2(2)). The client is caught if it provides any of these to consumers:**

- **E-commerce services.** Defined in Article 3(30) as "services provided at a distance, through websites and mobile device-based services by electronic means and at the individual request of a consumer with a view to concluding a consumer contract". Practical test: can a visitor complete a purchase, booking, subscription, or other consumer contract through the site or app? If yes, in scope.
- **Consumer banking services** (Article 3(28)): credit agreements, investment services, payment services, payment-account services, electronic money.
- **E-books and dedicated software** (Article 3(41)), including reader apps.
- **Electronic communications services**, excluding transmission used for machine-to-machine services.
- **Services providing access to audiovisual media services** (the access layer such as EPGs and player UI, not the programme content itself).
- **Elements of air, bus, rail and waterborne passenger transport services**: websites, mobile apps, e-ticketing, travel information.
- **Answering emergency communications to 112** (extended deadline, see below).

**Product scope (Article 2(1)), relevant if the client also ships hardware:** computer hardware and operating systems, payment terminals, ATMs, ticketing machines, check-in machines, interactive information terminals, consumer terminal equipment for electronic communications and audiovisual media, and e-readers.

**Who counts as caught:**

- **Consumer test.** A "consumer" is a natural person acting outside their trade, business, craft or profession (Article 3(22)). A pure B2B platform that only concludes contracts with businesses is not caught by the e-commerce limb. Mixed B2B and B2C sites are caught for the consumer path.
- **Territorial test.** A "service provider" is anyone who provides a service on the Union market **or makes offers to provide such a service to consumers in the Union** (Article 3(4)). A US, UK, or Australian client that ships to EU consumers and takes their orders online is in scope. Establishment in the EU is not required.
- **Brochure sites are out.** A marketing site with no transaction path, no login, and no consumer contract is not an e-commerce service under Article 3(30). Say so plainly to the client instead of selling EAA work that does not apply. National disability discrimination law may still apply separately.

**Microenterprise exemption (Articles 3(23) and 4(5)):**

- A microenterprise "employs fewer than 10 persons **and** which has an annual turnover not exceeding EUR 2 million **or** an annual balance sheet total not exceeding EUR 2 million".
- Read the logic carefully. The headcount test is mandatory. The financial test is satisfied by **either** turnover **or** balance sheet total being at or under EUR 2 million. Several vendor blogs state both financial tests must be met, which does not match the text.
- The exemption covers **services only**. A microenterprise that manufactures, imports, or distributes a covered **product** gets no exemption.
- There is no written grace period in the Directive for a business that grows past the threshold.
- Member states must still provide guidelines and tools to microenterprises (Article 4(6)).

**Content carve-outs (Article 2(4)) that stay out of scope even on an in-scope site:**

- Pre-recorded time-based media published before 28 June 2025.
- Office file formats published before 28 June 2025.
- Online maps and mapping services, if essential information for maps intended for navigational use is provided in an accessible digital manner.
- Third-party content that is neither funded, developed by, nor under the control of the operator.
- Archived content, meaning content not updated or edited after 28 June 2025.

**Other limits:**

- Urban, suburban and regional transport services are carved out of the **Annex I Section III** general service requirements by Article 4(3), but they are **not** fully exempt: the second sentence of Article 4(3) binds *all* services to Annex I Section IV, and Section IV point (d) sets requirements specifically for urban, suburban and regional transport. Separately, Article 2(2)(c) limits these operators to point (v), interactive self-service terminals, so their websites, apps, e-ticketing and travel information fall outside the service scope while their ticketing terminals stay in.
- **Fundamental alteration and disproportionate burden (Article 14).** A requirement does not apply where compliance would fundamentally alter the basic nature of the service or impose a disproportionate burden. This is a documented, assessed, notified exception, not a checkbox. An operator that receives public or private funding for accessibility improvement cannot rely on disproportionate burden.

**Transitional periods still live as of 2026-07-20:**

| Situation | Runs until |
|---|---|
| Service contracts concluded before 28 June 2025 | Expiry of the contract, maximum five years from 28 June 2025, so **28 June 2030** |
| Products lawfully used by a service provider before 28 June 2025 to deliver similar services | **28 June 2030** |
| Self-service terminals lawfully in use before 28 June 2025 (member state option) | End of economically useful life, maximum **20 years** after entry into use |
| Answering emergency communications to 112 | **28 June 2027** |

Do not let a client read the 2030 date as a deadline extension for a new website. The transition covers pre-existing contracts and deployed hardware, not a redesign shipping in 2026.

## What the site must have

| Requirement | What that means in the build |
|---|---|
| **Accessible website and app for the covered service** | Annex I Section III requires the service to be made "perceivable, operable, understandable and robust". The technical yardstick is EN 301 549. Build and test to **WCAG 2.1 Level AA** as the floor, which is what EN 301 549 v3.2.1 incorporates. Target WCAG 2.2 AA now, because EN 301 549 v4.1.x moves the baseline there (see Notes). |
| **Accessible identification, security and payment flows** | Annex I Section IV point (g) for e-commerce requires identification methods, electronic signatures, security and payment services to be perceivable, operable, understandable and robust. Covers checkout, 3-D Secure step-ups, OTP entry, CAPTCHA, session timeouts, and any embedded payment iframe. Third-party payment widgets are part of your delivery if you chose them. |
| **Accessibility information about what is being sold** | Annex I Section IV point (g) also requires the service to provide information on the accessibility of the products and services being sold, where that information is provided by the responsible economic operator. In practice: surface supplier accessibility data on product detail pages rather than dropping it. |
| **Annex V information inside the terms** | Annex V point 1 requires the provider to include, in the **general terms and conditions or an equivalent document**: (a) a general description of the service in accessible formats, (b) descriptions and explanations needed to understand how the service operates, (c) a description of how the relevant Annex I accessibility requirements are met. Build this as a real page, for example `/accessibility`, linked from the global footer, and cross-reference it from the T&Cs. |
| **Written and oral availability of that information** | Article 13(2) requires the information to be made available to the public "in written and oral format, including in a manner which is accessible to persons with disabilities". Written page alone is not enough. Provide a staffed phone line or an audio version, and state the channel on the page. |
| **Language complexity cap (banking only)** | Annex I Section IV point (e) caps the complexity of consumer banking information at **level B2 (upper intermediate)** of the Common European Framework of Reference for Languages. Run copy through a readability pass, not just a11y tooling. |
| **E-book requirements (publishing clients)** | Annex I Section IV point (f) for e-books: synchronised text and audio where audio accompanies text, no obstruction of assistive technology, accessible navigation and flexible rendition, accessibility metadata exposed so the file is discoverable, and DRM that does not block accessibility features. |
| **Disproportionate burden file, if relied on** | Article 14 requires the assessment to be documented, kept for **five years** after the service was last provided, renewed when the service changes, on authority request, or **at least every five years**, and notified to the relevant authority. If the client wants to skip a requirement, this file is the deliverable that makes that defensible. |
| **Non-conformity handling** | Article 13 requires procedures to keep the service in conformity as requirements change, corrective action where a service does not conform, and immediate notification to the competent national authority. Hand the client a written process, not just a code fix. |
| **Complaint route** | Article 29 requires member states to ensure adequate and effective means for consumers to take action on compliance. A named contact and response commitment on the accessibility page is the cheap version of this. Not a literal EAA text requirement, so present it as recommended. |

Note the terminology. The EAA does not use the phrase "accessibility statement" that the public-sector Web Accessibility Directive uses. It requires Annex V information. A statement modelled on the Web Accessibility Directive template will usually satisfy Annex V if it adds the "how the service meets Annex I" section, but do not assume the two are interchangeable.

## How to verify

Run all of this against the **transaction path**, not the homepage. Auditors and complainants go straight to checkout.

**Automated pass (catches roughly a third of issues, no more):**

- Run axe DevTools or Lighthouse against: home, category, product detail, cart, checkout step 1 through payment, account registration, login, password reset, order confirmation.
- Fail the build on any WCAG 2.1 AA violation. Add `@axe-core/playwright` to CI so regressions do not ship.
- Grep the built output for the usual smells: `<html` without a `lang` attribute, `tabindex="[1-9]`, `role="presentation"` on interactive elements, `<img` without `alt`, `onclick` on a `div` or `span`, `<button>` with no text node and no `aria-label`.

**Keyboard-only pass, no mouse touched:**

- Tab from page load to completed purchase. If you cannot finish the order, it fails.
- Confirm a visible focus ring at every stop, and that focus order matches visual order.
- Open and close every modal, dropdown, date picker, and cookie banner. Focus must move into the dialog, stay trapped, and return to the trigger on close.
- Check that the cookie or consent banner does not steal focus in a loop, and that it can be dismissed without a pointer.

**Screen reader pass:**

- NVDA plus Firefox on Windows, and VoiceOver plus Safari on macOS or iOS. Test the same purchase path.
- Confirm every form field announces its label, its required state, its format hint, and its error text. Validation errors must be programmatically associated, not just red.
- Confirm cart updates, price changes, and step transitions announce through a live region.

**DevTools checks:**

- Chrome DevTools, Elements panel, Accessibility pane: confirm computed accessible name and role on every control in checkout.
- Rendering pane: emulate `prefers-reduced-motion: reduce` and confirm animation stops.
- Contrast: check text and non-text UI (input borders, focus rings, icon buttons) at 3:1 or 4.5:1 as applicable.
- Zoom to 400% at 1280px width and confirm reflow with no horizontal scroll and no clipped content.

**Payment and identity flows specifically:**

- In the Network panel, follow the 3-D Secure or OTP step. Confirm the challenge iframe is keyboard reachable and screen reader readable. This is the single most common EAA failure point on otherwise decent sites.
- Confirm session timeouts warn the user and allow extension.
- Confirm any CAPTCHA has a non-visual alternative.

**Document checks:**

- Load the footer on every template and confirm the accessibility link is present.
- Open the accessibility page and confirm it contains all three Annex V elements, not just a WCAG conformance claim.
- Confirm the page states an oral channel (phone number or audio alternative) with real availability.
- Confirm the T&Cs reference or contain the Annex V information.
- If a disproportionate burden claim exists, confirm the dated assessment file exists, names who assessed it, and has a next-review date within five years.

## Penalties

The EAA itself sets no figure. Article 30(2) requires member states to lay down penalties that are "effective, proportionate and dissuasive" and adds that those penalties "shall also be accompanied by effective remedial action in case of non-compliance of the economic operator". Article 30(4) requires penalties to take into account the extent and seriousness of the non-compliance, the number of non-complying units, and the number of persons affected. The idea that penalties should not substitute for fixing the service sits in the recitals, not in Article 30, so do not quote it as operative text. The real exposure is national, and it varies widely.

| Member state | Penalty | Source |
|---|---|---|
| **Germany** (BFSG § 37) | Up to **EUR 100,000** ("bis zu hunderttausend Euro") for the more serious categories, including making a non-accessible product available, providing a non-accessible service, and CE marking breaches. Up to **EUR 10,000** ("bis zu zehntausend Euro") for information, labelling, and documentation breaches. | Official German statute text, verified. |
| **Ireland** (S.I. No. 636 of 2023) | Summary conviction: fine up to **EUR 5,000** (Class A) or up to 6 months imprisonment. On indictment: fine up to **EUR 60,000** or up to 18 months imprisonment. Company officers can be personally liable, and consumers can bring actions in the Circuit Court. Figures are taken from a DLA Piper analysis and match it exactly; UNVERIFIED against the statutory instrument text line by line, because irishstatutebook.ie refuses automated retrieval (HTTP 403) and was not read directly. UNVERIFIED: the claim that Ireland is the only member state attaching criminal penalties. The cited DLA Piper article does not say this and makes no comparison to other member states. Do not repeat it to a client. | DLA Piper, plus the S.I. on the Irish Statute Book. |
| **All other member states** | UNVERIFIED. Do not quote a figure to a client for any other country without checking that country's transposing act. Penalty regimes are genuinely different across the 27. | |

Beyond fines, authorities can order withdrawal of a product or require a service to be brought into conformity or discontinued. For most web clients the operational risk (an order to fix, plus complaint handling) arrives long before any fine does.

## Common ways sites fail this

- Auditing the homepage, shipping, and never testing checkout. The legal obligation lands hardest on the path to a consumer contract.
- Treating a third-party payment iframe, booking widget, or chat bubble as somebody else's problem. If you embedded it, it is in the service you delivered.
- Publishing a WCAG conformance badge and calling it the accessibility statement. Annex V wants a description of the service, an explanation of how it operates, and a mapping to Annex I requirements.
- Publishing the statement in writing only and ignoring the Article 13(2) oral format requirement.
- A cookie consent banner that traps keyboard focus or cannot be dismissed without a mouse. It is the first thing every user meets and the first thing every auditor tests.
- Assuming the microenterprise exemption applies because the company feels small, without checking headcount against the under-10 test, or forgetting that the exemption does not reach products.
- Assuming a non-EU client is out of scope. Article 3(4) catches offers made to consumers in the Union.
- Reading 28 June 2030 as a deadline for new work. It covers pre-existing contracts and already-deployed products.
- Relying on an accessibility overlay widget. Overlays do not deliver Annex I conformance and have themselves attracted complaints.
- Auto-playing carousels, unlabelled icon-only buttons, and colour-only error states surviving to production because only automated scanning was run.

## Sources

Official sources first. All retrieved 2026-07-20.

- [Directive (EU) 2019/882, full text, EUR-Lex](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32019L0882) (retrieved 2026-07-20) - Articles 2, 3, 4, 13, 14, and Annex I.
- [Directive (EU) 2019/882, ELI record](https://eur-lex.europa.eu/eli/dir/2019/882/oj/eng) (retrieved 2026-07-20)
- [EUR-Lex official summary: Accessibility of products and services](https://eur-lex.europa.eu/EN/legal-content/summary/accessibility-of-products-and-services.html) (retrieved 2026-07-20) - key dates, 112 extension to 2027, transitional periods.
- [Directive 2019/882 Article 3 (definitions)](https://www.legislation.gov.uk/eudr/2019/882/article/3) (retrieved 2026-07-20)
- [Directive 2019/882 Article 4 (accessibility requirements, microenterprise exemption)](https://www.legislation.gov.uk/eudr/2019/882/article/4) (retrieved 2026-07-20)
- [Directive 2019/882 Article 13 (obligations of service providers)](https://www.legislation.gov.uk/eudr/2019/882/article/13) (retrieved 2026-07-20)
- [Directive 2019/882 Article 14 (fundamental alteration and disproportionate burden)](https://www.legislation.gov.uk/eudr/2019/882/article/14) (retrieved 2026-07-20)
- [Directive 2019/882 Annex I Section IV (service-specific requirements)](https://www.legislation.gov.uk/eudr/2019/882/annex/I/section/IV) (retrieved 2026-07-20)
- [Directive 2019/882 Annex V (information on services)](https://www.legislation.gov.uk/eudr/2019/882/annex/V) (retrieved 2026-07-20)
- [BFSG § 37 Bußgeldvorschriften, gesetze-im-internet.de](https://www.gesetze-im-internet.de/bfsg/__37.html) (retrieved 2026-07-20) - German penalty amounts.
- [S.I. No. 636/2023, Irish Statute Book](https://www.irishstatutebook.ie/eli/2023/si/636/made/en/print) - UNVERIFIED: returns HTTP 403 to automated retrieval, so the text behind this link was not read. Open it in a browser before relying on the Irish figures.
- [European Commission: Web accessibility standards, latest changes](https://digital-strategy.ec.europa.eu/en/policies/latest-changes-accessibility-standard) (retrieved 2026-07-20) - confirms EN 301 549 v3.2.1 cited in the Official Journal in August 2021 and referencing WCAG 2.1.
- [European Commission: Web Accessibility Directive, standards and harmonisation](https://digital-strategy.ec.europa.eu/en/policies/web-accessibility-directive-standards-and-harmonisation) (retrieved 2026-07-20)
- [Draft ETSI EN 301 549 V4.1.0 (2025-11), PDF](https://www.etsi.org/deliver/etsi_en/301500_301599/301549/04.01.00_20/en_301549v040100ev.pdf) - UNVERIFIED: returns HTTP 403 to automated retrieval, so the version number and date on the cover page were not confirmed.
- [CCPC: European Accessibility Act guidelines for microenterprises](https://www.ccpc.ie/business/enforcement/accessibility/european-accessibility-act-guidelines-for-microenterprises/) (retrieved 2026-07-20)
- [DLA Piper: Navigating the Irish Accessibility Regulations](https://www.dlapiper.com/en-us/insights/publications/2025/10/navigating-the-irish-accessibility-regulations) (retrieved 2026-07-20) - source of the Irish penalty figures, secondary.

## Notes

**The standard is moving. Watch this.**

- EN 301 549 **v3.2.1** is the version cited in the Official Journal (August 2021) and it incorporates **WCAG 2.1 Level AA**. That citation was made under the Web Accessibility Directive 2016/2102.
- A draft **v4.1.0** was released in November 2025. The final **v4.1.1**, which aligns clauses 9, 10 and 11 with **WCAG 2.2 Level AA**, was reported as expected to be cited in the Official Journal around **October 2026**. UNVERIFIED as of 2026-07-20: whether that citation has happened, and whether the version number stayed at 4.1.1. Re-check before quoting a client a standard version.
- **Presumption of conformity caveat.** Standardisation request M/587 was issued to develop harmonised standards specifically for the EAA. UNVERIFIED as of 2026-07-20: whether any M/587 standard has been cited in the Official Journal under the EAA. If none has, then strictly there is no formal presumption of conformity available under Article 15 yet, and EN 301 549 is the de facto benchmark rather than a legal safe harbour. Do not write "EN 301 549 conformance guarantees EAA compliance" into a client contract.
- **Studio position:** build to WCAG 2.2 AA now. It is a superset of 2.1 AA, so it satisfies the current cited standard and absorbs the coming update without a second engagement.

**Conflicts and overlaps with other laws in this library:**

- The **Web Accessibility Directive (EU) 2016/2102** covers public sector bodies and has its own mandatory accessibility statement format plus a feedback mechanism. The EAA covers private sector products and services and uses Annex V instead. A client that is a public body or a public-sector supplier may be under both. Do not merge the two statements without checking each one's required elements.
- **National transpositions differ.** Germany (BFSG plus BFSGV), Ireland (S.I. 636/2023), France, Italy and others each have their own procedural rules, authorities, and penalty levels. The Directive is the floor. Always name the client's primary market and check that country's act.
- **The UK is not covered.** Post-Brexit the EAA does not apply to UK-only trading. The UK Equality Act 2010 obligations are separate and are not satisfied by EAA work. A UK client selling to EU consumers is caught by the EAA anyway via Article 3(4).
- **US clients** may face both the EAA (for EU consumers) and ADA Title III litigation domestically. WCAG 2.1 AA or better covers the practical ground for both, but the documentation obligations differ. The EAA wants Annex V information published; the ADA does not require a statement at all.
- **Consent banners sit at the intersection with GDPR and the ePrivacy rules.** The banner must be keyboard operable and screen reader usable while still blocking non-essential scripts before consent. Do not let the accessibility fix break the consent gate, or the consent gate break the keyboard trap rules.

**Litigation and enforcement to watch:** German reporting describes an enforcement pattern that starts with a complaint, moves to investigation and a warning with a deadline, and only then to a fine, alongside a rise in competitor `Abmahnung` (formal warning letter) activity against non-compliant sites. UNVERIFIED: volume and outcomes of that activity. Treat the warning-letter risk in Germany as real but do not quote statistics to clients.

**Intake question to add to every project brief:** "Can a consumer in the EU conclude a contract on this site or app?" If yes, the EAA is in scope and WCAG 2.2 AA plus an Annex V page go into the estimate. If no, say the EAA does not apply and check national discrimination law instead.
