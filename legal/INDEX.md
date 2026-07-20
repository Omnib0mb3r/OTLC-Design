# Legal Requirements: INDEX

> What a site must have to be lawful, separated from what it must have to be good.
> [`ANTI-SLOP.md`](../ANTI-SLOP.md) and [`guides/`](../guides/INDEX.md) cover craft and
> engineering. This directory covers obligation.

---

## Read this before using anything in here

**This is not legal advice, and neither is the skill that reads it.** It is a build
checklist maintained by a design studio so that sites ship with the artifacts the law
usually requires, instead of shipping with none of them and discovering the gap later.

Three things follow from that:

1. **The studio does not decide compliance. The client does.** Every project either gets
   sign-off from the client's counsel, or gets a written note that no counsel reviewed it
   and the client accepts that. Put it in `BRIEF.md` at intake, not in an email later.
2. **Generated policy text is a starting draft, never a deliverable.** A privacy policy
   that describes data flows the site does not actually have is worse than no policy: it
   is a written, dated misrepresentation. If a policy ships, it describes the real build.
3. **These files go stale.** Privacy and accessibility law moved every year from 2023
   through 2026 and will keep moving. Each file carries a `Last reviewed` date. Treat
   anything over six months old as a research task, not as fact.

For anything involving health data, financial data, children, or a regulated profession,
the answer is a lawyer, not this directory.

---

## How this is organized

```
legal/
  INDEX.md        this file: triage, disclaimer, how to maintain
  CHECKLIST.md    the per-project pass: intake questions -> required artifacts -> gate
  laws/           one file per law or regime, independently updatable
```

One law per file is deliberate. When a statute is amended, one file changes and the
change is legible in the diff. Nothing else needs touching.

Every file in `laws/` uses the same headings: **Applies when**, **What the site must
have**, **How to verify**, **Penalties**, **Common ways sites fail this**, **Sources**,
**Notes**. Read **Applies when** first and stop there if it does not apply.

---

## Triage: which files matter for this project

Answer these at intake (they are wired into [`PROCESS.md`](../PROCESS.md) Step 1). Each
"yes" pulls in the listed files.

| Intake question | If yes, read |
|---|---|
| Any visitor from the EU, EEA, UK, or Switzerland? | [`gdpr`](laws/gdpr.md), [`eprivacy-cookies`](laws/eprivacy-cookies.md) |
| Any California resident? | [`ccpa-cpra`](laws/ccpa-cpra.md), [`caloppa`](laws/caloppa.md) |
| US visitors outside California? | [`us-state-privacy-laws`](laws/us-state-privacy-laws.md) |
| Canadian visitors? | [`pipeda-canada`](laws/pipeda-canada.md), [`casl-canada`](laws/casl-canada.md) |
| Brazilian visitors? | [`lgpd-brazil`](laws/lgpd-brazil.md) |
| Any analytics, pixel, embed, or tag beyond strictly necessary? | [`eprivacy-cookies`](laws/eprivacy-cookies.md) |
| Users under 13 plausibly in the audience? | [`coppa`](laws/coppa.md) |
| Users under 18 can register or post content? | [`ca-minors-eraser-button`](laws/ca-minors-eraser-button.md) |
| Any personal data stored at all? | [`data-breach-notification`](laws/data-breach-notification.md) |
| Client is a US business, or a US public entity? | [`ada-wcag`](laws/ada-wcag.md) |
| Selling into the EU? | [`eu-accessibility-act`](laws/eu-accessibility-act.md) |
| Any marketing email or newsletter signup? | [`can-spam`](laws/can-spam.md), [`casl-canada`](laws/casl-canada.md) |
| Affiliate links, sponsorships, testimonials, reviews, or fee-bearing checkout? | [`ftc-disclosures`](laws/ftc-disclosures.md) |
| Takes card payments? | [`pci-dss`](laws/pci-dss.md) |
| Sells anything, or has a subscription or auto-renewal? | [`ecommerce-consumer-protection`](laws/ecommerce-consumer-protection.md) |
| Hosts user-submitted content? | [`dmca-copyright`](laws/dmca-copyright.md) |
| Uses any font, photo, icon, video, or library not authored by us? | [`content-licensing-attribution`](laws/content-licensing-attribution.md) |
| Healthcare client, or any patient data? | [`hipaa`](laws/hipaa.md) |
| Law firm or attorney client? | [`legal-industry-aba`](laws/legal-industry-aba.md) |
| Bank, lender, adviser, broker, or public company? | [`financial-glba-sec`](laws/financial-glba-sec.md) |

Two of these apply to essentially every project and are the floor, not the ceiling:
[`content-licensing-attribution`](laws/content-licensing-attribution.md) (every build
uses someone else's fonts) and [`ada-wcag`](laws/ada-wcag.md) (accessibility is already
an [`ANTI-SLOP.md`](../ANTI-SLOP.md) rule 20 gate, and the legal exposure is the reason
that gate is non-negotiable).

