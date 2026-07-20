# model-artifacts.md - per-model fingerprints and citation failure modes

Mechanical tells. Unlike the stylistic ones, a hit here is close to conclusive: these strings have no reason to exist in human-authored text.

**Source:** [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), §Markup and §Citations.

---

## Internal formatting and reference markup artifacts

Grep for these. Any hit both proves machine origin and identifies the model.

| Model | Artifact strings |
|-------|------------------|
| ChatGPT | `contentReference`, `oaicite`, `oai_citation`, `+1`, `turn0search0`, `attributableIndex` |
| Gemini | `[cite: 1]`, `[span_1]`, `[start_span]` |
| Grok | `grok_card`, `grok_render_citation_card_json` |
| DeepSeek | lenticular brackets `【 】`, dagger symbols |
| Perplexity | `attached_file`, `ppl-ai-file-upload` |
| Unclassified | `:::writing` |

Ready-to-run sweep:

```powershell
$pattern = 'contentReference|oaicite|oai_citation|turn0search|attributableIndex|\[cite: |\[span_\d|\[start_span\]|grok_card|grok_render_citation_card_json|attached_file|ppl-ai-file-upload|:::writing|[【】]'
Get-ChildItem -Recurse -Include *.md,*.txt,*.html,*.tsx,*.ts,*.js |
  Select-String -Pattern $pattern
```

---

## Idiolect differences between models

Each model and version writes distinctively, and what is typical of GPT-5 is not typical of GPT-4 or Gemini.

Comparing ChatGPT (circa GPT-4o-2024-08-06) and Grok (Grok-Beta, late 2024 / early 2025) against Gemini (1-5 Pro) and Claude (3.5-Sonnet):

- **Focusing on broader context** (the significance-inflation tell) is far more characteristic of ChatGPT and Grok than of Gemini and Claude.
- **Gemini and Claude responses tend to be more concise** than ChatGPT and Grok responses. Grokipedia articles are noted as extremely long.
- **Grok** additionally overuses superficially scientific vocabulary: `causal`, `empirical`, `correlate`. It still overuses `underscore` as of 2026, long after other models dropped it.

ChatGPT is likely the most widely used chatbot for Wikipedia edits, though this is unprovable and has many confounds.

**Practical use:** if text carries heavy significance-inflation plus length, suspect ChatGPT or Grok. If it carries the vocabulary tells but is terse, suspect Gemini or Claude. Both still need §1 to §4 of the skill applied.

---

## Other markup tells

**Use of Markdown in a non-Markdown medium.** `**bold**`, `*italic*`, `#header` where the target uses different syntax. Common in 2025 models.

**Broken wikitext.** Malformed syntax that fails to render. Note the false-positive warning: see [`false-positives.md`](false-positives.md) on bizarre markup, which is more often a browser extension or visual-editor slip.

**Non-existent or out-of-place categories.** References to structures that do not exist in the target system.

**Non-existent templates.** Calls to undefined template tags.

---

## Citation failure modes

LLMs now cite constantly. The citations are often wrong. Check the load-bearing ones by hand.

| Failure | What to check |
|---------|---------------|
| Broken external links | URL 404s, times out, or was never valid |
| Invalid DOIs and ISBNs | Malformed or non-existent identifiers |
| DOIs leading to unrelated articles | Well-formed DOI resolving to a paper that does not support the claim. The nastiest variant: it looks verified until you open it |
| Book citations with no page numbers or URLs | Unfalsifiable by construction |
| Incorrect or unconventional reference use | Non-standard formatting or placement |
| `utm_source=` in citation URLs | Tracking parameters copied straight out of a chatbot's browsing result |
| Named references declared but unused | A reference defined in the references section that nothing in the body cites |

**Rule:** a fabricated citation is a correctness bug, not a style issue. It outranks every stylistic tell in this skill. If a claim rests on a source, open the source.

---

## Historical artifacts

Largely gone from current models, still useful for dating text.

- Didactic disclaimers, November 2022 to 2024
- Per-section summaries
- Prompt-refusal text left in ("as an AI language model", "I'm sorry")
- Abrupt cutoffs mid-sentence
- `access-date` parameters stamped with an older model's era
