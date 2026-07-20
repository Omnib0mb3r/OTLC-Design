# Data Breach Notification: GDPR Articles 33-34, the US state notification statutes, and the sector rules (HIPAA, GLBA Safeguards, FTC HBNR, PCI DSS)

| Field | Value |
|---|---|
| **Jurisdiction** | EU/EEA and UK (GDPR Arts. 33-34); all 50 US states plus DC, Guam, Puerto Rico and the US Virgin Islands; US federal sector rules (HHS, FTC); PCI DSS applies by contract worldwide |
| **Regulator / enforcer** | EU/EEA data protection supervisory authorities and the UK ICO; US state attorneys general; HHS Office for Civil Rights (HIPAA); FTC (GLBA Safeguards Rule, Health Breach Notification Rule); acquiring bank and card brands (PCI DSS) |
| **In force since** | California SB 1386, the first state statute, effective 2003. GDPR applicable 25 May 2018. HIPAA Breach Notification Rule under HITECH, final Omnibus Rule compliance date 23 September 2013. FTC Health Breach Notification Rule since 2009. |
| **Last amended** | FTC Safeguards Rule notification duty (16 CFR 314.4(j)) effective 13 May 2024. FTC Health Breach Notification Rule amendments effective 29 July 2024. Texas AG deadline cut to 30 days effective 1 September 2023. HIPAA civil penalty amounts adjusted for inflation effective 28 January 2026. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. CIRCIA (US federal critical-infrastructure incident reporting) is still pending: see Notes. |

This is not one law. It is a stack of overlapping clocks that start at the same moment and run at different speeds. The shortest applicable clock governs the schedule. Everything below is written so the studio can decide, before launch, who gets told, in what order, and by when.

---

## Applies when

Answer these at intake. Any single "yes" pulls this file into scope.

**The baseline trigger (almost every project):**

- The site stores any personal data about an identifiable person, including a contact-form submission sitting in a database, a mailing list, or a user account table. There is no revenue floor and no headcount floor on the US state statutes or on GDPR breach duties. A one-person business with a contact form is caught.

**GDPR Articles 33-34 apply when:**

