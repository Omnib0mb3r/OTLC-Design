# Asset Licensing: Third-Party Content, Font, Icon, and Code License Obligations in a Web Build

| Field | Value |
|---|---|
| **Jurisdiction** | Global. Copyright is territorial but near-universal via the Berne Convention. License terms are contract, enforceable wherever the contract is. The Google Fonts privacy angle is EU/EEA/UK specific. |
| **Regulator / enforcer** | No single regulator. Enforced by rights holders directly (foundries, stock agencies, photographers, open-source maintainers) through civil courts. In the US: federal courts under Title 17. Font and stock claims usually arrive as a demand letter from the licensor or its agent, not a regulator. |
| **In force since** | Berne Convention 1886. US Copyright Act of 1976 (Title 17), effective 1978-01-01. DMCA section 1202 (copyright management information) effective 1998. Individual license texts vary: SIL OFL 1.1 (2007), CC 4.0 suite (2013-11-25), GPL-3.0 and AGPL-3.0 (2007). |
| **Last amended** | Varies per instrument. CC 4.0 is the current CC version. No newer OFL, GPL, or AGPL version has superseded those listed as of this review. |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. This is not one statute: it is a cluster of copyright law plus private license contracts that bind every build. |

> **Scope note.** This file is a build-time compliance checklist, not legal advice. Unlike the privacy laws in this library, most of the risk here is contractual: you agreed to terms at download time. Read the actual EULA for the actual asset. Foundry terms in particular vary so much that no general rule survives contact with a specific license.

## Applies when

Answer these at intake. Any "yes" pulls this file into scope.

- **The build ships any asset the studio did not create from nothing.** Photos, video, audio, fonts, icons, illustrations, 3D models, Lottie files, templates, code libraries. In practice this is every build.
- **The site loads any font from a third-party server** (`fonts.googleapis.com`, `use.typekit.net`, `fast.fonts.net`, a foundry CDN) **and has EU, EEA, or UK visitors.** This is a data protection trigger on top of the licensing one. See the GDPR file in this library.
- **A typeface is used on the web that was licensed for desktop use.** Buying a font for Illustrator does not license `@font-face`. These are separate tiers at essentially every commercial foundry.
- **The designer used a font from a personal subscription** (Adobe Fonts, Monotype Fonts, a foundry subscription) **and the client will own the site.** Subscription font rights usually do not transfer with the deliverable.
- **Any photo shows an identifiable person.** Triggers the model release question, which is separate from the copyright license.
- **Any photo shows private property, a recognizable building interior, branded goods, artwork, or a trademark.** Triggers the property release and trademark questions.
- **Any asset is marked "editorial use only."** Hard block on commercial, promotional, and advertising use, which includes an ordinary client marketing site.
- **Any asset is Creative Commons licensed.** Attribution is a license condition, so failing it makes the use an infringement, not a rudeness.
- **The CC license carries `NC` and the client is a commercial business.** Almost always disqualifying for a client marketing site.
- **The CC license carries `ND` and you cropped, recolored, filtered, or composited the asset.** Disqualifying.
- **The CC license carries `SA` and the asset is combined into a larger work you want to keep proprietary.** Check whether the combination is an adaptation.
- **Any npm, PyPI, or vendored dependency is GPL, AGPL, SSPL, or has a non-commercial or "fair use" style rider.** AGPL is the sharp one for hosted apps.
- **Any GPL-licensed JavaScript is served to the browser.** The FSF treats sending JS to a visitor as distribution, which triggers the source obligation. Running GPL code server-side does not.
- **The deliverable is a template, theme, or product that will be resold**, or the asset is the main value of a product for sale (merchandise, print-on-demand). Standard stock licenses do not cover this.
- **Any asset came from a Figma Community file, a Dribbble shot, a Pinterest board, an AI image tool, or a "free download" aggregator** with no license file. Treat provenance as unknown until proven.

**Who is not caught:** nothing meaningful. Even an all-custom build usually pulls in a font, an icon set, and a dependency tree.

## What the site must have

