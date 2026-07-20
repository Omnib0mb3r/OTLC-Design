# LGPD: Lei Geral de Protecao de Dados Pessoais (Lei nº 13.709/2018)

| Field | Value |
|---|---|
| **Jurisdiction** | Brazil (federal). Reaches non-Brazilian companies, see "Applies when". |
| **Regulator / enforcer** | ANPD, Agencia Nacional de Protecao de Dados. Renamed from *Autoridade* to *Agencia* and made a full regulatory agency by Lei nº 15.352/2026 (sanctioned 25 Feb 2026). Same acronym. |
| **In force since** | General provisions: 18 September 2020 (date fixed by Lei nº 14.058/2020). Sanctions (arts. 52 to 54): 1 August 2021 (art. 65, I). |
| **Last amended** | Lei nº 15.352, de 25 de fevereiro de 2026 (converted Medida Provisoria nº 1.317/2025; restructured the ANPD and amended the LGPD definition of *encarregado*). |
| **Last reviewed** | 2026-07-20 |
| **Status** | In force. |

## Applies when

Answer these at intake. Any one "yes" in the first group means LGPD applies.

- The site processes personal data and the processing operation happens in Brazilian territory (art. 3, I).
- The site offers goods or services to people located in Brazil, or processes data of people located in Brazil, whatever country the business or the servers sit in (art. 3, II). A US or EU client selling to Brazilian customers is caught. Portuguese-language pages, BRL pricing, or Brazil in a shipping or country dropdown are practical evidence of this.
- The personal data was collected in Brazilian territory, meaning the person was physically in Brazil at the moment of collection (art. 3, III and § 1).

Not caught: processing done by a natural person for purely private and non-economic ends, and processing done exclusively for journalistic, artistic, or academic purposes (art. 4). A commercial client site is never in these buckets.

Scale questions that change what you must build:

- **Is the client an "agente de tratamento de pequeno porte"?** Microempresa, empresa de pequeno porte, or startup under Resolucao CD/ANPD nº 2/2022. The revenue ceiling is the one in art. 3, II of Lei Complementar nº 123/2006: gross revenue at or below R$ 4,800,000.00 per calendar year. If yes, the client is not required to appoint an encarregado (Res. 2/2022, art. 11), may keep processing records in simplified form (art. 9), and gets double the standard deadlines (art. 14). Every other LGPD duty still applies.
- **Does the site send personal data outside Brazil?** Almost always yes for a studio build: US-hosted analytics, a US CRM, a US email platform, cloud hosting outside Brazil. This triggers Resolucao CD/ANPD nº 19/2024, see below.
- **Can under-18s use the site?** If the service is directed at or accessible to minors, Lei nº 15.211/2025 (ECA Digital) also applies as of 17 March 2026, and the ANPD enforces it. That is a separate file in this library; flag it at intake and do not treat LGPD compliance as covering it.

## What the site must have

