# analyzer/

> Procedures and prompts for **Step 2 of PROCESS.md** — extracting design data from reference URLs using Chrome DevTools MCP.

## Files

| File | Purpose |
|------|---------|
| [`extract-prompt.md`](extract-prompt.md) | The structured extraction prompt + output format Claude follows |

## How it is used

When the `design-website` skill runs Step 2 (Reference Analysis), for each reference URL provided at intake:

1. Read [`extract-prompt.md`](extract-prompt.md) for the extraction procedure
2. Use Chrome DevTools MCP to navigate to the URL
3. Run the extraction (computed type, color, spacing, grid, motion)
4. Capture screenshots at 4 breakpoints
5. Write the analysis to `[client-project]/references/[domain].md` using the documented output format

## Why a structured prompt

Without a structured extraction procedure, "look at this site and tell me what's going on" produces inconsistent output across projects. The prompt enforces:

- The same data fields are extracted every time
- Output is comparable across multiple references in the same project
- The synthesis step in Step 3 has predictable inputs

## Tooling fallback

If Chrome DevTools MCP cannot extract clean data from a reference (heavy JS, geo-blocked, login-walled, etc.):

1. Try Playwright MCP as a fallback (different rendering)
2. If still blocked, fall back to manual visual inspection — flag the reduced confidence in the analysis output
3. Consider whether the reference is actually appropriate for the project; references that can't be analyzed are also references the client probably can't access easily

## Output location

All reference analyses live in the **client project**, not this repo:

```
C:\dev\Projects\[client-name]\references\
├── [domain1].md
├── [domain2].md
└── [domain3].md
```

This repo's `references/INDEX.md` catalogs *known-good sites* generally. Per-project deep analyses belong with the project.