| Requirement | What that means in the build |
|---|---|
| **Font licenses that match actual usage tier** | For every typeface: hold a webfont license covering `@font-face` use, not only a desktop license. Record the licensee name, the domain(s) covered, and any usage cap. If the client owns the site, the license must be in the client's name or transferable to them. |
| **Self-hosted fonts by default** | Serve `.woff2` from the site's own origin or the client's own CDN. This removes the third-party request entirely and resolves the EU privacy issue at the same time. Google Fonts are redistributable and explicitly support self-hosting: their licenses (mostly SIL OFL 1.1, some Apache 2.0, Ubuntu fonts under UFL 1.0) permit it. |
| **No `fonts.googleapis.com` or `fonts.gstatic.com` request for EU-facing sites** | Loading fonts from Google's CDN transmits the visitor's IP address to Google. LG München I held on 2022-01-20 that doing this without consent is unlawful and awarded the plaintiff EUR 100 plus interest, an injunction, and a right to information. Self-host, or gate the request behind consent. Self-hosting is the correct fix; consent-gating a font is a bad user experience. |
| **Font files not left publicly enumerable when the EULA forbids it** | Some commercial EULAs require obfuscated paths or domain-locking. Check the specific EULA. Do not assume. |
| **Webfont usage within any metered cap** | Some commercial webfont licenses meter by monthly pageviews, unique visitors, or domain count, and require a paid upgrade past a threshold. The cap and the metric are set per purchase, so read the invoice and the EULA and record both. Set a calendar reminder if the client's traffic is growing toward a cap. |
| **Stock assets used within their tier** | Royalty-free (RF): one fee, perpetual, unlimited media, non-exclusive. Rights-managed (RM): priced to a specific use, duration, and placement, and limited to what was authorized. Comp or preview files must never reach production. Adobe Stock's standard license caps reproduction at 500,000 copies or viewers and forbids resaleable merchandise where the asset is the main value; the extended license lifts both. |
| **Editorial-only assets kept out of commercial contexts** | An "editorial use only" image cannot appear in a hero, an ad, a promo, a product page, or anything implying endorsement. Getty's terms restrict editorial content to newsworthy or public interest use and require a credit in the form `[Photographer]/[Collection] via Getty Images`. Adobe Stock likewise requires attribution and preservation of editorial context. |
| **Model and property releases confirmed where needed** | Getty warrants releases only where it specifically says a release exists, and states that releases are generally not obtained for editorial content. Where no release exists, the obligation to clear the person or property is yours. Free-license sources are the worst case here: the Unsplash License grants copyright permission only and says nothing about the people in the frame, so an Unsplash photo of an identifiable person used in advertising is a publicity-rights exposure with no indemnity behind it. |
| **Sensitive-use disclaimer where required** | Getty requires that a model shown in an unflattering or sensitive context (illness, addiction, and similar) carry a visible note such as "Stock photo. Posed by model" and an indication that the image is illustrative. Build this into the caption, not the alt text alone. |
| **CC attribution rendered in the page, in TASL form** | For every CC-licensed asset, credit must appear where a viewer can see it. Creative Commons recommends Title, Author, Source, License: the work's title, the creator's chosen name, a link to the original, and the license name with a link to its deed. CC BY 4.0 requires credit, a link to the license, and an indication of whether changes were made. A credit buried in a git commit or a source comment does not satisfy this. |
| **Adaptation notice where the asset was modified** | If you cropped, recolored, or composited a CC work, say so and, for an adaptation, state the original TASL plus your own contribution and license. |
| **Icon set licenses satisfied** | Font Awesome Free splits three ways: icons (SVG and JS) under CC BY 4.0, the packaged web and desktop font files under SIL OFL 1.1, and all non-font non-icon code under MIT. The embedded attribution comments in the distributed files carry the credit, so do not let a minifier or an SVG optimizer strip them. Lucide is ISC, with Feather-derived icons under MIT (Cole Bemis), and both require the notice to travel with copies. Noun Project free-tier icons are CC BY 3.0 and attribution is mandatory; the paid royalty-free tier removes the attribution requirement but caps units at 1,000 where the icon carries substantial product value. |
| **A licenses or credits page where attribution is owed** | Ship `/licenses` or `/credits` (or a clearly labeled section of the colophon) listing every asset that carries an attribution condition. Link it from the footer. This is the single artifact that resolves most CC and MIT notice obligations at once. |
| **Copyright management information left intact** | Do not strip IPTC/XMP credit and copyright fields from licensed images during your build pipeline, and do not remove license headers from vendored code. Removing this information is a separate statutory violation under US law, independent of whether the underlying use was licensed. Audit your image optimizer's metadata-stripping default. |
| **Dependency licenses inventoried and compatible** | Generate a dependency license report and keep it with the project. Permissive licenses (MIT, ISC, BSD, Apache 2.0) need the notice preserved in distributed bundles. Apache 2.0 additionally requires that a `NOTICE` file, if present upstream, be reproduced. |
| **No AGPL in a hosted product unless you intend to publish source** | AGPL-3.0 section 13 requires that a modified version interacted with remotely over a network prominently offer all such users the Corresponding Source at no charge from a network server. Running it as a SaaS is the trigger; there is no distribution exemption. Either remove it, buy a commercial exception, or plan to publish. |
| **No GPL JavaScript shipped to the browser without source** | The FSF's position is that JS distributed to visitors is distribution, so the source for that program must be released. Server-only GPL use does not trigger this. |
| **Records: a provenance manifest** | Keep one file per project recording, for every third-party asset: source, license or order number, licensee name, tier, cap, expiry, and where the license PDF lives. Retain for the life of the site plus the local limitation period. Without this, a demand letter three years from now is unanswerable. |

