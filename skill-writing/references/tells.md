# tells.md - complete taxonomy

Full reference behind [`../SKILL.md`](../SKILL.md). The skill body carries the working subset; this file carries everything, with verbatim watch-phrase lists.

**Source:** [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), en.wikipedia.org. Distilled 2026-07-20.

**Note on quoted examples:** where a source example contained an em dash, it is rendered here as `--` and flagged, because the global no-em-dash rule bans emitting the character even inside a quotation. The em dash in the original is itself one of the tells.

---

## Vocabulary eras

Which words cluster tells you which model generation produced the text. These are soft boundaries, not cutoffs.

| Era | Model | Overused words |
|-----|-------|----------------|
| 2023 to mid-2024 | GPT-4 | Additionally, boasts, bolstered, crucial, delve, emphasizing, enduring, garner, intricate/intricacies, interplay, key, landscape, meticulous/meticulously, pivotal, underscore, tapestry, testament, valuable, vibrant |
| Mid-2024 to mid-2025 | GPT-4o | align with, bolstered, crucial, emphasizing, enhance, enduring, fostering, highlighting, pivotal, showcasing, underscore, vibrant |
| Mid-2025 onward | GPT-5 | emphasizing, enhance, highlighting, showcasing, plus the notability/attribution vocabulary in §Canned notability below |

`delve` peaked in 2023 and early 2024, declined through 2024, and dropped off sharply in 2025. Its presence dates a text.

Grok is idiosyncratic across all eras: it overuses superficially scientific `causal`, `empirical`, `correlate`, and still overuses `underscore` as of 2026.

**Full master list (any era):** Additionally (especially sentence-initial), align with, boasts (meaning "has"), bolstered, crucial, delve, emphasizing, enduring, enhance, fostering, garner, highlight (as a verb), interplay, intricate/intricacies, key (as an adjective), landscape (as an abstract noun), meticulous/meticulously, pivotal, robust, showcase, tapestry (as an abstract noun), testament, underscore (as a verb), valuable, vibrant.

The lists are literal. Overuse of a word does not implicate its synonyms.

### Worked example (Jameh Mosque of Ashtarjan, 2024 revision)

> "The inscriptions also offer **valuable** insights into the construction of the mosque. They record the names of the **key** craftsmen involved [...] These names **highlight** the collaborative nature of mosque construction and **emphasize** the contributions of skilled artisans. [...] also **underscores** the **enduring** practice of pious patronage."

Six vocabulary hits in one paragraph. That density is the tell, not any single word.

---

## Content tells

### Undue emphasis on significance, legacy, and broader trends

*Words to watch:* stands/serves as, is a testament/reminder, a vital/significant/crucial/pivotal/key role/moment, underscores/highlights its importance/significance, reflects broader, symbolizing its ongoing/enduring/lasting, contributing to the, setting the stage for, marking/shaping the, represents/marks a shift, key turning point, evolving landscape, focal point, indelible mark, deeply rooted.

LLMs inflate a subject by asserting that arbitrary aspects of it contribute to some larger story. There is a small, identifiable repertoire of phrasings for this.

> "The Statistical Institute of Catalonia was officially established in 1989, **marking a pivotal moment** in the evolution of regional statistics in Spain. [...] The founding of Idescat **represented a significant shift** toward regional statistical independence [...] This initiative **was part of a broader movement** across Spain."

> "Kumba has long been **an important center** for trade and agriculture. [...] road networks [...] helped **solidify its role as a regional hub**."

### Canned emphasis on notability, attribution, and media coverage

*Words to watch:* independent coverage, local/regional/national/[country] media outlets, music/business/tech outlets, trade publications, profiled in, written by a leading expert, active social media presence.

The model enumerates sources to argue that the subject matters, often misattributing its own commentary to those sources. Common in 2025 and later output.

### Superficial analyses

*Words to watch:* highlighting/underscoring/emphasizing, ensuring, reflecting/symbolizing, contributing to, cultivating/fostering, encompassing, enhancing, valuable insights, align/resonate with.

Surface-level commentary arrives as a trailing participle phrase or is pinned on a vague source. Frequently this is unattributed opinion or synthesis wearing the costume of analysis.

### Promotional and advertisement-like language

*Words to watch:* boasts a, vibrant, rich, profound, enhancing, showcasing, exemplifies, commitment to, natural beauty, nestled, in the heart of, groundbreaking, renowned, featuring, diverse array.

Models drift to travel-guide or press-release tone even when prompted for neutrality.

### Vague attributions and overgeneralization of opinions

*Words to watch:* Industry reports, Observers have cited, Experts argue, Some critics argue, several sources/publications (when only a few are cited), such as (in front of an exhaustive list).

Weasel wording. Also inflates how many sources exist.

### Outline-like conclusions about challenges and future prospects

*Words to watch:* "Despite its ... faces several challenges", "Despite these challenges", headings named "Challenges and Legacy" or "Future Outlook".

A rigid closing formula: name difficulties, then offer vague positive reassessment or speculation about future initiatives.

### Leads treating broad titles as proper nouns

The model introduces a descriptive title as though it names a real-world entity. Reads unnatural immediately.

---

## Language and grammar tells

### Avoidance of basic copulatives

*Words to watch:* serves as / stands as / marks / functions as / operates as / represents [a], boasts / features / maintains / offers [a], refers to.

Marketing-adjacent substitutes for `is` and `are`.

### Negative parallelisms

Three variants:

