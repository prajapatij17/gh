<!--
SRL LETTER TEMPLATE — source of truth
=====================================
The lonvo-z-srl skill fills the {{TOKENS}} below and renders the result to a
.docx in ../output/. srl_letter_template.docx is generated from this file; edit
this file, not the .docx, when changing structure or boilerplate.

Tokens the skill replaces:
  {{DATE}}                 letter date (e.g. 17 July 2026)
  {{DOC_ID}}               unique draft ID (e.g. SRL-2026-0001)
  {{VERSION}}              draft version (e.g. 0.1 DRAFT)
  {{RECIPIENT_NAME}}       requester name, or "Healthcare Professional"
  {{RECIPIENT_ROLE}}       e.g. Physician / Pharmacist (optional)
  {{RECIPIENT_ORG}}        institution (optional)
  {{SALUTATION}}           e.g. "Dear Dr. Smith," or "Dear Healthcare Professional,"
  {{INQUIRY_RESTATEMENT}}  one-sentence restatement of the question
  {{CATEGORY}}             efficacy | safety | moa | dosing-pk | trial-design | comparison | general
  {{RESPONSE_BODY}}        structured, cited answer (or data-gap block)
  {{REFERENCES}}           numbered list of cited Source IDs -> full citations
  {{PREPARER}}             MI preparer name/role placeholder
Fixed boilerplate (fair balance, investigational disclaimer, DRAFT footer) is
part of the template and must NOT be removed.
-->

[COMPANY LETTERHEAD]
Medical Information Department

---

**Document ID:** {{DOC_ID}} **Version:** {{VERSION}}
**Date:** {{DATE}}
**Category:** {{CATEGORY}}

{{RECIPIENT_NAME}}
{{RECIPIENT_ROLE}}
{{RECIPIENT_ORG}}

{{SALUTATION}}

Thank you for your inquiry regarding **Lonvoguran Ziclumeran (Lonvo-Z /
NTLA-2002)**, an investigational in-vivo CRISPR/Cas9 gene-editing therapy under
study for the treatment of hereditary angioedema (HAE). This letter responds to
your request for medical information concerning:

> {{INQUIRY_RESTATEMENT}}

This is an unsolicited response to a specific request for medical information.
The information below is drawn from the referenced source documents and is
presented in a balanced, non-promotional manner.

## Response

{{RESPONSE_BODY}}

## Important safety and fair-balance information

The data above should be interpreted in the context of the full safety and
efficacy profile of Lonvo-Z as reported in the referenced sources. Reported
findings reflect the specific study populations, dose levels, and timepoints
described; results may not generalize to other patients or settings. Where
adverse events, limitations, or uncertainties are described in the sources, they
are presented alongside efficacy findings above and should not be omitted when
this information is conveyed.

## Investigational-product statement

**Lonvoguran Ziclumeran (Lonvo-Z / NTLA-2002) is an investigational agent. It
has not been approved by the FDA, EMA, or any other health authority, and its
safety and efficacy have not been established.** Nothing in this letter should be
construed as a recommendation to use Lonvo-Z outside of an approved clinical
trial, nor as promotion of an unapproved product.

## References

{{REFERENCES}}

---

Should you require further information, please contact the Medical Information
Department. We are happy to provide additional detail or clarification.

Sincerely,

{{PREPARER}}
Medical Information Department
[COMPANY NAME]

---

<sub>{{DOC_ID}} · {{VERSION}} · **DRAFT — NOT FOR DISTRIBUTION. Pending medical/regulatory review.** · Page [#]</sub>
