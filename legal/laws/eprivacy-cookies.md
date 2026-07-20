# ePrivacy / Cookies: Directive 2002/58/EC concerning the processing of personal data and the protection of privacy in the electronic communications sector (as amended by Directive 2009/136/EC)

| Field | Value |
|---|---|
| **Jurisdiction** | EU + EEA, via 30 separate national transposition laws. UK keeps its own version (PECR) post-Brexit. |
| **Regulator / enforcer** | National authorities, not a single EU body. Often the DPA (CNIL in France, AEPD in Spain, Garante in Italy, ICO in the UK), sometimes a telecoms regulator. EDPB coordinates but does not enforce. The GDPR one-stop-shop does **not** apply to cookie placement. |
| **In force since** | Directive adopted 12 July 2002. The consent requirement in its current form comes from Directive 2009/136/EC, consolidated text dated 19 December 2009. |
| **Last amended** | 2009 (Directive 2009/136/EC). The Directive itself has not been amended since. National laws under it change constantly: UK PECR was amended by the Data (Use and Access) Act 2025, commenced 5 February 2026. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. The proposed ePrivacy **Regulation** that would have replaced it was withdrawn by the European Commission in its 2025 Work Programme (announced 11 February 2025). The Directive and its national laws are what applies, indefinitely. |

The operative rule is Article 5(3), quoted in full:

> "Member States shall ensure that the storing of information, or the gaining of access to information already stored, in the terminal equipment of a subscriber or user is only allowed on condition that the subscriber or user concerned has given his or her consent, having been provided with clear and comprehensive information, in accordance with Directive 95/46/EC, inter alia, about the purposes of the processing. This shall not prevent any technical storage or access for the sole purpose of carrying out the transmission of a communication over an electronic communications network, or as strictly necessary in order for the provider of an information society service explicitly requested by the subscriber or user to provide the service."

Two things follow that developers routinely get wrong:

1. **The word "cookie" does not appear.** The trigger is storing or reading anything on the device. Pixels, `localStorage`, `sessionStorage`, IndexedDB, cache manipulation, and identifiers hashed on-device are all in scope per EDPB Guidelines 2/2023 (adopted 7 October 2024).
2. **It applies whether or not personal data is involved.** GDPR governs what you do with the data afterward. Article 5(3) governs the read/write itself. You can breach ePrivacy with a purely non-personal identifier.

---

## Applies when

Check each at intake. Any single "yes" pulls this file in.

- **The site stores or reads anything on a visitor's device beyond what the exemptions cover.** This includes cookies, `localStorage`, `sessionStorage`, IndexedDB, service worker cache used for tracking, device fingerprinting scripts, and tracking pixels that cause the browser to send stored identifiers.
- **The site is directed at, or reachable by, users in any EU or EEA member state.** There is no revenue threshold, no employee-count threshold, and no record-count threshold. A one-page brochure site with Google Analytics is caught.
- **The UK version (PECR reg. 6) applies separately** if there are UK visitors. Post-DUAA the UK now has exemptions the EU does not (see Notes). Do not assume one banner satisfies both.
- **Any third-party embed loads before consent:** YouTube (`youtube.com`, use `youtube-nocookie.com` and it still sets storage on play), Vimeo, Google Maps, Google Fonts served from Google's CDN, Recaptcha, Intercom, Hotjar, Meta Pixel, LinkedIn Insight, TikTok Pixel, Stripe's fraud scripts on non-checkout pages.
- **Any analytics at all in the EU.** Self-hosted Matomo in cookieless mode may fall under a national analytics exemption; Google Analytics does not.

### Who is NOT caught

- Storage strictly necessary for a service the user explicitly requested. Concretely: session cookies for a logged-in area, a shopping-cart cookie, a load-balancer affinity cookie, a CSRF token, a cookie storing the user's own cookie preferences, a cookie holding a language choice the user selected.
- Purely transmission-level technical storage.

### The "strictly necessary" test, stated precisely

