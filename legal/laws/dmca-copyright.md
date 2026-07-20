# DMCA / US Copyright: Title 17, U.S. Code (Copyright Act), including the Digital Millennium Copyright Act, Pub. L. 105-304

| Field | Value |
|---|---|
| **Jurisdiction** | United States (federal). Applies to the site operator if the operator is a US person or entity, or if the site is accessible in the US and a US copyright owner sues here. |
| **Regulator / enforcer** | No agency polices this. The US Copyright Office runs the designated-agent directory and the registration system. Enforcement is private civil litigation in federal district court, plus the Copyright Claims Board (CCB) for small claims. Criminal cases go to DOJ. |
| **In force since** | Copyright Act of 1976 (effective 1978-01-01). DMCA signed 1998-10-28, adding 17 U.S.C. 512, 1201, and 1202. |
| **Last amended** | The electronic designated-agent system replaced paper filings on 2016-12-01 (37 CFR 201.38). The CASE Act created the Copyright Claims Board, which began accepting claims in 2022. UNVERIFIED: no amendment to 17 U.S.C. 512 or 1202 between 2022 and this review date was confirmed in this session. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force |

## Applies when

Copyright applies to every site. The DMCA safe harbor only applies to some. Split these at intake.

**Copyright basics apply to every project, with no threshold:**

- The site publishes any text, photo, illustration, icon, font, video, audio, or code. Protection attaches automatically at creation. No notice and no registration is needed for the work to be protected (17 U.S.C. 102, 401(a)).
- The site uses any asset the studio did not create: stock photos, icon sets, fonts, code libraries, client-supplied images, screenshots, map tiles, or embedded media. Every one of these needs a license on file.
- The client wants to be able to sue someone who copies the site. That requires registration, and the timing rules below decide whether statutory damages are available.

**DMCA safe harbor under 17 U.S.C. 512(c) applies only when the site stores material at the direction of users.** Check for any of these:

- User comments, reviews, ratings with text, or a testimonial form that publishes without staff approval.
- Forums, message boards, community areas, or Q&A.
- File, image, video, or audio upload by users of any kind.
- User profiles with avatars, bios, or portfolio galleries.
- Marketplace, classifieds, or directory listings written by third parties.
- A CMS where people outside the client's organization have publishing rights.

**The safe harbor does not apply and no designated agent is needed when:**

- Every word and image on the site is authored or approved by the client before it goes live. A brochure site, a marketing site, or a blog with staff-only authoring is not a 512(c) service provider for its own content. The safe harbor protects a host from liability for what *other people* post, and it never protects the operator's own content.
- Comments are fully moderated before publication. UNVERIFIED: pre-moderation is widely treated as weakening or defeating safe-harbor eligibility because it can create knowledge of the material, but no case holding was confirmed in this session. Treat pre-moderation plus a designated agent as the safer combination rather than assuming pre-moderation alone is fine.

**Conditions that must be true for the safe harbor to hold, even when 512(c) is otherwise available (17 U.S.C. 512(i)):**

- The operator has adopted a repeat infringer termination policy, reasonably implements it, and informs users of it.
- The operator accommodates standard technical measures developed by broad industry consensus.
- The operator does not have actual knowledge of the specific infringing material, is not aware of facts making infringement apparent, and acts expeditiously to remove material once it knows.
- The operator does not receive a financial benefit directly attributable to infringing activity in a case where it has the right and ability to control that activity.

**Section 1202 (copyright management information) applies whenever the build touches other people's files:**

- The image pipeline processes photos the client or a third party supplied.
- Any build step resizes, converts, or optimizes images (this is nearly every modern build).
- The site republishes third-party images, PDFs, or documents.

**Registration timing (17 U.S.C. 412), if the client wants enforcement leverage:**

- To get statutory damages and attorney's fees, the work must be registered before the infringement starts, or, for a published work, within three months after first publication.
- Miss that window and the client is limited to actual damages and the infringer's profits, which for a website is usually too small to justify a lawsuit.

## What the site must have

