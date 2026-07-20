# HIPAA: Health Insurance Portability and Accountability Act of 1996, as amended by the HITECH Act of 2009

| Field | Value |
|---|---|
| **Jurisdiction** | United States, federal. Attaches to the regulated business, not to the visitor. A US covered entity is bound even when the visitor is overseas. A foreign clinic with no US covered-transaction billing is not bound. |
| **Regulator / enforcer** | HHS Office for Civil Rights (OCR). The court in AHA v. Becerra describes the structure: violations "are reported to HHS's Office for Civil Rights (OCR), who investigates reports and recommends corrective action." |
| **In force since** | Statute enacted 1996. The current text of the Privacy, Security, Enforcement, and Breach Notification Rules comes from the 2013 Omnibus Rule, 78 FR 5566, effective March 26, 2013, compliance date September 23, 2013. |
| **Last amended** | Penalty amounts: January 28, 2026 (91 FR 3665, doc 2026-01688). Substantive rule text: the reproductive health care privacy final rule of April 26, 2024 (89 FR 32976, doc 2024-08503, effective June 25, 2024) is the most recent final rule located, subject to the litigation caveat in Notes. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. One piece of OCR guidance relevant to web builds (the "Proscribed Combination" tracking rule) was vacated by a federal court on June 20, 2024. See Notes. |

## Applies when

Work through these at intake, in order. The first two questions decide everything else.

**Is the client a covered entity?** All three categories come from 45 CFR 160.103.

- The client is a **health plan** (insurer, HMO, employer group health plan, Medicare or Medicaid program).
- The client is a **health care clearinghouse** (processes nonstandard health data into standard format, e.g. a billing intermediary).
- The client is a **health care provider who transmits any health information in electronic form in connection with a covered transaction**. The electronic-transaction test is the trigger, not the practice of medicine. Covered transactions are claims, eligibility checks, referral authorizations, and similar payer-facing exchanges.
- **Not automatically caught:** a cash-only or direct-pay provider who never submits an electronic claim, eligibility check, or other covered transaction. This is common among concierge medicine, some therapists and counselors, med spas, and wellness practices. Ask specifically: "Do you or your billing service ever submit claims or check eligibility electronically to any insurer?" If the answer is no for all payers, the client is likely outside HIPAA and falls to FTC and state law instead. Get the client to confirm this in writing rather than deciding it yourself.
- **Not caught:** life insurers, most employers acting as employers, schools handling FERPA education records, and workers' compensation carriers. 45 CFR 160.103 excludes education records and employment records from PHI.

**Is the studio a business associate?** From the 45 CFR 160.103 definition, a business associate is a person who, on behalf of a covered entity, "creates, receives, maintains, or transmits" PHI. Applied to a web build:

- **Yes, BA, needs a BAA:** the site collects patient-identifying health information (intake forms, symptom descriptions, appointment reasons, prescription refill requests, patient portal), and the studio hosts it, has database access, receives form submissions by email, or can read submissions in a CMS.
- **Yes, BA:** the studio manages hosting or a CMS for a covered entity and could access stored PHI, even without ever looking at it. The 2013 Omnibus Rule is explicit: "an entity that maintains protected health information on behalf of a covered entity is a business associate and not a conduit, even if the entity does not actually view the protected health information" (78 FR 5566, 5572).
- **No, not a BA:** a purely informational brochure site with no forms that collect health information, no patient login, and no studio access to any system holding PHI. A generic "contact us" form asking only for name and email, routed straight to the client with no studio access, is a borderline case; treat it as PHI-collecting if any free-text field invites the visitor to describe a medical concern.
- **A subcontractor of a business associate is itself a business associate** under 45 CFR 160.103. If the studio is a BA, its hosting provider, form processor, backup vendor, and any agency subcontractor each need a BAA with the studio.
- **The conduit exception is narrow.** It is "limited to transmission services (whether digital or hard copy), including any temporary storage of transmitted data incident to such transmission" (78 FR 5572). An ISP is a conduit. A web host storing PHI is not.