## How to verify

Run all of these before delivery.

**Third-party requests**

1. Open DevTools, Network panel, hard reload with cache disabled, filter by `Font`. Every entry must be same-origin or the client's own CDN. Any `fonts.gstatic.com`, `use.typekit.net`, or foundry host is a finding.
2. Set the Network filter to third-party and reload the full site including interior pages. Anything unexpected is either a tracker or an asset you are hotlinking.
3. Grep the whole repo, including built output and any CMS-authored content: `fonts.googleapis.com`, `fonts.gstatic.com`, `use.typekit.net`, `typekit`, `p.typekit.net`, `fast.fonts.net`, `kit.fontawesome.com`. Check compiled CSS and any inlined `<style>` blocks, not only source. Tailwind and CMS themes reintroduce these silently.
4. Check for `@import url(https://fonts.googleapis.com...)` inside CSS, which the Network panel will show but a source grep of HTML will miss.

**Fonts**

5. List every `@font-face` `src` in the built CSS and map each family to a license document. If a family has no license document, it does not ship.
6. Confirm the license type on each document reads webfont, not desktop only. Confirm the licensee name matches whoever will own the site.
7. If the font came from a designer's subscription (Adobe Fonts, Monotype Fonts), confirm in writing whether the rights transfer to the client. Assume they do not until confirmed.
8. Check whether any font is used in the client's logo or wordmark. Logo use is a separate grant at many foundries and is a frequent gap.

**Images and video**

9. For every image in the build, confirm a source and license line exists in the provenance manifest. No orphans.
10. Grep the manifest for "editorial" and confirm none of those files appear in a marketing, hero, or ad context.
11. For every photo containing a recognizable face, confirm either a model release exists or the use is non-commercial and non-endorsing.
12. Run `exiftool` over the delivered image directory and confirm IPTC `Credit`, `Copyright`, and `Rights` fields survived the build pipeline where the license requires them. Check your image optimizer config: most strip all metadata by default.
13. Confirm no filename or path contains `comp`, `preview`, `watermark`, `-sample`, or a stock ID pattern suggesting an unlicensed download.

**Code and icons**

14. Generate a dependency license report (`license-checker`, `license-checker-rseidelsohn`, `pnpm licenses list`, `cargo-deny`, or equivalent) and read it. Do not skim it.
15. Grep the report for `GPL`, `AGPL`, `SSPL`, `CC-BY-NC`, `BUSL`, `Elastic`, `UNKNOWN`, and `UNLICENSED`. Every hit needs a decision recorded.
16. Confirm the production bundle still contains required license headers. Check your minifier's comment-preservation setting (`/*!` banners, Terser `comments: 'some'`).
17. Confirm SVGO or your icon pipeline has not stripped attribution comments from Font Awesome or other CC BY icon sources.
18. If a Font Awesome Pro kit is in use, confirm the kit domain allowlist matches the production domain and that the kit belongs to the client, not the studio.

**Attribution surface**

19. Load the site and click the footer credits or licenses link. Confirm it exists, resolves, and lists every asset with an attribution condition.
20. For each CC entry, confirm all four TASL parts are present and that the license name links to the license deed.
21. Confirm modified CC works are flagged as modified.

### Pre-delivery asset provenance checklist

One row per third-party asset. Nothing ships with a blank cell.

