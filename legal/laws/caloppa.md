# CalOPPA: California Online Privacy Protection Act (Business and Professions Code sections 22575-22579)

| Field | Value |
|---|---|
| **Jurisdiction** | California, USA. Reaches any operator anywhere in the world that collects personally identifiable information online from a consumer residing in California. There is no California-nexus test for the business itself. |
| **Regulator / enforcer** | California Attorney General, plus district attorneys and certain city attorneys, acting through the Unfair Competition Law (Bus. & Prof. Code section 17200 et seq.). Chapter 22 contains no enforcement or penalty clause of its own. The California Privacy Protection Agency (CPPA) does **not** enforce CalOPPA: its jurisdiction is the CCPA. |
| **In force since** | July 1, 2004. Section 22579 reads: "This chapter shall become operative on July 1, 2004." |
| **Last amended** | AB 370, Stats. 2013, Ch. 390, chaptered September 27, 2013, effective January 1, 2014. It amended section 22575 only, adding the Do Not Track disclosure at (b)(5), the third-party tracking disclosure at (b)(6), and the hyperlink alternative at (b)(7). No later amendment to sections 22575-22579 was located as of the review date. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. Not repealed, not superseded, and not folded into the CCPA. See "Notes" for how the two stack. |

## Applies when

Answer these at intake. All four in the first group must be true for the site to be in scope.

**Scope triggers**

- [ ] The client **owns** a website or online service. Section 22577(c) defines "operator" as a person or entity that owns the site or service, and expressly excludes "any third party that operates, hosts, or manages, but does not own, a Web site or online service on the owner's behalf or by processing information on behalf of the owner." The studio building the site is not the operator. The client is. Put the obligation in the client's name in `BRIEF.md`.
- [ ] The site or service is **operated for commercial purposes**. A purely personal blog, a hobby project with nothing for sale and no commercial intent, and a non-commercial community page are outside the statute. Anything selling, lead-generating, advertising, or supporting a business is inside it.
- [ ] The site **collects and maintains** personally identifiable information, as CalOPPA defines it (see below). "Maintains" matters: section 22577(a) covers information "maintained by the operator in an accessible form." Data collected and immediately discarded is a weaker case, but do not build a compliance position on that.
- [ ] At least one visitor is a **consumer residing in California**. In practice, assume yes for any publicly reachable site. Section 22577(d) defines "consumer" as "any individual who seeks or acquires, by purchase or lease, any goods, services, money, or credit for personal, family, or household purposes." The "by purchase or lease" qualifier is in the statute; do not drop it when paraphrasing.

**What counts as personally identifiable information (section 22577(a))**

CalOPPA's PII list is narrower and more concrete than the CCPA's "personal information." It covers individually identifiable information collected online by the operator from that individual and maintained in an accessible form, specifically:

- [ ] First and last name
- [ ] Home or other physical address, including street name and name of a city or town
- [ ] Email address
- [ ] Telephone number
- [ ] Social security number
- [ ] Any other identifier that permits the physical or online contacting of a specific individual
- [ ] Information concerning a user that the site or service collects online from the user and maintains in personally identifiable form in combination with any of the identifiers above

A contact form with name and email trips this on its own. A site that only runs analytics, with no form and no account, has a weaker fit against the closed list, but any newsletter signup, checkout, login, quote request, chat widget, or booking flow puts the site clearly in scope. Build for scope by default.

**Who is NOT caught**

- Hosts, agencies, and processors that do not own the site (section 22577(c)).
- Non-commercial sites.
- Sites that collect nothing that fits section 22577(a).
- **No revenue threshold. No employee count. No record count. No visitor count.** This is the important difference from the CCPA. A one-person consultancy with a contact form and forty visitors a month owes a CalOPPA-compliant privacy policy, and owes nothing under the CCPA.

**Sector carve-out worth knowing**

- Airlines. In *People ex rel. Harris v. Delta Air Lines, Inc.* (Cal. Ct. App., 1st Dist., No. A139238, decided May 25, 2016), the Court of Appeal held that the federal Airline Deregulation Act preempts state enforcement of CalOPPA against an air carrier, in that case over the Fly Delta mobile app. If the client is an air carrier, get counsel. Do not extend that holding to any other industry.

**Mobile apps**

