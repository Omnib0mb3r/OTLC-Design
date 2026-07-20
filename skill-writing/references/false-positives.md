# false-positives.md - what does NOT indicate AI writing

Read this before calling any text AI-generated. It exists because the failure mode of a tells catalogue is over-application.

**Source:** [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), §Ineffective indicators and §Caveats.

---

## The two caveats that outrank everything else

### Detection tools do not work

Automated AI-detection software is unreliable. Its output is not evidence and must never be cited as proof. Do not run text through a detector and report the score as a finding.

### Human detection is chance-level

Controlled study finding: human ability to distinguish LLM text from human text is **no better than random chance**. Your confidence that something "reads like AI" is not calibrated, and neither is anyone else's.

False accusations drive contributors away and create an atmosphere of suspicion. Before claiming AI use, consider whether the Dunning-Kruger effect or confirmation bias is driving the judgement.

---

## Ineffective indicators

Each of these gets used as a tell and should not be. Several point the opposite direction.

**Perfect grammar.** Modern LLMs are grammatically proficient, but so are many people. Plenty of writers come from professional writing backgrounds.

**Combination of casual and formal registers, or prose that sounds both "clinical" and "emotional".** More likely indicates the casual writing of someone in a technical field such as computer science. Also consistent with youth, a preference for mixed registers, playfulness, or neurodivergence. On a collaboratively edited document it may simply be several authors.

**"Bland" or "robotic" prose.** LLM output has specific traits and skews positive and verbose by default. Those tendencies are formulaic but do not necessarily scan as "robotic" to anyone unfamiliar with AI writing. Human writing can be bland on its own merits.

**"Fancy", "academic", or "formal" prose.** LLMs disproportionately favor certain words, many of which are longer and score harder on readability. Those are *specific words*. The correlation does not extend to formal, academic, or fancy-sounding prose in general.

**Transition words in isolation.** Older AI text formulaically overused `Additionally`, `Consequently`, `Notably`, often sentence-initially. Only a few transitions are overused this way. The pattern also has long precedent in essay-style human writing and is accepted by many style guides. Weak tell at best.

**Unsourced content.** More than 570,000 Wikipedia articles are tagged as needing citations and most predate LLMs. Meanwhile modern chatbots search the web and cite constantly. The citations are frequently wrong, but they are present. Absence of sources says nothing about authorship.

**Bizarre wikitext or bizarre markup.** LLMs do hallucinate templates and emit invalid syntax, but they do not tend to produce random-seeming inexplicable artifacts. Misplaced HTML tags like a stray `<span>` more often indicate a badly written browser extension or a known content-translation bug. Misplaced emphasis syntax rendering as `*Catch-22 i*s a satirical novel` points at a visual-editor mistake, which is far harder to notice than the same error in source editing.

**Correct markup.** Getting formatting right, even for complex structures, is normal for anyone using a preview button or a visual editor. Competence is not suspicious.

---

## The operating rule

**Density plus recency.** One tell proves nothing. Many tells clustered in text produced after November 2022 is a genuine signal. Even then:

> Signs alone do not prove a problem. The deeper policy violations (synthesis, non-neutral point of view, lack of verification) are what require addressing, rather than cosmetic fixes.

Translate to this repo's context: if a page's copy is puffed-up, unsourced, and generic, the deliverable is broken regardless of who or what wrote it. Fix the copy. Do not turn the review into an authorship trial.

When reporting in AUDIT mode, give a density judgement (`clean` / `some tells` / `heavily AI-flavored`) and never a binary verdict on authorship.
