# CAN-SPAM: Controlling the Assault of Non-Solicited Pornography And Marketing Act of 2003

| Field | Value |
|---|---|
| **Jurisdiction** | United States, federal. Applies to commercial email sent to a protected computer, which in practice means any recipient in the US, regardless of where the sender is |
| **Regulator / enforcer** | Federal Trade Commission (primary). Also: FCC, sector regulators (OCC, Federal Reserve, FDIC, NCUA, SEC, state insurance authorities, DOT, USDA, Farm Credit Administration), State attorneys general, and providers of Internet access service via a private right of action. DOJ for criminal provisions |
| **In force since** | January 1, 2004 (Pub. L. 108-187, section 16) |
| **Last amended** | Statute: no substantive amendment found as of 2026-07-20. Implementing rule (16 CFR Part 316) last substantively amended effective July 7, 2008 |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force |

**The one thing to carry out of this file:** CAN-SPAM is an opt-out regime. You may email a US recipient who never asked to hear from you, provided the message is honest and carries a working exit. Do that same thing to a Canadian recipient and you have likely broken CASL, which is opt-in. See [Notes](#notes).

---

## Applies when

Answer these at intake. There is no revenue threshold, no employee-count threshold, and no minimum send volume anywhere in this statute. One email triggers it.

- **The site sends, or will send, any email whose primary purpose is commercial advertisement or promotion of a product or service.** This is the only real trigger. A newsletter that promotes the client's services counts.
- **Any recipient is in the United States.** The Act reaches messages sent to a protected computer. A foreign business emailing US recipients is caught. A US business emailing only EU recipients is out of scope here and is in scope for GDPR and PECR instead.
- **The email is business-to-business.** B2B commercial email is fully covered. There is no B2B carve-out, which is a common and expensive misreading.
- **The client uses a contractor, agency, or affiliate to send on their behalf.** Liability attaches to the "sender", defined as the person who initiates the message and whose product, service, or website is promoted (15 U.S.C. 7702(16)). Hiring an ESP or an affiliate network does not move that liability off the client.
- **More than one company is advertised in a single message.** Each advertised company is a sender by default. Only one can be treated as the sole sender, and only if it is identified in the "from" line as the sole sender and it complies with the Act (16 CFR 316.2(m)).

**Not triggered by:**

- **Transactional or relationship messages**, for most requirements. Five categories qualify (15 U.S.C. 7702(17)): completing or confirming a transaction the recipient already agreed to; warranty, recall, safety, or security information; notice of a change in terms or features, or an account statement for an existing subscription or membership; information about an employment relationship or benefit plan; delivery of goods, services, updates, or upgrades the recipient is entitled to receive.
- **One exception applies even to those.** The header accuracy rule at 15 U.S.C. 7704(a)(1) covers "a commercial electronic mail message, **or a transactional or relationship message**". A password reset email with a forged From line violates CAN-SPAM. Nothing else in subsection (a) reaches transactional mail.
- **SMS and push notifications.** Not this statute. Text-message marketing to US numbers is TCPA territory and is opt-in with much harsher exposure. Do not reason about SMS from this file.

**Mixed-content messages: how to decide.** When a message carries both commercial and transactional content, 16 CFR 316.3 makes it commercial if either the subject line would lead a reasonable recipient to conclude it contains a commercial advertisement, or the transactional content does not appear substantially at the beginning of the body. Practical build rule: an order confirmation with a promo block below the receipt is usually still transactional. The same receipt with "50% off your next order" in the subject line is a commercial message and needs the full treatment below.

---

## What the site must have

Requirements come from 15 U.S.C. 7704(a) and 16 CFR Part 316. Most of this is email-template and backend work rather than page work, but the signup form and the footer are site deliverables.

| Requirement | What that means in the build |
|---|---|
| **Accurate header information** (7704(a)(1)) | From, To, Reply-To, and the originating domain and routing data must accurately identify the sender. Do not send from a domain the client does not control. Set up SPF, DKIM, and DMARC on the sending domain so the headers are both accurate and provable. Applies to transactional email too |
| **Non-deceptive subject line** (7704(a)(2)) | The subject must reflect what is in the message. No fake "Re:" or "Fwd:" prefixes, no fake reply threading, no "Your invoice is ready" on a promotion. Treat this as copy review, not engineering |
| **Identify the message as an advertisement** (7704(a)(5)(A)(i)) | Clear and conspicuous disclosure that the message is an ad. The Act does not dictate wording or placement. Waived where the recipient gave prior affirmative consent (7704(a)(5)(B)), which is the practical reason to keep a real consent record even under an opt-out regime |
| **Valid physical postal address** (7704(a)(5)(A)(iii)) | A real address in every commercial email. Under 16 CFR 316.2(p) this can be the current street address, a PO Box accurately registered with USPS, or a private mailbox accurately registered with a commercial mail receiving agency established under USPS regulations. Put it in the email template footer as a hardcoded merge field, not something an editor can delete. For a home-based client this is the reason to buy a registered mailbox before launch |
| **Clear and conspicuous opt-out notice** (7704(a)(5)(A)(ii)) | Visible notice of the right to unsubscribe, in the message. Not 6px grey text on white. This is an accessibility contrast problem as much as a legal one |
| **Functioning opt-out mechanism** (7704(a)(3)(A)) | A working return email address or other internet-based mechanism, clearly and conspicuously displayed. It may offer a menu of message types, but one option must be "stop sending me any commercial email from this sender" |
| **Opt-out mechanism live for 30 days minimum** (7704(a)(3)(A)) | The unsubscribe link must keep working for at least 30 days after the message was sent. Kills the pattern of unsubscribe URLs tied to a campaign that gets torn down when the campaign ends. Unsubscribe routes must outlive the campaign |
| **Honor opt-outs within 10 business days** (7704(a)(4)(A)(i)) | Business days, not calendar days. After that window, sending to that address is unlawful. Do not build a 30-day processing queue. Suppress immediately and treat the 10 days as the outer bound for propagation across systems, not as a target |
| **No fee, no hoops on the way out** (16 CFR 316.5) | The recipient may not be required to pay a fee, provide any information beyond their email address and opt-out preferences, or take any step other than sending a reply email or visiting **a single** internet web page. Bans: login-required unsubscribes, "tell us why" as a mandatory field, multi-page confirmation flows, CAPTCHA gates, asking for a password |
| **Never sell or transfer an opted-out address** (7704(a)(4)(A)(iv)) | Once someone opts out, the sender and anyone who knows about the opt-out may not sell, lease, exchange, transfer, or release that address. The statute carves out transfers "for any purpose other than compliance with this chapter or other provision of law", which is what makes a suppression-list vendor lawful. If the client sells or shares lists, opted-out addresses must be stripped from every export |
| **Suppression list, permanent** (records) | A durable store of every opted-out address, retained indefinitely and applied to every send across every tool. Suppression outlives the ESP contract. If the client migrates from Mailchimp to Klaviyo, the suppression list migrates first. Store a hash if you prefer, so long as matching still works |
| **Consent record for anyone you claim consented** (records) | Not required by the statute, but it is what supports the advertisement-disclosure waiver and what you produce if challenged. Log timestamp, IP, form URL, the exact checkbox or wording shown, and the version of the policy in force. This is the same log the [`gdpr`](gdpr.md) and [`casl-canada`](casl-canada.md) files need, so build it once |
| **Signup form wired honestly** (site UI) | If the form says "newsletter", the resulting list is used for the newsletter. Silently adding form-fill leads to a promotional blast is where header and subject-line honesty starts breaking down |
| **Sender designation, if multiple advertisers** (16 CFR 316.2(m)) | For co-marketing or partner emails, decide in the build who the single sender is, name that entity in the From line, and make sure that entity carries the address and the opt-out |

---

## How to verify

Do this against a real send from the production ESP with production templates, not against a local preview. Preview renderers strip footers.

1. **Send a live test to a mailbox you control.** Gmail plus a non-Gmail account, because rendering differs.
2. **Open the raw source.** In Gmail: the three-dot menu, then "Show original". Check that `From:`, `Reply-To:`, and `Return-Path:` all resolve to domains the client actually owns. Confirm `SPF: PASS`, `DKIM: PASS`, `DMARC: PASS` in the authentication summary.
3. **Grep the rendered HTML for the postal address.** Search the message body for the street or box number. If it is absent from any single template, that template fails. Check every template: welcome, newsletter, abandoned cart, re-engagement, and every automation step. The last one in an automation series is the one that usually ships without a footer.
4. **Count the clicks to unsubscribe.** Click the link. If the recipient lands anywhere other than a single page that completes the opt-out, or is asked to log in, or is asked for anything beyond an email address and preferences, it fails 16 CFR 316.5. One page, and the page must do the work.
5. **Watch the unsubscribe request in devtools.** Open the Network panel on the unsubscribe page. Confirm the request returns 2xx and that the page does not depend on a session cookie the recipient will not have. Open it in a private window with no session to prove that.
6. **Check the List-Unsubscribe headers.** In the raw source, look for `List-Unsubscribe:` and `List-Unsubscribe-Post: List-Unsubscribe=One-Click`. Not required by CAN-SPAM, required by Gmail for bulk senders. See Notes.
7. **Test the opt-out end to end, then send again.** Unsubscribe, then trigger another campaign to that address. It must not arrive. Do this before launch, because discovering a broken suppression path after a 40,000-message send is not recoverable.
8. **Confirm the unsubscribe URL survives campaign teardown.** Take an unsubscribe URL from a message sent 30-plus days ago in the client's existing history, if any, and load it. If it 404s, the 30-day rule is being broken structurally.
9. **Read the subject lines as a batch.** Export the campaign subject lines and read them in one sitting. Deception is easier to spot in a list than in a single message. Flag anything with "Re:", "Fwd:", a fake personal-reply framing, or a claim the body does not support.
10. **Check the ad disclosure on any list without a consent record.** If the client cannot show how an address joined the list, that address needs the advertisement disclosure. Purchased and scraped lists always need it.
11. **Verify suppression applies across tools.** If the client uses more than one sending system (marketing ESP plus a CRM plus a transactional provider), unsubscribe in one and confirm the address is suppressed in all of them that send commercial mail.

---

## Penalties

**Civil penalty, FTC: up to $53,088 per email.**

The chain matters, because vendor blogs quote this figure without it. A CAN-SPAM violation is treated as an unfair or deceptive act or practice proscribed under section 18(a)(1)(B) of the FTC Act (15 U.S.C. 7706(a)). Civil penalties for rule violations are set by FTC Act section 5(m)(1)(A), and the current inflation-adjusted amount is codified at 16 CFR 1.98(d) as **$53,088**, effective January 17, 2025.

**That figure is still current on 2026-07-20, and the reason is worth knowing.** The FTC normally re-adjusts every January. There was no 2026 adjustment. OMB Memorandum M-26-11 (April 17, 2026) cancelled it: the annual adjustment must be calculated from October CPI-U data, the government shutdown meant BLS never produced October 2025 data, and OMB concluded it had no statutory authority to substitute another method. Agencies were directed to "continue using the 2025 civil monetary penalty levels". So $53,088 is a 2025 number that remains operative through 2026. Expect a jump in January 2027 if October 2026 CPI-U data publishes normally.

The FTC treats each non-compliant message as a separate violation, so exposure scales with list size rather than with campaign count.

**Other routes:**

| Who | What they can recover | Source |
|---|---|---|
| State attorneys general | Up to $250 per violation (each message counts separately), capped at $2,000,000 in aggregate for violations other than header falsity under 7704(a)(1). Court may treble for willful and knowing violations or aggravated violations | 15 U.S.C. 7706(f) |
| Providers of Internet access service | Up to $100 per violation for header falsity under 7704(a)(1), up to $25 per violation for anything else, capped at $1,000,000 aggregate excluding 7704(a)(1). Trebling available on the same terms | 15 U.S.C. 7706(g) |
| DOJ, criminal | Sexually oriented material sent without the prescribed subject-line label carries fines under Title 18 or imprisonment up to 5 years, or both | 15 U.S.C. 7704(d)(5) |

**Largest CAN-SPAM penalty on record: $2.95 million.** Verkada, a security camera company, settled with the FTC on August 30, 2024. The CAN-SPAM allegations were sending commercial email without an unsubscribe option, failing to honor opt-out requests, and omitting a physical postal address. The FTC described it as the largest penalty it has obtained for a CAN-SPAM violation. This is a useful case to cite to a client, because the three failures are the three cheapest things on the list to get right.

Earlier reference point: Experian Consumer Services paid a $650,000 civil penalty in 2023 over marketing email that gave recipients no way to opt out. UNVERIFIED: that figure and date come from law-firm summaries; the FTC's own release was not retrievable during this review.

---

## Common ways sites fail this

- **The footer address is missing from one template.** Rarely all of them. It is the third email in a drip sequence, or the re-engagement campaign someone built in a hurry, or a template cloned before the address was added.
- **The client works from home and refuses to publish their address.** Legitimate concern, wrong resolution. Skipping the address is a violation. Register a USPS PO Box or a CMRA mailbox and use that. Budget for it at intake.
- **Unsubscribe requires a login.** Common on membership sites where the developer reused the account-preferences page as the unsubscribe target. Directly violates 16 CFR 316.5, because the recipient is being made to provide information beyond their email address.
- **Unsubscribe leads to a preference center with no "unsubscribe from everything" option.** The Act requires an option to stop all commercial email from that sender. A menu of categories with no global off switch fails.
- **Multi-step unsubscribe.** Click, then a confirmation page, then "are you sure", then a survey. More than a single web page fails.
- **Opt-outs processed on a slower cadence than the law allows.** A weekly or monthly sync between the CRM and the ESP quietly exceeds 10 business days when it fails once.
- **Suppression lost during a migration.** The client moves ESPs, imports the active list, leaves the unsubscribe list behind, and re-mails everyone who ever opted out. This produces spam complaints, a deliverability collapse, and per-message liability at the same time.
- **A purchased list gets emailed with no advertisement disclosure.** Buying a list is not itself unlawful under CAN-SPAM, which surprises people. Emailing it without the ad disclosure, an address, and a working opt-out is.
- **Fake "Re:" subject lines,** usually introduced by a growth consultant after handover, not by the studio.
- **Someone assumes CAN-SPAM covers the whole list.** It covers the US portion. The Canadian and EU addresses on the same list are governed by stricter regimes and the send goes out under the loosest one.
- **A transactional email gets a promotional subject line,** converting it into a commercial message that now needs a footer it does not have.

---

## Sources

Official sources first. All retrieved 2026-07-20.

- [15 U.S.C. 7704, Other protections for users of commercial electronic mail](https://www.law.cornell.edu/uscode/text/15/7704) (Cornell LII mirror of the US Code), retrieved 2026-07-20. Header, subject line, opt-out mechanism, 30-day and 10-business-day rules, transfer ban, advertisement disclosure, postal address, aggravated violations.
- [15 U.S.C. 7702, Definitions](https://www.law.cornell.edu/uscode/text/15/7702), retrieved 2026-07-20. Commercial message, transactional or relationship message, sender, initiate, affirmative consent.
- [15 U.S.C. 7706, Enforcement generally](https://www.law.cornell.edu/uscode/text/15/7706), retrieved 2026-07-20. FTC Act section 18(a)(1)(B) treatment, State AG and internet access service provider damages and caps.
- [15 U.S.C. 7707, Effect on other laws](https://www.law.cornell.edu/uscode/text/15/7707), retrieved 2026-07-20. Preemption and the falsity and deception carve-out.
- [15 U.S.C. 7713, Effective date](https://www.law.cornell.edu/uscode/text/15/7713), retrieved 2026-07-20. Effective January 1, 2004 per section 16 of Pub. L. 108-187.
- [16 CFR 316.2, Definitions](https://www.law.cornell.edu/cfr/text/16/316.2), retrieved 2026-07-20. Sender, single-sender designation, person, valid physical postal address.
- [16 CFR 316.3, Primary purpose](https://www.law.cornell.edu/cfr/text/16/316.3), retrieved 2026-07-20. Mixed-content tests.
- [16 CFR 316.5, Prohibition on charging a fee or imposing other requirements on recipients who wish to opt out](https://www.law.cornell.edu/cfr/text/16/316.5), retrieved 2026-07-20.
- [16 CFR 1.98, Adjustment of civil monetary penalty amounts](https://www.law.cornell.edu/cfr/text/16/1.98), retrieved 2026-07-20. Paragraphs (d) and (e): FTC Act section 5(m)(1)(A) and (B) at $53,088, effective January 17, 2025.
- [OMB Memorandum M-26-11, Cancellation of Penalty Inflation Adjustments for 2026](https://www.whitehouse.gov/wp-content/uploads/2026/04/M-26-11-Cancellation-of-Penalty-Inflation-Adjustments-for-2026-Regarding-the-Federal-Civil-Penalties-Inflation-Adjustment-Act-Improvements-Act-of-2015.pdf) (PDF), April 17, 2026, retrieved 2026-07-20. Primary source for why the 2025 penalty figure still applies in 2026.
- [FTC, CAN-SPAM Act: A Compliance Guide for Business](https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business). The FTC's plain-language guide and the best thing to hand a client. NOTE: this URL returned HTTP 403 to automated retrieval on 2026-07-20, so nothing in this file rests on it. It loads normally in a browser.
- [FTC, FTC Approves New Rule Provision Under The CAN-SPAM Act](https://www.ftc.gov/news-events/news/press-releases/2008/05/ftc-approves-new-rule-provision-under-can-spam-act), May 2008. The discretionary rule effective July 7, 2008. Returned HTTP 403 to automated retrieval on 2026-07-20, as ftc.gov does for all three FTC links in this list. The rule date is instead confirmed by the Part 316 source note, 73 FR 29677, May 21, 2008.
- [FTC, FTC Takes Action Against Security Camera Firm Verkada](https://www.ftc.gov/news-events/news/press-releases/2024/08/ftc-takes-action-against-security-camera-firm-verkada-over-charges-it-failed-secure-videos-other), August 30, 2024. Returned HTTP 403 to automated retrieval on 2026-07-20; the $2.95 million figure below was confirmed via the Hunton summary named next.
- [Hunton Andrews Kurth, FTC Announces Proposed Settlement with Security Camera Firm](https://www.hunton.com/privacy-and-information-security-law/ftc-announces-proposed-settlement-with-security-camera-firm-over-alleged-data-security-failures-and-can-spam-violations), retrieved 2026-07-20. Verkada $2.95 million, largest CAN-SPAM penalty.
- [Google, Email sender guidelines](https://support.google.com/a/answer/81126), retrieved 2026-07-20. Bulk sender threshold, spam rate, one-click unsubscribe headers. Not law, see Notes.

---

## Notes

**Opt-out versus opt-in is the whole story, and it is where multi-country lists go wrong.** CAN-SPAM lets you send a first commercial email to a US recipient with no prior permission, as long as the message is honest and offers a working exit. [`casl-canada`](casl-canada.md) does not: Canada requires express or implied consent before the first message, and it carries personal liability for directors and officers. [`gdpr`](gdpr.md) plus the ePrivacy rules in [`eprivacy-cookies`](eprivacy-cookies.md) generally require prior consent for marketing email to EU individuals, with a narrow soft-opt-in for existing customers on similar products. A single list containing US, Canadian, and EU addresses must be sent under the strictest applicable rule per recipient, or segmented by jurisdiction. The default assumption for any client with a mixed list should be: build to CASL and GDPR, and CAN-SPAM takes care of itself. The reverse never holds.

**A US-only client can still get caught.** Anyone can type a Canadian or EU address into a signup form. If the client has any international audience, capture country at signup or accept that the list is mixed.

**Preemption is narrower than clients think.** Section 7707(b) supersedes state statutes that expressly regulate commercial email, but it expressly preserves state law "to the extent that any such statute, regulation, or rule prohibits falsity or deception in any portion of a commercial electronic mail message". State trespass, contract, tort, fraud, and computer crime laws are also untouched. A deceptive subject line can therefore draw a state-law claim on top of the federal one. Several states have anti-spam falsity statutes that survive on this carve-out and have supported private litigation. UNVERIFIED: the specific state statutes and their current litigation posture were not researched for this file. If a client is running high-volume cold email, that is a research task and probably a counsel question.

**Gmail and Yahoo enforce more than the law does, and they enforce it faster.** Google's published sender guidelines require, for senders of more than 5,000 messages per day to Gmail accounts, a spam complaint rate below 0.30% in Postmaster Tools and support for one-click unsubscribe via the `List-Unsubscribe` and `List-Unsubscribe-Post: List-Unsubscribe=One-Click` headers (RFC 2369 and RFC 8058). None of this is statute, and a mailbox provider cannot fine anyone. It can stop delivering the client's mail, which for most clients is the more immediate loss. Build to these headers by default. UNVERIFIED: widely repeated claims that Gmail requires unsubscribes be honored within two days were not confirmed on Google's own page during this review; the retrieved page states no deadline. The statutory 10-business-day maximum is the number to design against, and immediate suppression satisfies both.

**One-click unsubscribe headers and CAN-SPAM interact well.** RFC 8058 one-click satisfies the single-web-page rule comfortably, since the recipient takes no steps at all. If the ESP supports it, turning it on improves both compliance posture and deliverability.

**The 10-business-day window is a ceiling, not a service level.** Nothing prevents immediate suppression, every ESP supports it, and the only reason a project ends up relying on the full window is a batch sync somebody chose. Argue for immediate suppression at build time.

**Watch for the statute going stale.** The core of CAN-SPAM has not changed since 2003 and the implementing rule has not changed substantively since 2008, which makes this one of the more stable files in this directory. The volatile part is the penalty figure. Re-check 16 CFR 1.98 every January, and note that January 2027 is likely to bring the adjustment that January 2026 skipped.

**Related files:** [`casl-canada`](casl-canada.md) for the opt-in contrast, [`gdpr`](gdpr.md) for EU marketing consent, [`ftc-disclosures`](ftc-disclosures.md) for what the email content itself may claim (endorsements, affiliate links, pricing), [`us-state-privacy-laws`](us-state-privacy-laws.md) and [`ccpa-cpra`](ccpa-cpra.md) for the separate question of whether the email address may be shared or sold at all.