The Attorney General's position is that "online service" in section 22575 includes mobile apps, which is why the 2012 notice letters and the Delta action targeted apps. The Delta dismissal turned on airline preemption, not on apps being outside CalOPPA. Treat a client's app as in scope.

## What the site must have

| Requirement | What that means in the build |
|---|---|
| **A privacy policy page** | One reachable URL, e.g. `/privacy`. Must be real HTML that loads without JavaScript and without a consent banner having been dismissed. Server-render it or pre-render it. Direct-load the route and confirm it is not a client-side-only path that 404s on refresh. |
| **Conspicuous posting on the homepage** | Section 22575(a) requires the operator to "conspicuously post its privacy policy." Section 22577(b) defines conspicuous posting as any one of: the actual policy on the homepage or first significant page after entry; an icon linking to it that **contains the word "privacy"** and uses a contrasting or otherwise distinguishable color; a text link (see next row); any other functional hyperlink "so displayed that a reasonable person would notice it"; or, for an online service, any other reasonably accessible means. |
| **The word "Privacy" in the link** | For the text-link route, section 22577(b)(3) is satisfied if the link does **one** of three things: (A) includes the word "privacy"; (B) is in capital letters equal to or larger than surrounding text; or (C) is in larger, contrasting, or set-off type. So the literal word is not the only lawful path, but it is the only one that does not depend on a judgment call about type treatment. **Ship the word.** Label the link `Privacy Policy` or `Privacy`. Do not bury it inside a `Legal` or `Terms` link, and do not label it `Your Data`, `Trust Center`, or an icon with no text. |
| **Link placement** | On the homepage **or the first significant page after entering the site**. Global footer is the normal answer, and it covers splash pages, age gates, campaign landing pages, and any alternate entry point. If a paid-ad landing page has a stripped footer, it still needs the link. |
| **Categories of PII collected** (22575(b)(1)) | List the actual categories the build collects. Walk the forms and the data model, not a template. |
| **Categories of third parties shared with** (22575(b)(1)) | List the categories of third-party persons or entities with whom the operator may share that PII. Enumerate from the real integrations: email service provider, CRM, payment processor, analytics, ad platforms, hosting, support chat. |
| **Review and change process** (22575(b)(2)) | Conditional. Required only "if the operator maintains a process for an individual consumer" to review and request changes to their PII. If the build has an account settings page, describe it and link to it. If there is no such process, this paragraph imposes nothing. Do not invent a process in the copy that the build does not have. |
| **Material change notification process** (22575(b)(3)) | Describe how users will be told when the policy materially changes: email to account holders, a site banner, a changelog on the policy page. Then build whatever you described. |
| **Effective date** (22575(b)(4)) | The policy must "identify its effective date." Put a visible dated line at the top of the policy page, e.g. `Effective date: 2026-07-20`. This is the single most commonly missing item and the cheapest to fix. |
| **Do Not Track disclosure** (22575(b)(5)) | Disclose how the site responds to browser "do not track" signals or other mechanisms that let a consumer exercise choice over collection of PII about their online activities over time and across third-party sites. **The statute requires disclosure, not compliance.** Saying "we do not respond to Do Not Track signals" is lawful. Saying "we honor Do Not Track" when the build ignores the header is a section 22576 violation of the operator's own posted policy. The AG's 2014 guide recommends a conspicuously labelled section and suggests headings such as "How We Respond to Do Not Track Signals," "Online Tracking," or "California Do Not Track Disclosures." Use one of those as an `<h2>` so it is findable. |
| **Do Not Track hyperlink alternative** (22575(b)(7)) | Instead of describing its own response, an operator may satisfy (b)(5) with "a clear and conspicuous hyperlink" in the policy to an online location describing a program or protocol the operator follows that offers the consumer choice, including the effects of that program. The AG's guide prefers the direct description. Prefer the direct description. If a link is used, the destination must state what the program does and how to exercise the choice. |
| **Third-party cross-site tracking disclosure** (22575(b)(6)) | Disclose whether other parties may collect PII about a consumer's online activities over time and across different websites when the consumer uses this site. If the build ships Google Analytics, a Meta Pixel, LinkedIn Insight, a chat widget, an embedded YouTube player, or any ad tag, the answer is yes and the policy must say so. |
| **Consent UI** | **Not required by CalOPPA.** CalOPPA is a disclosure statute. It mandates no cookie banner, no opt-in, no consent gate, and no script blocking. If the build has a banner, it is there for the GDPR, the ePrivacy Directive, or the CCPA opt-out, not for this law. Do not sell a client a banner citing CalOPPA. |
| **Records** | CalOPPA mandates no consent log and sets no retention period. Practice recommendation, not a statutory duty: keep the policy under version control with dated revisions, because the effective date at (b)(4) and the material-change process at (b)(3) both become provable only if the history exists. |