"Strictly necessary" means necessary **for the service the user asked for**, not necessary for the business. Analytics is necessary for the business. It is not strictly necessary for the user's requested service, so it needs consent. The EDPB taskforce flagged mislabelling as its Type I practice and noted that site owners must be able to **demonstrate** the essentiality of every cookie they list as essential. Security cookies are a common grey area: a cookie that prevents fraud on a login form is arguable; a cookie that feeds a third-party bot-scoring product with cross-site reach usually is not.

WP29 Opinion 04/2012 remains the reference list of exempt categories, and the taskforce explicitly recalled it, including the point that cookies retaining a user's own expressed preferences are exempt.

---

## What the site must have

| Requirement | What that means in the build |
|---|---|
| **Nothing non-exempt fires before consent** | This is the whole requirement. Tags must be gated in code, not merely "categorised" in a CMP UI. On first paint with no prior choice, the only network requests are to first-party origins and to whatever is strictly necessary. No GA, no pixels, no fonts CDN, no embedded video iframes. |
| **First-layer reject button** | The first layer of the banner must carry a reject control at the same level as accept, wherever an accept control appears. The EDPB taskforce position: a vast majority of authorities treat the absence of a refuse/reject option on any layer carrying a consent button as an infringement. Spain's AEPD requires accept and reject on the same layer with the same visibility, mandatory since 11 January 2024. |
| **Equal prominence for accept and reject** | Same size, same shape, same visual weight, same read order. The taskforce declined to set a universal contrast standard and requires case-by-case assessment, but explicitly named as manifestly misleading a reject button whose text-to-background contrast makes the text "unreadable to virtually any user". Build both buttons from the same component with the same token. |
| **No pre-ticked boxes anywhere** | Every category toggle on the second layer defaults to off. Confirmed by CJEU *Planet49* (C-673/17, 1 October 2019) and GDPR recital 32. Strictly necessary may be shown as a locked-on row, clearly labelled as not optional. |
| **Granular consent per purpose** | Separate toggles for analytics, marketing, personalisation. One master "accept all" is fine as an additional convenience; it cannot be the only option. |
| **Prior consent** | Consent is collected **before** the read/write, not concurrently and not after. Scroll, continued browsing, and page-navigation are not consent: consent requires a positive action. |
| **Unbundled consent** | Consent to cookies cannot be a condition of accessing content (see Cookie walls below), and cannot be rolled into acceptance of terms of service. |
| **Clear information before the choice** | Purposes, cookie duration, and whether third parties get access, all available at the point of choosing. The CJEU held duration and third-party access are required disclosures. A linked cookie policy listing every cookie by name, provider, purpose, and retention. |
| **Cookie policy page** | Live URL, typically `/cookie-policy` or a section of `/privacy`. Table of every cookie actually set, generated from a real scan and not from a template. Linked in the footer on every page and from the banner's first layer. |
| **Persistent withdrawal mechanism** | Withdrawal must be as easy as giving consent, available at any time. In practice: a permanent footer link ("Cookie settings" / "Manage cookies") on every page, or a small persistent hovering icon. The taskforce confirmed authorities **cannot mandate** the hovering icon specifically, but they will assess whatever you ship against the "as easy to withdraw as to give" test. A footer link that reopens the same banner passes; a policy page telling users to clear their browser does not. |
| **Withdrawal actually deletes** | On withdrawal, clear the non-exempt cookies already set and stop the tags. Flipping a stored preference while the GA cookie stays on the device is a failure. |
| **Consent records** | Log per consent event: an opaque user/session identifier, timestamp, the exact purposes accepted and rejected, the CMP and policy version shown, and the consent string if TCF is used. Retain for as long as the consent is relied on plus a defence period. Never log raw IP as the sole identifier if avoidable. |
| **Consent lifetime and re-prompting** | Store the choice so users are not re-asked on every visit. UNVERIFIED: CNIL's guidance is often reported as six months being best practice for retaining both consent and refusal, not a hard rule, with a longer period needing justification. The CNIL page cited below does not state this; it sets a six-month adaptation period for compliance, which is a different thing. Check the CNIL cookie recommendation directly before quoting a number to a client. Critically: **store refusals too.** Re-prompting a user who said no, on every page view, is a dark pattern. |
| **Site works fully when everything is refused** | Refusing must not break layout, navigation, or purchase. If refusing cookies leaves a blank rectangle where a video was, ship a styled placeholder with a click-to-load control that requests consent for that embed. |

