---
name: anti-ai-writing
description: Use whenever producing or reviewing prose of any kind: website and marketing copy, README and docs, commit messages, PR descriptions, emails, proposals, blog posts, UI strings, release notes, reports. Strips the ~60 documented tells that mark text as LLM-generated (AI vocabulary like "delve" and "showcasing", negative parallelism "not just X but Y", rule of three, copulative avoidance "serves as" instead of "is", puffery about broader significance, vague attribution, title-case headings, inline-header bold lists, em dashes, curly quotes, chatbot artifacts, fabricated citations). Also runs as an audit: given existing text, report which tells fire and rewrite. Invoked by "/anti-ai-writing", "does this sound like AI", "make this not sound AI-generated", "de-slop this copy", "audit this writing", or automatically before delivering any substantial prose. Companion to ANTI-SLOP.md, which covers visual slop; this covers prose slop.
---

# anti-ai-writing

Prose counterpart to [`ANTI-SLOP.md`](../ANTI-SLOP.md). That file stops a page from *looking* AI-generated. This one stops the words on it from *reading* AI-generated.

Source: the English Wikipedia project page [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), the most rigorously maintained catalogue of LLM text tells in existence, built from thousands of confirmed cases and cited to published studies. Distilled here into rules you apply, not trivia you know.

## Two modes

**WRITE mode** (default). You are producing prose. Apply the bans in §1 to §4 as you write. Do not write then clean; the cleaning pass never catches everything.

**AUDIT mode.** The user hands you text and asks whether it reads as AI, or asks you to fix it. Run §6.

Announce which mode you are in. Then work.

---

## The core problem, stated once

LLMs do not write badly. They write *identically*. Every tell below is a statistical fingerprint: a construction that appears at several times the human base rate. Any one of them is meaningless in isolation. Density is the signal.

That cuts both ways, and it is the single most common failure when applying this skill: **a human wrote it** is the default hypothesis, not the fallback. Read §5 before accusing any text of being AI-generated.

---

## 1. Vocabulary bans

These words are overused by LLMs at rates documented in peer-reviewed studies. Take this list **literally**. A word being overused does not make its synonyms suspect, and context matters (a literal underscore character is fine; "underscores the importance" is not).

**Hard-banned in produced prose:**

`additionally` (especially sentence-initial) · `align with` · `boasts` (meaning "has") · `bolstered` · `crucial` · `delve` · `emphasizing` · `enduring` · `enhance` · `fostering` · `garner` · `highlight` (as a verb) · `interplay` · `intricate` / `intricacies` · `key` (as an adjective) · `landscape` (as an abstract noun) · `meticulous` / `meticulously` · `pivotal` · `robust` · `showcase` · `tapestry` (as an abstract noun) · `testament` · `underscore` (as a verb) · `valuable` · `vibrant`

Grok-specific, banned too: superficially scientific `causal`, `empirical`, `correlate` used where plain words fit.

**Why the era matters.** Model generations have distinct vocabularies, so the list tells you *which* model wrote something, not just that one did. See [`references/tells.md`](references/tells.md) §Vocabulary eras. Post-2025 output has narrowed to four repeat offenders: `emphasizing`, `enhance`, `highlighting`, `showcasing`. Those four are the highest-priority bans today.

**How to apply.** Reach for the shorter, plainer word. `crucial` → `important`, or cut the adjective. `showcasing` → `showing`, or restructure the sentence so nothing needs showcasing. If the plain word feels weak, the sentence is weak; fix the sentence, not the adjective.

## 2. Construction bans

### 2.1 Never avoid the copulative

LLMs replace `is` and `are` with marketing-adjacent verbs. Banned: `serves as`, `stands as`, `marks`, `functions as`, `operates as`, `represents [a]`, `boasts`, `features`, `maintains`, `offers`, `refers to`.

> "The dashboard serves as a central hub for fleet telemetry."

Write `is`. "The dashboard is where fleet telemetry lands." If `is` reads flat, the problem is the noun phrase, not the verb.

### 2.2 Never use negative parallelism

Three shapes, all banned:

- `Not just X, but also Y` / `Not only X, but Y`
- `Not X, but Y` / `It's not X, it's Y`
- `X rather than Y` (the reversed form, heavy in Grok output)

> "This isn't just a sourcing issue, it's a systemic bias."
> "Not only dismissive but also unnecessarily harsh."