## How to verify

Run all of these against the built site before delivery, on the production or staging URL, not against local source only.

1. **Homepage link exists and reads right.** Load the homepage. Confirm a visible link whose text contains "Privacy". In DevTools console: `[...document.querySelectorAll('a')].filter(a => /privacy/i.test(a.textContent)).map(a => [a.textContent.trim(), a.href])`. Expect at least one result. Empty result is a fail.
2. **Link survives JavaScript being off.** Disable JS in DevTools (Command Menu, "Disable JavaScript"), hard-reload, confirm the link is still in the rendered footer. A link injected by a consent-management script disappears when that script is blocked by an ad blocker, which is a large fraction of California traffic.
3. **Every entry point has it.** Check the homepage, any splash or age gate, and every paid-ad landing page. Grep the build output for footer inclusion: `rg -l "Privacy" --glob "*.html"` and compare the count against the total page count. Any page template with a stripped footer is a gap.
4. **Policy URL direct-loads.** Open `/privacy` in a fresh incognito tab by typing the URL, not by clicking. Confirm HTTP 200 and rendered content. In the Network panel confirm the document response itself contains the policy text (check the Response tab, not the Elements panel, which shows post-JS DOM).
5. **Effective date is visible.** Ctrl-F the rendered policy for "Effective" or a date. Must be present and must not be a placeholder year.
6. **Do Not Track section is present.** Ctrl-F the policy for "Do Not Track". Must return a heading-level section, not a passing mention.
7. **Third-party tracking sentence is present and true.** Ctrl-F for "third part". Then open the Network panel, reload with cache disabled, sort by Domain, and list every request going to a host other than the site's own. Compare that list against what the policy claims. If the policy says no third parties collect information and `google-analytics.com`, `googletagmanager.com`, `connect.facebook.net`, or `snap.licdn.com` appear in the request list, the policy is false and the site is exposed under section 22576.
8. **DNT claim matches behavior.** If the policy claims the site honors DNT, verify it. In DevTools Network conditions or via an extension, send `DNT: 1`. Reload. Confirm the tracking requests identified in step 7 no longer fire. If they still fire, either fix the build or change the copy. A "we honor DNT" sentence over a build that ignores it is worse than saying nothing.
9. **Category lists match reality.** Open every form on the site. List every field name. Confirm each field's data category appears in the policy's collection list. Then list every outbound integration from the environment config and confirm each has a matching third-party category in the policy.
10. **Policy is not boilerplate.** Read it end to end for statements the build cannot support: references to a mobile app that does not exist, an account portal that does not exist, a physical retail location, or cookie categories the site does not set.

## Penalties

CalOPPA itself sets no fine. Sections 22575-22579 contain no penalty provision. Exposure comes from two places.

- **Unfair Competition Law civil penalty.** A CalOPPA violation is an unlawful business act actionable under Bus. & Prof. Code section 17200. Section 17206(a) provides a civil penalty "not to exceed two thousand five hundred dollars ($2,500) for each violation," recoverable in an action brought by the Attorney General, a district attorney, a county counsel as authorized, a city attorney of a city over 750,000 population, or certain city prosecutors. Section 17203 separately allows injunctive relief and restitution. Section 17206(b) directs courts to weigh the nature and seriousness of the conduct, the number of violations, persistence, duration, willfulness, and the defendant's net worth.
- **UNVERIFIED: how "each violation" is counted online.** The AG has argued in filings that each affected user or each download constitutes a separate violation, which is what makes the $2,500 figure meaningful at scale. No controlling California appellate decision fixing the per-violation unit for a CalOPPA-predicate UCL claim was located during this review. Do not quote a total exposure figure to a client.

**Two statutory limits that materially reduce real-world risk:**

