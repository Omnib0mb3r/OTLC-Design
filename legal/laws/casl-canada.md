# CASL: An Act to promote the efficiency and adaptability of the Canadian economy by regulating certain activities that discourage reliance on electronic means of carrying out commercial activities (S.C. 2010, c. 23)

| Field | Value |
|---|---|
| **Jurisdiction** | Canada (federal), applies to messages sent from or accessed in Canada |
| **Regulator / enforcer** | CRTC (lead, sections 6 to 9). Office of the Privacy Commissioner of Canada (address harvesting, PIPEDA overlap). Competition Bureau (false or misleading representations) |
| **In force since** | 2014-07-01 (CEM rules, sections 6 to 7). 2015-01-15 (computer program rules, section 8) |
| **Last amended** | 2026-01-01. Amendment history since 2017: 2023, c. 8 (Online Streaming Act, in force 2023-04-27, amended sections 5, 6 and 10, including the new section 6(7.1) online undertaking exception); 2024, c. 15, s. 270 (in force 2025-06-20, amended the penalty factors in section 20(3)); Statutes Repeal Act, S.C. 2008, c. 20, s. 3 (effective 2026-01-01, repealed sections 47 to 51 and 55) |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. The private right of action (sections 47 to 51 and 55) was **repealed** effective 2026-01-01, having never been brought into force. Reviving it would require new legislation |

CASL is commonly called "Canada's Anti-Spam Legislation". The Act itself has no short title.

---

## Applies when

Answer these at intake. Any single "yes" in the first group brings the site into scope.

**Jurisdiction triggers (section 12(1) for messages, section 8(2) for software)**

- [ ] Will any commercial electronic message be **sent from** a computer system located in Canada?
- [ ] Will any commercial electronic message be **accessed** on a computer system located in Canada? (This is the one that catches non-Canadian clients. A US business emailing a Canadian subscriber is in scope.)
- [ ] For software: will a program be installed on a computer system **located in Canada**, or is the installer **in Canada** at the time? ([section 8(2)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html))

There is **no revenue threshold, no employee threshold, and no record-count threshold**. CASL applies to a one-person business sending its first newsletter.

**Message-type triggers**

- [ ] Does the site send anything to an electronic address? [Section 1(1)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html) defines that as an address used to transmit an electronic message to an email account, an instant messaging account, a telephone account (which covers SMS), or "any similar account". Social media direct messages are not named in the statute; they are caught, if at all, by the residual "any similar account" branch.
- [ ] Would it be reasonable to conclude that **one of the purposes** of the message is to encourage participation in a commercial activity? That makes it a commercial electronic message (CEM). The bar is low. A "purpose", not "the purpose". A newsletter with one promotional link is a CEM.

**Out of scope for section 6 (still check the rest)**

- Interactive two-way voice calls between individuals, faxes to a telephone account, and voice recordings sent to a telephone account are excluded by [section 6(8)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html). Those fall under the CRTC Unsolicited Telecommunications Rules and the National Do Not Call List, which is a separate regime.
- Section 6 also does not apply to a CEM sent by one individual to another with whom they have a personal or family relationship as defined in [SOR/2013-221 s.2](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2013-221/FullText.html), or to a message that consists solely of an inquiry or application to a person engaged in a commercial activity ([section 6(5)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html)).
- Section 6(7.1), added by the Online Streaming Act in 2023, excludes certain messages sent by an online undertaking to a recipient who consented to receive a program from it.

**Exemptions from the consent requirement only (section 6(6))**

**Read this carefully.** Section 6(6) disapplies only **paragraph 6(1)(a)**, the consent requirement. It does **not** exempt the message from the content rules in section 6(2). A section 6(6) message still needs sender identification, contact information, and a working unsubscribe mechanism. Only the exclusions in SOR/2013-221 s.3 (below) switch off section 6 in full.

A CEM is exempt from the consent requirement if it **solely** does one of these ([section 6(6)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html)):

