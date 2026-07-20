# GDPR: Regulation (EU) 2016/679 (General Data Protection Regulation), plus UK GDPR and the Data (Use and Access) Act 2025

| Field | Value |
|---|---|
| **Jurisdiction** | EU and EEA (Norway, Iceland, Liechtenstein). Separately, the UK, via UK GDPR + Data Protection Act 2018 as amended by DUAA 2025. Reaches non-EU businesses under Article 3(2). |
| **Regulator / enforcer** | National supervisory authorities (Irish DPC, CNIL, Garante, and so on), coordinated by the European Data Protection Board. Lead authority under the Article 56 one-stop-shop. UK: Information Commissioner's Office (ICO). |
| **In force since** | Entered into force 24 May 2016. Applies from 25 May 2018 (Article 99). UK GDPR from 1 January 2021. |
| **Last amended** | EU: the operative provisions in this file are unchanged since 25 May 2018. The Data Omnibus that would amend GDPR is still in Council negotiation (see Notes). UK: substantially amended by the Data (Use and Access) Act 2025, main provisions in force 5 February 2026, complaints duty in force 19 June 2026. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. UK divergence is now live and growing. |

---

## Applies when

Answer these at intake. Any single "yes" in the first group pulls GDPR in.

**Territorial triggers (Article 3). Check each one.**

- [ ] The client has any establishment in the EU or EEA (office, branch, subsidiary, a single employee or agent with a stable arrangement), and the site's data processing happens in the context of that establishment's activities. Article 3(1). The place of processing and the location of the server do not matter.
- [ ] The site offers goods or services to people **located in** the EU/EEA, whether or not payment is required. Article 3(2)(a).
- [ ] The site monitors the behaviour of people **while they are in** the EU/EEA. Article 3(2)(b).

**"Located in", not "citizen of".** Article 3(2) turns on where the person is, not their nationality. A business outside the EU serving a German citizen who lives in Taiwan is not caught by that fact alone. The EDPB's own illustration is a Taiwanese bank whose customers reside in Taiwan but hold German citizenship: not subject to GDPR, because the bank is active only in Taiwan and its activities are not directed at the EU market (EDPB Guidelines 3/2018, Example 11). A US site that deliberately sells into France is caught even though every buyer is a French national on French soil.

**A US studio building a US client site IS caught when any of these are true.** The EDPB lists these as factors showing intent to offer goods or services into the Union. No single one decides it; they are weighed together (Guidelines 3/2018, section 2.b, drawing on CJEU Joined Cases C-585/08 and C-144/09, Pammer / Hotel Alpenhof):