- **The 30-day cure, precisely stated.** Section 22575(a) provides: "An operator shall be in violation of this subdivision only if the operator fails to post its policy within 30 days after being notified of noncompliance." Read the words. The cure window attaches to **subdivision (a)**, the duty to conspicuously post a policy. By its terms it does not extend to defective policy **content** under subdivision (b), and it does not extend to violating the operator's own posted policy. Practitioner summaries routinely describe CalOPPA as having "a 30-day cure period" without that limitation. Do not rely on the broad version. The AG used this mechanism in its 2012 round of notice letters to app developers.
- **The fault standard.** Section 22576 makes an operator liable only if it fails to comply with section 22575, or with its own posted policy, either "knowingly and willfully" or "negligently and materially." A minor omission promptly fixed is a poor enforcement target. A policy that affirmatively misdescribes the site's data flows is the opposite.

**No private right of action under CalOPPA.** The chapter creates none. Private plaintiffs have attempted CalOPPA-predicate UCL claims, but Proposition 64 standing under section 17204 requires the plaintiff to have "suffered injury in fact and lost money or property," which is hard to establish from a missing privacy link alone. The realistic enforcer is the Attorney General.

## Common ways sites fail this

- No effective date on the policy page. The most frequent single defect, and a one-line fix.
- No Do Not Track section at all. Extremely common on policies drafted after 2020, because CCPA-oriented templates cover the "Do Not Sell or Share" link and skip the older DNT disclosure entirely.
- The footer link is labelled `Legal` or `Terms`, with privacy reachable only one click deeper. Section 22577(b) wants the link on the homepage or first significant page.
- The policy link is rendered by the cookie-consent script, so it vanishes for anyone running an ad blocker or with JS disabled.
- A single-page app where `/privacy` works when clicked but returns a 404 on direct load or refresh.
- The policy says the site does not use cookies or does not share data, while GA4, a Meta Pixel, and a chat widget are all firing. This is a section 22576 violation of the operator's own posted policy, and it is worse than having no policy, because it is a dated written misstatement.
- The policy claims the site honors Do Not Track because it sounded good in the draft, with nothing in the build reading the header.
- A campaign landing page built outside the main template, with no footer and therefore no privacy link, that is also the first page a large share of visitors ever sees.
- Assuming a CCPA-compliant policy discharges CalOPPA. It usually does not, because it omits the DNT disclosure.
- Copying the client's old policy forward without re-reading it against the new build's integrations.

## Sources

Official sources first. All retrieved 2026-07-20.