**Thresholds.** HIPAA has no revenue, headcount, or record-count threshold for whether it applies. A solo physician who bills electronically is fully covered. Record counts only change breach notification mechanics (the 500-individual line in 45 CFR 164.406 and 164.408).

## What the site must have

| Requirement | What that means in the build |
|---|---|
| Notice of Privacy Practices published and linked | A dedicated page, linked from the global footer on every page, and linked from every form that collects PHI. 45 CFR 164.520(c)(3)(i) is the hook: "A covered entity that maintains a web site that provides information about the covered entity's customer services or benefits must prominently post its notice on the web site and make the notice available electronically through the web site." Do not write this document; the client's counsel or compliance officer supplies the text and the studio publishes it verbatim. |
| Signed BAA before any PHI touches studio infrastructure | Executed between client and studio, and between studio and every downstream vendor that can reach PHI, before launch and before any real patient data enters the system. 45 CFR 164.504(e) sets the required contents: permitted uses and disclosures, safeguards, reporting of unauthorized use and breaches, subcontractor flow-down, individual access and amendment support, accounting of disclosures, return or destruction on termination, and a termination right for material breach. |
| No third-party tracking on any page or flow that handles PHI | Meta Pixel, Google Analytics, Google Ads and Floodlight tags, TikTok pixel, LinkedIn Insight, session-replay tools (Hotjar, FullStory, Clarity), chat widgets, and A/B testing scripts must be absent from patient portals, logged-in areas, intake forms, appointment booking flows, symptom checkers, and bill-pay pages. See the tracking section below for the unauthenticated-page analysis. |
| Analytics vendor either eliminated or under a BAA | Google's own Analytics help documentation is explicit: "Google makes no representations that Google Analytics satisfies HIPAA requirements and does not offer Business Associate Agreements in connection with this service," and HIPAA-regulated customers "may only use Google Analytics on pages that are not HIPAA-covered." Practical options: self-hosted analytics on infrastructure the client controls, a vendor that signs a BAA in writing, or no analytics on PHI-handling pages. Verify the BAA exists as a signed document, not a marketing claim. |
| Forms transmit and store PHI encrypted | TLS on every page that collects or displays PHI, HSTS enabled, no mixed content. Encryption is an "addressable" implementation specification under 45 CFR 164.312(a)(2)(iv) and 164.312(e)(2)(ii), which means it must be implemented or a documented written justification must explain why an equivalent alternative was used. In a 2026 web build there is no defensible reason not to encrypt in transit and at rest. |
| Form submissions do not travel by plain email | Do not route intake or appointment forms to an unencrypted mailbox or a shared inbox. Store in an access-controlled system, or use a form processor that signs a BAA. Disable any plugin that emails a copy of submission contents to the studio. |
| Unique per-user accounts and automatic logoff on any portal | 45 CFR 164.312(a)(2)(i) requires a unique user identifier. Automatic logoff at 164.312(a)(2)(iii) is addressable, so implement a session timeout or document why not. Shared logins are a finding. |
| Audit logging | 45 CFR 164.312(b) requires "hardware, software, and/or procedural mechanisms that record and examine activity in information systems that contain or use electronic protected health information." Log PHI access with user, timestamp, and record identifier. Retain the logs. |
| Authentication controls | 45 CFR 164.312(d) requires procedures to verify that a person seeking access is the one claimed. Password reset flows must not leak whether an account exists or reveal PHI. |
| Breach response path written into the contract | If the studio is a BA, 45 CFR 164.410 requires it to notify the covered entity of a breach "without unreasonable delay and in no case later than 60 calendar days after discovery," and to identify each individual whose PHI was involved. Build the logging that makes that identification possible before you need it. |
| Hosting under a BAA | The host must sign a BAA. AWS, Azure, and Google Cloud offer BAAs covering a defined subset of services. Using a non-covered service inside a "HIPAA account" still breaks the BAA. Check the provider's covered-services list against the actual architecture. |
| Retention and disposal | Set a documented retention period for form submissions and logs. On contract termination, 45 CFR 164.504(e) requires return or destruction of PHI, or extension of protections if return is infeasible. Know where every copy lives, including backups and staging databases. |
| No PHI in non-production environments | Staging, demo, and test databases seeded with real patient records are a breach waiting to be found. Use synthetic data. |