- The EU or a Member State is named by reference to the good or service offered.
- The client pays a search engine for referencing to reach EU consumers, or runs ad campaigns aimed at an audience in an EU country.
- The activity is international by nature (tourism is the EDPB's example).
- The site lists a dedicated address or a phone number reachable from an EU country (an international dialling code is the tell).
- The site uses a top level domain other than that of the country the business sits in, including neutral ones such as `.eu`, or a country TLD such as `.de`.
- The site gives travel directions from EU Member States to where the service is delivered.
- The site names an international clientele domiciled in EU Member States, in particular by publishing testimonials written by them.
- The site uses a language or currency other than the one generally used in the trader's own country, especially one of an EU Member State (a EUR price toggle, a `/de` locale, a currency switcher).
- The client offers delivery of goods into EU Member States (check the shipping-country dropdown in the checkout).

**What is NOT enough on its own** (Recital 23, confirmed by the EDPB): the site merely being reachable from the EU; the site showing an email address or a postal address; a phone number without an international code; the site being in English when the business is in an English-speaking third country. Goods or services provided "inadvertently or incidentally" to someone in the EU fall outside scope.

**Monitoring (Article 3(2)(b)) is the trigger most US builds trip over.** The EDPB says monitoring covers, among others:

- Behavioural advertising.
- Geo-localisation, in particular for marketing.
- Online tracking by cookies or other techniques such as fingerprinting.
- Personalised diet and health analytics services online.
- CCTV.
- Market surveys and other behavioural studies based on individual profiles.
- Monitoring or regular reporting on an individual's health status.

Practically: a Meta Pixel, a TikTok pixel, a Google Ads remarketing tag, Hotjar or Clarity session recording, or any audience-building tag that fires for a visitor sitting in the EU is behavioural monitoring of behaviour taking place in the Union. The EDPB does not treat every collection of data as monitoring; it asks about the controller's purpose and any later profiling. Plain server logs or aggregate hit counting with no profiling are a weaker case for scope than a remarketing pixel, which is a strong one.

**UK triggers.** UK GDPR mirrors Article 3 with "the United Kingdom" substituted. If the site targets UK visitors or monitors their behaviour, run the UK column of every table below as well as the EU one. Since 5 February 2026 the two regimes give different answers in several places.

**Who is NOT caught**

- A US business with no EU establishment, selling only to US addresses, priced only in USD, shipping only domestically, with no EU-directed advertising and no behavioural tracking that reaches EU visitors. An EU visitor stumbling onto the site does not by itself create scope.
- Processing that is purely household or personal activity (Article 2(2)(c)). This does not cover a client's business site.

---

## What the site must have

| Requirement | What that means in the build |
|---|---|
| **A lawful basis recorded per purpose** (Art 6(1)) | For each processing purpose (contact form, newsletter, analytics, order fulfilment, session recording) write down which of the six bases applies: consent, contract, legal obligation, vital interests, public task, legitimate interests. One basis per purpose, chosen before launch, not retrofitted. Put the table in `BRIEF.md`. |
| **Privacy notice at the point of collection** (Arts 12-14) | A `/privacy` page in plain language, and a link to it next to every form that collects data, not only in the footer. It must name the controller and its contact details, the DPO or EU representative if there is one, each purpose and its lawful basis, the legitimate interests being relied on where that basis is used, recipients or categories of recipients (every third-party processor: host, CRM, email tool, analytics), transfers outside the EEA and the safeguard used, retention periods or the criteria for setting them, all data subject rights, the right to withdraw consent, the right to complain to a supervisory authority, and whether providing data is a statutory or contractual requirement. |
| **Consent that meets Art 4(11) and Art 7 where consent is the basis** | Freely given, specific, informed, unambiguous, and given by a statement or clear affirmative action. In the build: no pre-ticked boxes, no implied consent from scrolling or continued browsing, granular per-purpose toggles rather than one blanket switch, a "reject all" control given the same visual weight and click count as "accept all", consent that is not a precondition of service where the service does not need it (Art 7(4)), and withdrawal that is as easy as giving it (Art 7(3)). |
| **Non-essential scripts blocked until consent** | Tags fire only after an affirmative signal. Do not ship an "accept" banner over tags that already fired on page load. This obligation comes from the ePrivacy Directive Art 5(3) rather than GDPR itself; see [`eprivacy-cookies.md`](eprivacy-cookies.md) for the banner mechanics. GDPR supplies the standard those cookie consents have to meet. |
| **Consent records** (Art 7(1)) | Log, per consent event: an identifier for the user or device, timestamp, the exact purposes accepted and refused, the version or hash of the notice text shown, and the collection method. Store withdrawals the same way. Keep the log for as long as the processing runs plus a defensible period after. A consent banner with no server-side log cannot demonstrate consent, which is what Art 7(1) requires. |
| **Data subject rights, with a working route to exercise them** (Arts 15-22) | Access, rectification, erasure, restriction, portability, objection, and rights around solely automated decisions. Build one reachable channel (a form or a monitored address) and name it in the privacy notice. Rights requests are free (Art 12(5)) unless manifestly unfounded or excessive. |
| **DSAR response inside one month** (Art 12(3)) | One month from receipt. Extendable by two further months where the request is complex or numerous, but the extension and its reasons must be communicated to the person within the first month. If the site collects personal data, the client needs a named owner for this clock before launch. |
| **Processor contracts** (Art 28(3)) | A written data processing agreement with every vendor touching personal data: host, CDN, form handler, email service, CRM, analytics, session-recording tool, error tracker. Collect the DPAs during the build, not at delivery. |
| **Records of processing activities** (Art 30) | A written ROPA. The Art 30(5) exemption for organisations with fewer than 250 employees is narrow: it falls away if processing is likely to result in a risk to rights and freedoms, is not occasional, or includes special categories (Art 9) or criminal offence data (Art 10). Any site with a live analytics stack or a customer database is processing regularly, so the exemption usually does not apply. Assume the client needs one. |
| **Security appropriate to risk** (Art 32) | HTTPS everywhere with HSTS, encryption at rest for stored personal data, least-privilege access to the CMS and database, MFA on admin accounts, no personal data in client-side logs or in git. Enforcement of these lives in OTLC Guardian. |
| **Data protection by design and by default** (Art 25) | Collect only the fields needed for the stated purpose. Delete the "how did you hear about us" field nobody reads. Default settings must be the privacy-protective ones. |
| **DPIA where processing is high risk** (Art 35) | Required for systematic and extensive profiling with legal or similarly significant effects, large-scale processing of special categories, and large-scale systematic monitoring of a publicly accessible area. A marketing site rarely triggers it. A site doing behavioural scoring, health data, or biometric login does. Escalate to the client's counsel rather than deciding this in the build. |
| **DPO where Art 37(1) triggers** | Mandatory when the controller is a public authority or body; when core activities require regular and systematic monitoring of data subjects on a large scale; or when core activities consist of large-scale processing of Art 9 special categories or Art 10 criminal data. "Core activities" means the client's actual business, not its back-office HR. Most SMB sites do not trigger it. If a DPO exists, publish the contact details in the privacy notice and notify the supervisory authority. |
| **EU representative where the client is outside the EU** (Art 27) | If the client has no EU establishment but is caught by Art 3(2), it must designate a representative in writing, established in a Member State where the affected people are. Publish the representative's identity and contact details in the privacy notice so people and regulators can reach them. Exempt only if processing is occasional, excludes large-scale Art 9 or Art 10 data, and is unlikely to result in a risk. Regular analytics on EU visitors is not "occasional". The representative cannot be the same person as an external DPO. A UK-facing client outside the UK needs a UK representative under the equivalent UK GDPR provision. |
| **Transfer mechanism for data leaving the EEA** (Chapter V) | Every vendor hosting or receiving EU personal data outside the EEA needs one of: an adequacy decision (Art 45), Standard Contractual Clauses (Commission Implementing Decision (EU) 2021/914 of 4 June 2021) with a transfer impact assessment, Binding Corporate Rules, or an Art 49 derogation (narrow, not a routine solution). For US vendors, check whether the entity is on the Data Privacy Framework list; if it is, and the certification covers the relevant data type, no SCCs are needed for that transfer. See Notes on DPF risk. |
| **72-hour breach notification** (Arts 33-34) | The controller notifies the competent supervisory authority without undue delay and where feasible within 72 hours of becoming aware of a personal data breach, unless the breach is unlikely to result in a risk. Late notification must carry reasons for the delay. If the breach is likely to result in a high risk to individuals, they must be told without undue delay too (Art 34). Art 33(5) requires an internal register of all breaches whether or not they were notified. Deliverable: a one-page incident runbook naming who calls it, which authority is notified, and where the register lives. |
| **UK: a complaints process** (DPA 2018 s.164A, from DUAA s.103) | In force 19 June 2026. Every UK controller, regardless of size, must operate a route for data subjects to complain about UK GDPR infringements, including an electronic form, must acknowledge a complaint within 30 days, investigate without undue delay, and respond with an outcome. Build: a complaint form distinct from the general contact form, plus a line in the privacy notice pointing at it and at the ICO. |
| **UK: automated decision-making** (UK GDPR Arts 22A-22D, from DUAA s.80) | In force 5 February 2026. For significant automated decisions not involving special category data, the UK flipped the default from prohibited to permitted with safeguards. The Art 22C safeguards must still be built: tell the person the decision was made, let them make representations, give genuine human review by someone with authority and discretion to change the outcome, and let them contest it. Special category data still requires explicit consent or legal authorisation (Art 22B). The EU has not made this change, so a site serving both must satisfy the stricter EU Art 22. |

---

## How to verify

Run these before delivery, on the deployed URL, not on localhost.

1. **Pre-consent network check.** Open the site in a clean profile with devtools Network open, filter to `Fetch/XHR` and `JS`, hard-reload, and touch nothing. Any request to `connect.facebook.net`, `googletagmanager.com` firing a tag, `google-analytics.com`, `analytics.tiktok.com`, `clarity.ms`, `hotjar.com`, `doubleclick.net`, or any ad domain, before you click accept, is a failure. Note that loading GTM itself is arguably permissible if it fires nothing; the tags it fires are the problem, so check what actually goes out.
2. **Cookie check pre-consent.** Application panel, Storage, Cookies. Also check `localStorage`. Anything beyond a session cookie, a CSRF token, a load-balancer cookie, or the consent-state cookie itself is a failure. `_ga`, `_fbp`, `_gcl_au`, `_ttp` present before consent is a failure.
3. **Reject symmetry.** On first load, is there a reject control at the same level as accept, in the same visual weight, reachable in the same number of clicks? If "reject" is a text link and "accept" is a filled button, that is not freely given consent under Art 4(11).
4. **Withdrawal path.** Find the control that re-opens consent settings after the banner is dismissed. It must exist and be reachable from every page (usually a footer link). Withdraw consent, reload, and re-run check 1. Tags must stay silent.
5. **Consent log.** Accept a specific subset of purposes, then look at the stored record server-side. Confirm it captured timestamp, per-purpose choices, and notice version. If consent lives only in a browser cookie, the client cannot demonstrate consent to a regulator.
6. **Privacy notice completeness.** Grep the page for each Art 13 element. Fastest failures to spot: no retention period, no mention of international transfers, no list of third-party recipients, no supervisory-authority complaint right. Then check the reverse direction: every domain that appeared in check 1 must correspond to a named recipient in the notice.
7. **Form-level linkage.** Every form that collects personal data has a visible privacy notice link adjacent to the submit control, and any consent checkbox is unticked by default. Grep templates for `checked` on consent inputs.
8. **Vendor inventory versus DPAs.** List every third-party domain the site talks to (devtools, or `grep -rIn "https\?://" src/` for hardcoded endpoints). For each, confirm a signed DPA and a documented transfer mechanism. An entry with no DPA is a delivery blocker.
9. **DPF status check for US vendors.** Look each US vendor up on the Data Privacy Framework list and confirm it is "Active", that the certification covers the EU-U.S. DPF (and the UK Extension separately if UK data is in play), and that the covered data types match what you are sending. A lapsed or non-recertified listing means the transfer has no cover.
10. **UK complaints route.** If UK visitors are in scope, confirm the complaints form exists, is electronic, is distinct from the contact form, and that the acknowledgement path can meet 30 days.
11. **DSAR dry run.** Submit a request through the published channel and confirm it reaches a monitored human. An unmonitored `privacy@` alias is a common silent failure.

---

## Penalties

**EU.** Two tiers, both "whichever is higher", calculated on total worldwide annual turnover of the preceding financial year:

- Article 83(4): up to EUR 10,000,000 or 2% of turnover. Covers controller and processor obligations including Art 25 (by design), Art 27 (representative), Art 28 (processor contracts), Art 30 (records), Art 32 (security), Arts 33-34 (breach notification), Art 35 (DPIA), Art 37 (DPO).
- Article 83(5): up to EUR 20,000,000 or 4% of turnover. Covers the basic principles (Arts 5, 6, 7, 9), data subject rights (Arts 12-22), and transfers to third countries (Arts 44-49).

Article 82 gives individuals a separate right to compensation for material or non-material damage, which is a live litigation route in Germany, Austria, and the Netherlands independently of any regulator action.

**Reference points from actual enforcement**

- EUR 1.2 billion, Meta Platforms Ireland, Irish DPC, May 2023, for unlawful EU-US transfers. Largest to date. Under appeal.
- EUR 530 million, TikTok, Irish DPC, May 2025, for unlawful EU-China transfers. Under appeal. UNVERIFIED: the reported Irish High Court stay in November 2025 could not be confirmed against a court or DPC source on 2026-07-20.

**UK.** Under DPA 2018 as amended, the ICO's two tiers are the standard maximum of GBP 8,700,000 or 2% of total worldwide turnover, and the higher maximum of GBP 17,500,000 or 4%, in each case whichever is higher.

**UK PECR fines rose sharply.** DUAA 2025 lifted the PECR ceiling from GBP 500,000 to the UK GDPR levels (GBP 17,500,000 or 4%), effective with the main commencement on 5 February 2026. This matters because the ICO issues more penalties under PECR (cookies and direct marketing) than under UK GDPR. A non-compliant cookie banner on a UK-facing site now sits in a materially higher exposure band than it did in 2025.

---

## Common ways sites fail this

- Tags fire on page load and the banner is decorative. The single most common failure, and the easiest for a regulator or a complainant to reproduce.
- "Accept" is a button, "Reject" is a grey text link, or reject is buried one level down in "Manage preferences". Invalidates the consent.
- Consent stored only client-side, so the client cannot produce a record when asked.
- The privacy policy is a template that describes services the site does not use, and omits the three vendors it does use. A dated, published misrepresentation is worse than no policy.
- No retention periods stated, or "we keep data as long as necessary" with no criteria.
- A US client with a EUR price toggle, EU shipping in the checkout dropdown, and a Meta Pixel, treated as out of scope because "we're a US company".
- No Article 27 EU representative named, on a site that clearly targets EU customers. Cheap to fix, visible on the face of the privacy notice, and therefore easy for a regulator to spot.
- No DPA with the form handler or the email marketing tool.
- Contact form data flowing to a US CRM with no transfer mechanism documented.
- Nobody owns the one-month DSAR clock after handover, so the first request is missed.
- Treating UK and EU as one regime after 5 February 2026. They have diverged on automated decisions, DSAR search scope, legitimate interests, and complaints handling.
- Session recording or heatmap tools capturing form fields, which pulls in whatever the user typed before submitting.

---

## Sources

Official sources first. All retrieved 2026-07-20.

- [Regulation (EU) 2016/679 (GDPR), consolidated text, EUR-Lex](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng) - retrieved 2026-07-20. Articles 3, 6, 7, 12, 13, 27, 28, 30, 32, 33, 34, 35, 37, 82, 83, 99.
- [EDPB Guidelines 3/2018 on the territorial scope of the GDPR (Article 3), version 2.1, adopted 12 November 2019 (PDF)](https://www.edpb.europa.eu/sites/default/files/files/file1/edpb_guidelines_3_2018_territorial_scope_after_public_consultation_en_1.pdf) - retrieved 2026-07-20. Source for the targeting factor list, the monitoring activity list, the "mere accessibility is not enough" position, and the Article 27 representative guidance.
- [EDPB Guidelines 3/2018 landing page](https://www.edpb.europa.eu/our-work-tools/our-documents/guidelines/guidelines-32018-territorial-scope-gdpr-article-3-version_en) - retrieved 2026-07-20.
- [Article 27 GDPR text, gdpr-info.eu](https://gdpr-info.eu/art-27-gdpr/) - retrieved 2026-07-20. Unofficial mirror of the official text, used for the Art 27(2) exemption wording.
- [European Commission, Standard Contractual Clauses (SCC)](https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/standard-contractual-clauses-scc_en) - retrieved 2026-07-20. Implementing Decision (EU) 2021/914 of 4 June 2021.
- [European Commission, Adequacy decisions](https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/adequacy-decisions_en) - retrieved 2026-07-20.
- [European Commission press release: Commission renews decisions to allow for the free and safe flow of personal data with the UK (IP/25/3059)](https://ec.europa.eu/commission/presscorner/detail/en/ip_25_3059) - retrieved 2026-07-20. See caveat in Notes: this page did not render on retrieval and the dates were confirmed from the Hunton summary below.
- [Hunton, European Commission Renews UK Data Adequacy Decisions](https://www.hunton.com/privacy-and-information-security-law/european-commission-renews-uk-data-adequacy-decisions) - retrieved 2026-07-20. Renewal 19 December 2025, expiry 27 December 2031, mid-point review after four years.
- [U.S. Department of Commerce, Data Privacy Framework Program Overview](https://www.dataprivacyframework.gov/Program-Overview) - retrieved 2026-07-20.
- [Data Privacy Framework: How to re-certify](https://www.dataprivacyframework.gov/program-articles/How-to-Re-certify-under-the-Data-Privacy-Framework-(DPF)-Program) - retrieved 2026-07-20. Annual recertification requirement; removal from the list on failure to recertify.
- [FTC, Data Privacy Framework](https://www.ftc.gov/business-guidance/privacy-security/data-privacy-framework) - retrieved 2026-07-20.
- [Trump v. Slaughter, No. 25-332, U.S. Supreme Court, decided 29 June 2026 (PDF)](https://www.supremecourt.gov/opinions/25pdf/25-332_qn12.pdf) - retrieved 2026-07-20. Overrules Humphrey's Executor; holds FTC for-cause removal protections unconstitutional.
- [SCOTUSblog: Court allows Trump to fire FTC commissioner](https://www.scotusblog.com/2026/06/court-allows-trump-to-fire-ftc-commissioner-and-overturns-major-restraint-on-presidential-power/) - retrieved 2026-07-20.
- [GOV.UK, Data (Use and Access) Act 2025: plans for commencement](https://www.gov.uk/guidance/data-use-and-access-act-2025-plans-for-commencement) - retrieved 2026-07-20. Stage 3, Commencement No. 6 Regulations, 5 February 2026; s.103 complaints excluded from that stage.
- [ICO, The maximum amount of a fine under UK GDPR and DPA 2018](https://ico.org.uk/about-the-ico/our-information/policies-and-procedures/data-protection-fining-guidance/statutory-background/the-maximum-amount-of-a-fine-under-uk-gdpr-and-dpa-2018/) - retrieved 2026-07-20. GBP 8.7m / 2% and GBP 17.5m / 4%.
- [ICO, How does the UK Extension to the EU-US Data Privacy Framework work?](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/international-transfers/adequacy-regulations/how-does-the-uk-extension-to-the-eu-us-data-privacy-framework-work/) - retrieved 2026-07-20. UK-US Data Bridge, SI 2023/1028, in force 12 October 2023.
- [ICO, The Data (Use and Access) Act 2025: what does it mean for organisations?](https://ico.org.uk/about-the-ico/what-we-do/legislation-we-cover/data-use-and-access-act-2025/the-data-use-and-access-act-2025-what-does-it-mean-for-organisations/) - retrieved 2026-07-20. Returned HTTP 403 to automated retrieval on this date; open manually before relying on it.
- [DLA Piper Privacy Matters, New complaints handling rules under DUAA take effect on 19 June 2026](https://privacymatters.dlapiper.com/2026/06/uk-new-complaints-handling-rules-under-duaa-take-effect-on-19-june-2026-are-you-ready/) - retrieved 2026-07-20. 30-day acknowledgement, electronic complaint route, applies to all controllers.
- [Travers Smith, UK's data protection reforms take effect: a new era for automated decision-making](https://www.traverssmith.com/knowledge/knowledge-container/uks-data-protection-reforms-take-effect-a-new-era-for-automated-decision-making/) - retrieved 2026-07-20. DUAA s.80, UK GDPR Arts 22A-22D, in force 5 February 2026.
- [Mayer Brown, The Data Use and Access Act: PECR reform](https://www.mayerbrown.com/en/insights/publications/2025/06/the-data-use-and-access-act-pecr-reform-rules-relating-to-electronic-marketing-and-cookies-in-the-uk) - retrieved 2026-07-20. PECR ceiling raised from GBP 500,000 to UK GDPR levels.
- [European Parliament Legislative Train, Digital Omnibus package](https://www.europarl.europa.eu/legislative-train/theme-a-new-plan-for-europe-s-sustainable-prosperity-and-competitiveness/file-digital-package) - retrieved 2026-07-20. Status of the proposed GDPR amendments. Tabled 19 November 2025; still recorded as "tabled" on 20 June 2026.
- [European Parliament Legislative Train, Digital Omnibus on AI](https://www.europarl.europa.eu/legislative-train/theme-a-europe-fit-for-the-digital-age/file-digital-omnibus-on-ai) - retrieved 2026-07-20. Council general approach 13 March 2026, trilogue agreement 7 May 2026, Parliament plenary approval 16 June 2026, status "close to adoption" on 20 June 2026.
- [Judgment of 3 September 2025, Latombe v Commission, T-553/23, EUR-Lex CELEX 62023TJ0553](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A62023TJ0553) - retrieved 2026-07-20. General Court, Tenth Chamber (Extended Composition), action dismissed as unfounded; challenge to Implementing Decision (EU) 2023/1795.
- [Appeal brought on 31 October 2025 by Philippe Latombe, C-703/25 P, EUR-Lex CELEX 62025CN0703](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A62025CN0703) - retrieved 2026-07-20. Confirms the appeal case number and lodging date; does not show a disposal.
- [Commission Implementing Decision (EU) 2023/1795 of 10 July 2023 (EU-US Data Privacy Framework adequacy)](https://eur-lex.europa.eu/eli/dec_impl/2023/1795/oj) - retrieved 2026-07-20. Listed as in force on the Commission adequacy decisions page.
- [Data (Use and Access) Act 2025, section 80, legislation.gov.uk](https://www.legislation.gov.uk/ukpga/2025/18/section/80) - retrieved 2026-07-20. Heading "Automated decision-making"; inserts UK GDPR Arts 22A-22D.
- [EDPB, EU-US Data Privacy Framework FAQ for European individuals, version 2.0](https://www.edpb.europa.eu/documents/other-guidance/eu-us-data-privacy-framework-faq-for-european-individuals-version-20_en) - retrieved 2026-07-20.

---

## Notes

**The Data Privacy Framework is in force but its footing weakened in June 2026.** Commission Implementing Decision (EU) 2023/1795 of 10 July 2023 remains valid and DPF-certified transfers are lawful today. Two things bear watching:

1. Philippe Latombe's challenge (Case T-553/23) was dismissed by the General Court on 3 September 2025. He appealed to the CJEU on 31 October 2025 (Case C-703/25 P). UNVERIFIED: whether that appeal has been decided or withdrawn since; it was reported as pending as of May 2026 and I could not confirm its status as of 2026-07-20.
2. On 29 June 2026 the US Supreme Court decided *Trump v. Slaughter*, holding 6-3 that statutory for-cause removal protections for FTC Commissioners violate the separation of powers, and overruling *Humphrey's Executor*. The Commission's adequacy finding described the FTC as an independent enforcement authority and cited those removal protections. The link between that ruling and DPF validity is currently commentary rather than any decision by an EU institution, and no EU body has suspended or repealed the adequacy decision on this basis. Treat it as a risk to plan for, not a change in the law.

**Practical consequence for the studio.** For any new build sending EU personal data to a US vendor, prefer a vendor that can also sign the 2021 SCCs, or pick an EU-hosted alternative, so that a future annulment does not strand the client with no transfer mechanism. Note the vendor's DPF listing status and the fallback in `BRIEF.md`. If Schrems III lands, the fallback is already contracted rather than a scramble.

**SCCs for importers already subject to GDPR do not exist yet.** Where a non-EU recipient is itself directly caught by Art 3(2), the existing 2021 SCCs are not designed for that scenario. The Commission has been developing an additional set since 2024. UNVERIFIED as of 2026-07-20: no adoption confirmed; reporting in May 2026 said they had not been adopted. Check the Commission SCC page before assuming a mechanism exists for this case.

**The EU Data Omnibus would change GDPR itself and is unresolved.** The Commission tabled the Digital Omnibus on 19 November 2025 as two separate proposals: a Digital Omnibus on AI, and a Digital Omnibus Regulation carrying the GDPR and ePrivacy changes. The AI file moved fast: Council general approach 13 March 2026, trilogue agreement 7 May 2026, European Parliament plenary approval 16 June 2026 (423 for, 57 against, 174 abstentions), and the Parliament's own legislative tracker recorded it as "close to adoption" on 20 June 2026. UNVERIFIED: this file previously stated that the Council gave the AI Omnibus final adoption on 29 June 2026; that step is consistent with the timeline but could not be confirmed against a Council source on 2026-07-20. The data file is the one that matters here, and it was still recorded as merely "tabled" on 20 June 2026, meaning it is still in Council negotiation. Reporting says the provisions that would have moved cookie consent into GDPR and mandated single-click rejection were dropped from the Council's negotiating text after member states failed to agree, and may or may not return. Adoption is not expected before late 2026 at the earliest. Nothing in this file changes until it is adopted and published in the Official Journal. Re-read this file when it is.

**UK adequacy is secure until 2031 but conditional.** The Commission renewed both UK adequacy decisions on 19 December 2025 for six years, expiring 27 December 2031, with a mid-point review after four years. The renewal was explicitly held back until the Commission could see the effect of DUAA. Further UK divergence is the thing that would put it at risk, so track DUAA stages 4 and beyond.

**Do not treat UK and EU as interchangeable from 5 February 2026 onward.** Concrete divergences already live: recognised legitimate interests as a new UK lawful basis with no EU equivalent; a statutory "reasonable and proportionate" limit on DSAR searches plus a codified stop-the-clock while clarification is awaited; automated decision-making flipped to permitted-with-safeguards for non-special-category data; a statutory complaints duty on controllers from 19 June 2026 with no EU counterpart. A site serving both audiences must be built to the stricter standard on each axis, which is usually the EU one, except for complaints handling where the UK is stricter.

**Conflicts with other files in this library.** The cookie banner itself is governed by [`eprivacy-cookies.md`](eprivacy-cookies.md), not by GDPR; GDPR supplies the consent quality standard those banners must meet. Breach timing interacts with [`data-breach-notification.md`](data-breach-notification.md), where US state clocks run on different triggers and different deadlines than the GDPR 72 hours. Where a site is caught by both GDPR and [`ccpa-cpra.md`](ccpa-cpra.md), the opt-in default of GDPR and the opt-out default of California pull in opposite directions; building to GDPR opt-in satisfies both, and the reverse is not true. For anything involving health, financial, or children's data, this file is not sufficient and the answer is the client's counsel.

**Staleness watch.** The two items in this file most likely to be wrong first are the DPF status and the Data Omnibus status. Re-check both before any EU-facing build, regardless of the `Last reviewed` date above.
