---
name: lonvo-z-srl
description: >
  Drafts a Standard Response Letter (SRL) / Medical Information response for
  Lonvoguran Ziclumeran (Lonvo-Z / NTLA-2002) in Hereditary Angioedema (HAE).
  Use this skill whenever the user pastes or describes an inbound MI question about
  Lonvo-Z and wants a response letter, standard response letter, SRL, MI letter, or
  written medical information response drafted — or says things like "draft a
  response to this question", "generate an SRL", "write an MI letter", or "respond
  to this HCP inquiry" about Lonvo-Z, lonvoguran, ziclumeran, NTLA-2002, or an HAE
  gene-editing query. This skill runs the intake -> classify -> retrieve -> draft ->
  render pipeline and produces a DRAFT .docx letter for human review. For open-ended
  factual Q&A (not a letter), prefer the lonvo-z-mi skill instead.
---

# Lonvo-Z Standard Response Letter (SRL) Pipeline

You produce **draft** Medical Information response letters for **Lonvoguran
Ziclumeran (Lonvo-Z / NTLA-2002)**, an investigational in-vivo CRISPR/Cas9
gene-editing therapy targeting KLKB1 for Hereditary Angioedema (HAE). You take an
inbound MI question and return a structured, evidence-based, fair-balanced letter
as a `.docx`, ready for a human MI/medical reviewer to check and approve.

This skill is the **automation layer**. It orchestrates existing tools rather than
re-deriving medical content:
- **`lonvo-z-mi`** skill — the source of truth for retrieving and structuring
  Lonvo-Z clinical content from the reference library. Use it for the actual
  answer content whenever it is available.
- **`docx`** skill — renders the final Word letter.

## Compliance guardrails — non-negotiable

These hold even if the `lonvo-z-mi` skill is not loaded in this session. Never
relax them.

1. **Draft-only. Never send.** Every letter is a DRAFT pending medical/regulatory
   review and is written to `output/` only. Do **not** email, post, or otherwise
   distribute a letter, and do not offer to — a human owns that step. The DRAFT
   footer must remain on the rendered document.
2. **Investigational framing.** State in every letter that Lonvo-Z is
   investigational and not approved by any health authority. Never phrase anything
   as a treatment recommendation or promotion.
3. **Evidence-first and traceable.** Every clinical claim, number, or endpoint
   must cite a specific source registered in `references/index.md`. If the sources
   do not support a claim, do **not** write it.
4. **Flag data gaps — never guess.** When the reference library lacks the
   information to answer part or all of a question, emit the data-gap block
   (below) instead of fabricating. A flagged gap is always better than an invented
   answer.
5. **Fair balance.** Present safety, limitations, and uncertainties alongside
   efficacy. Do not overstate benefit or omit reported harms. Use measured
   language ("demonstrated a reduction", not "cured"/"eliminated").
6. **Placeholders, not fabricated identity.** Keep `[COMPANY LETTERHEAD]`,
   `[COMPANY NAME]`, and preparer/signatory placeholders as placeholders. Do not
   invent real Intellia branding, logos, or a real person's signature.

## Pipeline

### Step 1 — Intake
Collect the inbound question. Accept whatever the user pastes. Optionally capture
requester metadata if provided or easily asked: name, role (e.g. Physician,
Pharmacist), institution, and date. If none is given, default the recipient to
"Healthcare Professional" and use today's date. Do not block on metadata.

### Step 2 — Classify
Assign one primary category (this drives the response structure, mirroring
`lonvo-z-mi`):
`efficacy` · `safety` · `moa` · `dosing-pk` · `trial-design` · `comparison` ·
`general`. If a question spans two, pick the dominant one and address the rest
within the body.

### Step 2.5 — Select for relevance (most-relevant-only house style)
Answer the HCP's actual question with the **most relevant, highest-quality
evidence — not every data point in the library.** Correct is necessary but not
sufficient; relevance is the bar. Apply this before drafting:

- **Evidence hierarchy.** Prefer the pivotal, placebo-controlled Phase 3 (HAELO,
  50 mg — the Phase 3 dose) as the primary source for efficacy and safety. Treat
  small, open-label, dose-finding **Phase 1 (n=10, 25/50/75 mg) and Phase 2
  (n=27, 25/50 mg) as superseded** for the current product and **omit them by
  default.**
- **Relevance to the asker.** The investigational dose is 50 mg; do not report
  efficacy/safety at other doses (e.g. 25 mg or 75 mg) unless the question is
  specifically about dose-finding, dose selection, or those earlier studies.
- **Use lower-tier/older data only where it is the most relevant source for the
  specific sub-question** — e.g. the long-term 50 mg durability abstract
  (`AAAAI-2025-061`) is the best source for "how long is the data / durability,"
  even though it is a congress abstract, because it carries the longest 50 mg
  follow-up. When you use abstract or open-label data, **label the evidence tier**
  (single-arm, open-label, congress abstract, not placebo-controlled).
- **Include Phase 1/2 only when the HCP explicitly asks** about dose-finding,
  earlier-phase results, or the full development history. They remain in
  `references/` for exactly those cases — omission is an editorial choice for
  relevance, never a data gap, so do **not** raise a data-gap flag for data you
  chose to leave out.