The construction fakes insight by inventing a wrong assumption the reader never held, then correcting it. State the claim directly: "This is a systemic bias." Humans do use this form, especially in myth-busting writing, which is exactly why LLMs learned to overuse it. It is now a stereotype tell.

### 2.3 Never default to the rule of three

Three adjectives. Three short phrases. Three clauses joined by `and`. LLMs use triads to make shallow analysis sound thorough.

> "fast, reliable, and scalable"
> "It cut costs, improved throughput, and delighted customers."

Use two, or four, or one. If exactly three items are genuinely correct, keep them, but check that the third is real content rather than rhythm filler.

### 2.4 Never chase elegant variation

LLMs carry a repetition penalty, so they swap in synonyms rather than reuse a word. The result is a paragraph where one subject wears four different names and the reader loses track.

> "Soviet artistic constraints" → "the challenging climate of Soviet artistic constraints" → "the confines of state-imposed artistic norms"

Repeat the noun. Repetition is clarity. This is directly opposed to the writing advice most people absorbed in school, and that is the point.

## 3. Content bans

### 3.1 Never inflate significance

The largest single category. LLMs pad any subject with claims about its role in some broader story.

Banned phrases: `stands/serves as`, `is a testament/reminder`, `a vital/significant/crucial/pivotal/key role/moment`, `underscores/highlights its importance`, `reflects broader`, `symbolizing its ongoing/enduring/lasting`, `contributing to the`, `setting the stage for`, `marking/shaping the`, `represents/marks a shift`, `key turning point`, `evolving landscape`, `focal point`, `indelible mark`, `deeply rooted`.

> "The Statistical Institute of Catalonia was officially established in 1989, marking a pivotal moment in the evolution of regional statistics in Spain."

It was established in 1989. That is the sentence.

### 3.2 Never write superficial analysis via participle phrases

The trailing `-ing` clause that adds commentary instead of information: `highlighting`, `underscoring`, `emphasizing`, `ensuring`, `reflecting`, `symbolizing`, `contributing to`, `cultivating`, `fostering`, `encompassing`, `enhancing`, plus `valuable insights` and `align/resonate with`.

> "The API returns paginated results, ensuring efficient data transfer."

Cut everything after the comma. If the efficiency claim matters, make it its own sentence with a number in it.

### 3.3 Never use promotional register

Banned: `boasts a`, `vibrant`, `rich`, `profound`, `enhancing`, `showcasing`, `exemplifies`, `commitment to`, `natural beauty`, `nestled`, `in the heart of`, `groundbreaking`, `renowned`, `featuring`, `diverse array`.

LLMs drift into travel-brochure and press-release tone even when told to be neutral. This overlaps heavily with [`ANTI-SLOP.md`](../ANTI-SLOP.md) rule 18 and extends it well past the banned-phrase list there.

### 3.4 Never attribute vaguely

Banned: `Industry reports`, `Observers have cited`, `Experts argue`, `Some critics argue`, `several sources/publications` (when few are cited), `such as` in front of an exhaustive list.

Name the source or cut the claim. "Experts argue" means "I do not have a source."

### 3.5 Never write the challenges-and-future-prospects ending

The formula: acknowledge difficulties, then offer vague optimism. Banned: `Despite its ... faces several challenges`, `Despite these challenges`, section headings named `Challenges and Legacy` or `Future Outlook`.

Also banned as closers: `In summary`, `In conclusion`, `Overall`, and the per-section recap. End on the last real point.

## 4. Formatting bans

- **Title Case In Headings.** Sentence case. Always.
- **Boldface for emphasis.** LLMs bold mechanically, especially every instance of a chosen term and anything resembling "key takeaways". Bold is for genuine UI labels and defined terms, not stress.
- **Inline-header vertical lists.** The `• **Thing**: description` shape, repeated down the page. Inherited from readmes and sales decks. Use prose or a real table.
- **Em dashes.** Already banned outright by the global rule, and independently one of the loudest tells. En dashes too. Applies everywhere, including string literals, YAML, JSON, commit messages, and generated SVG.
- **Curly quotes and apostrophes.** Use straight ASCII `'` and `"` unless the target medium is typeset copy where curly is correct. Weak tell on its own (Word does it too), strong in combination.
- **Emoji as formatting.** As list markers, separators, or section decoration. Overlaps [`ANTI-SLOP.md`](../ANTI-SLOP.md) rule 21.
- **Skipped heading levels.** Jumping H2 to H4. Accessibility failure and a tell at once.
- **Thematic breaks before every heading.** The `---` above each section is a Markdown-to-wikitext conversion artifact.
- **Markdown leaking into a non-Markdown medium.** `**bold**` in plain-text email, wikitext, or a UI string.