- The client is established in the EU or EEA, **or** the site offers goods or services to people in the EU/EEA, **or** it monitors their behaviour (analytics profiling counts). Visitor location drives this, not company location.
- The UK is a separate jurisdiction with the same 72-hour structure under UK GDPR. A site serving both needs both an EU supervisory authority and the ICO identified in advance.
- Note the split of duties: the **controller** notifies the authority. A **processor** (which is what the studio usually is, and what most of the client's SaaS vendors are) notifies the controller, with no fixed hour count in the statute beyond "without undue delay".

**US state statutes apply when:**

- Any resident of any US state has "personal information" (as that state defines it) held by the client. The visitor's state of residence controls, not where the client or the server is. A Florida business with one Washington customer owes Washington's 30-day clock for that person.
- Definitions of covered "personal information" vary by state but commonly turn on a name combined with a Social Security number, driver's licence or state ID number, or a financial account number. Several states also cover a username or email address combined with a password or security question answer.
- **Encryption is the near-universal exemption.** Most state statutes do not treat acquisition of properly encrypted data as a reportable breach, provided the key was not also taken. This is the single highest-leverage build decision in this file.

**HIPAA Breach Notification Rule applies when:**

- The client is a covered entity (health plan, healthcare clearinghouse, or a healthcare provider transmitting health information electronically in connection with a covered transaction), **or** the studio or the client is a business associate handling protected health information on a covered entity's behalf.
- If a business associate relationship exists, a signed BAA is a prerequisite, and the BAA's own notification deadline to the covered entity is usually shorter than the regulatory one. Read the BAA, not just the rule.

**FTC Health Breach Notification Rule applies when:**

- The client offers a health app, wellness service, or connected device that holds identifiable health information and is **not** covered by HIPAA. This is the rule that catches the direct-to-consumer fitness tracker, the period tracker, and the supplement quiz that stores answers.

**GLBA Safeguards Rule (16 CFR 314.4(j)) applies when:**

- The client is a "financial institution" under FTC jurisdiction. This definition is much wider than banks and includes mortgage brokers, payday lenders, tax preparers, collection agencies, auto dealers arranging financing, and finders. A site that arranges consumer credit is likely in scope.

**PCI DSS incident obligations apply when:**

- The client accepts payment cards in any form, including a fully hosted checkout. Redirecting to Stripe or Shopify reduces the requirement set but does not remove the contractual duty to report a suspected compromise to the acquirer.

**Does not apply when:**

- The site collects nothing and stores nothing: a static brochure page with no forms, no analytics, no embedded third-party scripts, and no logs retaining IP addresses. This is rarer than clients assume. Server access logs holding IPs are personal data under GDPR.

---

## What the site must have

The deliverables here are mostly decisions and records rather than pages. The reason they belong in the build is that you cannot retrofit an audit trail after the incident that needs it.

| Requirement | What that means in the build |
|---|---|
| **A named breach owner and a deputy** | One person at the client (not the studio) who decides that a clock has started, plus a backup for holidays. Written into `BRIEF.md` at intake with a phone number, not an email alias. The GDPR clock runs on wall-clock hours including weekends. |
| **A written incident runbook** | A one-page document listing, in order: who is called first, who declares a breach, who contacts counsel, who contacts the insurer, who drafts notices, who signs off on sending them. Lives in the repo or the client's handbook. PCI DSS Requirement 12.10.1 makes an incident response plan mandatory for card-accepting clients and requires it to cover notification of payment brands and acquirers. |
| **Identified supervisory authority (GDPR)** | Name the specific authority and its online reporting form URL before launch. For cross-border processing, identify the lead supervisory authority. Do not plan to research this during the 72 hours. |
| **Identified state AG portals (US)** | For each state where the client has a meaningful customer base, record the AG breach-reporting URL. Several are web forms that require specified fields (Washington requires the affected-resident count, the data types, the exposure window, containment steps, and a redacted sample of the consumer notice). |
| **Encryption at rest, and key separation** | Encrypt the database and the backups, and keep the key management separate from the data store. Under GDPR Art. 34(3)(a) encryption that renders data unintelligible can remove the duty to notify individuals. Under most US state statutes it can remove the duty entirely. Both defences collapse if the key was accessible to the attacker. |
| **An audit trail that can answer "whose data, which fields, when"** | The build must be able to reconstruct scope. At minimum: row-level created/updated timestamps, access logging on any admin or export route, and log retention long enough to cover a slow discovery. If you cannot enumerate affected individuals, you cannot notify them, and you default to worst-case notification. |
| **A reachable contact field per user** | Every record of a person needs a route to reach them. Washington bars using a compromised email address to send the notice, so a postal address or a second channel matters for high-risk data sets. |
| **Log retention sized to reality** | Breaches are commonly discovered long after intrusion. Retain the logs needed to scope an incident well beyond a 7-day or 30-day default. Balance against data-minimisation duties and write the chosen window down. |
| **A processor and subprocessor inventory** | A list of every vendor touching personal data (host, CDN, email sender, analytics, form handler, CRM, payment processor) with a breach-notification contact for each. Under GDPR Art. 33(2) a processor must tell the controller without undue delay, so the client's contracts should impose a hard number (24 or 48 hours) rather than repeating "without undue delay". |
| **Contract clauses that flow the clock down** | The studio's own contract should say what the studio does if the studio is the one who discovers or causes the incident, and how fast it tells the client. If the studio is a HIPAA business associate, a BAA is required before any PHI is touched. |
| **Pre-drafted notice templates** | Draft the consumer notice, the authority notice, and the holding statement before launch. HIPAA prescribes contents at 45 CFR 164.404(c): what happened, the breach and discovery dates, the types of information involved, steps individuals should take, what the entity is doing, and a contact procedure including a toll-free number, email, website, or postal address. |
| **A breach register** | GDPR Art. 33(5) requires the controller to document every personal data breach including facts, effects, and remedial action, whether or not it was notified. HIPAA requires a log of sub-500 breaches for annual submission. Build the register at launch, as a spreadsheet if nothing else, because "we had no incidents" is not evidence and a regulator can ask for the record. |
| **A published security contact** | A `/.well-known/security.txt` file (RFC 9116) and a monitored inbox. Most small-site breaches are reported by an outsider. If nobody reads the inbox, the discovery date slips and every downstream clock is already burning. |
| **Cyber insurance details on the runbook** | Many policies require notice to the insurer within a short window and require the insurer's approval before engaging a forensics firm. Engaging your own responder first can void cover. |

### The clocks, ordered

Decide the order before launch, because these run in parallel and the drafting effort collides.

| Who | Clock | Trigger | Source |
|---|---|---|---|
| EU/UK supervisory authority | Without undue delay, and where feasible **not later than 72 hours** after becoming aware | Any personal data breach, unless unlikely to result in a risk to rights and freedoms | GDPR Art. 33(1) |
| Affected individuals (GDPR) | Without undue delay (no fixed hour count) | Breach **likely to result in a high risk** to rights and freedoms | GDPR Art. 34(1) |
| Controller (from processor) | Without undue delay after the processor becomes aware | Any personal data breach at the processor | GDPR Art. 33(2) |
| Acquirer and card brands | Immediately on suspicion, per the acquirer's contract | Suspected or confirmed cardholder data compromise | PCI DSS Req. 12.10.1 |
| NYDFS-regulated entities | **72 hours** after determining a cybersecurity incident occurred; **24 hours** for an extortion payment | Covered entity under 23 NYCRR Part 500 | 23 NYCRR 500.17 |
| FTC (GLBA Safeguards) | As soon as possible, **no later than 30 days** after discovery | Notification event involving unencrypted customer information of **at least 500 consumers** | 16 CFR 314.4(j) |
| State AGs (fastest tier) | **30 days**: Colorado, Florida, Maine, Washington. Texas AG is 30 days even though Texas consumers get 60. | Varies by state; AG thresholds are commonly 500 residents (CO, FL, WA) or 250 (TX) | See state citations in Sources |
| Individuals (HIPAA) | Without unreasonable delay, **no later than 60 calendar days** after discovery | Breach of unsecured protected health information | 45 CFR 164.404(b) |
| HHS Secretary (HIPAA) | **500 or more individuals**: contemporaneously with individual notice. **Fewer than 500**: log and submit within **60 days after the end of the calendar year**. | As above | 45 CFR 164.408 |
| Prominent media outlets (HIPAA) | Same 60-day outer limit | More than 500 residents of a single state or jurisdiction | 45 CFR 164.406 |
| Individuals and FTC (Health Breach Notification Rule) | Without unreasonable delay, **no later than 60 calendar days** after discovery. FTC notice is contemporaneous when 500 or more individuals are affected; otherwise an annual log within 60 days of year end. | Non-HIPAA health app or PHR breach | 16 CFR 318.4, 318.5 |
| Consumer reporting agencies | Varies. Florida and Maine both require it above 1,000 individuals at a single time, without unreasonable delay. | State-specific | Fla. Stat. 501.171(5); 10 MRS 1348 |

Two things to internalise from that table. First, the GDPR 72-hour clock is much shorter than any US clock, so a site with EU visitors is scheduled by GDPR. Second, the GDPR authority notice and the GDPR individual notice are **separate decisions with separate triggers**. Notifying the authority does not oblige you to notify individuals, and the reverse is also true. Article 33 asks whether there is a risk. Article 34 asks whether there is a high risk.

GDPR also allows phased reporting. Article 33(4) permits information to be supplied in stages where it is not all available at once, so an incomplete report inside 72 hours beats a complete report on day five.

---

## How to verify

Run these before delivery. Each is a real check with a real output.

1. **Prove you can scope an incident.** Ask the client's DBA or run it yourself: "list every user record touched between two dates, with the fields present". If the schema has no `updated_at`, no access log, and no soft-delete trail, the answer is unobtainable and the build fails this file. Fix before launch.
2. **Confirm encryption at rest is actually on.** Do not trust the hosting marketing page. For managed Postgres check the instance encryption setting in the provider console. For S3 or equivalent object storage confirm default bucket encryption. For backups, check the snapshot settings separately: unencrypted backups of an encrypted database is a common configuration.
3. **Confirm the key is not sitting next to the data.** Grep the repo and the environment for keys: `git grep -iE "(BEGIN (RSA|EC|OPENSSH) PRIVATE|aws_secret|ENCRYPTION_KEY|DB_PASSWORD)"` across the full history, not just HEAD. A key committed in 2024 and removed in 2025 is still in the history and still defeats the encryption safe harbour.
4. **Verify the log retention window.** Open the hosting or log provider's retention setting and read the number. Write it in `BRIEF.md`. If it is 7 days, that is not enough to scope a breach discovered in month three.
5. **Check the user table has a usable contact route.** `SELECT count(*) FROM users WHERE email IS NULL OR email = '';` Any non-zero count is a set of people you cannot notify.
6. **Enumerate third parties from the wire, not from memory.** Load the site with devtools Network open, filter to third-party domains, and reload with cache disabled. Every distinct third-party host is a processor that needs a breach contact in the inventory. Cross-check that list against the privacy policy: a host that appears in the Network panel and not in the policy is a documentation gap and often an undisclosed processor.
7. **Test the security contact.** Fetch `https://<domain>/.well-known/security.txt` and confirm it returns 200 with a current `Contact:` and an unexpired `Expires:` field. Then send a message to that address and confirm a human sees it.
8. **Read the vendor DPAs for their notification deadline.** Grep the signed agreements for "notif" and record the number of hours each vendor commits to. If a vendor only promises "without undue delay", the client's 72-hour clock depends on that vendor's goodwill.
9. **Dry-run the runbook.** Fifteen minutes, out loud, with the client: "It is Saturday 22:00 and a researcher emails that our user table is on a forum. What happens next?" Every step where the answer is "we would look that up" is a task to complete before launch.
10. **For card-accepting sites, confirm the acquirer contact.** The merchant agreement names who to call. Get that number onto the runbook. PCI DSS Req. 12.10.3 expects responders to be available 24/7.

---

## Penalties

- **GDPR.** Breaches of Articles 33 and 34 fall under Article 83(4)(a), which covers controller and processor obligations "pursuant to Articles 8, 11, 25 to 39 and 42 and 43". The ceiling is **10,000,000 EUR or 2% of total worldwide annual turnover of the preceding financial year, whichever is higher**. The underlying security failure can be charged separately under Article 32, and inadequate lawful basis or transparency sits in the higher 20,000,000 EUR / 4% tier under Article 83(5).
- **Florida.** Fla. Stat. 501.171(9) sets civil penalties of **$1,000 for each day up to the first 30 days** following a violation of subsection (3) or (4), then **$50,000 for each subsequent 30-day period or portion thereof for up to 180 days**, and if the violation continues beyond 180 days, a further amount **not to exceed $500,000**. The $500,000 is an additional figure for violations running past 180 days, not an overall cap on the total.
- **HIPAA.** For penalties assessed on or after **28 January 2026**, the inflation-adjusted per-violation minimums are **$145** (Tier 1, no knowledge), **$1,461** (Tier 2, reasonable cause), **$14,602** (Tier 3, willful neglect corrected within 30 days), and **$73,011** (Tier 4, willful neglect not corrected). The per-violation maximum is **$73,011** for Tiers 1 to 3 and **$2,190,294** for Tier 4, with a **$2,190,294** calendar-year cap for violations of an identical provision. UNVERIFIED: OCR has separately applied lower annual caps for Tiers 1 to 3 under a 2019 enforcement-discretion notice, and the studio should not rely on either figure without counsel confirming which applies.
- **California civil exposure.** Cal. Civ. Code 1798.150 gives consumers a private right of action where nonencrypted and nonredacted personal information is exfiltrated because the business failed to maintain reasonable security. Statutory damages run **$100 to $750 per consumer per incident, or actual damages, whichever is greater**. For a 50,000-record breach that is a class action with a floor in the millions, and it is the practical reason encryption at rest is a build requirement rather than a nice-to-have.
- **Other state AGs.** Most state statutes are enforced by the AG under that state's unfair or deceptive practices act, with per-violation penalties that vary widely. Check the specific state before quoting a number to a client.
- **PCI DSS.** Penalties are contractual, not statutory. Fines flow from the card brands through the acquiring bank to the merchant, and a compromised entity can be required to fund a PCI Forensic Investigator engagement and can lose the ability to process cards. UNVERIFIED: published fine schedules are not authoritative because the amounts are set in private brand and acquirer agreements. Read the client's merchant agreement.

---

## Common ways sites fail this

- **No audit trail, so no scope.** The most frequent and most expensive failure. Without per-record timestamps and access logs the client cannot say who was affected, so counsel advises notifying everyone. A 400-person breach becomes a 40,000-person notification, and the cost and reputational damage scale with it.
- **Backups left unencrypted while the primary database is encrypted.** The safe harbour is defeated by the weakest copy.
- **Treating the 72 hours as business hours.** It is not. It runs across a weekend and a public holiday. A runbook with only one named contact fails the first time that person is on a plane.
- **Assuming the vendor handles it.** A hosted form handler or CRM that suffers a breach makes the client the controller with the notification duty. The vendor is the processor. The letter still goes out over the client's name.
- **Confusing the Article 33 and Article 34 triggers.** Teams either notify individuals for every minor incident, which erodes trust and creates a public record, or skip individual notice on the theory that telling the regulator was enough.
- **Log retention set to the platform default.** Seven or fourteen days of logs is normal on cheap hosting and useless for an incident discovered in month four.
- **Only the shortest jurisdiction is researched.** A studio checks the client's home-state rule and misses that customers in Colorado, Florida, Maine, and Washington are on a 30-day clock, and that any EU customer collapses it to 72 hours for the authority notice.
- **security.txt absent or stale.** Researchers who cannot find a contact post publicly instead. The client learns about the breach from Twitter, and the discovery date is now also a PR event.
- **No BAA before touching PHI.** For healthcare clients this is a standalone violation independent of any breach, and it is usually discovered during the breach investigation.
- **Analytics or session-replay scripts on authenticated pages.** These export user data to a third party continuously. When that third party is breached the client owns the notification, and the client frequently did not know the script was there. This is why the devtools Network sweep is a delivery gate.
- **Notice templates written during the incident.** Drafting under time pressure with counsel, the insurer, and the client's CEO all editing produces late, inconsistent notices. Draft them calm.

---

## Sources

Official sources first. All retrieved 2026-07-20.

- [GDPR Article 33: Notification of a personal data breach to the supervisory authority](https://gdpr-info.eu/art-33-gdpr/) (retrieved 2026-07-20)
- [GDPR Article 34: Communication of a personal data breach to the data subject](https://gdpr-info.eu/art-34-gdpr/) (retrieved 2026-07-20)
- [GDPR Article 83: General conditions for imposing administrative fines](https://www.privacy-regulation.eu/en/article-83-general-conditions-for-imposing-administrative-fines-GDPR.htm) (retrieved 2026-07-20)
- [EDPB Guidelines 9/2022 on personal data breach notification under GDPR](https://www.edpb.europa.eu/our-work-tools/our-documents/guidelines/guidelines-92022-personal-data-breach-notification-under_en) (retrieved 2026-07-20; landing page only, PDF not retrieved: see Notes)
- [45 CFR 164.404: Notification to individuals (Cornell LII)](https://www.law.cornell.edu/cfr/text/45/164.404) (retrieved 2026-07-20)
- [45 CFR 164.408: Notification to the Secretary (Cornell LII)](https://www.law.cornell.edu/cfr/text/45/164.408) (retrieved 2026-07-20)
- [16 CFR 314.4: Elements of an information security program, including (j) FTC notification (Cornell LII)](https://www.law.cornell.edu/cfr/text/16/314.4) (retrieved 2026-07-20)
- [16 CFR 318.4: Timeliness of notification, Health Breach Notification Rule (Cornell LII)](https://www.law.cornell.edu/cfr/text/16/318.4) (retrieved 2026-07-20)
- [16 CFR 318.5: Method of notice, Health Breach Notification Rule (Cornell LII)](https://www.law.cornell.edu/cfr/text/16/318.5) (retrieved 2026-07-20)
- [23 NYCRR 500.17: Notices to superintendent (Cornell LII)](https://www.law.cornell.edu/regulations/new-york/23-NYCRR-500.17) (retrieved 2026-07-20)
- [Washington State Attorney General: Washington's Data Breach Notification Laws (RCW 19.255, RCW 42.56.590)](https://www.atg.wa.gov/washington-s-data-breach-notification-laws) (retrieved 2026-07-20)
- [Colorado Attorney General: Data Protection Laws (C.R.S. 6-1-716)](https://coag.gov/resources/data-protection-laws/) (retrieved 2026-07-20)
- [Florida Statutes 501.171: Security of confidential personal information (Florida Senate)](https://www.flsenate.gov/Laws/Statutes/2024/501.171) (retrieved 2026-07-20)
- [10 MRS 1348: Security breach notice requirements (Maine Legislature)](https://legislature.maine.gov/statutes/10/title10sec1348.html) (retrieved 2026-07-20)
- [Texas Business and Commerce Code 521.053 (Texas Statutes)](https://statutes.capitol.texas.gov/Docs/BC/htm/BC.521.htm) (retrieved 2026-07-20; the statutes.capitol.texas.gov viewer renders via script and returned only site navigation to automated retrieval, so the 60-day consumer deadline and the 30-day / 250-resident AG deadline were confirmed against the mirrored text at [texas.public.law](https://texas.public.law/statutes/tex._bus._and_com._code_section_521.053))
- [Cal. Civ. Code 1798.150: Private right of action (California Legislative Information)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=1798.150.&lawCode=CIV) (retrieved 2026-07-20)
- [NCSL: Security Breach Notification Laws (confirms all 50 states, DC, Guam, Puerto Rico, US Virgin Islands)](https://www.ncsl.org/technology-and-communication/security-breach-notification-laws) (retrieved 2026-07-20)
- [CISA: Cyber Incident Reporting for Critical Infrastructure Act of 2022 (CIRCIA)](https://www.cisa.gov/topics/cyber-threats-and-advisories/information-sharing/cyber-incident-reporting-critical-infrastructure-act-2022-circia) (retrieved 2026-07-20; page returned 403 to automated retrieval, status unconfirmed)
- [FTC: Safeguards Rule notification requirement now in effect (business guidance blog, May 2024)](https://www.ftc.gov/business-guidance/blog/2024/05/safeguards-rule-notification-requirement-now-effect) (retrieved 2026-07-20; page returned 403 to automated retrieval, the underlying rule text was verified at Cornell LII instead)
- [HHS: HIPAA Breach Notification Rule](https://www.hhs.gov/hipaa/for-professionals/breach-notification/index.html) (retrieved 2026-07-20; page returned 403 to automated retrieval, the underlying regulation text was verified at Cornell LII instead)
- [PCI SSC: Responding to a Cardholder Data Breach](https://listings.pcisecuritystandards.org/documents/Responding_to_a_Cardholder_Data_Breach.pdf) (retrieved 2026-07-20; PDF text not machine-extractable, see Notes)
- [Schellman: Incident Response in PCI DSS v4.0, Requirement 12.10 breakdown](https://www.schellman.com/blog/pci-compliance/incident-response-in-pci-dss-v4) (retrieved 2026-07-20; secondary source used for the 12.10 sub-requirement structure)
- [45 CFR 164.406: Notification to the media (Cornell LII)](https://www.law.cornell.edu/cfr/text/45/164.406) (retrieved 2026-07-20)
- [Unified Agenda RIN 1670-AA04, CIRCIA reporting requirements (reginfo.gov)](https://www.reginfo.gov/public/do/eAgendaViewRule?pubId=202604&RIN=1670-AA04) (retrieved 2026-07-20; listed at Final Rule Stage on the 2026 agenda)
- [Mercer: HHS adjusts 2026 HIPAA, certain ACA and MSP monetary penalties](https://www.mercer.com/insights/law-and-policy/hhs-adjusts-2026-hipaa-certain-aca-and-msp-monetary-penalties/) (retrieved 2026-07-20; secondary source for the 2026 inflation-adjusted figures, citing 91 FR published 28 January 2026)

---

## Notes

**Research gaps in this revision.** Several official sources blocked automated retrieval on 2026-07-20: ecfr.gov, federalregister.gov, ftc.gov, hhs.gov, ico.org.uk, and cisa.gov all returned 403 or redirected to a challenge page. Where that happened the regulation text was verified through Cornell LII (a faithful mirror of the CFR) instead of the agency's own page. Two items rest on secondary sources and should be re-checked against primary text before being quoted to a client: the 2026 HIPAA penalty figures, and the PCI DSS 12.10 sub-requirement numbering.

**The GDPR "aware" question is unresolved here.** Article 33 starts the clock "after having become aware" of the breach, and the statute does not define awareness. EDPB Guidelines 9/2022 are the interpretive authority and the PDF is linked above, but the document text could not be retrieved on this pass, so no specific standard is quoted in this file. This matters operationally, because the difference between "aware" at first suspicion and "aware" at confirmed certainty is often two of the three available days. Read Guidelines 9/2022 directly before advising a client on when their clock started.

**CIRCIA is pending and the reported status conflicts.** UNVERIFIED: sources retrieved on 2026-07-20 disagree about whether CISA's final rule under the Cyber Incident Reporting for Critical Infrastructure Act arrived in May 2026 or is still targeted for September 2026, and the CISA page could not be retrieved to settle it. The one primary signal obtained on this pass was the Unified Agenda entry for RIN 1670-AA04 (reginfo.gov, 2026 agenda), which still lists the rule at **Final Rule Stage**, implying the final rule had not published as of that agenda. Unified Agenda entries lag actual publication, so this narrows the question without closing it. The statutory shape is stable across all sources: 72 hours to report a covered cyber incident and 24 hours to report a ransomware payment. This will mostly miss small studio clients, since it targets critical-infrastructure sectors, but confirm the final rule's status and its covered-entity definition before telling a client in energy, water, health, or financial services that it does not apply to them.

**Watch the state patchwork for movement.** State legislatures amend these statutes most years, and the direction of travel is shorter deadlines and broader definitions of covered personal information. Texas cut its AG deadline from 60 days to 30 in 2023. Treat the 30-day tier (Colorado, Florida, Maine, Washington) as the current floor rather than a permanent one, and re-verify any state figure older than six months. This file and [`us-state-privacy-laws.md`](us-state-privacy-laws.md) go stale fastest in this directory.

**Conflicts with other files in this library.** Breach notification pulls against data minimisation. GDPR and the US state comprehensive privacy laws push toward collecting less and deleting sooner, while incident scoping needs enough log history to reconstruct what happened. Resolve it by retaining detailed *access* logs longer than the *personal data* itself, and by writing the reasoning down. Also read [`pci-dss.md`](pci-dss.md) for the scope question of what the client's SAQ level actually is, [`hipaa.md`](hipaa.md) for BAA mechanics and tracking-pixel exposure, [`gdpr.md`](gdpr.md) for the controller versus processor determination that decides who notifies whom, and [`ccpa-cpra.md`](ccpa-cpra.md) for the California private right of action that makes encryption at rest the highest-value line item in this file.

**The studio's own exposure.** If the studio holds client data (staging databases with production dumps, admin credentials, exports sitting in a Downloads folder) then the studio is a processor and possibly a controller in its own right. A production data dump copied to a laptop for debugging is the single most common way a design studio becomes the source of its client's breach. Decide the rule before the project starts: staging uses synthetic or masked data, and any production copy is time-boxed, encrypted, and logged.