### Online tracking technologies: the current state

This is the highest-frequency compliance failure in healthcare web work, and the legal position moved in 2024. Get this right.

**What OCR said.** OCR published a bulletin on use of online tracking technologies by HIPAA covered entities and business associates in December 2022, and issued a revised version on March 18, 2024. The revised bulletin took the position, quoted from the administrative record in the litigation, that "the mere fact that an online tracking technology connects the IP address of a user's device (or other identifying information) with a visit to a webpage addressing specific health conditions or listing health care providers is . . . a sufficient combination of information to constitute IIHI if the visit to the webpage is . . . related to" the individual's own health.

**What the court did.** In American Hospital Association v. Becerra, No. 4:23-cv-01110-P (N.D. Tex. June 20, 2024), Judge Pittman granted summary judgment in part for the hospital plaintiffs. The court labeled the quoted rule the "Proscribed Combination," declared it "UNLAWFUL, as it was promulgated in clear excess of HHS's authority under HIPAA," denied a permanent injunction, and granted vacatur, ordering "that the Proscribed Combination be VACATED."

**What the vacatur did not do.** Footnote 8 of the opinion limits the ruling: "Such vacatur is not intended to, and should not be construed as, limiting the legal operability of other guidance in the germane HHS document." The vacatur removed one enforcement theory: that an IP address combined with a visit to an *unauthenticated public webpage* about a condition or provider is, by itself, PHI. It did not change the statutory definition of PHI, and it did not authorize tracking scripts on pages where actual PHI is present.

**How to translate that into a build decision.**

- **Authenticated areas (patient portal, logged-in scheduling, bill pay, messaging): no third-party tracking, full stop.** Once a visitor is authenticated, the site knows who they are and the page content relates to their care. That is individually identifiable health information under the plain 45 CFR 160.103 definition, with no reliance on the vacated theory. Sending it to an advertising vendor without a BAA and without authorization is a disclosure violation.
- **Pages where the visitor types PHI (intake, symptom forms, appointment reason, refill requests): no third-party tracking.** Form field contents, URL query strings carrying condition names, and session-replay capture are direct PHI disclosures regardless of the vacatur. Session-replay tools are the worst offender because they capture keystrokes before submit.
- **Unauthenticated informational pages (a page describing a cardiology service line):** the vacated Proscribed Combination was the theory that made IP-plus-page-visit alone into PHI. With it vacated, OCR's path to enforcement on that fact pattern specifically is weakened. This is still not a green light. Advise removal, and if the client insists on marketing tags, get the decision in writing from the client's counsel, keep the tags off every page listed above, and confirm no identifiers leak (see verification below).
- **The residual risk is not only OCR.** Private plaintiffs sue on state wiretap and privacy theories rather than HIPAA, which has no private right of action. The AHA opinion itself cites the defense-side cases: Smith v. Facebook, Inc., 745 F. App'x 8, 9 (9th Cir. 2018), and Kurowski v. Rush System for Health, 683 F. Supp. 3d 836, 843 (N.D. Ill. 2023). Outcomes vary by circuit and by what actually got transmitted.
- **If the client is not a covered entity, the FTC rules instead.** The FTC Health Breach Notification Rule amendments took effect July 29, 2024. By its terms at 16 CFR 318.1(a), the rule "does not apply to HIPAA-covered entities, or to any other entity to the extent that it engages in activities as a business associate of a HIPAA-covered entity," which means it targets exactly the health apps and direct-pay services that fall outside HIPAA. UNVERIFIED: in the GoodRx matter the FTC is reported to have alleged the company "disclosed more than 500 consumers' unsecured PHR identifiable health information to third party advertising platforms like Facebook and Google, without the authorization of those consumers." Both the FTC case page and the complaint PDF returned HTTP 403 to automated retrieval on 2026-07-20, so this quotation was not confirmed against the primary document. Open the FTC case page in a browser before quoting it. A cash-only clinic outside HIPAA is not outside the law.