1. **Not just X, but also Y** - "Not only ... but ...", "It is not just ..., it's ..."
2. **Not X, but Y** - denies the first characteristic outright
3. **X rather than Y** - the reversed form, heavy in Grok output

The construction implies the reader held an incomplete or wrong view and is now being corrected.

> "This choice of language is **not only dismissive but also** unnecessarily harsh and confrontational."

> "These comments are **not just dismissive [em dash] they're outright disrespectful.**" (original used an em dash at the break)

> "'Self-Portrait' by Yayoi Kusama [...] constitutes **not only a work of self-representation, but** a visual document of her obsessions."

Common among human writers too, especially in myth-busting listicles. That is precisely why it is a stereotype tell now.

### Rule of three

Triadic structures: adjective-adjective-adjective, or short phrase, short phrase, and short phrase. Used to make shallow analysis appear comprehensive.

### Lexical diversity / elegant variation

Generative models carry a repetition penalty that discourages reusing a word, producing chains of synonyms for one referent.

> "the constraints of socialist realism" → "the challenging climate of Soviet artistic constraints" → "the confines of state-imposed artistic norms" (one concept, three names)
> "non-conformist artists" → "these artists" → "like-minded artists"
> "their creativity" → "the immense talent" → "their artistic aspirations"

Measured effect: post-2023 Wikipedia text shows higher lexical diversity than pre-2023, matching GPT-4o-mini and Gemini-1.5-Flash output.

Caveat: if separate edits were generated independently, this tell will not appear across them.

---

## Style tells

| Tell | Detail |
|------|--------|
| Title case in headings | "Impact of Technology and Digitalization", "Sustainable Development and Environmental Law" |
| Overuse of boldface | Mechanical, often every instance of a chosen term, or "key takeaways" styling. Inherited from readmes, sales material, how-to guides |
| Inline-header vertical lists | `• **Header**: description` repeated, often with a bare bullet, hyphen, en dash, or hash character instead of proper markup |
| Overuse of em dashes | Higher frequency than human writers, often spaced, contrary to typographic guidance. Mimics "punched up" promotional writing |
| Emoji as formatting | Emoji as list markers, separators, decoration |
| Unusual use of tables | Tables deployed where prose or a list belongs |
| Curly quotes and apostrophes | ChatGPT and DeepSeek in particular. Weak alone: professional typesetting and Word smart quotes do the same |
| Skipping heading levels | Starting at level 3 with no level 2. Accessibility failure |
| Thematic breaks before headings | `----` above each heading, a Markdown-to-wikitext conversion artifact |
| Markdown in the wrong medium | `**bold**`, `*italic*`, `#header` where the medium does not use Markdown |

---

## Communication intended for the user

Chatbot output that survived the copy-paste.

*Words to watch:* I hope this helps, Of course!, Certainly!, You're absolutely right!, Would you like..., is there anything else, let me know, more detailed breakdown, here is a.

Also: **collaborative framing** ("Let's explore", "We'll discuss"), **knowledge-cutoff disclaimers** and speculation about gaps in sources ("as of [date]"), and **phrasal templates and placeholder text** left unfilled.

---

## Edit-summary and comment tells

Relevant when reviewing PR descriptions, commit messages, or issue comments, not only wiki edits.

**Canned assurance of policy adherence.** *Words to watch:* ensured that ... adheres to, improved, in compliance/complies with, revised, verifiability, neutrality, neutral tone, encyclopedic tone.

**Mentions of preserved or retained information.** *Words to watch:* preserved/preserving, retained/retaining.

**Overemphasis on citations.** *Words to watch:* added sourced [information/content/infobox/section], added [coverage/citations/references], improved attribution.

**Comment-specific behaviors.** Text pasted from a chatbot into a discussion also tends to:

- Misquote policies and cite made-up shortcuts that lead nowhere
- Transclude maintenance banners whenever mentioning them
- Post long comments split into titled sections, in Markdown or as level-2/3 subheadings
- Assure others that the content adheres to policy, or that the author is trying to make sure it does
- Ask other editors to determine exactly what needs improving
- Accuse anyone who calls out AI use of acting on speculation and failing to present stronger evidence

---

## Miscellaneous

- **Pronounced shift in writing style** within one author's output
- **Submission statements** in draft submissions
- **Pre-placed maintenance templates** inserted preemptively
- **Canned user pages** with formulaic content
- **Permissions gaming**

---

## Signs of human writing

- **Age relative to November 2022.** Text predating ChatGPT's launch is very unlikely to be LLM output.
- **Ability to explain one's own editorial choices.** A writer who can justify a specific decision made it.
- **Syntax.** Irregular, non-formulaic sentence structure.

---

## Historical tells

Present in November 2022 to 2024 output, largely absent now. Still useful for dating text.

- **Didactic disclaimers.** *Words to watch:* it's important/critical/crucial to note/remember/consider, worth noting, may vary.
- **Section summaries.** A recap at the end of each section.
- **"In summary" conclusions.** *Words to watch:* In summary, In conclusion, Overall.
- **Prompt refusal.** *Words to watch:* as an AI language model, as a large language model, "I cannot offer medical advice, but I can...", I'm sorry.
- **Abrupt cutoffs.** Text ending mid-sentence.
- **Outdated `access-date` parameters** in citations, indicating an earlier model.

---

## Provenance

| Added | Source | What it contributed |
|-------|--------|---------------------|
| 2026-07-20 | [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) | Entire initial taxonomy |

Append a row whenever a new source is folded in.
