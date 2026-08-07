# Vendor Risk Assessment — HippocratiCloud

Third-party risk assessment of HippocratiCloud, Smith Family Medicine's cloud-hosted
EHR provider. Built as part of ISMS coursework, using the same fictional practice as
the risk register and HIPAA-NIST crosswalk in this repo.

## Scope

HippocratiCloud hosts SFM's full electronic health record system. It has access to
every patient record SFM holds. No other vendor touches a comparable volume or
sensitivity of data.

**Tier: Critical.** A vendor at this access level is functionally equivalent to SFM's
own infrastructure — a compromise here is a compromise of SFM's entire patient
dataset, not a partial exposure.

## Assessment Methodology

Findings are scored using HITRUST's **PRISMA maturity model**, the scoring approach
HITRUST itself uses to evaluate individual controls during CSF certification. Five
levels, low to high:

| Level | Name | Meaning |
|---|---|---|
| 1 | Policy | A policy exists on paper |
| 2 | Procedure | The org knows how to execute the policy |
| 3 | Implemented | The control is actually in place and running |
| 4 | Measured | The org tracks and evaluates the control's effectiveness over time |
| 5 | Managed | The org acts on those measurements to actively improve the control |

HITRUST's own rule: Managed can't outscore Measured — you can't manage what you
aren't measuring, though you can measure something without fully managing it.

One control below found no policy at all. HITRUST's scale doesn't have a level for
that, so a **0 — Non-Existent** tier was added below Policy, consistent with how
maturity models like COBIT handle a true absence of any governance.

A signed Business Associate Agreement (BAA) is a HIPAA legal requirement for any
vendor handling PHI, not a maturity question — it's covered separately, not scored on
this scale.

---

## Findings

### Data Security — Level 3, Implemented

AES-256 encryption at rest. TLS 1.2+ enforced for all data in transit. Both controls
are in place and operating. No evidence of ongoing effectiveness tracking (log
review, periodic testing) was provided, which is what would push this to Measured.

### Access Control — Level 2, Procedure

RBAC is enforced for SFM's own users. HippocratiCloud support staff can request
temporary elevated access to specific patient records for support tickets. That
access is logged, but doesn't require SFM approval per instance. The exception
undermines the control enough to hold this at Procedure rather than Implemented —
the org knows what should happen, but what actually happens in practice has a gap.

**Recommendation:** Require SFM approval, not just logging, for any support-staff
elevated access to records. Target: 60 days.

### Compliance Certifications — Not PRISMA-scored

HippocratiCloud maintains a current SOC 2 Type II report — independent third-party
validation of its controls. It is not HITRUST certified. HITRUST is the
healthcare-specific standard and maps more directly to HIPAA's Security Rule than
SOC 2 does. For a Critical-tier vendor, that's a real gap, though the SOC 2 report
keeps it from being disqualifying on its own.

**Recommendation:** Request a HITRUST certification roadmap, even if full
certification runs past 90 days. Target: 90 days to produce the roadmap.

### Incident History & Breach Notification — Level 4, Measured

Contractual breach notification is 24 hours — ahead of the 24-72 hour range typical
in BAAs. HippocratiCloud disclosed a 2025 incident involving unauthorized access to a
subset of records through a misconfigured API endpoint. They track incident response
metrics (time-to-detect, time-to-contain) and ran a documented post-incident review
after the 2025 incident, feeding findings back into containment and notification
procedure. That tracking-over-time is what earns Measured, not just Implemented.

### Business Continuity / Disaster Recovery — Level 1, Policy

Weekly full backups, daily incremental. A cold site is in place, but the SLA around
it is loose — no firm RTO/RPO commitment. Cold site is the weakest DR tier: minimal
standby infrastructure, slow to activate. For a Critical-tier vendor holding all
PHI, this is undersized. A policy exists, but execution doesn't back it up.

**Recommendation:** Upgrade to a warm or hot site with defined RTO/RPO commitments.
Target: 90 days.

### Subcontractor Risk (Fourth-Party) — Level 0, Non-Existent

HippocratiCloud backs up to Azure and contracts HVAC maintenance for the facility
housing their servers. HVAC personnel have physical access to the server room but
don't touch PHI systems directly, so HIPAA's BAA flow-down requirement likely doesn't
apply here — that requirement is about PHI access, not physical proximity. What does
apply is Facility Access Controls (the same HIPAA standard covered in this repo's
crosswalk, mapped to NIST CSF's PR.AA). No escort requirement, supervision policy, or
access log exists for non-employee personnel in spaces housing PHI systems. No
policy of any kind — hence Level 0, not Level 1.

**Recommendation:** Establish a physical access policy and log for non-employee
personnel in server spaces. Target: 30 days.

---

## Overall Determination

**Continue the vendor relationship, contingent on a 90-day remediation plan and a
formal re-assessment at the end of that window.**

Full vendor replacement was considered given the Critical tier and the number of
findings, but migrating a live EHR platform is itself a major disruption and risk
event — arguably comparable in impact to some of the risks this assessment is meant
to prevent. Termination is disproportionate to findings that are maturity gaps, not
active compromises. HippocratiCloud has real strengths to build from: current SOC 2,
aggressive breach notification terms, and a demonstrated incident response process.

Continued relationship past 90 days is conditional on demonstrated progress against
the four remediation items above, not automatic.

| # | Remediation Item | Target |
|---|---|---|
| 1 | Require SFM approval for support-staff elevated access to records | 60 days |
| 2 | Upgrade DR from cold site to warm/hot site with defined RTO/RPO | 90 days |
| 3 | Establish physical access policy/log for non-employee server room access | 30 days |
| 4 | Provide a HITRUST certification roadmap | 90 days |

---

## Related

- [Risk Register](./risk-register.md) — Risk 8 (Cloud Storage Misconfiguration)
  covers SFM's side of this same vendor relationship.
- [HIPAA → NIST CSF 2.0 Crosswalk](./HIPAA-NIST-CSF-2.0-Crosswalk.md) — the Facility Access
  Controls finding above maps directly to standard #6 in that crosswalk (PR.AA).
