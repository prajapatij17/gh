# SRL Library — Approved Standard Response Letters

This folder holds **medically/regulatory-approved** standard response letters
(SRLs) for recurring Lonvo-Z inquiries. It is the pipeline's first stop: before
drafting anything new, the `lonvo-z-srl` skill checks here for an existing
approved letter on the topic and reuses it.

A file lives here **only after it has cleared review**. Fresh drafts stay in
`output/` until a human approves them; approved letters then graduate into this
folder.

## Naming convention

```
SRL_<category>_<slug>_v<version>.md
```

- `<category>`: `efficacy` · `safety` · `moa` · `dosing-pk` · `trial-design` ·
  `comparison` · `general`
- `<slug>`: short topic, kebab-case (e.g. `attack-rate-reduction`)
- `<version>`: `1`, `2`, … bump on any content change

Example: `SRL_efficacy_attack-rate-reduction_v1.md`

## Each approved SRL should record

- **Approval metadata** at the top: document ID, version, approval date,
  approver, next review date.
- **The inquiry** it answers (and common paraphrases, so the pipeline can match).
- **The response body** with inline citations to `references/index.md` Source IDs.
- **Fair-balance** and **investigational-product** statements.

## Current status

Empty — no approved SRLs yet. As letters generated in `output/` are reviewed and
approved, add them here so future matching inquiries reuse approved content
instead of re-drafting.