- [ ] **Asset** identified by file path in the repo
- [ ] **Type**: photo, video, audio, font, icon, illustration, library, template
- [ ] **Source**: exact URL or vendor, not "the internet" or "the designer sent it"
- [ ] **License or order number**, and where the license PDF or receipt is stored
- [ ] **Licensee of record**: studio or client, and whether it transfers on handover
- [ ] **Tier**: RF, RM, standard, extended, editorial, desktop, webfont, app, server
- [ ] **Usage cap**: pageviews, impressions, copies, units, domains, seats. Write "none" only if the EULA actually says so
- [ ] **Expiry or renewal date**, and whether the site breaks when it lapses
- [ ] **Attribution required**: yes/no. If yes, where it is rendered on the site
- [ ] **Release status** for photos: model release, property release, neither, not applicable
- [ ] **Editorial-only**: yes/no, and if yes, the context it appears in
- [ ] **Modified**: yes/no, and whether the license permits modification
- [ ] **AI-generated**: yes/no, and the tool and prompt if yes
- [ ] Client has been given a copy of the manifest and the license documents at handover

## Penalties

**United States, copyright infringement.** Statutory damages under 17 U.S.C. 504(c) run from $750 to $30,000 per work infringed, at the court's discretion. Willful infringement raises the ceiling to $150,000 per work. Where the infringer proves it was unaware and had no reason to believe the act was infringing, the court may reduce the award to as low as $200. Statutory damages require timely registration by the rights holder; otherwise the claim is for actual damages and profits.

**United States, removing copyright management information.** 17 U.S.C. 1203(c)(3)(B) sets statutory damages for a section 1202 violation at not less than $2,500 and not more than $25,000 per violation. This is the exposure for stripping credit and copyright metadata, and it is independent of the infringement claim.

**EU, hotlinked Google Fonts.** LG München I awarded EUR 100 plus interest at five points over the base rate, an injunction against continued transmission, and an obligation to provide information about the data processed. The per-claimant figure is small. The risk is volume: the same claim can be brought by every visitor, and mass demand-letter campaigns have followed this ruling. Separately, GDPR administrative fines apply in principle to unlawful transfers, though the Munich case was a civil damages claim, not a regulatory fine.

**Font foundries and stock agencies.** These almost always arrive as a contractual demand: retroactive licensing at list rate for the tier you should have bought, often multiplied, plus costs. UNVERIFIED: specific multipliers and settlement figures vary by licensor and are not published. Do not quote a number to a client.

**Open-source enforcement.** Typically injunctive: comply, or stop distributing. Compliance for an AGPL violation means publishing your source, which is usually the outcome the client least wants and cannot be undone.

## Common ways sites fail this

- A `fonts.googleapis.com` link stays in the head after the fonts were supposedly self-hosted, usually because a starter template, a CMS theme, or an email template still references it.
- The designer bought a desktop license for the display face and shipped it as a webfont. Nobody checked which tier the invoice was for.
- The font came from the designer's personal Adobe Fonts or Monotype subscription. The site is handed to the client, the studio's subscription eventually lapses or the relationship ends, and the client's typography is now unlicensed or broken.
- The client's new logo is set in a licensed retail typeface with no logo grant.
- An editorial-only image is used in the hero because it looked right and the "editorial" tag was not visible in the download folder.
- An Unsplash photo of an identifiable person is used in an ad-like context. The copyright side is clean and the publicity-rights side is wide open.
- CC BY attribution exists only in a code comment, a commit message, or a README, and never renders in the page.
- A CC BY-NC asset ships on a commercial client site.
- A CC BY-ND asset is cropped to fit a hero aspect ratio.
- The image optimizer strips all IPTC and XMP metadata by default, deleting credit and copyright fields that the license required be preserved.
- SVGO strips the Font Awesome attribution comment out of icon sprites.
- An AGPL library gets pulled in transitively and nobody reads the license report before launch.
- A GPL jQuery plugin from 2014 is still in the bundle and is being served to browsers with no source offer.
- Icons are pulled from a Figma Community file whose author had no right to redistribute them.
- Assets are carried over from the client's previous site with no records, and everyone assumes the previous agency licensed them properly.
- The Font Awesome Pro kit is on the studio's account, so the client's site depends on the studio's subscription indefinitely.

## Sources

Official license texts, statutes, and court records first.