### What a compliant banner literally looks like

First layer, and this fits in a single component:

```
┌────────────────────────────────────────────────────────────────────┐
│  Cookies on example.com                                            │
│                                                                    │
│  We use cookies that are needed to run this site. We would also    │
│  like to set analytics cookies to understand how the site is       │
│  used, and marketing cookies to measure our advertising.           │
│  You can change your choice at any time via "Cookie settings"      │
│  in the footer. See our Cookie Policy for the full list.           │
│                                                                    │
│   ┌──────────────┐  ┌──────────────┐  ┌────────────────────────┐   │
│   │  Reject all  │  │  Accept all  │  │  Manage preferences    │   │
│   └──────────────┘  └──────────────┘  └────────────────────────┘   │
│      identical         identical          may be a text button     │
│      styling           styling                                     │
│                                                                    │
│  [Cookie Policy]  [Privacy Policy]                                 │
└────────────────────────────────────────────────────────────────────┘
```

Rules encoded in that sketch:

- Reject and Accept are the same component with the same tokens. If Accept is a filled primary button, Reject is a filled primary button. Swapping Reject to a ghost/outline style is the single most common violation in the wild.
- Reject sits on the first layer, not behind "Manage preferences".
- There is no X or close control that dismisses the banner without a decision, because dismissal is ambiguous and leaves you with no lawful basis. If you must offer a close affordance, it must behave exactly as "Reject all", and be labelled to say so.
- The banner does not block the page behind a full-screen scrim that makes content unreadable, unless the underlying content stays accessible on reject.
- Body copy states the purposes in plain language before the buttons.
- Links to the full policy are inside the first layer.

Second layer ("Manage preferences"):

```
┌────────────────────────────────────────────────────────────────────┐
│  Cookie preferences                                    [ Close X ] │
│                                                                    │
│  Strictly necessary                              Always active     │
│  Needed for the site to work: session, security, your cookie       │
│  choice. Cannot be switched off.                    [ locked on ]  │
│                                                                    │
│  Analytics                                          [ OFF ○───  ]  │
│  Helps us count visits and see which pages are used.               │
│  Google Analytics 4 (Google Ireland Ltd), 14 months.               │
│                                                                    │
│  Marketing                                          [ OFF ○───  ]  │
│  Used to measure and target advertising.                           │
│  Meta Pixel (Meta Platforms Ireland Ltd), 90 days.                 │
│                                                                    │
│   ┌──────────────┐  ┌──────────────┐  ┌────────────────────────┐   │
│   │  Reject all  │  │  Accept all  │  │  Save my choices       │   │
│   └──────────────┘  └──────────────┘  └────────────────────────┘   │
└────────────────────────────────────────────────────────────────────┘
```

Every optional toggle renders OFF on first load. Vendor name and retention period sit next to each category.

### Cookie walls

EDPB Guidelines 05/2020 on consent, para. 39: access to services and functionalities must not be made conditional on consent to storage or access on the user's terminal equipment. A hard cookie wall (accept or you cannot read the page) does not produce freely given consent.

"Consent or pay" is the contested variant. EDPB Opinion 08/2024 (adopted 17 April 2024) held that in most cases **large online platforms** will not obtain valid consent from a binary consent-or-pay choice, and that they should offer a third option: a free alternative without behavioural advertising. Note the scope: the Opinion addresses large online platforms, and the EDPB signalled broader guidance to follow. For a studio building a normal client site, the practical rule is: do not build a cookie wall, and treat consent-or-pay as a decision that needs the client's counsel in writing.