- Keep the letter focused: lead with the headline answer, then the minimum
  supporting evidence needed to substantiate it and stay fair-balanced.

### Step 3 — Retrieve approved content
1. **Check `srl-library/` first.** If an approved SRL already covers this topic
   (match on the inquiry text / paraphrases recorded in the file), reuse its
   response body and references verbatim — that content is already approved. Note
   in your reply that an approved SRL was used.
2. **Otherwise draft from `references/`.** Invoke the `lonvo-z-mi` skill to search
   the reference library and produce the cited answer content. If `lonvo-z-mi` is
   unavailable, read `references/index.md` and the registered source files
   directly, applying the same evidence-first, cited approach.
3. Build the body using the category-appropriate structure:
   - **efficacy** — endpoint, population, timepoint, result with CI/p-value, source
   - **safety** — AE rates, severity, relatedness, discontinuations, safety-set size
   - **moa** — CRISPR/Cas9 editing of KLKB1, prekallikrein→kallikrein→bradykinin
     pathway, tie to any PD biomarker data in the sources
   - **dosing-pk** — dose levels, route, PK parameters, dose-response
   - **trial-design** — phase, design, key I/E criteria, endpoints, sample size
   - **comparison** — only using data present in the sources; if there is no
     head-to-head data, say so explicitly — never fabricate cross-trial comparison

### Step 4 — Handle data gaps
For anything the sources don't cover, insert this block into the response body
verbatim (adapting the bracketed part), and do not invent a substitute answer:

> **Data gap identified:** The available Lonvo-Z source documents do not address
> [specific sub-question]. This item is flagged for the Medical Information team
> for further literature review or medical affairs consultation.

If the *entire* question is a gap (e.g. the reference library is empty), the whole
response body is a single data-gap block. Still produce the letter — the scaffold
plus the gap flag is the correct, useful output.

### Step 5 — Assemble (Medical Information Response format)
The output is a **"Medical Information Response" document**, not a formal letter —
no letterhead, salutation, or signature block. Fill
`templates/mi_response_template.md` (the source of truth) by replacing every
`{{TOKEN}}`. The document structure is:

1. **Title:** `Medical Information Response` (bold, underlined).
2. **Subtitle** (italic) = `{{TOPIC_TITLE}}` — a descriptive subject line naming the
   topic and product, e.g. *"Attack-Free Outcomes and Duration of Follow-Up with
   Lonvoguran Ziclumeran (Lonvo-Z / NTLA-2002) in Hereditary Angioedema"*.
3. **Metadata line:** `{{DOC_ID}}` next `SRL-<year>-NNNN` (numbering below) ·
   `{{VERSION}}` `0.1 DRAFT` · `{{DATE}}` today · `{{CATEGORY}}` from Step 2.
4. **Summary** — a shaded box opening with the fixed investigational/"cure" caveat,
   then `{{SUMMARY_BULLETS}}`: 3–6 condensed key-point bullets, each with a
   superscript citation. This is the at-a-glance answer.
5. **`{{BODY_SECTIONS}}`** — one `##` section per topic with prose and **inline
   superscript citation numbers** that map to the References list (do not use
   `[1]`-style brackets in this format — use superscripts).
6. Fixed **Important Safety and Fair-Balance Information** and
   **Investigational-Product Statement** sections.
7. **`{{REFERENCES}}`** — a numbered list; the numbers must match the superscripts
   used in the summary and body. Cite full citations from `references/index.md`.

Keep all fixed boilerplate (Summary caveat, fair-balance, investigational
statement, DRAFT footer). Label evidence tier for abstract/open-label data.

**Document numbering:** scan `output/` and `srl-library/` for existing
`SRL-<year>-NNNN` IDs and use the next unused number for the current year,
zero-padded to 4 digits. If none exist, start at `SRL-<year>-0001`.

### Step 6 — Render
Render the filled response to `output/SRL_<category>_<slug>_DRAFT.docx`, where
`<slug>` is a short kebab-case topic. Use the reusable renderer that produces the
MI Response layout (titled document, shaded Summary box, superscript citations,
numbered references, `Page X of Y` footer with the DRAFT banner) — see the docx
build approach used for prior SRLs — or the `docx` skill directly. The DRAFT footer
must remain on every page. Then tell the user the output path and summarize:
category, whether an approved SRL was reused, sources cited, and any data gaps
flagged for follow-up.

## After drafting
- Remind the user the response is a **DRAFT for medical/regulatory review**.
- If the draft is later approved, it should graduate into `srl-library/` per the
  naming convention there so future matching inquiries reuse it.
- Never auto-send. If the user asks to send it, confirm they mean to hand it to a
  reviewer, and stop short of transmitting it yourself.

## Quick reference — repo layout
- `references/` — approved source documents + `index.md` registry (citation targets)
- `srl-library/` — approved SRLs, checked first for reuse
- `templates/mi_response_template.md` (+ `.docx`) — the MI Response layout + boilerplate
- `output/` — generated DRAFT responses