- provides a quote or estimate the recipient requested
- facilitates, completes, or confirms a commercial transaction the recipient previously agreed to
- provides warranty, product recall, or safety/security information about a product the recipient uses
- provides factual notification of ongoing subscription, membership, account, loan, or similar status
- provides information directly related to an existing employment relationship or benefit plan
- delivers a product, goods, or service, including updates, under an existing transaction

Full exclusions from section 6 in the [Electronic Commerce Protection Regulations, SOR/2013-221, s.3](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2013-221/FullText.html):

- messages between employees, representatives, consultants, or franchisees of the same organization about that organization's activities
- messages between two organizations that already have a relationship, about the recipient organization's activities (the B2B exemption, read narrowly by the courts, see Notes)
- messages sent in response to a request, inquiry, or complaint, or otherwise solicited
- messages to satisfy a legal obligation or enforce a legal right
- messages sent and received on an electronic messaging service, where the section 6(2) information and unsubscribe mechanism are conspicuously published on the interface and the recipient has consented
- messages sent to a limited-access secure and confidential account to which only the account provider can send
- messages a sender reasonably believes will be accessed in a foreign state listed in the schedule to the regulations, where the message conforms to that state's substantially similar law
- registered charity messages whose **primary purpose** is fundraising
- political party or candidate messages whose **primary purpose** is soliciting contributions

Separately, [SOR/2013-221 s.4(1)](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2013-221/FullText.html) exempts from paragraph 6(1)(a) only (not from section 6(2)) the **first** message sent after a third-party referral. It requires both that the message disclose the full name of the individual who made the referral and that it state the message is sent as a result of the referral. The referrer must have a qualifying relationship with both the sender and the recipient.

**Beware:** these are message-level exemptions, not sender-level. An exempt transactional receipt does not exempt the marketing newsletter from the same sender.

---

## What the site must have

### Consent

