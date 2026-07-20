# CA Eraser Button: California Business and Professions Code sections 22580-22582 (Privacy Rights for California Minors in the Digital World, SB 568)

| Field | Value |
|---|---|
| **Jurisdiction** | California, USA. Reaches any operator worldwide whose site or app is directed to minors residing in California, or that has actual knowledge a California minor is using it. |
| **Regulator / enforcer** | California Attorney General (and district attorneys / certain city attorneys) via the Unfair Competition Law, Bus. & Prof. Code section 17200. Chapter 22.1 contains no enforcement clause of its own. |
| **In force since** | January 1, 2015 (section 22582 sets the operative date; enacted by SB 568, Stats. 2013, Ch. 336) |
| **Last amended** | Section 22580 amended by AB 3067, Stats. 2018, Ch. 347, effective January 1, 2019 (added cannabis and cannabis products to the restricted list). No amendment to section 22581 located since enactment. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. Not enjoined. Separate from the California Age-Appropriate Design Code Act (AB 2273), which is partly enjoined: see the CAADCA section below. |

## Applies when

Answer these at intake. Any single "yes" in the first group pulls the site into scope.

**Scope triggers (section 22581, the eraser button)**

- [ ] The site, web app, online service, or mobile app is **directed to minors**, meaning it was "created for the purpose of reaching an audience that is predominately comprised of minors, and is not intended for a more general audience comprised of adults" (section 22580(e), which supplies the definition used across the chapter). A general-audience site that happens to have some teen users is not "directed to minors."
- [ ] OR the operator has **actual knowledge** that a minor is using the site or app. Actual knowledge, not "should have known." Collecting a birth date, an age gate, a school affiliation field, or a user telling support "I'm 15" can create it.
- [ ] AND the site has **registered users** (accounts). The removal right in section 22581(a) runs only to "a minor who is a registered user." A brochure site with no accounts and no user posting has nothing to erase.
- [ ] AND users can **post** content, where "posted" means content "that can be accessed by a user in addition to the minor who posted" it (section 22581(f)). Comments, reviews, forum threads, profile bios, uploaded photos, public wishlists, gallery submissions, and Q&A all count. A private-only field visible to nobody but the user and staff does not.

**Who counts as a minor**

- [ ] "Minor" means a natural person **under 18 years of age who resides in California** (section 22580(d)). This is under 18, not under 13. COPPA's under-13 rule is a different law with different duties. A site can be fully COPPA-exempt and still owe this.

**Additional trigger for the advertising rules (section 22580)**

- [ ] The site is directed to minors AND carries advertising or promotion of any restricted product (full list under "What the site must have"), OR
- [ ] The operator has actual knowledge a minor is using the site and serves that minor targeted advertising for a restricted product "based upon information specific to that minor" such as profile, activity, address, or location (section 22580(b)), OR
- [ ] The operator knowingly discloses a minor's personal information to a third party for the purpose of marketing restricted products to that minor (section 22580(c)).

**Who is NOT caught**

- Operators with no registered accounts and no user-posted content (for 22581).
- Third parties who merely host or process for the operator: "operator" excludes a third party that operates, hosts, or manages the site on the operator's behalf (section 22580 definitions).
- Sites with no California users at all, since "minor" is limited to California residents. In practice, assume California traffic unless the site is geo-restricted.
- There is **no revenue threshold, no employee count, and no record count**. Unlike the CCPA, a two-person business with a teen forum is in scope.

**Important limit:** section 22581(e) says the law "shall not be construed to require an operator ... to collect age information about users." Do not add an age gate solely to satisfy this statute. Adding one can manufacture the actual knowledge that puts the site in scope.

## What the site must have