- [Cal. Bus. & Prof. Code section 22575 (California Legislative Information)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=BPC&sectionNum=22575.) - retrieved 2026-07-20
- [Cal. Bus. & Prof. Code section 22577, definitions including "conspicuously post" (California Legislative Information)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=BPC&sectionNum=22577.) - retrieved 2026-07-20
- [Cal. Bus. & Prof. Code section 17206, UCL civil penalty (California Legislative Information)](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=BPC&sectionNum=17206) - retrieved 2026-07-20
- [AB 370 (2013-2014), bill history and text (California Legislative Information)](https://leginfo.legislature.ca.gov/faces/billNavClient.xhtml?bill_id=201320140AB370) - retrieved 2026-07-20
- [California Attorney General, "Making Your Privacy Practices Public" (May 2014), PDF](https://oag.ca.gov/sites/all/files/agweb/pdfs/cybersecurity/making_your_privacy_practices_public.pdf) - retrieved 2026-07-20
- [California Attorney General, CalOPPA notice letter to app developers (2012), PDF](https://oag.ca.gov/system/files/attachments/press_releases/CalOPPA%20Letter_0.pdf) - retrieved 2026-07-20
- [California Attorney General, Global Privacy Control guidance page](https://oag.ca.gov/privacy/ccpa/gpc) - retrieved 2026-07-20
- [California Privacy Protection Agency, updated CCPA monetary thresholds](https://cppa.ca.gov/regulations/cpi_adjustment.html) - retrieved 2026-07-20
- [Cal. Code Regs. tit. 11, section 7025, opt-out preference signals (Cornell LII)](https://www.law.cornell.edu/regulations/california/11-CCR-7025) - retrieved 2026-07-20. Note: this LII copy carries the version filed March 29, 2023 and does not reflect the regulations effective January 1, 2026. For current text use the CPPA regulations page.
- [California Privacy Protection Agency, regulations index, including the package listed as "CCPA Regulations (Effective January 1, 2026)"](https://cppa.ca.gov/regulations/) - retrieved 2026-07-20
- [Cal. Bus. & Prof. Code section 22576 (FindLaw)](https://codes.findlaw.com/ca/business-and-professions-code/bpc-sect-22576/) - retrieved 2026-07-20
- [Cal. Bus. & Prof. Code section 22578, local preemption (FindLaw)](https://codes.findlaw.com/ca/business-and-professions-code/bpc-sect-22578/) - retrieved 2026-07-20
- [Cal. Bus. & Prof. Code section 22579, operative date (FindLaw)](https://codes.findlaw.com/ca/business-and-professions-code/bpc-sect-22579/) - retrieved 2026-07-20
- [People ex rel. Harris v. Delta Air Lines, Inc., No. A139238 (Cal. Ct. App. May 25, 2016) (FindLaw caselaw)](https://caselaw.findlaw.com/court/ca-court-of-appeal/1736333.html) - retrieved 2026-07-20
- [Loeb & Loeb, analysis of the AG's Do Not Track guidance (June 2014)](https://www.loeb.com/en/insights/publications/2014/06/california-attorney-general-provides-guidance-fo__) - retrieved 2026-07-20
- [Hunton, summary of the AG's CalOPPA guidance (May 21, 2014)](https://www.hunton.com/privacy-and-cybersecurity-law-blog/2014/05/21/california-attorney-general-releases-guidance-recent-changes-caloppa/) - retrieved 2026-07-20

## Notes

**CalOPPA and the CCPA coexist. The CCPA did not replace it.**

They are different instruments with different reach, and the practical consequence for this studio is that CalOPPA catches almost every client while the CCPA catches few of them.

| | CalOPPA | CCPA / CPRA |
|---|---|---|
| Threshold | None. Any commercial operator collecting PII from a California resident. | Applies only above a threshold. As of January 1, 2025 the annual gross revenue threshold is **$26,625,000**, adjusted for CPI in odd-numbered years (source: CPPA). Other threshold prongs are covered in `ccpa-cpra.md`. |
| What it demands | Disclosure in a posted policy. | Disclosure plus substantive consumer rights (access, deletion, correction, opt-out of sale and sharing) plus signal handling. |
| Do Not Track | Must **disclose** the response. Honoring is optional. | Different mechanism. Cal. Code Regs. tit. 11 section 7025 requires covered businesses to **honor** opt-out preference signals such as Global Privacy Control, treating a valid signal as an opt-out of sale/sharing. |
| Enforcer | Attorney General via the UCL. | Attorney General and the CPPA. |

Do not conflate DNT with GPC in policy copy. DNT is a legacy browser header that the site must describe. GPC is a signal that a CCPA-covered business must obey. A policy that answers only one of them, for a client covered by both laws, is incomplete. Route CCPA questions to `ccpa-cpra.md`.

**A small client is the interesting case.** A ten-person California business is almost certainly below every CCPA threshold and is unambiguously inside CalOPPA. That client still needs a conspicuously linked, dated policy with a DNT section. This is the most common gap the studio will encounter, and it is the cheapest to close.

**Local ordinances are preempted.** Section 22578 declares website privacy policy posting a matter of statewide concern and preempts city, county, and local agency rules on the subject. No need to research municipal requirements for this specific duty.

**Watch items:**

- The revised CCPA regulations took effect January 1, 2026. Practitioner commentary reports that amended section 7025 adds a duty to show the consumer on the site that an opt-out preference signal was received and processed. **UNVERIFIED against the final adopted regulation text as of 2026-07-20.** Confirm directly against the CPPA regulations page before building UI to satisfy it, and record the outcome in `ccpa-cpra.md` rather than here.
- No CPI adjustment for 2027 had been announced as of the review date. The $26,625,000 figure above is the current one.
- The real litigation pressure in California right now is not CalOPPA enforcement. It is private plaintiff activity over trackers, pixels, and session replay under the California Invasion of Privacy Act and related theories. CalOPPA compliance does not defend against that, but an accurate third-party disclosure written under 22575(b)(6) forces the build team to enumerate every tracker on the site, which is the same inventory that exposure analysis needs. Treat the disclosure exercise as the audit.
- Section 22575 has not been amended since 2013. If the Legislature revisits it (the DNT provision is aging poorly now that most browsers have deprecated the header UI), this file needs a re-review.