| Requirement | What that means in the build |
|---|---|
| Privacy notice (Aviso de Privacidade) | A page at a stable URL, in Portuguese, linked from the footer of every page. It must state, per art. 9, the purpose of processing, the form and duration, the controller's identity and contact, who the data is shared with, the data subject's rights, and the legal basis relied on for each processing purpose. |
| A named legal basis for every processing purpose | Pick from the ten bases in art. 7. In practice a marketing site uses: *consentimento* (I) for marketing cookies and newsletter signup, *execucao de contrato* (V) for checkout and account data, *cumprimento de obrigacao legal* (II) for tax and invoicing records, and *legitimo interesse* (IX) for necessary cookies, security logs, and fraud prevention. Write the chosen basis next to each purpose in the privacy notice. Consent is not a catch-all: art. 8 requires it be specific and separate, so a single "I accept the terms" checkbox does not carry marketing consent. |
| Cookie banner with real granularity | Per the ANPD *Guia Orientativo: Cookies e Protecao de Dados Pessoais*, necessary cookies can rest on legitimate interest with notice and a right to object. Non-necessary cookies (marketing, analytics beyond what is needed to run the service) need active consent, with the ability to accept or reject by category. The banner must link to the cookie policy or privacy notice. Rejecting must be as easy as accepting, and withdrawal must be free and facilitated. |
| Scripts blocked until consent | Non-necessary tags do not fire on load. Google Analytics, Meta Pixel, TikTok Pixel, ad tech, session replay, and third-party embeds stay dormant until the visitor opts in for that category. |
| Encarregado (DPO) named and published | Art. 41 requires the controller to appoint an encarregado, and § 1 requires the identity and contact details be published clearly and objectively, preferably on the controller's website. Resolucao CD/ANPD nº 18/2024 adds that the appointment must be a formal written, dated, and signed act, that the encarregado must have autonomy, and that no specific certification is required. Put the name and a working contact address in the privacy notice, and ideally in the footer. Small-scale agents that skip the appointment must still publish a working communication channel for data subjects. |
| Rights request channel | The site must let a visitor exercise the art. 18 rights (confirmation, access, correction, anonymisation or deletion, portability, information on sharing, withdrawal of consent). Art. 19 sets the response timing: a simplified response immediately, or a complete declaration within 15 days. Build a form or a monitored address that routes to whoever actually handles this, and make sure the 15-day clock is owned by a person. |
| Consent records | Art. 8 § 2 puts the burden of proving consent on the controller. Log, per consent event: timestamp, the categories accepted and refused, the banner text version shown, and a durable visitor identifier. Keep it queryable. |
| International transfer mechanism | If personal data leaves Brazil, Resolucao CD/ANPD nº 19/2024 requires one of: an ANPD adequacy decision, ANPD standard contractual clauses (clausulas-padrao contratuais) incorporated without modification, ANPD-recognised equivalent clauses, ANPD-approved specific clauses, or global corporate rules. The deadline to retrofit existing contracts passed on 23 August 2025. All EU member states and the three EFTA countries in the EEA (Iceland, Liechtenstein, Norway) were recognised as adequate by Resolucao CD/ANPD nº 32, de 26 de janeiro de 2026. UNVERIFIED: whether the decision also names EU institutions, bodies, and agencies. The decision does not cover transfers made exclusively for public security, national defence, state security, or criminal investigation. **The United States has no adequacy decision**, so US-hosted vendors need the ANPD standard clauses in the contract. |
| Incident response plan | Resolucao CD/ANPD nº 15/2024 requires the controller to notify the ANPD and affected data subjects within 3 business days of learning that an incident affected personal data and poses relevant risk or damage. Small-scale agents get 6 business days. The notice content is specified. This is an operational commitment the client must own before launch, not a page you build. |

## How to verify

- Load the site in a clean profile with devtools Network open. Before touching the banner, filter for `google-analytics`, `googletagmanager`, `facebook`, `connect.facebook.net`, `tiktok`, `hotjar`, `clarity`. Any request to these before consent is a finding.
- Check Application > Cookies and Application > Local Storage before consent. Anything beyond session, CSRF, load balancing, and the consent-state cookie itself is a finding.
- Click "reject" or the equivalent. Reload. Confirm the non-necessary tags still do not fire and the choice persisted.
- Count clicks to reject versus clicks to accept from the first banner view. If reject takes more clicks, fix it.
- Grep the built output for the tag IDs (`G-`, `GTM-`, pixel IDs) and confirm each one sits behind a consent gate rather than a hardcoded `<script>` in the document head.
- Open the privacy notice and check it names a legal basis per purpose, names the controller with contact details, and names the encarregado or a data subject communication channel. If any of these is a placeholder, the page is not deliverable.
- Confirm the rights request form or address actually delivers to a real inbox someone monitors. Send a test.
- Ask the client for the signed appointment document for the encarregado, or written confirmation they qualify as a small-scale agent and have a published channel instead.
- Ask the client whether the ANPD standard contractual clauses are in place with each non-Brazilian processor the site sends data to. List those processors from the Network tab so the question is concrete.
- Confirm the privacy notice and banner are available in Portuguese. An English-only notice on a site targeting Brazil is a defect.

## Penalties

Art. 52 of the LGPD sets the sanctions. Verified figures:

- Simple fine of up to **2% of the legal entity's revenue in Brazil in its last fiscal year, excluding taxes, capped at R$ 50,000,000.00 per infraction** (art. 52, II).
- Daily fine, subject to the same overall cap (art. 52, III).
- Warning with a deadline for corrective measures, publication of the confirmed violation, blocking of the data until it is brought into compliance, deletion of the data, partial suspension of a database or of processing activities for up to 6 months (renewable), and partial or total prohibition of processing activities (art. 52, I, IV, V, VI, X, XI, and XII; incisos VII to IX were vetoed and do not exist).

Resolucao CD/ANPD nº 4/2023 (Regulamento de Dosimetria, in force 27 February 2023) sets how the base fine is calculated. The ANPD classifies the infraction as leve, media, or grave and applies a base rate to revenue net of taxes. The base rate bands are: leve 0.08% to 0.15%, media 0.13% to 0.50%, grave 0.45% to 1.50%. Aggravating factors include specific and generic recidivism and failure to comply with ANPD orders; mitigating factors include stopping the infraction before proceedings open, having good-practice policies in place, and cooperating.

Enforcement reality as of mid-2026: monetary fines have been small. The first LGPD fine, against the telemarketing firm Telekall Infoservice for processing WhatsApp contact data without a legal basis and for failing to appoint an encarregado, was two penalties of R$ 7,200.00 each, R$ 14,400.00 in total, announced 6 July 2023. UNVERIFIED: secondary reporting states that figure was still roughly the total of pecuniary fines issued into early 2026, because most sanctioned entities were public bodies that do not pay fines. I could not confirm the running total against an ANPD source. Do not sell this as a low-risk law on that basis: the ANPD became a full regulatory agency in February 2026 with 200 new specialist posts, and its non-monetary powers (blocking, deletion, suspension of processing) can stop a site's operation regardless of fine size.

## Common ways sites fail this

- Reusing a GDPR cookie banner and never naming a legal basis per purpose in the Portuguese privacy notice.
- Firing Google Analytics and the Meta Pixel on page load, with the banner as decoration.
- "Accept all" as a prominent button and rejection buried behind a settings modal.
- No encarregado named anywhere on the site, and no substitute communication channel either.
- A privacy notice in English only on a site whose whole audience is Brazilian.
- Treating a signup checkbox as consent for marketing cookies, analytics, and newsletter at once, when art. 8 requires specific and separate consent.
- Shipping data to US vendors with no ANPD standard contractual clauses in the processor contracts, usually because nobody asked.
- No consent log, so the client cannot discharge the art. 8 § 2 burden of proving consent.
- No owner for the 15-day rights response clock or the 3-business-day incident clock.

## Sources