### Google Consent Mode v2

Google requires Consent Mode v2 signals for advertisers and publishers handling EEA end-user data; it became a condition of using Google advertising features for EEA traffic in **March 2024**. Missing it degrades remarketing and audience features rather than triggering a regulator, but it is a client-facing failure.

Four parameters: `ad_storage`, `analytics_storage`, `ad_user_data`, `ad_personalization`.

Set defaults to denied before the Google tag loads, and before any `config` or `event` command:

```javascript
gtag('consent', 'default', {
  'ad_storage': 'denied',
  'ad_user_data': 'denied',
  'ad_personalization': 'denied',
  'analytics_storage': 'denied'
});
```

Then `gtag('consent', 'update', {...})` with `'granted'` for exactly the categories the user accepted.

Basic vs advanced, per Google's own documentation:

| Mode | Tag loading | Data before consent |
|---|---|---|
| **Basic** | "Blocked until user interaction with a consent banner." | None. No data is sent before the user consents, not even the default consent status. |
| **Advanced** | "Loads with defaults set to `denied`, unless configured otherwise." | Cookieless pings carrying consent state and measurement are sent when consent is denied. |

**Choose basic mode unless the client has taken legal advice on advanced.** Advanced mode sends a request to Google from a user who refused, which is exactly the behaviour a regulator examines. It gives better conversion modelling, which is why vendors push it. That is a business tradeoff for the client to make on record, not a default for the studio to pick.

Consent Mode is a Google product requirement layered on top of the law. Implementing it is not by itself compliance: the tag must genuinely not write storage pre-consent.

### IAB TCF

The IAB Europe Transparency and Consent Framework is an ad-tech signalling standard, not a legal safe harbour. Only relevant if the client runs programmatic advertising. If the site has no ad inventory, do not install a TCF CMP; it adds vendor lists, complexity, and legal exposure for nothing.

If it is in scope:

- Current framework version is **v2.3**, released 19 June 2025. The adoption deadline for participants was **28 February 2026**, so any implementation shipping now must be on v2.3. Its main change makes the `disclosedVendors` segment mandatory in the TC String.
- v2.2 removed legitimate interest as an available legal basis for Purposes 3, 4, 5 and 6 (personalised ads profile, select personalised ads, personalised content profile, select personalised content). Consent is the only option for those.
- The CMP must disclose the number of third-party vendors on the first layer. There is no cap, but IAB's own policy warns that an unjustifiably large number harms informed choice and raises legal risk. A banner disclosing 800+ vendors is a liability. Prune the vendor list to those actually used.
- The taskforce position on legitimate interest is directly relevant: the legal basis for the read/write under Article 5(3) **cannot** be legitimate interest, and where Article 5(3) is breached, the downstream GDPR processing cannot be compliant either. A TCF banner that lets vendors run on legitimate interest for storage is wrong regardless of what the framework permits.

---

## How to verify

Run all of these before delivery. They take about fifteen minutes.

**1. Clean-profile network audit (the decisive test)**

- Open an incognito/private window, DevTools Network tab, "Preserve log" on, filter set to All.
- Load the homepage. Do not touch the banner.
- Sort by domain. Every third-party domain in that list is a finding. Expect to see only your own origin and your own CDN.
- Specifically grep the request list for: `google-analytics.com`, `googletagmanager.com` (the container itself is arguable; anything it fires is not), `doubleclick.net`, `facebook.net`, `connect.facebook.net`, `hotjar`, `clarity.ms`, `linkedin.com`, `tiktok.com`, `youtube.com`, `fonts.googleapis.com`, `fonts.gstatic.com`.

**2. Storage audit pre-consent**

- DevTools → Application → Storage. Check Cookies, Local Storage, Session Storage, IndexedDB.
- Before any interaction, the only entries should be strictly necessary ones. Write down every key you find and justify each in the cookie policy.
- Run this in the console to dump what is set:
  ```javascript
  console.table(document.cookie.split('; ').map(c => c.split('=')[0]));
  console.table(Object.keys(localStorage));
  ```