| Requirement | What that means in the build |
|---|---|
| Removal mechanism for registered minors (section 22581(a)(1)) | A working control that lets a registered user delete their own posted content, OR a request path (form, email, ticket) that results in removal. Self-serve delete is the cheaper build: it needs no ticket queue and no SLA. Put a delete action on every user-generated object: comment, review, post, upload, profile field. If you use the request model, the request must actually be honored, not just received. |
| Notice that the right exists (section 22581(a)(2)) | A statement in the privacy policy AND somewhere the user will actually see it: account settings page, a line in the posting UI, or the help center. Policy-only is the common shortcut and is weaker, since the statute requires notice "to a minor who is a registered user," not burial in a document. |
| Clear instructions (section 22581(a)(3)) | Step-by-step wording of how to remove: where to click, or exactly what to send and to what address. "Contact us" is not instructions. Give the literal path: "Settings > My Posts > Delete", or "email privacy@example.com with the URL of the post." |
| Notice that removal is not complete (section 22581(a)(4)) | A plain sentence next to the removal control and in the policy: "Removing your post hides it from other users and the public. It may remain on our servers, and we cannot remove copies that other people made or reposted." This exact disclaimer is required and is the most commonly missing piece. |
| Restricted-product advertising block (section 22580(a)) | If the site is directed to minors, no ad slot, affiliate link, sponsor block, or promoted content may market: alcoholic beverages; firearms or handguns; ammunition or reloaded ammunition; handgun safety certificates; aerosol paint containers capable of defacing property; etching cream capable of defacing property; tobacco, cigarettes, cigarette papers, blunt wraps, or smoking/ingestion paraphernalia; cannabis and cannabis products; BB devices; dangerous fireworks; tanning services using ultraviolet radiation; dietary supplements containing ephedrine group alkaloids; lottery tickets or shares; Salvia divinorum or Salvinorin A; body branding; permanent tattoos; drug paraphernalia; electronic cigarettes; obscene matter; and less lethal weapons. Verify with the current text of section 22580(i) at build time. |
| No targeted restricted-product ads to known minors (section 22580(b)(1)) | If any ad network or personalization layer can target on a minor's profile, activity, address, or location, restricted-product categories must be excluded for that user. In practice: category blocklists in the ad network config, plus notice to the network under section 22580(h)(1) that the property is directed to minors. |
| Ad network notice (section 22580(h)(1)) and good-faith safe harbor (section 22580(b)(2)) | Two separate provisions, do not merge them. Section 22580(h)(1) deems an operator in compliance with **subdivision (a)** for marketing served by an advertising service if the operator "notifies the advertising service, in the manner required by the advertising service, that the site, service, or application is directed to minors." Section 22580(b)(2) separately deems an operator in compliance with **paragraph (b)(1)** if it takes "reasonable actions in good faith designed to avoid" the prohibited marketing. Build evidence of both: written notice to each ad partner in that partner's required form, plus the blocklist configuration. Keep both. |
| Records | Retain the removal-request log (request received, date, action taken, date completed) and the ad-network notice/blocklist config. There is no statutory retention period here, so the studio default applies. Suggest 24 months minimum so you can answer an AG inquiry. |
| Behavior NOT required | No consent banner, no cookie blocking, no age verification, and no honoring of Global Privacy Control are required **by this statute**. Those obligations come from the CCPA/CPRA and from other files in this library. Do not conflate them. |

## How to verify

Run these before delivery.

