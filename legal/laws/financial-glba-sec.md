# Financial services: GLBA Safeguards and Privacy Rules, SEC Regulation S-P, the SEC Marketing Rule, Regulation FD, FINRA Rule 2210, and Truth in Lending advertising

| Field | Value |
|---|---|
| **Jurisdiction** | United States, federal. Applies to the business, not the visitor. A US financial institution is caught regardless of where its site visitors sit. A non-US firm is caught if it is SEC-registered, FINRA-member, or offers consumer credit to US consumers |
| **Regulator / enforcer** | FTC (Safeguards Rule, for non-bank financial institutions outside another regulator's jurisdiction). SEC (Regulation S-P, Marketing Rule, Regulation FD). FINRA (Rule 2210, for broker-dealer members). CFPB (Regulation P privacy notices, Regulation Z / TILA advertising). Federal banking agencies and state insurance authorities for their own sectors. State attorneys general under state UDAP and state securities law |
| **In force since** | GLBA: 12 November 1999. FTC Safeguards Rule as overhauled: 10 January 2022, with the bulk of the technical controls applicable 9 June 2023. Safeguards breach notification: 13 May 2024. SEC Marketing Rule compliance date: 4 November 2022. Regulation FD: 23 October 2000. Reg S-P incident response and customer notification: 3 December 2025 (larger entities) and 3 June 2026 (smaller entities). TILA: 1968 |
| **Last amended** | SEC Regulation S-P amendments published 3 June 2024 (89 FR 47688), effective 2 August 2024. FTC Safeguards Rule last amended 13 November 2023 (88 FR 77499), effective 13 May 2024 |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. Every regime in this file is live as of 2026-07-20, including both Reg S-P compliance tiers, the later of which passed on 3 June 2026 |

---

## Read this before anything else: the brief contains a common error

**Regulation FD does not apply to investment advisers as a regulated party.** Regulation FD binds
*issuers* that have a class of securities registered under section 12 of the Exchange Act or are
required to file reports under section 15(d) (17 CFR 243.101(b)). Investment advisers appear in
Regulation FD only as *recipients*: they are on the list of persons to whom an issuer may not
selectively disclose material nonpublic information (17 CFR 243.100(b)(1)(ii)).

If a studio is building a site for a registered investment adviser, Regulation FD is not the
governing rule. The Marketing Rule is. Regulation FD becomes relevant only when the client is a
public company and the build touches its investor relations pages. Both are covered below,
separately, because they attach to different clients.

---

## The instruments in this file

Seven separate regimes. They attach to different client types. Read the scope column before
assuming any of them applies.

| Instrument | Citation | Who it binds | Site-visible? |
|---|---|---|---|
| GLBA Safeguards Rule | 16 CFR Part 314 | Non-bank financial institutions under FTC jurisdiction | Mostly backend, plus breach notice |
| GLBA privacy notices (CFPB) | Regulation P, 12 CFR Part 1016 | Financial institutions under CFPB jurisdiction | Yes: a privacy notice document |
| GLBA privacy notices (SEC) | Regulation S-P, 17 CFR Part 248 Subpart A | Broker-dealers, investment companies, registered advisers, transfer agents, funding portals | Yes: a privacy notice document |
| GLBA privacy notices (FTC) | 16 CFR Part 313 | Motor vehicle dealers only, per 12 U.S.C. 5519 | Yes, for auto dealer clients |
| Reg S-P safeguards and incident response | 17 CFR 248.30 | Same SEC-registered set as above | Backend, plus a 30-day customer notice |
| SEC Marketing Rule | 17 CFR 275.206(4)-1 | SEC-registered investment advisers | Yes: nearly every page |
| Regulation FD | 17 CFR Part 243 | Issuers with section 12 registered securities or section 15(d) reporting duties | Yes: IR pages, earnings, webcasts |
| FINRA Rule 2210 | FINRA Rule 2210 | FINRA member broker-dealers | Yes: nearly every page |
| TILA advertising | Regulation Z, 12 CFR 1026.16 and 1026.24 | Creditors advertising consumer credit | Yes: every rate, payment, and fee shown |

---

## Applies when

Answer these at intake. Each yes pulls in the matching section below.

### GLBA Safeguards Rule (16 CFR Part 314)

The definition of "financial institution" here is far wider than banks. 16 CFR 314.2(h) adopts
the Bank Holding Company Act section 4(k) test: any institution whose business is an activity
"financial in nature or incidental to such financial activities". The rule's own examples include:

- Mortgage brokers ("brokering loans is a financial activity")
- Auto dealers that lease vehicles on a non-operating basis for longer than 90 days
- Tax preparation services
- Real and personal property appraisers
- Finders ("acting as a finder is an activity that is financial in nature")
- Credit counselors and investment advisory services
- Career counselors specializing in finance, accounting, or audit placements
- Travel agencies operated in connection with financial services

Also check:

- Does the client collect any record containing nonpublic personal information about a consumer who obtains a financial product or service for personal, family, or household purposes? That is "customer information" under 16 CFR 314.2(d).
- Is the client outside the enforcement authority of another regulator under GLBA section 505? 16 CFR 314.1(b) applies the rule to financial institutions "over which the Federal Trade Commission has jurisdiction", and excludes institutions subject to another section 505 regulator. A broker-dealer or SEC-registered adviser follows Reg S-P instead, not Part 314. A bank follows its banking agency's rules.
- **Record count threshold:** 16 CFR 314.6 states verbatim that "Section 314.4(b)(1), (d)(2), (h), and (i) do not apply to financial institutions that maintain customer information concerning fewer than five thousand consumers." Everything else in 314.4 applies at any size. There is no floor for encryption, MFA, access control, or breach notification.
- **Breach notification threshold:** 16 CFR 314.4(j) triggers at a notification event involving at least 500 consumers.

### GLBA privacy notices

- Does the client have "customers" (a consumer with a continuing relationship) rather than one-off consumers? A customer relationship triggers an initial notice and, subject to the exception, an annual notice.
- Which regulator's version applies? CFPB Regulation P (12 CFR Part 1016) for most non-bank financial institutions; SEC Regulation S-P (17 CFR Part 248) for broker-dealers, investment companies, registered advisers, transfer agents, and funding portals; FTC 16 CFR Part 313 only for motor vehicle dealers described in 12 U.S.C. 5519. 16 CFR 313.1(b) is explicit that the FTC's privacy rule now reaches only "persons described in 12 U.S.C. 5519 that are predominantly engaged in the sale and servicing of motor vehicles, the leasing and servicing of motor vehicles, or both".
- Does the client share nonpublic personal information with nonaffiliated third parties outside the 1016.13, 1016.14, and 1016.15 exceptions? If yes, an opt-out notice and mechanism are required and the annual notice exception is lost.

### SEC Regulation S-P incident response (17 CFR 248.30)

- Is the client a broker, dealer, investment company, SEC-registered investment adviser, funding portal, or registered transfer agent? Note that 17 CFR 248.3(r) reaches investment companies whether or not registered, so business development companies are caught, while private funds relying on section 3(c)(1) or 3(c)(7) are not.
- Compliance is already required for every tier. The release provided an 18-month compliance period for larger entities and 24 months for smaller entities, measured from the 3 June 2024 publication date. That computes to 3 December 2025 and 3 June 2026 respectively.
- "Larger entity" per Table 3 of the adopting release: investment companies with net assets of $1 billion or more as of the most recent fiscal year end (counted with other funds in the same group of related investment companies); registered investment advisers with $1.5 billion or more in assets under management; all broker-dealers and all transfer agents that are not small entities under the Exchange Act for Regulatory Flexibility Act purposes.

### SEC Marketing Rule (17 CFR 275.206(4)-1)

- Is the client registered, or required to be registered, with the SEC as an investment adviser? State-registered advisers follow state rules, which in most states track the Marketing Rule but are not identical. Confirm the client's registration status from Form ADV before building.
- Does the site contain any communication "to more than one person" offering advisory services? That is an advertisement under 17 CFR 275.206(4)-1(e)(1). A public marketing website is an advertisement in essentially all of its content.
- Does the site contain hypothetical performance of any kind? A communication to even one person is an advertisement if it contains hypothetical performance.
- Does the site display client quotes, endorsements, third-party ratings, awards, "as seen in" logos, or a referral or solicitor arrangement?
- Does the site display any performance figures, backtests, model portfolios, projected returns, or a returns calculator?

### Regulation FD (17 CFR Part 243)

- Does the client have a class of securities registered under section 12 of the Exchange Act, or is it required to file reports under section 15(d)? Closed-end investment companies are included. Other investment companies and foreign private issuers are excluded.
- Does the build touch investor relations pages, earnings releases, webcast infrastructure, an investor email list, or a company social media account used for financial information?

### FINRA Rule 2210

- Is the client a FINRA member broker-dealer, or is any registered representative's content going on the site?
- Will any written or electronic communication be made available to more than 25 retail investors within any 30 calendar-day period? That makes it a "retail communication" under FINRA Rule 2210(a)(5). 25 or fewer is "correspondence". A public website is always a retail communication.
- Has the firm been a FINRA member for less than one year? New members must file retail communications used in electronic or other public media with FINRA at least 10 business days before first use, for the first year of membership.

### TILA / Regulation Z advertising (12 CFR 1026.16 and 1026.24)

- Does the site advertise consumer credit? This covers mortgage lenders and brokers, personal loan lenders, auto finance, credit cards, HELOCs, and buy-now-pay-later products structured as credit.
- Does any page state a rate, an APR, a monthly payment, a downpayment, a number of payments, a repayment period, or a finance charge amount? Those are the closed-end triggering terms in 12 CFR 1026.24(d)(1).
- Is the credit secured by a dwelling? That pulls in 12 CFR 1026.24(f) and the prohibited practices in 1026.24(i).
- Is it open-end credit (a card or a HELOC)? That routes to 12 CFR 1026.16 instead of 1026.24.

---

## What the site must have

### GLBA Safeguards Rule: 16 CFR 314.4 elements

Most of this is infrastructure rather than page content. A studio that builds and hosts the site
is frequently a "service provider" under 16 CFR 314.2(r) and inherits contract obligations.

| Requirement | What that means in the build |
|---|---|
| Qualified individual, 314.4(a) | A named person responsible for the security program. May be at a service provider, but the client keeps responsibility and must designate senior personnel to oversee. Put the name in the project record |
| Written risk assessment, 314.4(b) | Written, with stated evaluation criteria and mitigation. 314.4(b)(1) is waived below 5,000 consumers, the duty to assess risk is not |
| Access controls, 314.4(c)(1) | Least privilege. Every CMS role, database user, and admin account limited to the customer information that role needs. Periodic review, not a one-time setup |
| Data inventory, 314.4(c)(2) | An actual list of the data, systems, devices, and facilities holding customer information. Includes the form plugins, the CRM, the analytics warehouse, the backup bucket |
| Encryption, 314.4(c)(3) | All customer information encrypted in transit over external networks **and at rest**. TLS alone is half the requirement. Database and backup encryption is the other half. A written compensating-control approval from the qualified individual is the only alternative |
| Secure development, 314.4(c)(4) | Secure development practices for in-house applications, and an evaluation procedure for any third-party application that transmits, accesses, or stores customer information. That includes the form plugin and the chat widget |
| Multi-factor authentication, 314.4(c)(5) | MFA for **any individual accessing any information system**, which includes non-admin accounts. CMS logins, hosting panel, database console, VPN. Only a written alternative approved by the qualified individual excuses it |
| Disposal, 314.4(c)(6) | Delete customer information no later than two years after the last date it was used, unless a business or legal reason requires keeping it. Build the deletion job, do not leave form submissions in the database forever |
| Change management, 314.4(c)(7) | Documented procedures for changes to systems holding customer information |
| Monitoring and logging, 314.4(c)(8) | Log authorized user activity and detect unauthorized access or use. Ship application and access logs somewhere they are retained and reviewed |
| Testing, 314.4(d) | Continuous monitoring, or annual penetration testing plus vulnerability assessments at least every six months and after any material change. 314.4(d)(2) is waived below 5,000 consumers |
| Training, 314.4(e) | Security awareness training kept current against the risk assessment, plus qualified security personnel |
| Service providers, 314.4(f) | Reasonable steps to select and retain capable providers, **contractual** safeguard requirements, and periodic reassessment. If the studio hosts the site, the studio signs one of these |
| Incident response plan, 314.4(h) | A written plan covering goals, internal processes, roles, communications, remediation, documentation, and revision. Waived below 5,000 consumers |
| Board report, 314.4(i) | Written report from the qualified individual to the board at least annually. Waived below 5,000 consumers |
| Breach notification, 314.4(j) | On discovering a notification event involving at least 500 consumers, notify the FTC as soon as possible and no later than 30 days after discovery. Build the internal path that gets this to counsel fast |

The 314.4(j) notice must contain the institution's name and contact information, a description of
the types of information involved, the date or date range if determinable, the number of consumers
affected or potentially affected, a general description of the event, and whether a law enforcement
official has provided a written determination that public disclosure would impede an investigation.
The FTC stated in the adopting release that it "intends to enter notification event reports into a
publicly available database". Treat a Safeguards breach report as public.

A law enforcement official may request an initial delay of up to 30 days from the date notice was
given to the FTC, extendable by up to a further 60 days in writing.

### GLBA privacy notices

| Requirement | What that means in the build |
|---|---|
| Initial privacy notice | Clear and conspicuous notice not later than when the customer relationship is established (12 CFR 1016.4). Build it as a real page with a stable URL, not a PDF buried in a footer |
| Content per 1016.6 | Categories of nonpublic personal information collected and disclosed, categories of nonaffiliated third parties, the opt-out right and how to exercise it, and the security and confidentiality policies |
| Annual notice | Required at least once in any 12 consecutive month period during the relationship (12 CFR 1016.5), **unless** the exception applies |
| Annual notice exception | Both conditions must hold: the institution shares nonpublic personal information with nonaffiliated third parties only under 12 CFR 1016.13, 1016.14, or 1016.15, and it has not changed its disclosure policies and practices from what was last disclosed. Most small advisory and brokerage clients qualify. If the exception is lost, an annual notice is due within 100 days of the change |
| Opt-out notice and method | Required wherever sharing goes beyond those exceptions (12 CFR 1016.7). Build a working opt-out, not a mailto |
| **Delivery, and the part studios get wrong** | 12 CFR 1016.9(a) requires delivery "so that each consumer can reasonably be expected to receive actual notice". 1016.9(b) states that to "only post a sign in your branch or office or generally publish advertisements" does **not** satisfy this. Posting the notice on the website is sufficient only where the consumer conducts the transaction electronically and the site requires the consumer to acknowledge receipt as a necessary step to obtaining the product or service |
| Annual notice by continuous posting | Permitted only where the customer uses the website to access financial products and services electronically, agrees to receive notices at the website, and the current notice is posted continuously in a clear and conspicuous manner (12 CFR 1016.9(c)) |
| Oral delivery | Prohibited. 12 CFR 1016.9(d) bars providing any required notice solely by oral explanation |

The practical build consequence: a linked privacy notice in the footer is not delivery. If the
site opens accounts or takes applications, the notice needs an acknowledgement checkbox or
equivalent gate inside the flow, and the acknowledgement needs to be logged.

### SEC Regulation S-P incident response (17 CFR 248.30)

| Requirement | What that means in the build |
|---|---|
| Written safeguards policies | Administrative, technical, and physical safeguards for customer information |
| Incident response program | Written, reasonably designed to detect, respond to, and recover from unauthorized access to or use of customer information. Must include procedures to assess nature and scope, contain and control the incident, and notify affected individuals |
| Customer notification | Where sensitive customer information was or is reasonably likely to have been accessed or used without authorization, notify affected individuals as soon as practicable and **no later than 30 days** after becoming aware. Build the templates and the affected-customer query before you need them |
| Notice contents | A description of the incident and the type of sensitive information involved, the date or estimated date, contact information including a toll-free number, email, and postal address, a recommendation to review account statements, an explanation of fraud alerts, guidance on obtaining credit reports, and a reference to FTC identity theft resources |
| Service provider notification | The covered institution must require service providers to notify it **no later than 72 hours** after becoming aware that a breach in security has occurred. If the studio hosts or processes, this clause lands in the studio's contract |
| Law enforcement delay | The Attorney General may delay notice up to 30 days, then a further 30 days, then up to 60 days in extraordinary circumstances involving national security |
| Recordkeeping | Written records documenting compliance. Retention for investment companies and comparable entities is not less than six years, the first two in an easily accessible place |

"Sensitive customer information" is defined in the rule as any component of customer information
whose compromise "could create a reasonably likely risk of substantial harm or inconvenience to an
individual identified with the information", with examples including Social Security numbers,
government identification numbers, biometric records, and unique electronic identification numbers
or routing codes.

### SEC Marketing Rule (17 CFR 275.206(4)-1)

This one shapes almost every page of an adviser's site.

| Requirement | What that means in the build |
|---|---|
| No untrue or unsubstantiated statements, 206(4)-1(a)(1) and (a)(2) | Every claim on the site needs a reasonable basis the adviser can demonstrate to the SEC on demand. "Award-winning", "top-ranked", "consistently outperform" all need backup on file |
| Fair and balanced treatment of risks, 206(4)-1(a)(4) | Any page discussing potential benefits must give fair and balanced treatment of material risks or limitations. A benefits list with no risk treatment fails. Risk language cannot live only on a separate disclosures page |
| Specific investment advice, 206(4)-1(a)(5) | References to specific past recommendations must be fair and balanced. Do not build a "our best calls" section |
| Performance presented fair and balanced, 206(4)-1(a)(6) | No cherry-picked windows, no excluding losing periods |
| **Testimonials and endorsements: disclosure, 206(4)-1(b)(1)** | Clearly and prominently disclose whether the person giving it is a current client or investor or is not, whether cash or non-cash compensation was provided, and a brief statement of any material conflicts of interest. "Clearly and prominently" means the disclosure sits with the testimonial, in the same visual block, at the same weight. A footnote, a hover tooltip, an asterisk to the footer, or a separate disclosures page all fail |
| Testimonials: oversight and written agreement, 206(4)-1(b)(2) | The adviser must have a reasonable basis for believing the testimonial complies, 206(4)-1(b)(2)(i), and a written agreement with the person describing the scope of the agreed-upon activities and the terms of compensation, 206(4)-1(b)(2)(ii). The written agreement and the disqualification provision are excused by the de minimis exemption in 206(4)-1(b)(4)(i), where total compensation is **$1,000 or less (or the equivalent value in non-cash compensation) during the preceding twelve months** |
| Testimonials: disqualification, 206(4)-1(b)(3) | The adviser may not compensate an "ineligible person" for a testimonial or endorsement. Run the check before the quote goes on the page |
| Third-party ratings, 206(4)-1(c) | The adviser must have a reasonable basis for believing the underlying questionnaire or survey was structured to make it equally easy to give favorable and unfavorable responses. The site must clearly and prominently disclose the date of the rating, the period it covers, the identity of the third party, and any compensation the adviser paid. This catches every "Top Financial Advisor 2026" badge in a footer |
| **Net alongside gross performance, 206(4)-1(d)(1)** | Gross performance may not appear unless net performance appears with at least equal prominence, calculated over the same time period and using the same methodology. A gross-only chart is a violation |
| Prescribed time periods, 206(4)-1(d)(2) | Performance results must include one, five, and ten year periods, each presented with equal prominence, ending on a date no less recent than the most recent calendar year end. Build the chart component to render all three or none |
| No implied SEC approval, 206(4)-1(d)(3) | Never state or imply that the SEC approved or reviewed the performance calculation or presentation |
| Hypothetical performance, 206(4)-1(d)(6) | Backtests, model portfolios, projected or target returns, and interactive return calculators are hypothetical performance. Requires policies and procedures for the intended audience, plus disclosure of the criteria used, the assumptions made, and the risks and limitations. Practically: do not put a returns projector on a public marketing page |
| Related, extracted, and predecessor performance, 206(4)-1(d)(4), (d)(5), (d)(7) | Related performance must include all related portfolios unless exclusion does not materially alter the result. Extracted performance requires the total portfolio results. Predecessor performance requires the same managers and sufficiently similar accounts |
| Recordkeeping, 17 CFR 275.204-2 | Copies of all advertisements disseminated, 204-2(a)(11). Substantiation that testimonials, endorsements, and third-party ratings comply, 204-2(a)(15). All accounts, books, internal working papers, and documents necessary to form the basis for or demonstrate the calculation of any performance or rate of return, 204-2(a)(16). Retained **not less than five years, the first two in an appropriate office of the adviser** (204-2(e)) |

The recordkeeping duty has a direct build consequence: every published version of every marketing
page is a record. Version control the marketing site and keep the deployment history. A CMS that
overwrites without history destroys required records.

### Regulation FD (public company clients only)

| Requirement | What that means in the build |
|---|---|
| Simultaneous disclosure for intentional selective disclosure | If the issuer intentionally discloses material nonpublic information to a covered recipient, public disclosure must be simultaneous (17 CFR 243.100(a)(1)) |
| Prompt disclosure for non-intentional | Where it was not intentional, public disclosure must be "prompt", defined in 17 CFR 243.101(d) as as soon as reasonably practicable and in no event after the later of 24 hours or the commencement of the next day's trading on the New York Stock Exchange |
| Method of public disclosure | Furnishing or filing a Form 8-K, or another method reasonably designed to provide broad, non-exclusionary distribution (17 CFR 243.101(e)) |
| **IR page build consequences** | Press releases and earnings materials publish at the same instant they go to the wire. No staged or embargoed publication where a subset of visitors can reach the URL early. No sequential-ID or guessable URLs for unpublished releases. No CDN cache that serves a draft. No password-gated analyst area holding material information the public pages lack |
| Webcasts | An open-access webcast with advance public notice and free access is the standard approach. Do not build an analyst-only dial-in for material information |
| Archive | Keep prior releases and webcast replays reachable, since selective removal can itself skew the information available |

### FINRA Rule 2210 (broker-dealer clients)

| Requirement | What that means in the build |
|---|---|
| Principal approval before use | An appropriately qualified registered principal must approve each retail communication **before the earlier of its use or filing** (Rule 2210(b)(1)). A public web page is a retail communication. Nothing ships to production before principal sign-off. Build the approval gate into the deploy process, not into a Slack thread |
| Record of approval | Retain a copy of the communication, the dates of first and last use, the name of the approving principal and the date of approval, the name of the preparer or distributor if not pre-approved, and the source of any statistical table, chart, graph, or other illustration |
| Retention period | Per SEA Rule 17a-4(b), which sets **three years, the first two in an easily accessible place**, for communications relating to the business. FINRA Rule 4511 sets six years for records with no otherwise specified period. Site content archives must survive redesigns |
| Filing with FINRA | New members file retail communications used in electronic or other public media at least 10 business days before first use, for one year from the date membership became effective. Certain categories (custom investment company performance rankings, security futures materials) file at least 10 business days prior to first use. Others (registered investment company communications, public direct participation programs, collateralized mortgage obligations, derivative securities) file within 10 business days of first use |
| Content standards, Rule 2210(d)(1) | Fair and balanced, based on principles of fair dealing and good faith, providing a sound basis for evaluating the facts. No omission of a material fact or qualification that would make the communication misleading |
| **No projections** | Communications "may not predict or project performance, imply that past performance will recur or make any exaggerated or unwarranted claim". This kills growth projectors, "your portfolio in 10 years" calculators, and forward-looking return charts on retail pages |
| BrokerCheck link, Rule 2210(d)(8) | A readily apparent reference and hyperlink to BrokerCheck on the initial web page the firm intends to be viewed by retail investors, and on any web page that includes a professional profile of a registered person |
| Social media and interactive forums | Real-time interactive electronic forums are excluded from the pre-approval requirement but remain subject to supervision comparable to correspondence. Static social profile content and pinned posts are retail communications and do need pre-approval |

### TILA / Regulation Z advertising

| Requirement | What that means in the build |
|---|---|
| Actually available terms, 1026.24(a) and 1026.16(a) | State only terms the creditor actually offers or will arrange. No illustrative rates that nobody can get |
| Clear and conspicuous, 1026.24(b) | Applies to every required disclosure in the ad |
| APR required, 1026.24(c) | If a rate of finance charge is stated, it must be stated as an "annual percentage rate", using that term. If the rate may increase after consummation, say so. Any simple annual or periodic rate shown must be less conspicuous than the APR |
| **Closed-end triggering terms, 1026.24(d)(1)** | Four triggers: "the amount or percentage of any downpayment", "the number of payments or period of repayment", "the amount of any payment", "the amount of any finance charge". Stating any one of them requires the full set of additional disclosures |
| Additional disclosures once triggered, 1026.24(d)(2) | The amount or percentage of the downpayment, the terms of repayment reflecting the repayment obligations over the full term including any balloon payment, and the annual percentage rate with a note if it may increase after consummation |
| Dwelling-secured rates and payments, 1026.24(f) | Where more than one simple annual rate applies, disclose each rate, the period it applies, and the APR, with equal prominence and in close proximity to the advertised rate. Where payment amounts are stated, disclose each payment amount over the term including any balloon, and for first-lien dwellings state that the payments do not include taxes and insurance and that the actual obligation is greater |
| Multi-page and electronic ads, 1026.24(e) | A multi-page or electronic ad counts as a single ad only if the credit terms table is clear and conspicuous and other statements of terms cross-reference where the table begins. A one-page site with rates in a hero and disclosures three scrolls down does not automatically qualify |
| Prohibited practices, dwelling-secured, 1026.24(i) | No calling a variable rate "fixed" without the prescribed ARM labeling; no misleading comparisons to rates available for less than the full term; no false claims of government endorsement; no using the consumer's current lender's name without equal-prominence identification of the advertiser and a clear statement of non-affiliation; no misleading debt-elimination claims; no calling a for-profit broker or creditor a "counselor"; no providing trigger terms or required disclosures only in a foreign language while providing other required information only in English |
| Open-end triggering terms, 1026.16(b) | Any term required by 1026.6(b)(3), stated affirmatively or negatively, triggers disclosure of any minimum, fixed, transaction, activity or similar finance charge, any periodic rate expressed as an APR with a variable-rate note, and any membership or participation fee |
| Home equity plans, 1026.16(d) | Loan fees expressed as a percentage of the credit limit plus an estimate of other opening fees, the periodic rate as an APR, the maximum APR for variable plans, initial rate duration and a reasonably current rate for discounted or premium rates, and a balloon payment statement where applicable. Tax deductibility statements are constrained and "free money" language is prohibited |
| Promotional rates, 1026.16(g) | Disclose the promotional period, the post-promotional rate or fee, and place "introductory" or "intro" in immediate proximity to the promotional rate |
| Exemption worth knowing | 1026.24(f) does not apply to envelopes, banner ads, or pop-up ads that link to an application or solicitation. Do not extend that exemption to the landing page itself |

---

## How to verify

### Safeguards Rule and Reg S-P

1. Ask for the qualified individual's name and the date of the last written risk assessment. Put both in the project record. If nobody can answer, the program does not exist.
2. Count the consumers in the client's data. Above or below 5,000 changes which 314.4 elements apply, and it is the first question in a Safeguards conversation.
3. Test MFA on **every** login surface, the admin panel included: CMS, hosting control panel, database console, DNS registrar, email, CI/CD, and the analytics account. 314.4(c)(5) says "any individual accessing any information system".
4. Verify encryption at rest, not only in transit. Confirm TLS with `curl -sI https://client.example` and check the certificate, then separately confirm database encryption, disk encryption, and that automated backups are encrypted. Encryption in transit alone does not satisfy 314.4(c)(3).
5. Grep the repository for form submissions written to a store with no expiry: `rg -i "contact_submissions|leads|applications|form_entries"`. Then check whether any deletion job exists: `rg -i "cron|scheduled|purge|retention|delete_after"`. 314.4(c)(6) requires disposal no later than two years after last use.
6. Open the access log configuration. Confirm authorized user activity is logged and shipped somewhere retained, per 314.4(c)(8).
7. List every third-party script and embed on the site, then map each to a service provider contract. `rg -i "<script[^>]*src=" --glob '!node_modules'` plus the network tab on a full page load. Any vendor that touches customer information needs a contract with safeguard terms under 314.4(f).
8. For SEC-registered clients, confirm the hosting and processing contracts include the 72-hour service provider breach notification clause from 17 CFR 248.30(a)(5). If the studio is the provider, read the studio's own contract.
9. Ask for the written incident response plan and the customer notification template. If the 30-day Reg S-P clock starts and the template does not exist, the clock does not pause.

### Privacy notices

10. Load the privacy notice URL directly. Confirm it is an HTML page with a stable URL, not a PDF, and that it is reachable without JavaScript.
11. Walk the account opening or application flow. Confirm the notice is delivered inside the flow with an acknowledgement step, not only linked in the footer. 12 CFR 1016.9(b) is explicit that general publication does not satisfy delivery.
12. Trigger a test application and confirm the acknowledgement is written to the database with a timestamp and a notice version identifier.
13. Check the notice for a version or revision date. If the client is relying on the annual notice exception, the notice content must match what was last delivered, and the client must not be sharing outside 1016.13, 1016.14, and 1016.15.

### Marketing Rule (adviser clients)

14. Screenshot every testimonial, endorsement, award badge, and rating on the site. For each, confirm the required 206(4)-1(b)(1) or (c) disclosures render in the same visual block, at comparable font size and contrast. Inspect computed `font-size`, `color`, and `opacity` in devtools against surrounding body text.
15. Disable CSS and reload. Confirm each disclosure still appears adjacent to its testimonial in source order, rather than being repositioned there by CSS.
16. Grep for disclosures hidden behind interaction: `rg -i "tooltip|aria-expanded|<details|read more|show disclosure"` near testimonial markup. A disclosure that requires a click is not clearly and prominently displayed.
17. For every performance figure or chart, confirm a net figure appears with at least equal prominence over the same period. Grep for gross-only language: `rg -i "gross of fees|before fees|gross return"`.
18. Confirm one, five, and ten year periods all render, with equal prominence, ending no earlier than the most recent calendar year end. Check the chart component's default props as well as the rendered pages.
19. Search for hypothetical performance features: `rg -i "backtest|back-test|projected|projection|hypothetical|model portfolio|calculator|target return|what if"`. Any interactive return calculator on a public page needs a conversation with the client's chief compliance officer before it ships.
20. Grep for implied regulator endorsement: `rg -i "SEC approved|SEC registered means|approved by the SEC|reviewed by the SEC"`. Note that "SEC-registered" is also misleading if presented as a credential.
21. Confirm the marketing site is under version control with retained history, and that the client can produce any past version of any page for five years.

### FINRA (broker-dealer clients)

22. Confirm a registered principal approved the exact content being deployed, and that the approval record captures the principal's name and the approval date. Ask to see it.
23. Load the initial retail page and every registered person's profile page. Confirm a visible BrokerCheck reference and working hyperlink on each. `rg -i "brokercheck"` across templates, then verify the rendered link resolves.
24. Grep for projection language: `rg -i "projected|will grow|expected return|guaranteed|assured|estimate your future|retirement calculator"`. Rule 2210(d)(1)(F) bars predicting or projecting performance in retail communications.
25. Check whether the site archives previous versions in a form that survives a redesign. A CMS that overwrites pages in place will not satisfy SEA Rule 17a-4(b)(4).
26. Confirm whether the client has been a member for less than one year. If so, the 10-business-day advance filing applies and the launch date has to accommodate it.

### Regulation FD (public company clients)

27. Try to reach an unpublished press release by guessing the URL pattern. If releases live at sequential or predictable paths, or if the CMS renders drafts at a public URL before the publish time, that is a live Regulation FD exposure.
28. Watch the network tab during a publish. Confirm nothing is served from cache or CDN edge ahead of the wire release timestamp.
29. Confirm any analyst or investor login area contains no material information absent from the public pages.

### Regulation Z (lending clients)

30. Grep every page for the four closed-end triggering terms: `rg -i "down ?payment|[0-9]+ months|[0-9]+ ?yr|per month|/mo|monthly payment|finance charge"`. For each hit, confirm the full 1026.24(d)(2) disclosure set appears.
31. Confirm every stated rate uses the exact phrase "annual percentage rate" or "APR" and that no simple or periodic rate is more prominent than the APR.
32. For dwelling-secured ads, compare font size and visual weight of the APR against the advertised teaser rate. The APR must have equal prominence and close proximity.
33. Load at 360px width. Confirm the required disclosures remain with the triggering term and do not fall three screens below the rate in the hero.
34. Grep for the 1026.24(i) prohibited patterns: `rg -i "fixed rate|government approved|government backed|eliminate your debt|debt free|counselor|your current lender"`.
35. If the site has Spanish or other non-English pages, confirm the required disclosures appear in the same language as the triggering terms. Providing trigger terms in Spanish and disclosures only in English is a specific 1026.24(i)(7) violation.

---

## Penalties

**FTC, for Safeguards Rule and FTC-jurisdiction GLBA matters**

| Provision | Maximum civil penalty | Basis |
|---|---|---|
| 15 U.S.C. 45(l), violation of a final cease and desist order | **$53,088** | 16 CFR 1.98, applying to penalties assessed after 17 January 2025 |
| 15 U.S.C. 45(m)(1)(A), violation of a trade regulation rule | **$53,088** | Same |
| 15 U.S.C. 45(m)(1)(B) | **$53,088** | Same |

UNVERIFIED: whether the FTC can obtain a civil penalty for a first-instance Safeguards Rule
violation. 15 U.S.C. 6805(a)(7) directs the FTC to enforce GLBA "under the Federal Trade
Commission Act", and the Safeguards Rule's authority citation is 15 U.S.C. 6801(b) and 6805(b)(2),
not section 18 of the FTC Act. The section 45(m)(1)(A) civil penalty attaches to trade regulation
rules promulgated under section 18. The reliably available remedies against a first-time violator
are injunctive relief and a consent order; the $53,088 per-violation figure then attaches to any
subsequent breach of that order under 15 U.S.C. 45(l). Do not quote a per-violation Safeguards
penalty to a client without checking with counsel.

**SEC, for Marketing Rule, Regulation S-P, and Regulation FD**

Advisers Act sections 203(i) and 209(e), per violation, for penalties imposed after 15 January 2025
on violations occurring after 2 November 2015:

| Tier | Natural person | Any other person |
|---|---|---|
| First tier (any violation) | **$11,823** | **$118,225** |
| Second tier (fraud, deceit, manipulation, or deliberate or reckless disregard of a regulatory requirement) | **$118,225** | **$591,127** |
| Third tier (second tier conduct that directly or indirectly resulted in substantial losses or significant risk of substantial losses to others, or substantial pecuniary gain to the person charged) | **$236,451** | **$1,182,251** |

The SEC published a notice on 7 July 2026 (91 FR 41722) stating there will be no inflation
adjustment for 2026, so the January 2025 amounts continue to apply. Exchange Act section 21B
carries the same tier structure and, in the January 2025 notice, the same amounts.

**CFPB, for Regulation P and Regulation Z violations by covered persons**

Per 12 CFR 1083.1, for penalties assessed after 15 January 2025:

| Tier | Maximum |
|---|---|
| Tier 1, any violation | **$7,217** |
| Tier 2, reckless violation | **$36,083** |
| Tier 3, knowing violation | **$1,443,275** |

12 U.S.C. 5565(c)(2) states these as maximums per day during which the violation continues.

**TILA private liability, 15 U.S.C. 1640**

| Transaction type | Statutory damages |
|---|---|
| Open-end credit not secured by real property or a dwelling | Twice the finance charge, minimum **$500**, maximum **$5,000** |
| Closed-end credit secured by real property or a dwelling | Not less than **$400**, not greater than **$4,000** |
| Consumer leases | 25 percent of the total of monthly payments, minimum **$200**, maximum **$2,000** |
| Class actions | The lesser of **$1,000,000** or **1 percent of the creditor's net worth**, in total across the series of class actions arising from the same failure by the same creditor |

Limitation period: generally one year from the occurrence of the violation, extended to three years
for violations of 15 U.S.C. 1639, 1639b, or 1639c.

**An important limit on TILA private damages for advertising.** 15 U.S.C. 1640(a) attaches
liability to a creditor who fails to comply "with any requirement imposed under this part,
including any requirement under section 1635 of this title, subsection (f) or (g) of section 1641
of this title, or part D or E of this subchapter". The credit advertising provisions sit in Part C
of subchapter I, "Credit Advertising and Limits on Credit Card Fees" (15 U.S.C. 1661 to 1665e),
which that list does not include. Advertising-only
violations are therefore generally an administrative enforcement matter for the CFPB or the FTC
rather than a private statutory damages claim. That is not a reason to relax: the CFPB per-day
figures above are larger than the private ones, and a misleading ad is separately actionable as a
deceptive practice under the FTC Act, the Consumer Financial Protection Act, and state UDAP law.

**FINRA**

FINRA fines are set under the FINRA Sanction Guidelines rather than a statutory per-violation cap,
and can be accompanied by censure, restitution, suspension of individuals, or expulsion of the
firm. UNVERIFIED: current FINRA Sanction Guideline fine ranges for Rule 2210 violations. Check the
current Sanction Guidelines PDF on finra.org per matter rather than quoting a figure.

---

## Common ways sites fail this

1. **Encryption at rest is skipped.** TLS is configured, the team calls it done, and the database and the S3 backup bucket are unencrypted. 16 CFR 314.4(c)(3) requires both.
2. **MFA on the admin panel only.** The rule says any individual accessing any information system. The DNS registrar, the hosting panel, and the CI/CD account are all in scope, and they are the accounts that actually get taken over.
3. **Form submissions live forever.** A contact or application form writes to a table nobody ever prunes. 314.4(c)(6) requires disposal no later than two years after last use.
4. **The privacy notice is a footer link and nothing else.** 12 CFR 1016.9(b) states that generally publishing does not satisfy delivery. If the site opens accounts, the notice needs an in-flow acknowledgement.
5. **The privacy notice is a PDF.** It fails accessibility, it fails on mobile, and it makes version control of a required record harder than it needs to be.
6. **Testimonial disclosures pushed to a footnote.** An asterisk next to a client quote resolving to fine print at the bottom of the page is not "clear and prominent" under 206(4)-1(b)(1). The disclosure belongs in the same block as the quote.
7. **Award badges with no rating disclosure.** A "Top Advisor 2026" badge in the footer with no date, period covered, identity of the rating body, or statement of compensation paid. 206(4)-1(c) requires all four.
8. **Gross-only performance charts.** A chart component built to show one series, fed gross returns. Net must appear with at least equal prominence over the same period.
9. **A cherry-picked performance window.** A "since 2020" chart because 2022 sits badly in a ten-year view. 206(4)-1(d)(2) requires one, five, and ten year periods with equal prominence.
10. **A returns calculator on a public adviser page.** Almost always hypothetical performance under 206(4)-1(d)(6), and almost never accompanied by the required criteria, assumptions, risks, and limitations.
11. **A retirement projector on a broker-dealer page.** FINRA Rule 2210(d)(1)(F) bars predicting or projecting performance in retail communications outright.
12. **No BrokerCheck link on the team bios.** Firms remember the homepage and forget that every page carrying a registered person's professional profile needs the reference and hyperlink.
13. **Content shipped before principal approval.** A designer pushes a copy fix on Friday. Rule 2210(b)(1) requires principal approval before the earlier of use or filing, with no exception for small changes.
14. **A redesign wipes the content archive.** SEA Rule 17a-4(b)(4) requires three years of business communications, the first two easily accessible, and Advisers Act 204-2(e) requires five years for advertisements. A CMS migration that drops history destroys required records.
15. **Draft press releases reachable at a guessable URL.** Sequential IDs on an IR site, or a CMS preview path with no auth, is a Regulation FD exposure sitting in plain sight.
16. **A rate in the hero, disclosures below the fold.** A mortgage landing page states "3.99%" and "$1,240/mo" at the top and puts the APR and repayment terms three screens down. Both are triggering terms under 1026.24(d)(1).
17. **A simple interest rate shown larger than the APR.** 1026.24(c) requires the APR to be the prominent figure.
18. **"Fixed rate" on an ARM product page.** Named explicitly as a prohibited practice in 1026.24(i)(1).
19. **Spanish landing pages with English-only disclosures.** 1026.24(i)(7) names this specifically, and it is the single most common language-related lending ad violation.
20. **Assuming the Safeguards Rule only covers banks.** Mortgage brokers, tax preparers, auto dealers, appraisers, finders, and credit counselors are all named in the rule's own examples in 16 CFR 314.2(h).
21. **Applying the FTC privacy rule to the wrong client.** 16 CFR Part 313 now reaches motor vehicle dealers under 12 U.S.C. 5519 only. Everyone else follows Regulation P or Regulation S-P.
22. **Treating a Safeguards breach report as confidential.** The FTC stated it intends to enter 314.4(j) notification event reports into a publicly available database.

---

## Sources

Official sources first. All retrieved 2026-07-20.

**GLBA Safeguards Rule**

- [16 CFR 314.1, Purpose and scope](https://www.law.cornell.edu/cfr/text/16/314.1) (retrieved 2026-07-20)
- [16 CFR 314.2, Definitions](https://www.law.cornell.edu/cfr/text/16/314.2) (retrieved 2026-07-20)
- [16 CFR 314.4, Elements](https://www.law.cornell.edu/cfr/text/16/314.4) (retrieved 2026-07-20)
- [16 CFR 314.6, Exceptions (the fewer-than-5,000-consumers provision)](https://www.law.cornell.edu/cfr/text/16/314.6) (retrieved 2026-07-20)
- [Standards for Safeguarding Customer Information, 86 FR 70272 (9 December 2021), effective 10 January 2022](https://www.federalregister.gov/documents/2021/12/09/2021-25736/standards-for-safeguarding-customer-information) (retrieved 2026-07-20)
- [Standards for Safeguarding Customer Information, delay of effectiveness, 87 FR 71509 (23 November 2022), moving 314.4(a), (b)(1), (c)(1) through (8), (d)(2), (e), (f)(3), (h), and (i) to 9 June 2023](https://www.govinfo.gov/content/pkg/FR-2022-11-23/html/2022-25201.htm) (retrieved 2026-07-20)
- [Standards for Safeguarding Customer Information, breach notification amendment, 88 FR 77499 (13 November 2023), effective 13 May 2024](https://www.govinfo.gov/content/pkg/FR-2023-11-13/html/2023-24412.htm) (retrieved 2026-07-20)
- [15 U.S.C. 6805, Enforcement](https://www.law.cornell.edu/uscode/text/15/6805) (retrieved 2026-07-20)

**GLBA privacy notices**

- [12 CFR 1016.4, Initial privacy notice to consumers required (Regulation P)](https://www.law.cornell.edu/cfr/text/12/1016.4) (retrieved 2026-07-20)
- [12 CFR 1016.5, Annual privacy notice to customers required, including the paragraph (e) exception](https://www.law.cornell.edu/cfr/text/12/1016.5) (retrieved 2026-07-20)
- [12 CFR 1016.9, Delivering privacy and opt out notices](https://www.law.cornell.edu/cfr/text/12/1016.9) (retrieved 2026-07-20)
- [16 CFR 313.1, Purpose and scope (FTC privacy rule, now limited to motor vehicle dealers)](https://www.law.cornell.edu/cfr/text/16/313.1) (retrieved 2026-07-20)
- [17 CFR Part 248 Subpart A, Regulation S-P privacy and opt out notices](https://www.law.cornell.edu/cfr/text/17/part-248/subpart-A) (retrieved 2026-07-20)

**SEC Regulation S-P safeguards and incident response**

- [17 CFR 248.30, Procedures to safeguard customer information, including response programs for unauthorized access](https://www.law.cornell.edu/cfr/text/17/248.30) (retrieved 2026-07-20)
- [Regulation S-P: Privacy of Consumer Financial Information and Safeguarding Customer Information, 89 FR 47688 (3 June 2024), Release Nos. 34-100155; IA-6604; IC-35193, effective 2 August 2024](https://www.federalregister.gov/documents/2024/06/03/2024-11116/regulation-s-p-privacy-of-consumer-financial-information-and-safeguarding-customer-information) (retrieved 2026-07-20)
- [Same release, full text on govinfo, containing section II.F "Compliance Period" and Table 3 designating larger entities](https://www.govinfo.gov/content/pkg/FR-2024-06-03/html/2024-11116.htm) (retrieved 2026-07-20)

**SEC Marketing Rule and adviser recordkeeping**

- [17 CFR 275.206(4)-1, Investment adviser marketing](https://www.law.cornell.edu/cfr/text/17/275.206(4)-1) (retrieved 2026-07-20)
- [17 CFR 275.204-2, Books and records to be maintained by investment advisers](https://www.law.cornell.edu/cfr/text/17/275.204-2) (retrieved 2026-07-20)
- [Investment Adviser Marketing, 86 FR 13024 (5 March 2021), Release No. IA-5653, effective 4 May 2021, with section II.K stating an eighteen-month transition to the compliance date](https://www.govinfo.gov/content/pkg/FR-2021-03-05/html/2020-28868.htm) (retrieved 2026-07-20)

**Regulation FD**

- [17 CFR 243.100, General rule regarding selective disclosure](https://www.law.cornell.edu/cfr/text/17/243.100) (retrieved 2026-07-20)
- [17 CFR 243.101, Definitions, including "issuer", "promptly", and "public disclosure"](https://www.law.cornell.edu/cfr/text/17/243.101) (retrieved 2026-07-20)

**FINRA**

- [FINRA Rule 2210, Communications with the Public](https://www.finra.org/rules-guidance/rulebooks/finra-rules/2210) (retrieved 2026-07-20)
- [FINRA Rule 4511, General Requirements (books and records)](https://www.finra.org/rules-guidance/rulebooks/finra-rules/4511) (retrieved 2026-07-20)
- [17 CFR 240.17a-4, Records to be preserved by certain exchange members, brokers and dealers](https://www.law.cornell.edu/cfr/text/17/240.17a-4) (retrieved 2026-07-20)

**Truth in Lending**

- [12 CFR 1026.24, Advertising (closed-end credit)](https://www.law.cornell.edu/cfr/text/12/1026.24) (retrieved 2026-07-20)
- [12 CFR 1026.16, Advertising (open-end credit)](https://www.law.cornell.edu/cfr/text/12/1026.16) (retrieved 2026-07-20)
- [15 U.S.C. 1640, Civil liability](https://www.law.cornell.edu/uscode/text/15/1640) (retrieved 2026-07-20)

**Penalties**

- [16 CFR 1.98, Adjustment of civil monetary penalty amounts (FTC), amounts applying to penalties assessed after 17 January 2025](https://www.law.cornell.edu/cfr/text/16/1.98) (retrieved 2026-07-20)
- [SEC, Adjustments to Civil Monetary Penalty Amounts, 90 FR 2767 (13 January 2025), Release Nos. 33-11350; 34-102134; IA-6808; IC-35442, effective 15 January 2025](https://www.govinfo.gov/content/pkg/FR-2025-01-13/html/2025-00513.htm) (retrieved 2026-07-20)
- [SEC, No Adjustment to Civil Monetary Penalty Amounts, 91 FR 41722 (7 July 2026)](https://www.federalregister.gov/documents/2026/07/07/2026-13629/no-adjustment-to-civil-monetary-penalty-amounts) (retrieved 2026-07-20)
- [12 CFR 1083.1, Adjustment of civil penalty amounts (CFPB), applying to penalties assessed after 15 January 2025](https://www.law.cornell.edu/cfr/text/12/1083.1) (retrieved 2026-07-20)
- [17 CFR 201.1001, Adjustment to civil monetary penalties (SEC rule text and historical table)](https://www.law.cornell.edu/cfr/text/17/201.1001) (retrieved 2026-07-20)

---

## Notes

**The Reg S-P compliance dates are computed, not quoted.** The adopting release states an
18-month compliance period for larger entities and 24 months for smaller entities, both measured
from the Federal Register publication date. It does not print the calendar dates in the text this
file was able to retrieve. Publication was 3 June 2024, so the dates are 3 December 2025 and
3 June 2026. Both have passed. If a client disputes its tier, the operative question is Table 3:
$1 billion in fund net assets, $1.5 billion in adviser assets under management, or non-small-entity
status under the Exchange Act for broker-dealers and transfer agents.

**Registration status is the intake question that decides everything.** Whether a client is
SEC-registered, state-registered, a FINRA member, or none of those changes which of the seven
regimes above applies. An adviser with under $100 million in assets under management is usually
state-registered and therefore outside the SEC Marketing Rule as such, though most states have
adopted parallel rules. Get the CRD number and the Form ADV before designing anything with a
testimonial or a performance chart in it.

**UNVERIFIED: SEC staff guidance on the Marketing Rule since adoption.** The Division of
Investment Management has issued FAQs and risk alerts on the Marketing Rule, including on
extracted performance and on presenting portfolio or investment characteristics without
accompanying net figures. This file could not retrieve sec.gov during the review, so no specific
FAQ position is stated here. Before shipping any performance display that departs from the plain
net-alongside-gross reading of 206(4)-1(d)(1), check the current Marketing Rule FAQ on sec.gov and
the client's chief compliance officer.

**UNVERIFIED: current FINRA Sanction Guideline ranges.** No figure is stated in this file. Pull
the current Sanction Guidelines from finra.org per matter.

**Where this file conflicts with others in the library.** The SEC Marketing Rule and FINRA Rule
2210 are stricter than the general FTC endorsement and review rules in
[`ftc-disclosures.md`](ftc-disclosures.md). Where a client is an SEC-registered adviser or a FINRA
member, the industry rule governs the testimonial and the FTC rules apply on top rather than
instead. The clearest divergence: the FTC Consumer Reviews Rule permits a compliant, disclosed
testimonial from a paid endorser; the Marketing Rule adds a written agreement requirement and a
disqualification check, and FINRA adds principal pre-approval and a filing obligation. Build to the
strictest applicable set.

**Overlap with state data breach law and state privacy law.** Satisfying 16 CFR 314.4(j) or
17 CFR 248.30 does not satisfy state breach notification statutes, which run on their own clocks
and their own definitions of personal information. GLBA-regulated data also carries entity-level or
data-level exemptions under several state privacy laws, including the CCPA as amended, so a
financial client's consent banner obligations may differ from a general commercial client's. See
[`ccpa-cpra.md`](ccpa-cpra.md) and [`gdpr.md`](gdpr.md) before assuming the same cookie and consent
build applies.

**Watch: the Safeguards breach reports are public.** The FTC said in the 2023 adopting release
that it intends to publish 314.4(j) notification event reports in a public database. That converts
a security failure into a reputational event with a permanent public record, which changes the
argument for building the technical controls properly the first time.