## 5. Do not accuse text of being AI without reading this

False accusations poison collaboration and are usually wrong. Controlled studies find humans distinguish LLM text from human text at **no better than chance**. AI detection tools are unreliable and must not be treated as evidence.

These are **not** evidence of AI, and several point the other way:

- **Perfect grammar.** Plenty of people write well for a living.
- **Mixed casual and formal register.** Indicates a technical writer, a young writer, playfulness, neurodivergence, or several editors on one document.
- **Bland or robotic prose.** LLM output skews positive and verbose, which does not read as "robotic" to most people. Human bland is still bland.
- **Fancy, academic, or formal vocabulary.** LLMs overuse *specific words*. The correlation does not generalize to formal writing.
- **Transition words alone.** `Additionally`, `Consequently`, `Notably` are overused by older models but are also standard essay style, endorsed by many style guides.
- **Unsourced claims.** Predates LLMs by decades. Modern chatbots cite constantly, just often wrongly.
- **Broken or bizarre markup.** More often a browser extension, a visual editor slip, or a known platform bug.
- **Correct markup.** Getting complex formatting right is normal for anyone using a preview button.

Full text at [`references/false-positives.md`](references/false-positives.md).

**The rule:** density plus recency. One tell proves nothing. A dozen tells clustered in text written after November 2022 is a strong signal. Even then, the actionable problem is usually the underlying defect (unsourced claim, puffery, fabricated citation), not the authorship. Fix the defect, do not litigate the author.

## 6. AUDIT mode procedure

Given text to review:

1. **Count, do not vibe.** Walk §1 to §4. List every tell that fires, with the exact quoted span and which rule it violates.
2. **Check citations if any exist.** Broken links, invalid or fabricated DOIs and ISBNs, DOIs resolving to unrelated papers, book citations with no page numbers, `utm_source=` tracking params left in URLs, named references declared but never used. Verify at least the load-bearing ones. See [`references/model-artifacts.md`](references/model-artifacts.md).
3. **Grep for chatbot artifacts.** `contentReference`, `oaicite`, `oai_citation`, `turn0search0`, `attributableIndex`, `[cite: 1]`, `[span_1]`, `[start_span]`, `grok_card`, `grok_render_citation_card_json`, `attached_file`, `ppl-ai-file-upload`, `:::writing`, lenticular brackets `【】`. Any hit is near-conclusive and identifies the model.
4. **Grep for reader-directed chatter.** `I hope this helps`, `Of course!`, `Certainly!`, `You're absolutely right!`, `Would you like`, `is there anything else`, `let me know`, `more detailed breakdown`, `here is a`, `Let's explore`, `as an AI language model`, `as a large language model`, `it's important to note`, `worth noting`, `may vary`, knowledge-cutoff disclaimers, unfilled `[placeholder]` brackets.
5. **Run §5 against your own findings.** Strike every finding that rests only on an ineffective indicator.
6. **Report** as: tell, quoted span, rule number, suggested rewrite. Give a density judgement (`clean` / `some tells` / `heavily AI-flavored`), never a binary verdict on authorship.
7. **Rewrite only if asked.** Auditing and rewriting are different requests.

## 7. Reference files

Load these when you need the full taxonomy; the rules above are the working subset.

- [`references/tells.md`](references/tells.md) - complete taxonomy with verbatim watch-phrase lists, vocabulary eras, and source examples
- [`references/false-positives.md`](references/false-positives.md) - full ineffective-indicators text and the detection-accuracy caveats
- [`references/model-artifacts.md`](references/model-artifacts.md) - per-model fingerprints, citation failure modes, historical tells

## 8. Relationship to the rest of the system

- [`ANTI-SLOP.md`](../ANTI-SLOP.md) rules 18 and 19 are the visual system's copy rules. This skill is their expansion. When `OTLC-Design` reaches Step 4 (Build) and writes any user-facing string, this skill applies.
- Additions follow the same closing-loop mechanic as the rest of the repo. When a new tell slips through into delivered work, add it here and commit `skill-writing: <what changed>`. See [`HANDOVER.md`](../HANDOVER.md).
- This skill is source-extensible. New sources beyond the Wikipedia page get distilled into the same rule shape (ban, why, how to apply) and folded into §1 to §4, with provenance noted in [`references/tells.md`](references/tells.md).