**3. Reject path**

- Reload clean, click "Reject all".
- Re-run steps 1 and 2. Nothing new from a tracking domain should appear, on the landing page or after navigating three pages deep.
- Confirm the banner does not reappear on the next page view or the next visit within the retention window.

**4. Accept path and withdrawal**

- Reload clean, click "Accept all", confirm tags now fire (proves the gate is real and not just cosmetic).
- Click the footer "Cookie settings" link, withdraw consent.
- Re-check Application → Storage. The analytics and marketing cookies must be **gone**, not just marked inactive.

**5. Banner design check**

- Screenshot the first layer. Is there a reject control? Is it on this layer? Measure it: same width, height, background, border-radius, and font-weight as accept?
- Inspect both buttons and diff their computed styles. If the classes differ, that is your finding.
- Open the second layer. Every optional toggle must render off. Screenshot as evidence.
- Confirm there is no close/X that dismisses without a decision.

**6. Keyboard and screen reader**

- Tab through the banner. Reject must be reachable, and reaching it must not require more keystrokes than reaching accept.
- The banner should trap focus while open and be announced. This overlaps the `ada-wcag.md` gate; a banner that fails keyboard access fails twice.

**7. Consent Mode (if Google tags present)**

- In the console before interacting: `dataLayer.filter(e => e[0] === 'consent')` and confirm a `default` entry with all four parameters set to `denied`.
- Confirm the default call appears in the DOM **before** the gtag/GTM script tag.
- Google Tag Assistant will show the consent state per tag.

**8. Cookie policy accuracy**

- Diff the cookie list in the policy against the actual accept-path storage dump from step 4. Any cookie set but not listed, or listed but not set, is a defect. Regenerate the policy from a real scan.

---

## Penalties

Penalties come from **national law**, not the Directive, and vary widely by member state.