| Requirement | What that means in the build |
|---|---|
| Copyright notice in the footer | Optional under 17 U.S.C. 401(a), but include it. Format per 401(b): the symbol `©` (or the word "Copyright" or "Copr."), the year of first publication, and the copyright owner's name. Example: `© 2026 Acme Holdings Ltd`. Use the client's correct legal entity name, not the trading name, unless the entity actually holds the copyright. |
| What the notice does | Under 401(d), where a proper notice appears on copies the defendant had access to, a court gives no weight to that defendant's innocent-infringement defense in mitigation of damages. That matters because innocent infringement can otherwise drop statutory damages to as low as $200 per work (504(c)(2)). |
| What the notice does not do | It does not create, extend, or register the copyright. It is not required for protection. It does not by itself let the client sue, and it does not unlock statutory damages. Only registration does that. Do not let a client believe the footer line is their legal protection. |
| Auto-updating year | A `new Date().getFullYear()` footer is fine in practice and very common. Note that 401(b) refers to the year of first publication, so a strictly correct notice for a site published in 2019 is `© 2019` or `© 2019-2026`. Prefer a range: it stays accurate and it signals the site is maintained. |
| Terms of use with an IP clause | State who owns the site content, what visitors may do with it, and that user-submitted content grants the operator a license to display it. Without that license grant, publishing a user's own photo back to the site is technically the operator infringing the user. |
| DMCA policy page (UGC sites) | A page at a stable URL, typically `/dmca` or `/copyright`, linked from the footer. It must contain the designated agent's contact details and the takedown procedure. |
| Designated agent posted on the site (37 CFR 201.38) | The page must list: the service provider's full legal name and physical street address, all alternate names the public would likely search under (trading names, app names, domain names), the agent's name (a person, position, department, or entity), and the agent's physical mail address, telephone number, and email address. A contact form alone is not enough. |
| Designated agent registered with the Copyright Office | Register through the Office's online system at the DMCA Designated Agent Directory. Paper designations are no longer accepted. Fee is $6 for a designation, amendment, or resubmission. Posting on the site alone does not qualify the operator: both the site posting and the Office registration are required. |
| Three-year renewal | Under 37 CFR 201.38, a designation expires and becomes invalid three years after it is registered unless renewed. Set a calendar reminder at registration plus 34 months and hand it to the client in writing. An expired designation means no safe harbor. This is the single most-missed step in the whole process. |
| Repeat infringer policy | Written into the terms of use or the DMCA page. It must state that accounts of repeat infringers will be terminated in appropriate circumstances, and users must be informed of it. It must also be actually implemented, which means the backend needs a way to record strikes against an account and a way to disable that account. A policy with no strike field in the database is a policy that is not reasonably implemented. |
| Strike and termination records | A table or field recording, per user: each valid takedown received, the date, the material, and the action taken. This is the evidence that the policy is implemented if the safe harbor is ever tested. |
| Takedown intake | The agent email must reach a monitored human inbox. Route it to a shared mailbox, not a personal one that leaves when someone quits. |
| Takedown procedure documented | The DMCA page should list what a valid notice must contain per 17 U.S.C. 512(c)(3)(A): a physical or electronic signature of a person authorized to act for the copyright owner, identification of the work claimed to be infringed, identification of the material claimed to be infringing with information reasonably sufficient to locate it, contact information for the complaining party, a statement of good-faith belief that the use is unauthorized, and a statement under penalty of perjury that the information is accurate and the sender is authorized to act. |
| Removal behavior | On a valid notice, remove or disable access to the material expeditiously, and take reasonable steps to promptly notify the user whose material was removed (512(g)(2)). Build an admin action that unpublishes content without hard-deleting it, so it can be restored. |
| Counter-notice procedure | Document the 512(g)(3) elements: the user's physical or electronic signature, identification of the removed material and where it appeared before removal, a statement under penalty of perjury of good-faith belief that removal resulted from mistake or misidentification, the user's name, address, and telephone number, and consent to the jurisdiction of the relevant federal district court. |
| Restore window | On receiving a valid counter-notice, forward it to the original complainant and restore the material not less than 10 and not more than 14 business days after receipt, unless the complainant first notifies the agent that it has filed suit seeking to restrain the user (512(g)(2)(C)). Build this as a scheduled task, not a memory. |
| Image metadata preserved | Configure the image pipeline to keep IPTC, XMP, and copyright EXIF fields on third-party images. Stripping them is the Section 1202(b) exposure described below. |
| Asset license records | A file in the repo (for example `ASSETS.md` or `licenses/`) listing every third-party asset, its source URL, its license, the license purchase or download date, and any attribution the license requires. Deliver it to the client. |
| Required attributions rendered | Some licenses (Creative Commons BY, some icon and font licenses) require visible credit. If required, put it in the footer or on a `/credits` page, not buried in an HTML comment. |

