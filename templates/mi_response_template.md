<!--
MEDICAL INFORMATION RESPONSE TEMPLATE — source of truth
========================================================
Modeled on the standard industry "Medical Information Response" document format
(titled response with a shaded Summary box, detailed sections, inline superscript
citations, and a numbered reference list) — NOT a formal letter (no letterhead,
salutation, or signature block).

The lonvo-z-srl skill fills the {{TOKENS}} and renders to a .docx in ../output/.
mi_response_template.docx is generated from this file; edit this file, not the
.docx, when changing structure or boilerplate.

Tokens:
  {{TOPIC_TITLE}}   descriptive subject line, e.g.
                    "Attack-Free Outcomes and Duration of Follow-Up with Lonvo-Z…"
  {{DOC_ID}}        SRL-<year>-NNNN
  {{VERSION}}       e.g. 0.1 DRAFT
  {{DATE}}          e.g. 17 July 2026
  {{CATEGORY}}      efficacy | safety | moa | dosing-pk | trial-design | comparison | general
  {{SUMMARY_BULLETS}}  3–6 condensed key-point bullets with superscript cites
  {{BODY_SECTIONS}}    detailed sections (## heading + prose, inline superscript cites)
  {{REFERENCES}}       numbered full citations matching the superscript numbers
Fixed boilerplate (Summary caveat, Investigational-Product Statement, fair-balance,
DRAFT footer) must NOT be removed. Inline citations use superscript numbers that map
to the References list.
-->

# Medical Information Response

*{{TOPIC_TITLE}}*

**Document ID:** {{DOC_ID}}  ·  **Version:** {{VERSION}}  ·  **Date:** {{DATE}}  ·  **Category:** {{CATEGORY}}

## Summary

> **Lonvoguran Ziclumeran (Lonvo-Z / NTLA-2002) is an investigational agent that
> has not been approved by the FDA, EMA, or any other health authority; its safety
> and efficacy have not been established. "Cure" is not an endpoint that has been
> evaluated in the lonvo-z clinical program.** This response is provided in answer
> to an unsolicited request for medical information and is presented in a balanced,
> non-promotional manner. Information is drawn from the referenced source documents.

{{SUMMARY_BULLETS}}

{{BODY_SECTIONS}}

## Important Safety and Fair-Balance Information

The information above should be interpreted in the context of the full safety and
efficacy profile of Lonvo-Z as reported in the referenced sources. Reported
findings reflect the specific study populations, dose levels, and timepoints
described and may not generalize to other patients or settings. Where adverse
events, limitations, or uncertainties are described in the sources, they are
presented alongside efficacy findings and should not be omitted when this
information is conveyed.

## Investigational-Product Statement

**Lonvoguran Ziclumeran (Lonvo-Z / NTLA-2002) is an investigational agent. It has
not been approved by the FDA, EMA, or any other health authority, and its safety
and efficacy have not been established.** Nothing in this response should be
construed as a recommendation to use Lonvo-Z outside of an approved clinical trial,
nor as promotion of an unapproved product.

## References

{{REFERENCES}}

---

<sub>{{DOC_ID}} · {{VERSION}} · **DRAFT — NOT FOR DISTRIBUTION. Pending medical/regulatory review.** · Page X of Y</sub>