---

## The law files

### Privacy and data protection

| File | Covers |
|---|---|
| [gdpr.md](laws/gdpr.md) | EU/EEA General Data Protection Regulation, plus UK divergence |
| [eprivacy-cookies.md](laws/eprivacy-cookies.md) | EU cookie consent: what a lawful banner actually does |
| [ccpa-cpra.md](laws/ccpa-cpra.md) | California, including Global Privacy Control and opt-out links |
| [caloppa.md](laws/caloppa.md) | California policy-link and Do Not Track disclosure rules |
| [us-state-privacy-laws.md](laws/us-state-privacy-laws.md) | Every other US state comprehensive privacy law, with thresholds |
| [pipeda-canada.md](laws/pipeda-canada.md) | Canada federal, plus the stricter Quebec Law 25 |
| [lgpd-brazil.md](laws/lgpd-brazil.md) | Brazil |
| [coppa.md](laws/coppa.md) | US children under 13 |
| [ca-minors-eraser-button.md](laws/ca-minors-eraser-button.md) | California minors under 18 |
| [data-breach-notification.md](laws/data-breach-notification.md) | Who gets told, in what order, on what clock |

### Accessibility

| File | Covers |
|---|---|
| [ada-wcag.md](laws/ada-wcag.md) | ADA Titles II and III, Section 508, WCAG conformance targets |
| [eu-accessibility-act.md](laws/eu-accessibility-act.md) | EAA and EN 301 549, applicable since June 2025 |

### Marketing and advertising

| File | Covers |
|---|---|
| [can-spam.md](laws/can-spam.md) | US email, opt-out regime |
| [casl-canada.md](laws/casl-canada.md) | Canada email, opt-in regime, personal liability |
| [ftc-disclosures.md](laws/ftc-disclosures.md) | Endorsements, affiliates, fake reviews, junk fees, click-to-cancel |

### Commerce and security

| File | Covers |
|---|---|
| [pci-dss.md](laws/pci-dss.md) | Card data, SAQ scope, payment page script integrity |
| [ecommerce-consumer-protection.md](laws/ecommerce-consumer-protection.md) | Price transparency, withdrawal rights, auto-renewal, refunds |

### Intellectual property

| File | Covers |
|---|---|
| [dmca-copyright.md](laws/dmca-copyright.md) | Copyright notice, DMCA safe harbor, takedown procedure |
| [content-licensing-attribution.md](laws/content-licensing-attribution.md) | Fonts, stock, icons, code licenses, attribution |

### Regulated industries

| File | Covers |
|---|---|
| [hipaa.md](laws/hipaa.md) | Health data, business associate agreements, tracking pixel exposure |
| [legal-industry-aba.md](laws/legal-industry-aba.md) | Attorney advertising rules |
| [financial-glba-sec.md](laws/financial-glba-sec.md) | GLBA Safeguards, SEC and FINRA marketing rules |

---

## Where this fits in the workflow

| Step | What happens |
|---|---|
| **1. Intake** | Run the triage table. Record the answers and the resulting law list in `BRIEF.md`. Ask who reviews compliance. |
| **3. Synthesis** | Required artifacts become real pages and UI in the sitemap. A cookie banner is a design problem; deciding it at Step 5 means retrofitting it. |
| **4. Build** | Implement the artifacts. Consent gating is build work, not a plugin bolted on at the end. |
| **5. Verify** | Run [`CHECKLIST.md`](CHECKLIST.md) as a delivery gate alongside Lighthouse and axe. |
| **6. Post-mortem** | A law that bit during the project, or a new one, gets a file here. |

---

## Maintaining this directory

**Updating an existing law.** Edit only that file. Update `Last reviewed`, and `Last
amended` if the statute itself changed. Add the source you used. Commit
`legal: update <slug> for <what changed>`.

**Adding a law.** Copy the heading structure from any existing file, exactly. Add a row
to the triage table above and to the correct category table. Add its trigger to the
Step 1 intake questions in [`PROCESS.md`](../PROCESS.md) if it needs a new question.
Commit `legal: add <slug>`.

**Retiring a law.** Do not delete the file. Set `Status` to repealed or superseded, say
what replaced it, and keep it. A client site built in 2026 may still be audited against
the rules of 2026.

**Review cadence.** Sweep the whole directory twice a year, and always before starting a
project in a regulated industry. [`us-state-privacy-laws.md`](laws/us-state-privacy-laws.md)
goes stale fastest; new states keep arriving.

Related: security implementation lives in **OTLC Guardian** at
`C:\dev\Projects\otlc-guardian\`, which has an audit engine that enforces it. This
directory says what the law requires. Guardian says whether the code does it.
