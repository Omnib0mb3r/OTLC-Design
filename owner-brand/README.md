# owner-brand/

> The operator's standing brand system. Read by the `OTLC-Design` skill when the intake
> branch resolves to **internal site** or **internal app**, so the skill does not ask
> brand-discovery questions that were answered years ago.

---

## This directory is local-only

**Everything here except this README is gitignored.** The repo is public; a personal brand
guide, voice rules, and brand tokens are not. The files live on the operator's disk and the
skill reads them normally. They are simply not published.

Two consequences:

1. **This directory is not recoverable from git history.** Back it up separately. The rest
   of the repo can be restored from the remote; this cannot.
2. **A fresh clone has no brand profile.** Internal mode will have nothing to load until
   the directory is populated. Customer mode is unaffected, because customer work never
   reads this directory at all.

---

## Expected shape

Populate it like this. The skill resolves these paths, so the names matter.

```
owner-brand/
  README.md              this file (the only tracked one)
  profile.md             index of every brand surface; the skill's entry point
  voice.md               voice rules that hold across all surfaces
  brands/
    <surface>.md         one file per brand surface (colors, type, layout rules)
  tokens/
    <surface>.css        drop-in CSS custom properties for that surface
  source/
    <BrandGuide>.docx    the authoring document, if one exists
```

A "surface" is one coherent brand identity. Most operators have more than one: a personal
or studio brand, plus a separate identity for any publication or product line with its own
look. Each gets a file in `brands/` and a matching token file in `tokens/`.

If a source `.docx` or Figma file exists, it is the authority and the markdown files are
derived working copies. Claude reads the markdown; the source document settles disputes.

---

## How the skill uses it

When intake resolves to internal site or internal app:

1. Read `profile.md` to enumerate the available surfaces.
2. Ask one disambiguation question if there is more than one: *"Which brand surface?"*
3. Load the matching `brands/<surface>.md` and `tokens/<surface>.css`.
4. Skip brand-discovery intake. Colors, type, and voice are already settled.
5. Still ask the project-specific questions: goals, scope, optional references, hosting.

For **customer work this directory is never loaded.** Client projects start brand discovery
from the client's own references and brief. The operator's brand may inform instincts, such
as font-pairing habits or anti-slop reflexes, but it never overrides client direction. That
boundary is [`ANTI-SLOP.md`](../ANTI-SLOP.md) rule 23, and it exists because importing the
developer's aesthetic into client work means delivering the wrong brand.

---

## Updating

1. Edit the source document, if there is one.
2. Update the derived markdown and token CSS to match.
3. Bump the version line at the top of `profile.md`.
4. There is nothing to commit: the directory is gitignored. Make sure the backup runs.

If the source document and the markdown drift, Claude should flag it at the start of
internal-mode work and ask for reconciliation rather than guessing which one is current.

---

## Anti-pattern

Do not let the markdown drift away from the source document through small edits made
mid-project. If a rule feels right while building and is not in the brand guide, it is a
candidate for the next guide revision, not a silent change to a derived file.

## Adapting this repo for your own use

Replace this directory wholesale. Nothing in it generalizes: it encodes one operator's
brand decisions. The structure above is the contract the skill expects; the contents are
yours to define.
