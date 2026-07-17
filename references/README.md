# References — Lonvo-Z Source Library

This folder holds the **approved evidence** the SRL pipeline cites from:
publications, congress posters, abstracts, the Investigator's Brochure, and any
other medically-reviewed source documents for **Lonvoguran Ziclumeran (Lonvo-Z /
NTLA-2002)**.

Everything the pipeline writes into a letter must trace back to a document
registered here. If a question can't be answered from these sources, the
pipeline flags a **data gap** rather than guessing.

## How to add a source

1. **Drop the file here.** PDFs, posters, and Word docs are all fine.
   - Convert PDFs to text with the `pdf` skill (or the registered markitdown MCP
     server) so the content is searchable if the raw PDF isn't extractable.
2. **Register it in `index.md`.** Add one row: assign a short **Source ID**
   (e.g. `NEJM-2025`, `ACAAI-2025-P1234`), the full citation, type, date, and
   the filename. Citations in generated letters point at these IDs.
3. **Note supersession.** If a new document updates or replaces older data, say
   so in the index `Notes` column so the pipeline prefers the current source.

## What counts as an approved source

Only include material cleared for MI use. Do **not** add draft manuscripts,
internal speculation, competitor promotional material, or anything not
medically/regulatory reviewed. The quality of every draft letter is capped by
the quality of what lives here.

## Current status

No source documents are loaded yet. Add your Lonvo-Z publications/posters and
register them in `index.md` to enable cited drafts. Until then the pipeline runs
but will correctly return data-gap responses.