1. **Scope check.** Confirm in writing with the client whether the property is "directed to minors" and whether any intake field, support flow, or CRM records an age or birth date. Record the answer in the project file. This is the decision that drives everything else.
2. **Removal control exists.** Log in as a non-admin test user, post one item of each user-generated type (comment, review, upload, profile bio). For each, confirm a delete or removal-request control is visible to the author. Any type without one is a gap.
3. **Removal actually removes.** Delete the test post, then load the item URL while logged out and in a second browser profile. Expect a 404 or a "not available" state. Then check any list, feed, search index, sitemap, and RSS/JSON feed that included it. A post that vanishes from the profile page but is still in `/feed.json` or the sitemap fails section 22581(d)(1), which requires it be "no longer visible to other users of the service and the public."
4. **Cache and CDN.** After deletion, re-request the item URL with cache busting and check response headers for a stale cache hit. Purge rules must fire on delete. Also check any static site generator output: a rebuilt page that still contains the content is a live failure.
5. **Grep the copy.** Search the built site for the four required elements. In the repo: grep the privacy policy and settings templates for "remove", "delete", and the incomplete-removal disclaimer. If the phrase warning that removal may not be complete or comprehensive is absent anywhere in the shipped HTML, requirement (a)(4) is unmet.
6. **Instructions are literal.** Read the removal instructions as if you had never seen the site. If you cannot follow them to completion without guessing, they are not "clear instructions."
7. **Ad audit (directed-to-minors sites only).** Open DevTools, Network panel, filter to Doc/XHR/Script, and load the site with an ad blocker disabled. List every third-party ad or affiliate domain. Then in the Elements panel, inspect rendered ad slots across several reloads. Any restricted-product creative is a violation. Also open the ad network dashboard and confirm the category blocklist is applied to this property, not just to the account default.
8. **Third-party embeds.** Check the Application panel for third-party storage and the Network panel for beacons from social embeds and analytics. These do not violate section 22580 by themselves, but on a directed-to-minors site they often carry retargeting that can serve restricted categories.
9. **Confirm the current statute text.** Before delivery, load the leginfo links in Sources and confirm section 22580(i) and section 22581 have not changed. This library is reviewed periodically, and the statute can be amended between reviews.

## Penalties

- **Chapter 22.1 specifies no penalty and no private right of action.** The statute is silent on consequences. This is a fact about the text, not an estimate.
- The generally cited enforcement route is the Unfair Competition Law, Bus. & Prof. Code section 17200, with civil penalties **up to $2,500 per violation** under section 17206, recoverable by the Attorney General, a district attorney, or certain county/city attorneys. Law firm analyses of SB 568 state this as the expected mechanism (Cooley and Orrick, both in Sources; each names the UCL and the $2,500 figure). Treat the $2,500 figure as the UCL penalty cap, which is verified, and treat its application to Chapter 22.1 as the prevailing practitioner reading rather than a settled holding.
- Private plaintiffs under the UCL are limited to injunctive relief and restitution. Civil penalties under section 17206 are available only to public prosecutors.
- **UNVERIFIED:** no public enforcement action or settlement brought specifically under sections 22580-22581 was located during this review. Absence of a located action is not proof that none exists. Do not tell a client the law is unenforced.

## Common ways sites fail this

- Shipping the delete button but omitting the required warning that removal is not complete or comprehensive. This is the single most common miss, and it is the cheapest to fix.
- Writing the removal right into the privacy policy only, with no notice or instruction anywhere near the account or the posting UI.
- "Clear instructions" that read "contact us to request removal" with no address, no form, and no described steps.
- Soft-deleting a post so it disappears from the author's profile while it stays live in the sitemap, an RSS/JSON feed, a search index, an AMP copy, or a CDN cache.
- A comment or review widget from a third party (Disqus-style) where deletion in the host CMS does not propagate to the vendor, so the content stays public.
- Adding an age gate to "be safe," thereby creating actual knowledge that a minor is using the site and pulling a general-audience site into scope it was not in before.
- Assuming COPPA compliance covers this. COPPA is under 13 and federal. This is under 18 and California, with a different duty (removal, not parental consent).
- Running a standard programmatic ad stack on a kids' or teen property with no category blocklist, so alcohol, vape, cannabis, or lottery creatives serve.
- Treating the CAADCA as dead because of the injunction and skipping the parts that are not enjoined.

## Sources

Official sources first. All retrieved 2026-07-20.