## How to verify

**Footer notice**

- Load the production home page and read the footer. Confirm the symbol, a year, and a name are all present.
- Confirm the name matches the client's legal entity. Check it against the contract or the companies register, not against what someone said in a kickoff call.
- If the year is dynamic, change the system clock or evaluate the expression and confirm it does not render `© NaN` or `© 1970`.

**DMCA page (UGC sites only)**

- `curl -I https://site.example/dmca` and confirm a 200, not a redirect to a 404 or a soft 404.
- Click the footer link on a rendered page. A page that exists but is not linked is a page nobody finds.
- Read the page and check off each 37 CFR 201.38 item: full legal name, physical street address, alternate names, agent name, agent postal address, agent phone, agent email. A missing street address or phone number is the usual gap.
- Send a real test email to the agent address from an outside account and confirm it lands in a monitored inbox and does not bounce.

**Copyright Office registration**

- Search the client's name and every alternate name in the Copyright Office DMCA Designated Agent Directory at https://dmca.copyright.gov/osp/. Confirm a live record exists.
- Read the registration date on that record and compute the expiry at three years. If it is inside 3 months of expiring, renew before delivery.
- Confirm the details in the directory match the details on the site page character for character. Mismatched addresses between the two are a common defect.

**Repeat infringer policy**

- Grep the terms and the DMCA page for the termination language: `grep -ri "repeat infringer" ./content ./src`.
- Inspect the database schema for the mechanism, not the prose. Confirm there is a way to record a strike against a user and a way to disable that user. `grep -ri "strike\|suspend\|ban\|terminate" ./prisma ./migrations ./models`.
- Confirm an admin can actually unpublish a single piece of user content from the UI. Do it once on staging.

**Image metadata (Section 1202)**

- Run `exiftool` on a source image and on the built output of the same image, then compare:
  `exiftool -G -a -Copyright -Artist -Creator -Rights -CreditLine -IPTC:all source.jpg build/output.jpg`
- If the copyright and creator fields are present in the source and absent in the output, the pipeline is stripping CMI. Fix the pipeline before delivery.
- Check the specific tool config. `sharp` strips metadata unless you call `.keepMetadata()` or `.withMetadata()`. `imagemin` and `mozjpeg` strip by default. Next.js image optimization strips metadata from optimized output. Confirm behavior with `exiftool` rather than trusting documentation.
- Watch a real request in the devtools Network panel: open the optimized image URL the browser actually fetched (not the source file in the repo) and run `exiftool` on that downloaded response. On a CDN-optimized site the CDN, not the build, is often what strips the data.

**Third-party assets**

- Open the asset license file and pick three entries at random. Confirm each license is real and the source URL resolves.
- Grep for hotlinked external images that were never licensed: `grep -rE "src=[\"']https?://" ./src --include=*.html --include=*.tsx --include=*.jsx`.
- Check the font licenses specifically. Webfont licenses are usually capped by monthly pageviews or by domain, and a font licensed for the studio's use is not licensed for the client's site.

## Penalties

There is no regulator fine here. The exposure is civil damages, and it is per work, which is how image cases get expensive fast.