## How to verify

Run these before delivery, on the production build, with a real page load.

1. **Request audit for tracker beacons.** Open DevTools, Network panel, filter by `facebook.com`, `connect.facebook.net`, `google-analytics.com`, `analytics.google.com`, `googletagmanager.com`, `doubleclick.net`, `tiktok.com`, `hotjar`, `clarity.ms`, `fullstory`, `linkedin.com`. Load in order: home page, a service-line page, the intake form, the appointment booking flow, a logged-in portal page. Any hit from an authenticated page or a PHI form page is a defect.
2. **Inspect the payload, not only the domain.** Click each surviving third-party request and read the query string and POST body. Look for the page URL in `dl` or `dr` parameters, form field values, `em` or hashed-email parameters, appointment reason text, and condition names embedded in the path. A GA request carrying `/conditions/hepatitis-c-treatment` in the document location is transmitting the sensitive part even if you consider the IP question settled.
3. **Grep the built output.** Search the deployed bundle and templates for `gtag(`, `fbq(`, `dataLayer`, `googletagmanager`, `_hjSettings`, `clarity`, `<script` blocks injected by tag managers. Tag managers are the usual way a pixel reappears after you removed it, because marketing can add tags without a deploy. Check who has container access.
4. **Check the tag manager container as a separate artifact from the site.** Ask for a screenshot of the container's tag list. A clean site with a dirty container is a launch blocker.
5. **Submit a real form and follow the data.** Fill the intake form with a marker string like `ZZTESTCONDITION`. Then grep the studio's inbox, the CMS submission store, logs, and any error-tracking service (Sentry, Rollbar, Datadog) for that string. Error trackers capturing form state are a common accidental PHI sink.
6. **Confirm TLS everywhere.** Load every PHI page over `http://` and confirm the redirect to HTTPS. Check the `Strict-Transport-Security` response header. Run the page through DevTools Security panel and confirm no mixed content.
7. **Test session behavior on the portal.** Log in, leave the session idle past the configured timeout, and confirm logoff. Log out and press the browser back button to confirm PHI pages are not served from cache. Check for `Cache-Control: no-store` on PHI responses.
8. **Test the password reset and login flows for account enumeration.** Submit a known-bad address and a known-good address and compare responses. Different messaging tells an attacker who is a patient there.
9. **Confirm the BAA chain on paper.** List every vendor that can reach PHI: host, CDN, form processor, email relay, backup, error tracking, analytics, chat, scheduler. For each, produce the signed BAA. Any vendor without one either gets removed or gets blocked from PHI.
10. **Confirm the NPP link renders** on every page footer and resolves to a live page, and that the client, not the studio, authored it.
11. **Check staging and demo data** for real patient records. Query the non-production database for real-looking names and dates of birth.

## Penalties

Civil money penalty tiers are set by 45 CFR 160.404, but the dollar figures printed in that section are the un-adjusted statutory amounts ($100 to $50,000 per violation, $1,500,000 calendar-year cap). Reading 160.404 on its own will give you stale numbers. The current inflation-adjusted amounts live in the table at **45 CFR 102.3**.

The amounts below took effect **January 28, 2026** (91 FR 3665) and apply to penalties assessed on or after that date for violations occurring on or after November 2, 2015. The adjustment applied the 1.02598 multiplier published in OMB Memorandum M-25-02. Note that M-25-02 is the *2025* multiplier, derived from the October 2024 CPI-U (315.664 / 307.671 = 1.02598). HHS published its 2025 annual adjustment late, in January 2026, so these figures are one cycle behind the calendar. A catch-up adjustment could land at any time. Re-check 45 CFR 102.3 before quoting a number to a client.

| Culpability tier | Minimum per violation | Maximum per violation | Calendar-year cap for identical violations |
|---|---|---|---|
| Did not know, and would not have known by exercising reasonable diligence | $145 | $73,011 | $2,190,294 |
| Reasonable cause, not willful neglect | $1,461 | $73,011 | $2,190,294 |
| Willful neglect, corrected within 30 days | $14,602 | $73,011 | $2,190,294 |
| Willful neglect, not corrected within 30 days | $73,011 | $2,190,294 | $2,190,294 |

