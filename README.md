# Lonvo-Z Medical Information Response Automation

Automates drafting **Standard Response Letters (SRLs)** / Medical Information (MI)
responses for **Lonvoguran Ziclumeran (Lonvo-Z / NTLA-2002)**, an investigational
in-vivo CRISPR/Cas9 gene-editing therapy for Hereditary Angioedema (HAE).

You paste an inbound MI question; the pipeline classifies it, pulls approved
evidence from a reference library, and produces a **DRAFT** Medical Information
Response document (titled response with a shaded Summary box, not a formal letter) for a
human MI/medical reviewer to check and approve. Manual intake, Lonvo-Z only.

## How it works

```
 you paste a question
         │
         ▼
  ┌───────────────────────────────────────────────┐
  │  lonvo-z-srl skill  (the automation)           │
  │  1 intake → 2 classify → 3 retrieve            │
  │  4 flag gaps → 5 assemble → 6 render .docx      │
  └───────────────────────────────────────────────┘
     │ reuses                    │ renders
     ▼                           ▼
  lonvo-z-mi (retrieval)      docx (Word letter)
     │
     ▼
  references/ ── approved sources cited in every claim
```

## Usage

0. **Load your evidence.** Put approved Lonvo-Z publications, posters, and
   abstracts in [`references/`](references/) and register each in
   [`references/index.md`](references/index.md). This is what letters cite.
   *(No sources are loaded yet — until you add them, drafts correctly return
   data-gap responses instead of fabricating answers.)*
1. **Paste an MI question** and ask for a response letter / SRL. The
   `lonvo-z-srl` skill triggers automatically.
2. **Get a draft.** A `SRL_<category>_<slug>_DRAFT.docx` appears in
   [`output/`](output/), with the answer, fair-balance and investigational
   statements, cited references, and any data gaps flagged.
3. **Human review.** An MI/medical reviewer checks and approves the draft.
   Nothing is ever sent automatically.
4. **Graduate approved letters.** Approved SRLs move into
   [`srl-library/`](srl-library/); the pipeline checks there first and reuses
   approved content for matching future inquiries.

## Compliance guardrails (built into the skill)

- **Draft-only, never sent.** Output is always a DRAFT pending medical/regulatory
  review; the pipeline does not email or distribute anything.
- **Investigational framing.** Every letter states Lonvo-Z is investigational and
  not approved by any health authority — no treatment recommendations, no promotion.
- **Evidence-first + traceable.** Every clinical claim cites a specific source in
  `references/index.md`. No source → an explicit **data-gap** flag, never a guess.
- **Fair balance.** Safety and limitations presented alongside efficacy.
- **No fabricated identity.** The MI Response is product-focused; no invented
  company letterhead, branding, or signatory.

## Layout

| Path | Purpose |
|------|---------|
| `.claude/skills/lonvo-z-srl/` | The driver skill — the intake→draft pipeline |
| `references/` | Approved source documents + `index.md` citation registry |
| `srl-library/` | Approved SRLs, checked first for reuse |
| `templates/mi_response_template.md` | MI Response structure + fixed boilerplate (source of truth) |
| `templates/mi_response_template.docx` | Word template rendered from the `.md` |
| `output/` | Generated DRAFT letters |

## Related

The `lonvo-z-mi` skill (Medical Information expert for Lonvo-Z) handles
open-ended MI Q&A and reference indexing. This repo's `lonvo-z-srl` skill builds
on it to produce formatted **response letters**.