| Exposure | Amount | Source |
|---|---|---|
| Statutory damages for copyright infringement | Not less than $750 and not more than $30,000 per work infringed, as the court considers just | [17 U.S.C. 504(c)(1)](https://www.law.cornell.edu/uscode/text/17/504) |
| Willful infringement | Court may increase the award to not more than $150,000 per work | [17 U.S.C. 504(c)(2)](https://www.law.cornell.edu/uscode/text/17/504) |
| Innocent infringement | Court may reduce the award to not less than $200 per work. A proper copyright notice on copies the defendant had access to blocks this defense | [17 U.S.C. 504(c)(2)](https://www.law.cornell.edu/uscode/text/17/504), [17 U.S.C. 401(d)](https://www.law.cornell.edu/uscode/text/17/401) |
| Removing or falsifying copyright management information | Not less than $2,500 and not more than $25,000 per violation | [17 U.S.C. 1203(c)(3)(B)](https://www.law.cornell.edu/uscode/text/17/1203) |
| Repeat 1202 violation within 3 years of a prior judgment | Court may increase the award up to triple the amount otherwise awarded | [17 U.S.C. 1203(c)(4)](https://www.law.cornell.edu/uscode/text/17/1203) |
| Actual damages | Available instead of statutory damages: the owner's actual loss plus the infringer's profits attributable to the infringement | [17 U.S.C. 504(b)](https://www.law.cornell.edu/uscode/text/17/504) |
| Attorney's fees | At the court's discretion to the prevailing party, but only if the registration timing in 412 was met | [17 U.S.C. 505](https://www.law.cornell.edu/uscode/text/17/505), [17 U.S.C. 412](https://www.law.cornell.edu/uscode/text/17/412) |
| Copyright Claims Board | Up to $30,000 per proceeding. Participation is voluntary and a respondent may opt out | [ccb.gov](https://ccb.gov/) |
| Bad-faith takedown or counter-notice | Whoever knowingly materially misrepresents that material is infringing, or that it was removed by mistake, is liable for damages including costs and attorney's fees incurred by the alleged infringer, any copyright owner, or the service provider | [17 U.S.C. 512(f)](https://www.law.cornell.edu/uscode/text/17/512) |

Losing the safe harbor is not itself a penalty. It removes the shield, and the operator then faces the 504(c) numbers above for material its users posted.

The CCB opt-out window is 60 days, set by statute rather than regulation: a respondent properly served with a notice and claim has 60 days from the date of service to give the Board written notice that it is opting out (17 U.S.C. 1506(i)). Miss it and the proceeding becomes binding. Advise a served client to calendar the date immediately.

## Common ways sites fail this

- The DMCA page exists and the agent was never registered with the Copyright Office. Posting on the site is half the requirement. Half gets no safe harbor.
- The agent was registered once at launch and never renewed. The designation silently expired at three years and nobody noticed. This is the most common failure in the whole area.
- The DMCA page lists an email address and nothing else. No legal name, no street address, no phone. The regulation requires all of them.
- The agent email points at a personal address belonging to a developer or an agency employee who has since left.
- The terms of use promise a repeat infringer policy and the database has no way to record a strike or disable an account. The policy is not implemented, so it does not count.
- The site launched with user comments and nobody ever asked whether it needed a designated agent, because the intake questionnaire only asked about privacy law.
- The image build pipeline strips all EXIF, IPTC, and XMP for file-size reasons, including the copyright and creator fields on photographer-supplied photos. Nobody made a decision about it: it was the default.
- Stock photos were licensed for the comp or the pitch deck and then shipped to production under a license that never covered web use.
- A webfont licensed to the studio was deployed on the client's domain. The license was per-domain.
- Client-supplied images turn out to have been pulled from Google Images by the client's marketing person. Nobody asked for provenance, and the studio built the page that publishes them.
- The footer reads `© 2019` because the year was hardcoded at launch, which tells every visitor the site is abandoned.
- The footer names the trading name while a different legal entity owns the copyright, so the notice identifies the wrong owner.
- Takedown arrives, someone deletes the content permanently, then a valid counter-notice arrives and the material cannot be restored inside the 10-to-14-business-day window.
- Removed content is restored immediately on receiving a counter-notice, before the 10-business-day floor. The statute sets a minimum as well as a maximum, and jumping the gun forfeits the protection the process is there to provide.

## Sources

Official sources first. All retrieved 2026-07-20.

- [17 U.S.C. 512, Limitations on liability relating to material online](https://www.law.cornell.edu/uscode/text/17/512) (Cornell LII, reproducing the US Code). Retrieved 2026-07-20.
- [17 U.S.C. 1202, Integrity of copyright management information](https://www.law.cornell.edu/uscode/text/17/1202) (Cornell LII). Retrieved 2026-07-20.
- [17 U.S.C. 1203, Civil remedies](https://www.law.cornell.edu/uscode/text/17/1203) (Cornell LII). Retrieved 2026-07-20.
- [17 U.S.C. 504, Remedies for infringement: Damages and profits](https://www.law.cornell.edu/uscode/text/17/504) (Cornell LII). Retrieved 2026-07-20.
- [17 U.S.C. 401, Notice of copyright: Visually perceptible copies](https://www.law.cornell.edu/uscode/text/17/401) (Cornell LII). Retrieved 2026-07-20.
- [17 U.S.C. 412, Registration as prerequisite to certain remedies](https://www.law.cornell.edu/uscode/text/17/412) (Cornell LII). Retrieved 2026-07-20.
- [37 CFR 201.38, Designation of agent to receive notification of claimed infringement](https://www.law.cornell.edu/cfr/text/37/201.38) (Cornell LII, reproducing the CFR). Source for the three-year expiry and the required website contact details. Retrieved 2026-07-20.
- [US Copyright Office, DMCA Designated Agent Directory](https://www.copyright.gov/dmca-directory/). Registration portal and the rule that paper designations are no longer accepted. Retrieved 2026-07-20.
- [US Copyright Office, Fees](https://www.copyright.gov/about/fees.html). Source for the $6 designation, amendment, or resubmission fee. Retrieved 2026-07-20.
- [Copyright Claims Board](https://ccb.gov/). Source for the $30,000 per-claim cap and the voluntary opt-out. Retrieved 2026-07-20.
- [17 U.S.C. 1506, Conduct of proceedings](https://www.law.cornell.edu/uscode/text/17/1506) (Cornell LII). Source for the 60-day respondent opt-out window at 1506(i). Retrieved 2026-07-20.

## Notes

**The safe harbor question belongs in intake, not in the build.** Ask one question: can anyone outside the client's staff cause text or files to appear on this site without a staff member approving it first? Yes means designated agent. No means skip the whole 512 apparatus and just get the copyright notice and asset licenses right. Most sites the studio builds are "no", and adding a DMCA page to a brochure site is harmless but pointless.

**Sell the three-year renewal as a maintenance line item.** The client will not remember. If the studio holds the retainer, hold the calendar reminder too. If the client self-manages, put the expiry date in the handover document in bold and get them to acknowledge it in writing. A lapsed designation converts a protected host into an unprotected one, and nobody finds out until a lawsuit.

**Section 1202 metadata stripping is the live risk area for a design studio, because it is caused by a default nobody chose.** Plaintiffs (often photographers, sometimes at volume) have brought 1202(b) claims over image optimization pipelines removing copyright and creator fields. The statute requires intentional removal plus knowledge, or reasonable grounds to know, that the removal will induce, enable, facilitate, or conceal infringement, so an automated pipeline is not automatically a violation. UNVERIFIED: courts are split on how far 1202(b) reaches, including an "identicality" requirement adopted in some circuits (that the defendant distributed an identical copy with CMI removed), but no specific circuit holdings were confirmed in this session. Do not tell a client they are safe on that basis. The cheap answer is to keep the metadata: preserve copyright and creator fields on third-party images and accept the file-size cost. Stripping metadata from the client's *own* images is fine, since the client owns them.

**Registration is a separate service and worth mentioning to the client.** The footer notice costs nothing and does little. Registration within three months of publication is what makes an infringement claim economically viable, because it unlocks statutory damages and fees. The studio does not need to do the filing, but flagging the three-month window at launch is genuine value and takes one sentence.

**Interaction with other laws in this library:**

- Takedown and counter-notice handling processes personal data (names, addresses, phone numbers, and a jurisdiction consent). Under GDPR and the US state privacy laws, that data needs a retention period and a lawful basis, and forwarding a counter-notice to the complainant discloses the user's real name and address to a stranger. Say so in the privacy policy and in the DMCA page, so users are not surprised.
- Consent logs, DMCA strike records, and takedown correspondence all have different retention drivers. Do not fold them into one blanket retention rule.
- The accessibility rules in this library apply to the DMCA page too. It is a real page and it needs to be reachable by keyboard and readable by a screen reader, not an unlinked orphan.

**Not covered in this file:** 17 U.S.C. 1201 (circumvention of technical protection measures) is DMCA but rarely touches a website build. It matters if the project involves DRM, access controls on paid content, or scraping past a paywall. Treat that as a separate question and research it fresh.