- [California Business and Professions Code, Division 8, Chapter 22.1 (sections 22580-22582), leginfo](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=BPC&division=8.&chapter=22.1.) (retrieved 2026-07-20)
- [Business and Professions Code section 22581, leginfo](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=22581&lawCode=BPC) (retrieved 2026-07-20)
- [Business and Professions Code section 22580, leginfo](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=22580&lawCode=BPC) (retrieved 2026-07-20)
- [SB 568 (2013-2014), bill history, leginfo](https://leginfo.legislature.ca.gov/faces/billNavClient.xhtml?bill_id=201320140SB568) (retrieved 2026-07-20)
- [AB 3067 (2017-2018), Internet: marketing: minors: cannabis, leginfo](https://leginfo.legislature.ca.gov/faces/billNavClient.xhtml?bill_id=201720180AB3067) (retrieved 2026-07-20)
- [California Civil Code section 1798.99.35 (CAADCA penalties and notice-and-cure), leginfo](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?sectionNum=1798.99.35&lawCode=CIV) (retrieved 2026-07-20; full text verified against this source)
- [California Civil Code Title 1.81.47, sections 1798.99.28-1798.99.40 (CAADCA), leginfo](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=CIV&division=3.&part=4.&title=1.81.47.) (retrieved 2026-07-20)
- [Business and Professions Code section 17206 (UCL civil penalty), FindLaw](https://codes.findlaw.com/ca/business-and-professions-code/bpc-sect-17206/) (retrieved 2026-07-20)
- [NetChoice, LLC v. Bonta, No. 25-2366 (9th Cir. Mar. 12, 2026), opinion PDF, US Courts](https://cdn.ca9.uscourts.gov/datastore/opinions/2026/03/12/25-2366.pdf) (retrieved 2026-07-20)
- [NetChoice, LLC v. Bonta, No. 25-2366 (9th Cir. 2026), Justia docket page](https://law.justia.com/cases/federal/appellate-courts/ca9/25-2366/25-2366-2026-03-12.html) (retrieved 2026-07-20)
- [AB 1043 (2025-2026), Digital Age Assurance Act, bill text, leginfo](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260AB1043) (retrieved 2026-07-20)
- [Business and Professions Code section 22580, FindLaw (restricted product list)](https://codes.findlaw.com/ca/business-and-professions-code/bpc-sect-22580/) (retrieved 2026-07-20)
- [Cooley, New California Privacy Law for Minors Has Taken Effect as of January 1, 2015](https://www.cooley.com/news/insight/2015/new-california-privacy-law-for-minors-has-taken-effect-as-of-january-1-2015) (retrieved 2026-07-20)
- [Orrick, New California Law for Minors Went Into Effect Jan. 1: What You Need to Know to Comply](https://www.orrick.com/en/Insights/2015/02/New-California-Law-for-Minors-Went-Into-Effect-Jan-1-What-You-Need-to-Know-to-Comply) (retrieved 2026-07-20)
- [Cooley, NetChoice v. Bonta: Ninth Circuit Narrows Injunction Against California's Age-Appropriate Design Code Act (Mar. 30, 2026)](https://www.cooley.com/news/insight/2026/2026-03-30-netchoice-v-bonta-ninth-circuit-narrows-injunction-against-californias-ageappropriate-design-code-act) (retrieved 2026-07-20)
- [Holland & Knight, Ninth Circuit Issues Mixed Ruling on California Age-Appropriate Design Code Act (Mar. 2026)](https://www.hklaw.com/en/insights/publications/2026/03/ninth-circuit-issues-mixed-ruling-on-california-age-appropriate-design) (retrieved 2026-07-20)
- [DLA Piper Privacy Matters, The Ninth Circuit's Latest CAADCA Ruling (Mar. 2026)](https://privacymatters.dlapiper.com/2026/03/the-ninth-circuits-latest-caadca-ruling-navigating-an-evolving-compliance-landscape/) (retrieved 2026-07-20)
- [NetChoice, NetChoice v. Bonta case page (procedural history)](https://netchoice.org/netchoice-v-bonta/) (retrieved 2026-07-20)

## Notes

### The CAADCA (AB 2273) is a different law, and it is partly enjoined

The California Age-Appropriate Design Code Act, Civil Code sections 1798.99.28 to 1798.99.40, was signed in 2022 and took effect January 1, 2023, but its substantive business obligations in section 1798.99.31 were set to become operative **July 1, 2024**. It has never taken full effect. NetChoice sued, and the litigation is still running.

Procedural history:

- December 14, 2022: complaint filed, N.D. Cal.
- September 18, 2023: district court granted a preliminary injunction against the whole act.
- August 16, 2024: Ninth Circuit affirmed the injunction as to the Data Protection Impact Assessment requirement, vacated the rest, and remanded for analysis under the Supreme Court's *Moody* framework.
- March 13, 2025: on remand, the district court again enjoined the act.
- **March 12, 2026: Ninth Circuit decided the second appeal, No. 25-2366.** It affirmed in part, vacated in part, and remanded.

**What remains enjoined after March 12, 2026 (do not build to these, they are blocked):**

- The Data Protection Impact Assessment requirement and the provisions not severable from it (carried over from the 2024 ruling).
- Section 1798.99.31(b)(1) through (b)(4): the "materially detrimental" use restriction, the default profiling restriction, the collection/retention limit keyed to the "best interests of children," and the secondary-use limit. Held unconstitutionally vague because terms such as "materially detrimental," "best interests," and "well-being" fail to give businesses fair notice.
- Section 1798.99.31(b)(7): the dark patterns restriction.
- Section 1798.99.35(c)(2): the 90-day notice-and-cure provision.

**What is no longer covered by the injunction (potentially enforceable now, subject to the remand):**

- Section 1798.99.31(a)(5): age estimation with a reasonable level of certainty, or applying child-level protections to all users. The Ninth Circuit held NetChoice had not met the demanding standard for facial First Amendment relief on this provision or on the act's coverage definition, and sent it back for factual development.
- High-privacy default settings for child users.
- Privacy policies, terms, and community standards in language suited to the age of children likely to access the service.
- An obvious signal to the child when the service is monitoring or tracking the child, including precise geolocation.
- Accessible tools for children to exercise privacy rights and report concerns.

**How to advise a client right now:** the safe posture is to treat the non-enjoined CAADCA items as live obligations for any service "likely to be accessed by children," because the appellate injunction no longer covers them and the district court has not yet resolved severability. The enjoined items should not drive build work. This split is unstable. Confirm the docket before relying on this section.

**CAADCA penalties** (Civil Code section 1798.99.35): up to **$2,500 per affected child** for each negligent violation and up to **$7,500 per affected child** for each intentional violation, in a civil action brought by the Attorney General only. Note that the 90-day cure safe harbor in section 1798.99.35(c)(2) is itself enjoined, so a business cannot currently count on it.

**UNVERIFIED:** whether an en banc petition or a certiorari petition has been filed since March 12, 2026, and the current state of proceedings on remand. No filing was confirmed during this review. Check the N.D. Cal. and Ninth Circuit dockets before advising a client.

### Interaction with other laws in this library

- **COPPA** (federal, under 13) is separate and stricter on collection. A site can owe COPPA parental consent duties and the section 22581 removal duty at the same time, for different age bands.
- **CCPA/CPRA** gives a broader deletion right to all California consumers regardless of age, plus opt-in consent for selling or sharing the personal information of consumers under 16. A CCPA-grade deletion flow will usually satisfy section 22581(a)(1), but it will **not** satisfy (a)(2) through (a)(4) on its own, because those require minor-facing notice, instructions, and the incompleteness warning. Do not mark this file satisfied just because a CCPA deletion request page exists.
- **AB 1043, the Digital Age Assurance Act**, signed October 13, 2025, takes effect **January 1, 2027**. It puts age-bracket signals at the operating system and app store level (under 13, 13 to under 16, 16 to under 18, at least 18) and requires developers to request that signal on download and launch. Retrofit deadlines for pre-existing devices and apps run to July 1, 2027. Penalties mirror the CAADCA at $2,500 negligent and $7,500 intentional per affected child. This matters here because a received age signal is a strong candidate for **actual knowledge** under sections 22580 and 22581. From 2027, apps that consume the signal may find themselves in scope for this statute automatically. Flag this on any app project scoped for 2026 delivery with a 2027 lifespan.

### Watch items

- Section 22581 has not been amended since enactment and has never been squarely tested in court. Its constitutionality has been questioned in academic commentary since 2013. Nothing suggests it is at risk today, but a NetChoice-style challenge is plausible given the current run of First Amendment litigation over minors' online laws.
- The restricted-product list in section 22580(i) grows by amendment (cannabis was added in 2018). Re-verify the list at each annual review rather than trusting this file's copy.