- [Lei nº 13.709/2018 (LGPD), full text, Planalto](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm) (retrieved 2026-07-20)
- [Lei nº 15.352, de 25 de fevereiro de 2026, Camara dos Deputados](https://www2.camara.leg.br/legin/fed/lei/2026/lei-15352-25-fevereiro-2026-798731-publicacaooriginal-178208-pl.html) (retrieved 2026-07-20)
- [ANPD, Transferencia Internacional de Dados (Res. 19/2024, adequacy decisions)](https://www.gov.br/anpd/pt-br/assuntos/assuntos-internacionais/transferencia-internacional-de-dados) (retrieved 2026-07-20)
- [Resolucao CD/ANPD nº 2, de 27 de janeiro de 2022, agentes de tratamento de pequeno porte](https://www.gov.br/anpd/pt-br/acesso-a-informacao/institucional/atos-normativos/regulamentacoes_anpd/resolucao-cd-anpd-no-2-de-27-de-janeiro-de-2022) (retrieved 2026-07-20)
- [Resolucao CD/ANPD nº 4, de 24 de fevereiro de 2023, Regulamento de Dosimetria (PDF)](https://www.gov.br/anpd/pt-br/assuntos/noticias/anpd-publica-regulamento-de-dosimetria/Resolucaon4CDANPD24.02.2023.pdf) (retrieved 2026-07-20)
- [ANPD, Guia Orientativo: Cookies e Protecao de Dados Pessoais (PDF)](https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia-orientativo-cookies-e-protecao-de-dados-pessoais.pdf) (retrieved 2026-07-20)
- [ANPD, first LGPD fine (Telekall Infoservice)](https://www.gov.br/anpd/pt-br/assuntos/noticias/anpd-aplica-a-primeira-multa-por-descumprimento-a-lgpd) (retrieved 2026-07-20)
- [Resolucao CD/ANPD nº 18, de 16 de julho de 2024, encarregado (PDF, IPEA mirror)](https://www.ipea.gov.br/protecaodedados/arquivos/Resolucao_cd_regulamento_atuacao_encarregado.pdf) (retrieved 2026-07-20)
- [Senado Federal, Sancionada lei que cria a Agencia Nacional de Protecao de Dados](https://www12.senado.leg.br/noticias/materias/2026/02/26/sancionada-lei-que-cria-a-agencia-nacional-de-protecao-de-dados) (retrieved 2026-07-20)
- [Resolucao CD/ANPD nº 4/2023, article text (LegisWeb mirror, used for alíquota-base bands)](https://www.legisweb.com.br/legislacao/?id=442688) (retrieved 2026-07-20)
- [Resolucao CD/ANPD nº 15, de 24 de abril de 2024, incident notification (LegisWeb mirror)](https://www.legisweb.com.br/legislacao/?id=458235) (retrieved 2026-07-20)
- [Resolucao CD/ANPD nº 32, de 26 de janeiro de 2026, EU/EEA adequacy decision (DOU)](https://www.in.gov.br/web/dou/-/resolucao-n-32-de-26-de-janeiro-de-2026-683334547) (retrieved 2026-07-20)
- [LGPD article text mirror, used to verify arts. 3, 7, 19, 41, 52, 65](https://lgpd-brasil.info/) (retrieved 2026-07-20)

## Notes

- **Source caveat.** planalto.gov.br refused connections from this machine on every attempt during research, and several gov.br pages returned 401. Article text for arts. 3, 7, 19, 41, 52, and 65 was verified against the lgpd-brasil.info mirror, and the art. 52 fine cap was independently corroborated by art. 15, II of Resolucao nº 4/2023. Before relying on any exact wording for a client deliverable, open the Planalto link and confirm. On the 2026-07-20 re-check, planalto.gov.br still refused the connection and the ANPD Telekall news page returned 401 to automated fetches; both open normally in a browser, so treat those two as live links that block bots rather than as dead links.
- **In-force date precision.** The 1 August 2021 date for the sanctions articles is verified from art. 65. The general in-force date is 18 September 2020, fixed by Lei nº 14.058/2020 rather than by the original art. 65 vacatio. Art. 65 as enacted set 24 months from publication for the general provisions; Lei nº 14.058/2020 landed on 18 September 2020 and that is the date to cite.
- **MP number discrepancy.** The Senado states Lei nº 15.352/2026 originated from Medida Provisoria nº 1.317/2025 via a projeto de lei de conversao. The enacted text itself, at art. 20, revokes a different measure, Medida Provisoria nº 1.319, de 17 de setembro de 2025. Both statements can be true, but if the MP number matters for a client memo, check the Congresso Nacional tramitation record rather than relying on this file.
- **Watch the ANPD's new posture.** The agency conversion in February 2026 came with 200 specialist posts filled by public exam. Expect enforcement volume to rise from the historically low base. Judge current risk by enforcement activity, not by the historical fine total.
- **ECA Digital overlaps.** Lei nº 15.211/2025 has applied since 17 March 2026 and is enforced by the ANPD. It bans age self-declaration for age-restricted services and requires auditable age-verification mechanisms. If a client site is directed at or usable by minors, LGPD work alone does not discharge it.
- **Interaction with GDPR.** For a client caught by both, the LGPD file is mostly a delta on top of GDPR work: the same consent architecture usually satisfies both, but LGPD adds the encarregado publication duty, Portuguese-language notices, and the ANPD standard contractual clauses for transfers out of Brazil. GDPR SCCs do not substitute. Since late January 2026 the EU and EEA are adequate for Brazil-to-EU flows, which simplifies EU-hosted stacks but does nothing for US-hosted ones.
- **Consent versus legitimate interest for analytics.** The ANPD cookie guide allows legitimate interest for necessary cookies only. Do not let a client argue analytics into that bucket without a documented legitimate interest assessment, and note this is a live area where ANPD guidance is softer than the equivalent EU position.