For violations occurring before February 18, 2009, the table at 45 CFR 102.3 publishes an adjusted maximum of $198 per violation with a $49,848 calendar-year cap. Read that against the applicability clause in the same rule, which states that the adjusted amounts apply where "the violation occurred on or after November 2, 2015," and that if the violation occurred before that date, or a penalty was assessed before September 6, 2016, "the pre-adjustment civil penalty amounts in effect before September 6, 2016, will apply." The two provisions pull in different directions for a pre-2009 violation. Do not quote a pre-2009 figure to a client without counsel reconciling it.

"Per violation" is the number that matters. OCR has counted violations per affected individual and per day of non-compliance, so a tracking script on a portal used by 50,000 patients is not a single violation.

Business associates are directly liable. A studio that is a BA can be penalized by OCR on its own, separately from the client.

UNVERIFIED: state attorneys general also have enforcement authority under HITECH, and separate state health-privacy statutes carry their own penalties. Not verified in this pass. Check the state-specific file for the client's state.

UNVERIFIED: OCR's published enforcement actions specifically naming tracking technologies were not retrievable in this pass, because hhs.gov blocks automated retrieval. Check the OCR enforcement highlights and breach portal manually before quoting any settlement figure to a client.

## Common ways sites fail this

- Meta Pixel installed site-wide by a marketing agency, including on the patient portal login and the appointment booking flow.
- Google Analytics left on because "it's just analytics," transmitting page URLs that name the condition the visitor is reading about.
- Session-replay or heatmap tools capturing keystrokes inside an intake form before submit.
- Intake form results emailed to the studio's own inbox during the build and never switched off at launch.
- No BAA with the host, or a BAA with the host that does not cover the specific services actually used.
- Real patient records copied into a staging database for testing.
- Error tracking (Sentry and similar) capturing form state or request bodies containing PHI, with no scrubbing configured.
- Appointment confirmation URLs with the reason for visit in the query string, which then leaks in the `Referer` header to every third-party asset on the page.
- Notice of Privacy Practices written by the studio from a template instead of supplied by the client's counsel.
- A tag manager container that marketing controls, letting pixels return weeks after a clean launch.
- Treating the June 2024 vacatur as blanket permission to reinstall pixels.
- Assuming a cash-only wellness client is unregulated and skipping the FTC Health Breach Notification Rule analysis.

## Sources

Official and primary sources first. All retrieved 2026-07-20. Every URL below was confirmed to return HTTP 200 on that date except the hhs.gov bulletin, which returns 403. Two federalregister.gov links (the Security Rule proposal and the reproductive health final rule) return 200 but redirect automated clients to an anti-bot interstitial; both open normally in a browser, and both documents were independently confirmed to exist through the Federal Register API.