- [17 U.S.C. 504 (remedies for infringement: damages and profits)](https://www.law.cornell.edu/uscode/text/17/504), Cornell LII, retrieved 2026-07-20
- [17 U.S.C. 1203 (civil remedies, integrity of copyright management information)](https://www.law.cornell.edu/uscode/text/17/1203), Cornell LII, retrieved 2026-07-20
- [LG München I, judgment of 2022-01-20, Az. 3 O 17493/20 (Google Fonts, dynamic IP transmission)](https://www.gesetze-bayern.de/Content/Document/Y-300-Z-BECKRS-B-2022-N-612), Bayern.Recht, retrieved 2026-07-20
- [SIL Open Font License 1.1, full text](https://openfontlicense.org/documents/OFL.txt), retrieved 2026-07-20
- [GNU Affero General Public License v3.0, full text (section 13, remote network interaction)](https://www.gnu.org/licenses/agpl-3.0.en.html), Free Software Foundation, retrieved 2026-07-20
- [GNU GPL Frequently Asked Questions (web server use, JavaScript distribution, LGPL linking)](https://www.gnu.org/licenses/gpl-faq.html), Free Software Foundation, retrieved 2026-07-20
- [CC BY 4.0 license deed](https://creativecommons.org/licenses/by/4.0/), Creative Commons, retrieved 2026-07-20
- [Creative Commons FAQ (license variants, NC, ND, SA conditions)](https://creativecommons.org/faq/), retrieved 2026-07-20
- [Creative Commons recommended practices for attribution (TASL)](https://wiki.creativecommons.org/wiki/Recommended_practices_for_attribution), retrieved 2026-07-20
- [Getty Images content license agreement (RF vs RM, editorial restrictions, releases, sensitive use)](https://www.gettyimages.com/eula), retrieved 2026-07-20
- [Getty Images terms of use (embed and editorial use)](https://www.gettyimages.com/company/terms), retrieved 2026-07-20
- [Adobe Stock license terms (standard vs extended, 500,000 cap, editorial use only)](https://stock.adobe.com/license-terms), retrieved 2026-07-20
- [Unsplash License](https://unsplash.com/license), retrieved 2026-07-20
- [Font Awesome Free license file (CC BY 4.0 icons, OFL 1.1 fonts, MIT code)](https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/LICENSE.txt), retrieved 2026-07-20
- [Lucide license file (ISC, plus MIT for Feather-derived icons)](https://raw.githubusercontent.com/lucide-icons/lucide/main/LICENSE), retrieved 2026-07-20
- [Noun Project terms of use (CC BY 3.0 free tier, royalty-free paid tier, 1,000 unit cap)](https://thenounproject.com/legal/terms-of-use/), retrieved 2026-07-20
- [google/fonts repository README (licenses in use, self-hosting options)](https://raw.githubusercontent.com/google/fonts/main/README.md), retrieved 2026-07-20

## Notes

**Could not verify on this review.** Adobe (`helpx.adobe.com/fonts/using/font-licensing.html`) and Monotype (`monotypefonts.com/pages/eula`) both failed to return content, and Shutterstock (`shutterstock.com/license`) returned HTTP 403. Nothing specific about Adobe Fonts entitlements, Monotype pageview metering, or Shutterstock standard versus enhanced license terms is asserted in this file. Verify those three directly against the current EULA before relying on them. This is the largest gap here and the one most worth closing on the next review, because Adobe Fonts and Monotype cover most commercial type in circulation.

**Webfont pageview caps have no universal rule.** Metering models differ by foundry and have changed repeatedly. Some meter monthly pageviews, some cumulative, some unique visitors, some domains, some sell perpetual unlimited. Any number written into this file would go stale. Record the cap per purchase in the project manifest instead.

**The Google Fonts issue is two problems wearing one coat.** Licensing is fine: Google Fonts are redistributable and self-hosting is expressly supported. The exposure is data protection, because the browser's request hands the visitor's IP to a third party. Self-hosting closes both at once, which is why it is the default in this system rather than a conditional recommendation. Cross-reference the GDPR file in this library for the lawful-basis analysis.

**Watch the German demand-letter wave.** Following the 2022 Munich ruling, mass automated claims were filed against sites embedding Google Fonts. UNVERIFIED: subsequent German decisions reportedly treated some of these campaigns as abusive, and at least one criminal investigation was reported. The status and outcome of that follow-up litigation was not confirmed on this review. Do not tell a client the risk has passed. The fix costs an hour.

**AI-generated assets are an open question this file does not resolve.** Getty's terms prohibit using their content to train machine learning models. The converse (whether an AI-generated image the studio produced is protectable, and whether it carries infringement risk from its training data) is unsettled and litigation is active. Record AI-generated assets in the manifest so the answer can be applied retroactively when it arrives.

**Provenance is the deliverable that survives you.** Most of these failures are not detectable from the site itself years later. The manifest, handed to the client with the license documents at handover, is what turns a demand letter into a five-minute answer. Treat it as a required artifact, not paperwork.

**Related files in this library.** GDPR (third-party asset requests as data transfers, consent gating), accessibility (icon and image alt text obligations are separate from licensing and are not satisfied by a credit line).
