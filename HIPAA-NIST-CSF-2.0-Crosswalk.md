# HIPAA Security Rule → NIST CSF 2.0 Crosswalk

A crosswalk mapping all 18 HIPAA Security Rule standards (Administrative, Physical, and
Technical Safeguards) to their corresponding NIST Cybersecurity Framework (CSF) 2.0
function and category. Built as part of ISMS coursework, using Smith Family Medicine
(a fictional mid-sized medical practice) as the applied context.

## Why this exists

HIPAA's Security Rule establishes *what* covered entities are legally required to do
to protect electronic PHI (ePHI), but it doesn't prescribe *how*. NIST CSF 2.0 provides
a widely adopted structure for organizing cybersecurity controls. Mapping one to the
other lets an organization show, standard by standard, which control category
addresses each legal requirement — useful for gap analysis, audit preparation, and
communicating a security program's coverage to both compliance and technical
stakeholders.

**Precedent:** NIST itself maintains an official mapping between the two, published in
[NIST SP 800-66 Revision 2](https://csrc.nist.gov/pubs/sp/800/66/r2/final),
*Implementing the HIPAA Security Rule: A Cybersecurity Resource Guide*, developed in
collaboration with the HHS Office for Civil Rights. Per Appendix D of that guide, the
actual mapping table is hosted online in NIST's Cybersecurity and Privacy Reference
Tool (CPRT) rather than in the PDF itself, and is intentionally broad — it includes
CSF subcategories that both directly and indirectly relate to each HIPAA standard,
rather than a single primary mapping. This crosswalk takes a narrower approach by
design: one primary CSF category per HIPAA standard, presented as a single scannable
table, intended as a quick-reference companion rather than a replacement for NIST's
more exhaustive mapping.

## Scope

Covers all **18 standards** under the Security Rule's Administrative (9), Physical (4),
and Technical (5) Safeguards, plus the related Organizational Requirement for Business
Associate Contracts. Mappings are presented at the NIST CSF 2.0 **category** level
(e.g., `PR.AA`) rather than subcategory level, for consistency — several standards
reasonably map to more than one subcategory within a category, so category-level
mapping avoids implying a false precision. Readers who need subcategory-level detail
should consult NIST's official mapping in the
[Cybersecurity and Privacy Reference Tool (CPRT)](https://csrc.nist.gov/projects/cprt),
referenced in SP 800-66 Rev 2, Appendix D.

## Crosswalk

| # | HIPAA Standard | Citation | Type | NIST CSF 2.0 Category |
|---|---|---|---|---|
| 1 | Access Control | §164.312(a)(1) | Technical | PR.AA — Identity Management, Authentication & Access Control |
| 2 | Security Awareness & Training | §164.308(a)(5) | Administrative | PR.AT — Awareness & Training |
| 3 | Risk Analysis | §164.308(a)(1) | Administrative | ID.RA — Risk Assessment |
| 4 | Audit Controls | §164.312(b) | Technical | DE.CM — Continuous Monitoring |
| 5 | Contingency Plan | §164.308(a)(7) | Administrative | RC.RP — Incident Recovery Plan Execution |
| 6 | Facility Access Controls | §164.310(a)(1) | Physical | PR.AA — Identity Management, Authentication & Access Control |
| 7 | Transmission Security | §164.312(e)(1) | Technical | PR.DS — Data Security |
| 8 | Integrity Controls | §164.312(c)(1) | Technical | PR.DS — Data Security |
| 9 | Security Incident Procedures | §164.308(a)(6) | Administrative | RS.MA — Incident Management |
| 10 | Business Associate Contracts | §164.314(a) | Organizational | GV.SC — Cybersecurity Supply Chain Risk Management |
| 11 | Assigned Security Responsibility | §164.308(a)(2) | Administrative | GV.RR — Roles, Responsibilities & Authorities |
| 12 | Workforce Security | §164.308(a)(3) | Administrative | PR.AA — Identity Management, Authentication & Access Control |
| 13 | Information Access Management | §164.308(a)(4) | Administrative | PR.AA — Identity Management, Authentication & Access Control |
| 14 | Evaluation | §164.308(a)(8) | Administrative | ID.IM — Improvement |
| 15 | Workstation Use | §164.310(b) | Physical | PR.PS — Platform Security |
| 16 | Workstation Security | §164.310(c) | Physical | PR.PS — Platform Security |
| 17 | Device and Media Controls | §164.310(d)(1) | Physical | PR.DS — Data Security |
| 18 | Person or Entity Authentication | §164.312(d) | Technical | PR.AA — Identity Management, Authentication & Access Control |

## Notes on methodology

- Mappings reflect the *primary* CSF category a standard's core intent addresses. Some
  standards plausibly touch more than one category (for example, Contingency Planning
  has clear ties to both Recover and Identify); where that was the case, the category
  most directly aligned with the standard's stated purpose was selected.
- Two mappings were revised during development after initial placement in an adjacent
  function: Audit Controls was first placed under Identify (asset-focused) before being
  corrected to Detect (monitoring-focused), and Contingency Plan was first placed under
  Respond before being corrected to Recover, since the standard concerns restoring
  operations rather than containing an active incident. Both corrections reflect a
  recurring distinction in CSF 2.0: functions that sound adjacent (Identify vs. Detect,
  Respond vs. Recover) often describe different points in an incident timeline.

## Related

- [Risk Register](./risk-register.md) — risk assessment for the same fictional
  practice, several of whose controls (MFA, SIEM, encryption) map directly back to the
  CSF categories referenced above.