- [45 CFR 160.103, definitions (covered entity, business associate, PHI)](https://www.law.cornell.edu/cfr/text/45/160.103) - retrieved 2026-07-20
- [45 CFR 160.404, amount of a civil money penalty](https://www.law.cornell.edu/cfr/text/45/160.404) - retrieved 2026-07-20. Note: shows un-adjusted statutory amounts. Use 45 CFR 102.3 for current figures.
- [45 CFR 102.3, inflation-adjusted civil monetary penalty table (eCFR)](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-A/part-102/section-102.3) - retrieved 2026-07-20 via the eCFR versioner API for date 2026-07-01
- [45 CFR 164.520, notice of privacy practices (eCFR)](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-164/subpart-E/section-164.520) - retrieved 2026-07-20 via the eCFR versioner API for date 2026-07-01
- [45 CFR 164.312, technical safeguards](https://www.law.cornell.edu/cfr/text/45/164.312) - retrieved 2026-07-20
- [45 CFR 164.402, definition of breach](https://www.law.cornell.edu/cfr/text/45/164.402) - retrieved 2026-07-20
- [45 CFR 164.404, notification to individuals](https://www.law.cornell.edu/cfr/text/45/164.404) - retrieved 2026-07-20
- [45 CFR 164.406, notification to the media](https://www.law.cornell.edu/cfr/text/45/164.406) - retrieved 2026-07-20
- [45 CFR 164.408, notification to the Secretary (GovInfo CFR XML)](https://www.govinfo.gov/content/pkg/CFR-2023-title45-vol2/xml/CFR-2023-title45-vol2-sec164-408.xml) - retrieved 2026-07-20
- [45 CFR 164.410, notification by a business associate](https://www.law.cornell.edu/cfr/text/45/164.410) - retrieved 2026-07-20
- [45 CFR 164.504, business associate contract requirements](https://www.law.cornell.edu/cfr/text/45/164.504) - retrieved 2026-07-20
- [American Hospital Association v. Becerra, No. 4:23-cv-01110-P (N.D. Tex. June 20, 2024), Opinion and Order, ECF No. 67 (GovInfo)](https://www.govinfo.gov/content/pkg/USCOURTS-txnd-4_23-cv-01110/pdf/USCOURTS-txnd-4_23-cv-01110-0.pdf) - retrieved 2026-07-20
- [2013 HIPAA Omnibus Final Rule, 78 FR 5566 (Jan. 25, 2013), conduit exception discussion at 5572](https://www.federalregister.gov/documents/full_text/text/2013/01/25/2013-01073.txt) - retrieved 2026-07-20
- [HHS Annual Civil Monetary Penalties Inflation Adjustment, 91 FR 3665 (Jan. 28, 2026), doc 2026-01688](https://www.federalregister.gov/documents/full_text/text/2026/01/28/2026-01688.txt) - retrieved 2026-07-20
- [HIPAA Security Rule to Strengthen the Cybersecurity of Electronic Protected Health Information, proposed rule (Jan. 6, 2025), doc 2024-30983](https://www.federalregister.gov/documents/2025/01/06/2024-30983/hipaa-security-rule-to-strengthen-the-cybersecurity-of-electronic-protected-health-information) - retrieved 2026-07-20
- [FTC Health Breach Notification Rule, final rule, 89 FR 47028 (May 30, 2024), doc 2024-10855, effective July 29, 2024](https://www.federalregister.gov/documents/full_text/text/2024/05/30/2024-10855.txt) - retrieved 2026-07-20
- [16 CFR 318.1, scope of the FTC Health Breach Notification Rule (eCFR)](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-318/section-318.1) - retrieved 2026-07-20 via the eCFR versioner API for date 2026-07-01
- [Google Analytics Help, HIPAA and Google Analytics](https://support.google.com/analytics/answer/13297105?hl=en) - retrieved 2026-07-20; source for the statement that Google does not offer a BAA for Analytics
- [Nevada Revised Statutes chapter 603A, consumer health data (NRS 603A.400 to 603A.550)](https://www.leg.state.nv.us/NRS/NRS-603A.html) - retrieved 2026-07-20; source for NRS 603A.550(2)(a), no private right of action
- [HIPAA Privacy Rule to Support Reproductive Health Care Privacy, final rule (Apr. 26, 2024), doc 2024-08503](https://www.federalregister.gov/documents/2024/04/26/2024-08503/hipaa-privacy-rule-to-support-reproductive-health-care-privacy) - retrieved 2026-07-20
- [OCR bulletin, Use of Online Tracking Technologies by HIPAA Covered Entities and Business Associates](https://www.hhs.gov/hipaa/for-professionals/privacy/guidance/hipaa-online-tracking/index.html) - **could not be retrieved on 2026-07-20**; hhs.gov returns HTTP 403 to automated requests. The bulletin's operative language quoted in this file comes from the administrative record as reproduced verbatim in the AHA v. Becerra opinion. Open this URL in a browser to read the current version and check whether OCR has posted a revision or a withdrawal notice.
- [FTC v. GoodRx Holdings, Inc., FTC case page](https://www.ftc.gov/legal-library/browse/cases-proceedings/2023090-goodrx-holdings-inc) - **could not be retrieved on 2026-07-20**; ftc.gov returns HTTP 403 to automated requests, for both the case page and the complaint PDF. The GoodRx quotation in this file is therefore marked UNVERIFIED. Open in a browser before citing it.

## Notes

- **Re-check the bulletin page before every healthcare engagement.** OCR could revise, withdraw, or replace the tracking bulletin, or re-issue the vacated rule through notice-and-comment rulemaking, which would cure the APA defect the court identified. The court explicitly said it "can envision numerous solutions that would reduce regulatory flux while ensuring IIHI is protected moving forward."
- **The vacatur's geographic reach is a live question.** The court vacated the rule under 5 U.S.C. 706 rather than issuing a nationwide injunction. Universal vacatur is contested doctrine. Do not tell a client the rule is dead everywhere for all purposes.
- **UNVERIFIED: appeal status.** Whether HHS appealed to the Fifth Circuit, and any outcome, could not be confirmed. Re-checked 2026-07-20: the district court opinion itself was retrieved and verified in full from GovInfo (ECF No. 67, 31 pages), but CourtListener's search API returned no matching docket for 4:23-cv-01110 or for any Fifth Circuit appeal, and hhs.gov continues to block automated retrieval. Absence of a result here is a tooling limitation, not evidence there was no appeal. Confirm before relying on the vacatur in client advice.
- **The January 2025 Security Rule proposal would change the build checklist materially** if finalized. It proposes removing the "addressable" category so that encryption, multi-factor authentication, and similar controls become mandatory. A Federal Register search on 2026-07-20 covering everything published from 2025-01-07 forward returned no final rule, no withdrawal, and no comment-period extension tied to doc 2024-30983, so it appears to remain a proposal. This is a negative search result rather than a confirmed status. Re-check the docket.
- **UNVERIFIED: the April 2024 reproductive health care privacy rule may have been vacated or narrowed by litigation** in 2025. Checked on 2026-07-20 and not resolved. A Federal Register search returned no rescinding, amending, or withdrawing document. The eCFR as of 2026-07-01 still carries the rule's operative text: 45 CFR 164.502(a)(5)(iii), the prohibition on certain reproductive health care uses and disclosures, and 45 CFR 164.509, the attestation requirement, both sourced to 89 FR 33063, Apr. 26, 2024. That is not proof the rule survived, because a judicial vacatur does not strip text from the CFR until the agency publishes a removal document. One loose thread worth noting: 45 CFR 164.520 was also amended by the same April 2024 rule (its source note cites 89 FR 33064), yet the current text of 164.520 contains no reproductive health language at all. Do not read that either way without checking the docket. This affects Notice of Privacy Practices content, which the client's counsel supplies anyway. Flag it to counsel rather than resolving it in the build.
- **UNVERIFIED: the July 2023 joint FTC and OCR letter** to roughly 130 hospital systems and telehealth providers about tracking technologies is widely reported but could not be retrieved in this pass (ftc.gov and hhs.gov both returned 403). Do not cite a specific recipient count to a client without confirming it.
- **Conflicts with other files in this library.** A cookie consent banner built for GDPR or CCPA does not solve HIPAA. HIPAA has no consent-banner mechanism that legitimizes disclosing PHI to an advertising vendor; the lawful routes are a BAA or a valid HIPAA authorization from the individual, and a banner click is neither. Do not let a consent management platform become the answer to the tracking question on a healthcare site. Where a state comprehensive privacy law also applies, run both analyses and take the stricter result.
- **State law frequently exceeds HIPAA** on health data, particularly Washington's My Health My Data Act and Nevada's consumer health data law (NRS 603A.400 to 603A.550), both of which reach non-covered entities. They differ on enforcement, and the difference matters for risk pricing. Washington's act is enforceable through the Consumer Protection Act, which supports private suits. Nevada's expressly is not: NRS 603A.550(2)(a) provides that the provisions "[d]o not create a private right of action," leaving enforcement to the Attorney General as a deceptive trade practice. Check the state file for the client's state and for the states where patients are located.
- **HIPAA has no private right of action**, which is why plaintiffs' firms bring pixel cases under state wiretap statutes instead. That changes the risk calculus but does not lower it, because those statutes can carry statutory damages per violation.