| Jurisdiction | Maximum / notable | Source |
|---|---|---|
| France | Article 82 of the French Data Protection Act. CNIL fined Google €150m (€90m Google LLC + €60m Google Ireland) and Facebook Ireland €60m on 31 December 2021 for making refusal harder than acceptance. | [CNIL / DLA Piper](https://privacymatters.dlapiper.com/2022/01/france-cookies-new-record-sanctions-for-tech-giants-cnil-fines-facebook-ireland-60-million-euros-and-google-150-million-euros/) |
| France | CNIL fined Google €325m total on 1 September 2025 (€200m Google LLC, €125m Google Ireland), plus €100,000 per day for failure to remediate within six months. Grounds included invalid consent for advertising cookies at account creation and reject being harder than accept. | [CNIL](https://www.cnil.fr/en/cookies-and-advertisements-inserted-between-emails-google-fined-325-million-euros-cnil) |
| France | CNIL fined Condé Nast €750,000 on 27 November 2025 for placing cookies without consent on the Vanity Fair site. Shows mid-size publishers are in scope, not only platforms. | [noyb](https://noyb.eu/en/noyb-win-conde-nast-fined-eu750000-placing-cookies-without-consent) |
| France (earlier) | Google €100m and Amazon €35m, December 2020. | [Hunton](https://www.hunton.com/privacy-and-information-security-law/cnil-fines-google-and-amazon-135-million-euros-for-alleged-cookie-violations) |
| UK | PECR maximum rose from £500,000 to **£17.5m or 4% of global annual turnover, whichever is higher**, via the Data (Use and Access) Act 2025 s.115, commenced 5 February 2026 by SI 2026/82 (Commencement No. 6). The new cookie exceptions sit in s.112, commenced the same day. | [Mayer Brown](https://www.mayerbrown.com/en/insights/publications/2025/06/the-data-use-and-access-act-pecr-reform-rules-relating-to-electronic-marketing-and-cookies-in-the-uk) |
| Germany | UNVERIFIED: secondary sources state a maximum of €300,000 under TDDDG. Not confirmed against the statute text. Do not quote this figure to a client without checking § 28 TDDDG. | [Securiti](https://securiti.ai/blog/german-ttdsg-guide/) |

Beyond fines, the realistic risk for a small client is an order to comply with a deadline, plus the reputational cost of a public decision. Regulators have generally opened with orders rather than penalties for first-time, non-platform infringers.

---

## Common ways sites fail this

- **Tags fire before consent.** The CMP shows a banner while GTM has already loaded GA and the Meta Pixel. The banner is decoration over an ungated site. This is the single most common failure and the easiest to detect.
- **"Accept all" is a filled primary button, "Reject" is a grey outline or a text link.** Direct hit on the taskforce's Type C, D and E practices.
- **No reject on the first layer.** Reject is buried behind "Manage preferences" → scroll → toggle three switches → "Save". Taskforce Type A.
- **Pre-ticked category toggles on the second layer.** Taskforce Type B, and settled since *Planet49* in 2019.
- **An X that closes the banner without a decision**, after which tracking runs anyway.
- **Everything labelled "strictly necessary."** Analytics categorised as essential so it never needs consent. Taskforce Type I.
- **No withdrawal path.** Consent is collected once and there is no footer link, so the user cannot change their mind.
- **Withdrawal that does not delete.** The preference flips, the GA cookie stays on the device.
- **Refusal is not stored**, so the banner reappears on every page load until the user gives in. Nudging by attrition.
- **The cookie policy is a template.** It lists cookies the site does not set and omits ones it does. A regulator diffs it against a scan in about a minute.
- **Google Fonts loaded from `fonts.gstatic.com`.** German courts have treated this as an unconsented transfer. Self-host the fonts; it is faster anyway.
- **A YouTube embed on the homepage.** The iframe alone reaches out on load. Use a click-to-load facade.
- **Consent Mode installed instead of gating.** The team believes `gtag('consent', ...)` is the compliance measure. It is a signal to Google, not a gate.
- **One banner assumed to cover EU and UK.** Since February 2026 these regimes differ.

---

## Sources

Official sources first. All retrieved 2026-07-20.

- [Directive 2002/58/EC, consolidated text of 19 December 2009 (EUR-Lex, CELEX 02002L0058-20091219)](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02002L0058-20091219). Retrieved 2026-07-20. Article 5(3) verbatim.
- [EDPB, Report of the work undertaken by the Cookie Banner Taskforce, adopted 17 January 2023 (PDF)](https://www.edpb.europa.eu/system/files/2023-01/edpb_20230118_report_cookie_banner_taskforce_en.pdf). Retrieved 2026-07-20. Source for Type A, B, C, D, E, H, I and K positions quoted above.
- [EDPB, Guidelines 2/2023 on the technical scope of Art. 5(3) of the ePrivacy Directive, version 2, adopted 7 October 2024 (PDF)](https://www.edpb.europa.eu/system/files/2024-10/edpb_guidelines_202302_technical_scope_art_53_eprivacydirective_v2_en_0.pdf). Retrieved 2026-07-20. Pixels, local storage, on-device hashed identifiers.
- [EDPB, Opinion 08/2024 on valid consent in the context of consent or pay models implemented by large online platforms, adopted 17 April 2024](https://www.edpb.europa.eu/our-work-tools/our-documents/opinion-board-art-64/opinion-082024-valid-consent-context-consent-or_en). Retrieved 2026-07-20.
- [CNIL, Google fined €325 million, 1 September 2025](https://www.cnil.fr/en/cookies-and-advertisements-inserted-between-emails-google-fined-325-million-euros-cnil). Retrieved 2026-07-20.
- [CNIL, Cookies and other tracking devices: CNIL publishes new guidelines](https://www.cnil.fr/en/cookies-and-other-tracking-devices-cnil-publishes-new-guidelines). Retrieved 2026-07-20. Note: this page does **not** support the six-month consent/refusal retention figure. The six months it mentions is an adaptation period for compliance. Source needed for the retention figure.
- [ICO, Guidance on the use of storage and access technologies (final, published 29 April 2026)](https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guidance-on-the-use-of-storage-and-access-technologies/). Retrieved 2026-07-20 (HTTP 200 with a normal browser user-agent; the ICO edge blocks some automated clients). Publication date and DUAA exception detail cross-checked against the Hunton summary below.
- [Hunton, UK ICO Publishes Guidance on Storage and Access Technologies](https://www.hunton.com/privacy-and-cybersecurity-law-blog/uk-ico-publishes-guidance-on-storage-and-access-technologies). Retrieved 2026-07-20. Publication date and the DUAA statistical/appearance exceptions.
- [Google, Set up consent mode on websites (Tag Platform developer docs)](https://developers.google.com/tag-platform/security/guides/consent). Retrieved 2026-07-20.
- [Google, Consent mode concepts, basic vs advanced](https://developers.google.com/tag-platform/security/concepts/consent-mode). Retrieved 2026-07-20. Source for the basic/advanced table.
- [IAB Europe, All you need to know about the transition to TCF v2.3](https://iabeurope.eu/all-you-need-to-know-about-the-transition-to-tcf-v2-3/). Retrieved 2026-07-20. Release 19 June 2025, deadline 28 February 2026.
- [IAB Europe, TCF v2.2 implementation FAQs](https://iabeurope.eu/tcf-faqs/). Retrieved 2026-07-20. Legitimate interest removed for Purposes 3-6; first-layer vendor count.
- [Belgian Data Protection Authority, The Market Court rules in the IAB Europe case](https://www.dataprotectionauthority.be/citizen/the-market-court-rules-in-the-iab-europe-case). Retrieved 2026-07-20.
- [Freshfields, IAB Europe judgment (C-604/22), CJEU 7 March 2024](https://technologyquotient.freshfields.com/post/102j2qz/iab-europe-judgment-c-604-22-the-cjeu-clarifies-the-notion-of-personal-data-an). Retrieved 2026-07-20. TC String as personal data, scope of joint controllership.
- [Bird & Bird, Planet49: CJEU rules on cookie consent (C-673/17, 1 October 2019)](https://www.twobirds.com/en/insights/2019/global/planet49-cjeu-rules-on-cookie-consent). Retrieved 2026-07-20.
- [Hunton, European Commission Withdraws ePrivacy Regulation Proposal](https://www.hunton.com/privacy-and-information-security-law/european-commission-withdraws-eprivacy-regulation-and-ai-liability-directive-proposals). Retrieved 2026-07-20.
- [Mayer Brown, The Data (Use and Access) Act: PECR reform](https://www.mayerbrown.com/en/insights/publications/2025/06/the-data-use-and-access-act-pecr-reform-rules-relating-to-electronic-marketing-and-cookies-in-the-uk). Retrieved 2026-07-20. £17.5m / 4% ceiling. Note: this article does not give a commencement date.
- [Data (Use and Access) Act 2025, s.112 (storing information in terminal equipment)](https://www.legislation.gov.uk/ukpga/2025/18/section/112). Retrieved 2026-07-20. Commencement 5 February 2026 by SI 2026/82 reg. 2(w).
- [Data (Use and Access) Act 2025, s.115 (Commissioner's enforcement powers)](https://www.legislation.gov.uk/ukpga/2025/18/section/115). Retrieved 2026-07-20. Commencement 5 February 2026 by SI 2026/82 reg. 2(y).
- [EDPB, Guidelines 05/2020 on consent under Regulation 2016/679, version 1.1, adopted 4 May 2020 (PDF)](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf). Retrieved 2026-07-20. Para. 39, cookie walls.
- [Einwilligungsverwaltungsverordnung (EinwV), 6 February 2025, BGBl. 2025 I Nr. 32](https://www.gesetze-im-internet.de/einwv/). Retrieved 2026-07-20. In force 1 April 2025 per Art. 3.
- [Linklaters, Spanish regulator requires a reject button in cookie banners](https://techinsights.linklaters.com/post/102ijm9/spanish-data-regulator-changes-approach-and-requires-a-reject-button-in-cookie). Retrieved 2026-07-20. AEPD same-layer rule, 11 January 2024 deadline.
- [noyb, cookie banner complaints project](https://noyb.eu/en/project/cookie-banners). Retrieved 2026-07-20. Origin of the complaints that produced the EDPB taskforce.

---

## Notes

**The EU and UK have now genuinely diverged. Stop treating them as one region.** The Data (Use and Access) Act 2025 added exceptions to UK consent that do not exist in EU law: storage for **statistical purposes** (measuring use with a view to making improvements) and for **appearance/functionality** adaptation. Both come with a condition: the site must give users "a simple and free" way to object, and must stop on objection. That means a UK-only site can lawfully run some analytics without prior consent, provided it offers a working opt-out, while the identical build in Germany cannot. If a client has both audiences, either geo-branch the consent logic or apply the stricter EU rule everywhere. Applying the stricter rule everywhere is usually the right call for a small site: one code path, no geo-IP dependency.

**ePrivacy will not be replaced.** The Regulation proposal was withdrawn in February 2025. Anyone planning around "when the ePrivacy Regulation lands" is planning around something that is not coming. The fragmented national-law situation is the permanent state.

**No one-stop-shop.** GDPR's lead-authority mechanism does not apply to cookie placement; the taskforce confirmed this explicitly. A site reachable across the EU can be pursued by any national authority whose residents it reaches. There is no "our DPA is Ireland" shelter for cookies.

**Germany's Consent Management Ordinance (EinwV).** Issued 6 February 2025 by the federal digital and transport ministry with Bundesrat consent (BGBl. 2025 I Nr. 32), in force from 1 April 2025, intended to let users express cookie choices once via a recognised consent-management service. UNVERIFIED as of 2026-07-20: whether any services have actually been recognised under it and whether honouring their signal is now expected in practice. Worth a check before building a German-market site.

**IAB TCF litigation is unresolved and trending against the regulator.** The Belgian Market Court annulled the DPA's February 2022 decision on 14 May 2025, on procedural grounds, while confirming the substantive infringement findings and the EUR 250,000 fine. UNVERIFIED: a further ruling on 9 January 2026 said to annul the DPA's validation of IAB Europe's action plan and send it back to the DPA. The Belgian DPA's own case page records nothing after 14 May 2025 and its news feed through 2026 carries no such item; confirm before relying on it. The CJEU (C-604/22, 7 March 2024) held the TC String is personal data and IAB Europe is a joint controller for its creation and use, but not for downstream vendor processing. Net effect: TCF is not unlawful, IAB Europe's liability is narrower than the DPA argued, and none of it changes the obligations on the individual site owner. Do not let a client's ad-tech vendor cite these rulings as a reason to loosen the banner.

**Watch for browser-level signals.** Global Privacy Control is legally binding in California (see `ccpa-cpra.md`) and has no equivalent status under ePrivacy. Honouring GPC in the EU is good practice and costs almost nothing once consent state is already centralised, but it does not substitute for the banner.

**Conflicts with other files in this library:** overlaps `gdpr.md` (the downstream processing and the lawful basis for it), `ccpa-cpra.md` (opt-out model rather than opt-in, so a single global banner design will not satisfy both without branching), and `ada-wcag.md` (the banner is UI and must meet the same keyboard and contrast gates as everything else). Where GDPR and ePrivacy both apply to one tag, ePrivacy governs the read/write and GDPR governs what happens after, and a failure at the ePrivacy step makes the GDPR step unlawful too.

**Recheck date.** National guidance under this Directive moves faster than the Directive. Re-review before any EU or UK project, and no later than 2027-01-20.