CASL is opt-in. The **sender carries the burden of proving consent**. This is statutory: "A person who alleges that they have consent to do an act that would otherwise be prohibited under any of sections 6 to 8 has the onus of proving it" ([section 13](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html), confirmed by the [CRTC FAQ](https://crtc.gc.ca/eng/com500/faq500.htm)). If the log is missing, the consent did not exist.

| Consent type | Duration | Source |
|---|---|---|
| **Express** | No expiry. Runs until the recipient withdraws it | [CRTC FAQ](https://crtc.gc.ca/eng/com500/faq500.htm) |
| **Implied: existing business relationship, purchase or lease of a product, goods, service, land, or interest in land** | 2 years from the transaction date. If the purchase involves ongoing use or purchase under a subscription, account, loan, or similar relationship, the 2 years runs from the day that relationship **terminates** ([section 10(14)(a)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html)) | [section 10(10)(a)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html) |
| **Implied: existing business relationship, inquiry or application about a product or service** | 6 months from the inquiry | [section 10(10)(e)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html) |
| **Implied: existing non-business relationship, donation, gift, volunteer work, or attendance at a meeting** | 2 years from that event, and the counterparty must be a registered charity, political party or organization, or a candidate | [section 10(13)(a) and (b)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html) |
| **Implied: existing non-business relationship, membership in a club, association, or voluntary organization** | 2 years, with the clock starting on the day the **membership terminates**, so it runs for the life of the membership plus 2 years | [section 10(13)(c)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html), [section 10(14)(b)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html) |
| **Implied: conspicuous publication** | No fixed clock, but three conditions must all hold (below) | [section 10(9)(b)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html) |
| **Implied: address disclosed to the sender by the recipient** | No fixed clock, same conditions as conspicuous publication | [section 10(9)(c)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html) |

Conspicuous publication and disclosure both require **all three** of: the address was published or disclosed by the recipient themselves, there is no statement beside it refusing unsolicited CEMs, and the message is relevant to that person's business role, functions, or duties ([CRTC guidance](https://crtc.gc.ca/eng/com500/guide.htm)). Scraping a "contact@" address off a website is usually not enough. See the CompuFinder outcome in Notes.

### Build deliverables

| Requirement | What that means in the build |
|---|---|
| Opt-in checkbox, unchecked by default | Every signup form (newsletter, footer bar, popup, gated download, checkout upsell) gets a real `<input type="checkbox">` with no `checked` attribute. Pre-checked boxes do not produce express consent. No consent-by-continuing, no consent buried in terms of service. |
| Consent request must state its purpose | Label text says what they will receive and from whom. "Send me marketing emails from Acme Co." is fine. "Keep me updated" is not. Required by [section 10(1)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html). |
| Consent request must identify the requester and give contact info | Near the checkbox or one click away: the business name (including the name it carries on business under), a mailing address, and one of a phone number, email address, or web address. [SOR/2012-36 s.4](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2012-36/page-1.html). |
| Consent request must say consent can be withdrawn | Literal statement next to the checkbox: "You can unsubscribe at any time." Required by [SOR/2012-36 s.4](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2012-36/page-1.html). |
| Separate consent per purpose | Consent must be "sought separately for each act". Do not bundle marketing email consent with SMS consent, with software installation consent, or with terms acceptance. One checkbox per purpose. |
| Sender identification in every CEM | Email/SMS template footer carries the sender name, and the name of anyone the message is sent on behalf of, plus a statement saying which one is sending. [SOR/2012-36 s.2](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2012-36/page-1.html). |
| Contact info in every CEM, valid 60 days | Mailing address (a P.O. box is acceptable, per the [CRTC FAQ](https://crtc.gc.ca/eng/com500/faq500.htm)) plus one of a phone number reaching an agent or voice mail, an email address, or a web address. Required by [section 6(2)(b)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html) and [SOR/2012-36 s.2(1)](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2012-36/page-1.html). The 60-day validity requirement is [section 6(3)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html), not 6(2). If it is not practicable to include this in the message, [SOR/2012-36 s.2(2)](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2012-36/page-1.html) allows a link to a web page that is readily accessible at no cost, set out clearly and prominently. |
| Unsubscribe mechanism in every CEM | Set out "clearly and prominently", "able to be readily performed", free, and using the same electronic means as the message (or another practicable means). [section 11(1)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html), [SOR/2012-36 s.3](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2012-36/page-1.html). The unsubscribe address or web page must stay valid for a minimum of 60 days after send: [section 11(2)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html). |
| Unsubscribe must not demand extra data | The unsubscribe flow may not require a login, a password, a reason, a survey, or any field beyond the address being removed. |
| Honour unsubscribes within 10 business days | Suppression must propagate to every sending system without delay and in any event within 10 business days ([section 11(3)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html)). Build a shared suppression list, not a per-list flag. This clock also applies to unsubscribes received by any other channel (a reply, a phone call, a contact form). |
| Consent log | Per address, store: consent type (express or implied), exact timestamp, source URL or form ID, the exact label/wording shown at the time, IP address, and for implied consent the triggering event and its date so the 2-year or 6-month clock can be computed. Store the wording, not a pointer to current wording, because the copy will change. |
| Implied-consent expiry job | A scheduled task that stops sending to an address once its 2-year or 6-month clock runs out. Without this, the list silently goes non-compliant. |
| Retention of consent records | CASL sets no explicit retention period. Keep records at least as long as consent is relied on plus the limitation period in [section 23(1)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-3.html): no proceeding may be commenced later than three years after the day the subject matter of the proceeding **became known to a designated person** under section 14. That is a discovery clock, not a clock that starts at the send date, so it can run well past three years from the message. UNVERIFIED: no regulator has published a minimum retention figure. |

### Software installation (section 8)

This catches more than desktop apps. Section 8 covers installing "a computer program on any other person's computer system" during commercial activity. In practice on a web build:

| Situation | Treatment |
|---|---|
| Cookies, HTML, JavaScript, an operating system, or a program executable only through another program the user already consented to | **Deemed express consent** under [section 10(8)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html), but only "if the person's conduct is such that it is reasonable to believe that they consent". The CRTC is explicit: "if the person disables Javascript in their browser, you would not be considered to have consent under CASL since their conduct would not indicate that they consent to that type of program" ([CRTC](https://crtc.gc.ca/eng/internet/install.htm)). If the user has blocked JavaScript or cookies, the deemed consent is gone and you must not force it. |
| Telecommunications service provider programs installed solely to protect network security from a current and identifiable threat, network update/upgrade programs installed by the network operator, and programs necessary to correct a failure | Also deemed express consent, but these come from [SOR/2013-221 s.6](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2013-221/FullText.html) specifying programs under section 10(8)(a)(vi), not from the section 10(8) list itself. Rarely relevant to a web build. |
| User downloads and installs the software themselves | Outside CASL. "CASL does not apply to owners or authorized users installing software on their own computer systems" ([CRTC](https://crtc.gc.ca/eng/internet/install.htm)). |
| Your site or app pushes an installable component, browser extension, agent, SDK, or auto-update the user did not initiate | Express consent required, with purpose, identity, mailing address plus one other contact, a withdrawal statement, and a general description of function. |
| The program collects personal information stored on the device, interferes with the user's control of the device, changes settings/preferences/commands, or changes or interferes with data | **Enhanced disclosure** under [sections 10(4) and 10(5)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html): describe the material elements and their impact on the computer system "clearly and prominently, and separately and apart from the licence agreement". Burying it in an EULA is a violation on its face. |

Note that CASL's deemed consent for cookies does **not** discharge privacy-law consent. PIPEDA and Quebec's Law 25 govern the personal information the cookie collects. Do not tell a client "CASL says cookies are fine, so we need no banner."

---

## How to verify

**Consent capture**

1. Open every signup surface (footer form, popup, checkout, gated asset, contact form). In devtools Elements, confirm the consent input has no `checked` attribute and no `defaultChecked` in the React/Vue source.
2. Grep the codebase for `checked` and `defaultChecked` on marketing consent fields. Grep for `hidden` inputs named like `consent`, `optin`, `subscribe` set to a truthy value.
3. Submit a form with the box unticked. Watch the Network panel. Confirm the payload carries the false value and confirm no address lands in the marketing list.
4. Submit with the box ticked. Query the consent store and confirm timestamp, source, IP, and the exact label string were persisted.
5. Confirm the consent copy near the checkbox contains the business name, a withdrawal statement, and either contact info or a link to it.
6. Confirm each purpose has its own control. One checkbox that reads "email and SMS" fails.

**Message content**

7. Send a test CEM to yourself from every template (welcome, newsletter, abandoned cart, re-engagement, SMS). For each: read the footer and confirm sender name, mailing address, one other contact method, and the unsubscribe control are present and visible without scrolling past dark-on-dark or 8px grey text. "Clearly and prominently" is the standard.
8. In the rendered email, confirm the unsubscribe is a real link or button, not an image-only element that dies with images off, and not white text on white.
9. Click unsubscribe. Count clicks to completion. Confirm no login, no password, no reason field, no confirmation email required to finish, no extra data requested.
10. Watch the request in devtools. Confirm the unsubscribe endpoint returns success without authentication.
11. Re-send to the same address. Confirm suppression. Then confirm suppression propagated to every other sending system (ESP, CRM, SMS gateway, transactional provider) rather than one list.
12. Diary the unsubscribe URL and the contact address for 61 days and confirm both still resolve. Automate this as a monitor if the client rotates infrastructure.

**Implied consent hygiene**

13. Query the list for addresses whose only basis is implied consent and whose triggering event is older than 2 years (or 6 months for inquiries). The count must be zero at send time. If the expiry job does not exist, that is the finding.
14. Confirm any scraped or purchased addresses are not present. Ask the client directly where each import came from and record the answer.

**Software**

15. Load the site with JavaScript disabled and with cookies blocked. Confirm nothing attempts to install or re-enable against the user's setting.
16. Audit any installable component, extension, or SDK the site distributes: confirm the consent screen states purpose, identity, contact info, and withdrawal, and that any personal-information collection or settings changes are disclosed on a screen separate from the EULA.

---

## Penalties

| Item | Amount | Source |
|---|---|---|
| Maximum administrative monetary penalty, individual | **$1,000,000 per violation** | [section 20(4)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-3.html) |
| Maximum administrative monetary penalty, any other person (including corporations) | **$10,000,000 per violation** | [section 20(4)](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-3.html) |

Real amounts issued are far below the maximums. Verified examples:

- **CompuFinder (3510395 Canada Inc.)**: notice of violation set at **$1.1 million** on 2015-03-05, reduced to **$200,000** by the CRTC on 2017-10-19 after representations, upheld on appeal ([Compliance and Enforcement Decision CRTC 2017-368](https://crtc.gc.ca/eng/archive/2017/2017-368.htm)).
- **Hudson's Bay Company**: **$120,000** undertaking dated 2024-06-10, for sending CEMs lacking a readily accessible unsubscribe mechanism, plus a commitment to review its compliance program ([CRTC enforcement actions](https://crtc.gc.ca/eng/ce/actions.htm); also discussed in the [CRTC enforcement report, Oct 2024 to Mar 2025](https://crtc.gc.ca/eng/internet/pub/20250331.htm)).
- **Gap Inc.**: **$200,000** undertaking plus compliance program, 2021-12-06 ([CRTC enforcement actions](https://crtc.gc.ca/eng/ce/actions.htm)).
- **Jimmy Genesse**: **$50,000** AMP, notice of violation 2025-08-13, for violations of paragraph 7(1)(a) (altering transmission data) ([CRTC enforcement actions](https://crtc.gc.ca/eng/ce/actions.htm)).

**Personal liability.** This is the one to raise with client directors.

- **Section 31**: "An officer, director, agent or mandatary of a corporation that commits a violation is liable for the violation if they directed, authorized, assented to, acquiesced in or participated in the commission of the violation, whether or not the corporation is proceeded against." ([section 31](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-4.html)) The corporation does not need to be pursued first, and the individual cap is $1,000,000 per violation.
- **Section 32**: the business is liable for violations by its employees acting in the scope of employment and by its agents acting within their authority, whether or not that person is identified or proceeded against. A rogue contractor or an affiliate marketer is the client's problem.
- **Section 33**: due diligence is a defence. A documented compliance program, written policies, training records, and audit logs are what "due diligence" looks like in evidence. This is the practical reason the consent log matters.

**There is no private right of action, and the provisions that would have created one are now gone.** Sections 47 to 51 and 55 would have let individuals sue. The sequence:

1. Their coming-into-force date of 2017-07-01 was cancelled by [Order in Council SI/2017-31](https://gazette.gc.ca/rp-pr/p2/2017/2017-06-14/html/si-tr31-eng.html) (P.C. 2017-580, made 2017-06-02, registered 2017-06-14), which repealed paragraph (c) of P.C. 2013-1323. No replacement date was ever set.
2. Because they sat un-proclaimed for more than nine years after CASL received royal assent on 2010-12-15, they fell to the automatic repeal in the [Statutes Repeal Act, S.C. 2008, c. 20](https://laws-lois.justice.gc.ca/eng/AnnualStatutes/2008_20/FullText.html). Section 3 of that Act repeals any listed provision "on December 31 of the year in which the report is laid unless it comes into force on or before that December 31 or during that year either House of Parliament adopts a resolution that the Act or provision not be repealed."
3. The [consolidated Act](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html) now shows sections 47 to 51 and 55 as "[Repealed before coming into force, 2008, c. 20, s. 3]", effective 2026-01-01.

As of 2026-07-20 the practical answer to a client is unchanged (no one can sue you directly under CASL), but the legal reason is different. This is no longer a dormant provision awaiting proclamation. Restoring a private right of action would take a new bill through Parliament.

---

## Common ways sites fail this

- Pre-checked opt-in box on a signup or checkout form. The single most common failure and the easiest to spot.
- One checkbox covering email plus SMS plus a partner list. Consent must be sought separately for each act.
- Unsubscribe link that requires signing in to an account to complete.
- Unsubscribe that only removes the address from the one list it was sent from, while the CRM keeps sending.
- Unsubscribe requests arriving by reply email or contact form that nobody routes into the suppression list, blowing the 10-business-day clock.
- No mailing address in the email footer. Businesses that operate from home skip it, not knowing a P.O. box is acceptable.
- Contact page or unsubscribe endpoint torn down during a site relaunch inside the 60-day window from the last send.
- Importing a purchased or scraped list and calling it conspicuous publication. The three conditions almost never hold for scraped addresses.
- Implied consent with no expiry job, so a 2-year-old customer list keeps receiving mail forever.
- Treating a "no consent" record as a "not asked yet" record and re-asking. A request for consent is itself a CEM if it has a commercial purpose.
- Relying on the B2B exemption because the recipient's address ends in a company domain. The exemption needs a relationship between the two organizations, not just a corporate mailbox.
- Consent copy that never states the recipient can withdraw consent.
- Shipping a browser extension or desktop helper whose data-collection behaviour is described only inside the EULA.
- Telling a Canadian client that a GDPR-style cookie banner satisfies CASL, or that CASL's deemed cookie consent satisfies Law 25.

---

## Sources

Official:

- [Act text, S.C. 2010, c. 23, consolidated](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/FullText.html) (retrieved 2026-07-20)
- [Act, page 2: sections 10 and 11, consent and unsubscribe](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html) (retrieved 2026-07-20)
- [Act, page 3: section 20, administrative monetary penalties](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-3.html) (retrieved 2026-07-20)
- [Act, page 4: sections 31 to 33, director liability, vicarious liability, due diligence](https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-4.html) (retrieved 2026-07-20)
- [Electronic Commerce Protection Regulations (CRTC), SOR/2012-36](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2012-36/page-1.html) (retrieved 2026-07-20)
- [Electronic Commerce Protection Regulations, SOR/2013-221 (exemptions)](https://laws-lois.justice.gc.ca/eng/regulations/SOR-2013-221/FullText.html) (retrieved 2026-07-20)
- [CRTC, Frequently Asked Questions about CASL](https://crtc.gc.ca/eng/com500/faq500.htm) (retrieved 2026-07-20)
- [CRTC, Guidance on Implied Consent](https://crtc.gc.ca/eng/com500/guide.htm) (retrieved 2026-07-20)
- [CRTC, CASL Requirements for Installing Computer Programs](https://crtc.gc.ca/eng/internet/install.htm) (retrieved 2026-07-20)
- [CRTC, The Act, regulations, and guidelines](https://crtc.gc.ca/eng/internet/anti/reg.htm) (retrieved 2026-07-20)
- [CRTC, Enforcement actions](https://crtc.gc.ca/eng/ce/actions.htm) (retrieved 2026-07-20)
- [CRTC, Enforcing CASL, report for Oct 2024 to Mar 2025](https://crtc.gc.ca/eng/internet/pub/20250331.htm) (retrieved 2026-07-20)
- [CRTC, Compliance and enforcement processes](https://crtc.gc.ca/eng/ce/caslpro.htm) (retrieved 2026-07-20)
- [Canada Gazette, Order in Council SI/2017-31, private right of action](https://gazette.gc.ca/rp-pr/p2/2017/2017-06-14/html/si-tr31-eng.html) (retrieved 2026-07-20)
- [Statutes Repeal Act, S.C. 2008, c. 20](https://laws-lois.justice.gc.ca/eng/AnnualStatutes/2008_20/FullText.html), the mechanism that repealed CASL sections 47 to 51 and 55 (retrieved 2026-07-20)
- [Compliance and Enforcement Decision CRTC 2017-368, CompuFinder](https://crtc.gc.ca/eng/archive/2017/2017-368.htm) (retrieved 2026-07-20)
- [Office of the Privacy Commissioner, guidance for businesses doing e-marketing](https://www.priv.gc.ca/en/privacy-topics/privacy-laws-in-canada/the-personal-information-protection-and-electronic-documents-act-pipeda/r_o_p/canadas-anti-spam-legislation/casl-compliance-help-for-businesses/casl_guide/) (retrieved 2026-07-20)

Secondary (used only for case outcomes and history):

- [Torys, FCA confirms CASL is constitutional but limits the business communications exemption](https://www.torys.com/insights/publications/2020/06/fca-confirms-casl-is-constitutional-but-limits-business-communications-exemption) (published 2020-06-15, retrieved 2026-07-20). Confirms the FCA dismissed both of CompuFinder's appeals, leaving the $200,000 penalty standing.
- [Barry Sookman, Supreme Court denies CompuFinder leave to appeal](https://www.barrysookman.com/2021/03/04/supreme-court-denies-compufinder-leave-to-appeal-in-casl-charter-and-constitutional-challenge/) (retrieved 2026-07-20)

---

## Notes

**Constitutionality is settled.** In *3510395 Canada Inc. v. Canada (Attorney General)*, 2020 FCA 103 (2020-06-05), the Federal Court of Appeal upheld CASL's CEM scheme as valid federal trade and commerce legislation, found the section 2(b) Charter infringement saved under section 1, and the Supreme Court denied leave to appeal in March 2021. Do not expect a client's "this law is unconstitutional" argument to go anywhere.

**The B2B exemption is narrower than clients think.** In the same case the court held that a contractual relationship built on a small number of transactions touching very few employees is not a relationship for the purposes of the business-to-business exemption. Advise clients not to lean on it for cold outreach.

**Conspicuous publication was also read narrowly.** CompuFinder lost on addresses harvested from sites that gave no indication the address holder had published them, and lost outright on addresses published next to a statement asking not to receive CEMs. Treat any scraped list as unconsented.

**Private right of action is dead, not dormant.** This reverses the guidance that stood from 2017 to 2025. SI/2017-31 removed the start date and left the provisions pending Parliamentary review, but the review never produced a proclamation, and the Statutes Repeal Act repealed sections 47 to 51 and 55 outright effective 2026-01-01. The 2017 INDU committee report, *Canada's Anti-Spam Legislation: Clarifications Are in Order* (December 2017, 42nd Parliament, 1st Session), recommended clarifying CASL. UNVERIFIED: I could not confirm the exact recommendation count in that report (previously stated here as 13), any legislative response to it, or any CASL amendment bill active in 2026. Do not tell a client the private right of action is coming; tell them it would require new legislation.

**Enforcement pattern is warnings and negotiated undertakings, not headline fines.** In the Oct 2024 to Mar 2025 period the CRTC issued 16 warning letters, 105 notices to produce, 2 preservation demands, and concluded 1 undertaking. Over 208,000 complaints reached the Spam Reporting Centre in that period, with lack of consent the top category at 48%. The realistic risk to a small client is a notice to produce that demands consent records they cannot produce, followed by a settlement.

**Interaction with other laws in this library.**
- *PIPEDA and Quebec Law 25*: CASL governs whether you may send. Privacy law governs collecting and using the address itself, and Law 25 adds its own express-consent and de-indexing rules. Both apply at once.
- *CAN-SPAM (US)*: opposite default. CAN-SPAM is opt-out, CASL is opt-in. A US client's existing email stack will almost always be non-compliant for Canadian recipients. Never reuse a CAN-SPAM footer and call it done.
- *GDPR*: consent standards are close enough that a GDPR-grade consent flow usually satisfies CASL's consent capture, but GDPR does not require the mailing address or the 60-day validity, so the footer still needs CASL-specific fields.

**Watch the section 6(6) exemptions during scope creep.** A transactional template that is exempt today stops being exempt the moment marketing content is added to it, because the exemption requires the message do that thing *solely*. Order confirmations with a "you may also like" block are CEMs.
