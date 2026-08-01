# Smith Family Medicine — Information Security Risk Register

This risk register was developed as part of the Information Security Management System
(ISMS) coursework for Smith Family Medicine, a fictional mid-sized medical practice. It
identifies key information security risks, scores them using a numeric likelihood ×
impact methodology, documents existing (deliberately imperfect) controls, and proposes
tiered low-effort/high-effort treatment options for each risk.

## Methodology

### Likelihood Scale

A pure frequency-based scale, grounded in sector-level threat activity rather than
internal historical data (which a practice of this size would not have readily
available).

| Level | Descriptor | Basis |
|---|---|---|
| 1 | Rare | No known occurrence in the healthcare sector |
| 2 | Unlikely | Occurred in-sector, not at similar-sized practices |
| 3 | Possible | Has occurred at similar-sized healthcare practices |
| 4 | Likely | Actively trending against healthcare organizations currently |
| 5 | Almost Certain | Currently occurring/attempted against Smith Family Medicine, or a novel/unquantifiable threat (treated as worst-case by default) |

*Sources such as the HHS OCR Breach Portal, HIMSS Cybersecurity Survey, and HC3 threat
briefs would inform tier placement in a real assessment.*

**Note on inherent vs. residual/target likelihood:** the five tiers above describe the
same magnitude of likelihood regardless of when they're applied, but the *evidence
used to select a tier* differs by context. **Inherent likelihood** is assessed against
sector-wide threat activity, since no controls yet exist to differentiate Smith Family
Medicine from any other practice. **Residual and target likelihood** are instead
assessed against the likelihood of a *successful* occurrence given SFM's current or
planned controls — i.e., how much of the original attack pathway those controls
actually close off. This is why residual/target likelihood can move independently of
sector-wide trend data.

### Impact Scale

Weighted toward patient care disruption and PHI exposure, given HIPAA's Breach
Notification Rule thresholds (500+ affected individuals triggers mandatory HHS and
media notification).

| Level | Descriptor | Criterion |
|---|---|---|
| 1 | Negligible | No operational impact |
| 2 | Minor | Some operational impact, not affecting patient care |
| 3 | Major | Disrupts a single provider/department for less than a day, interrupting patient care; no PHI exposure |
| 4 | Severe | Disrupts the whole practice for less than a week, and/or PHI breach below HHS's 500-record threshold |
| 5 | Critical | Disrupts the whole practice for a week or more, and/or PHI breach at or above 500 records (HHS + media notification required) |

**Risk Score** = Likelihood × Impact (max 25)

**Known limitation:** this impact scale is patient-care-centric and does not cleanly
score risks that are primarily financial or fraud-related without operational
disruption (see Risk 7).

### Treatment Strategies

- **Mitigate** — reduce likelihood/impact via additional controls
- **Accept** — retain risk as-is; within acceptable tolerance
- **Transfer** — shift risk via insurance, contract, or third party
- **Avoid** — eliminate the activity/exposure causing the risk

Low-effort options represent near-term, resource-light actions the practice could
realistically implement without significant budget or staffing changes. High-effort
options represent the target state the practice should work toward as resources allow,
and are used to calculate the target residual risk shown for each item below.

---

## Risk Register

### Risk 1 — Ransomware / EHR System

**Risk Statement:** Due to inconsistent patching, outdated software on the EHR system
could be exploited by ransomware, resulting in encrypted patient records and disrupted
patient care.

| | Likelihood | Impact | Score |
|---|---|---|---|
| Inherent | 5 | 5 | 25 |
| Residual | 5 | 4 | 20 |
| Target (high-effort) | 3 | 4 | 12 |

**Existing Controls:** A backup strategy exists but is applied inconsistently.

**Treatment Strategy:** Mitigate

- *Low effort:* Establish a monthly patch cycle for the EHR system and supporting
  infrastructure to reduce exposure to known vulnerabilities.
- *High effort:* Above, plus a formal backup schedule (weekly full, daily incremental)
  to reduce recovery time and data loss in a ransomware event.

---

### Risk 2 — Phishing / Email Compromise

**Risk Statement:** Due to gaps in employee security awareness, a phishing attack could
compromise a staff email account, resulting in unauthorized access to sensitive
communications or systems.

| | Likelihood | Impact | Score |
|---|---|---|---|
| Inherent | 4 | 4 | 16 |
| Residual | 4 | 4 | 16 |
| Target (high-effort) | 2 | 4 | 8 |

**Existing Controls:** Phishing awareness posters are displayed; no formal Security
Education, Training & Awareness (SETA) program exists.

**Treatment Strategy:** Mitigate

- *Low effort:* Conduct quarterly phishing simulation and awareness training.
- *High effort:* Above, plus a phishing-reporting incentive program to encourage
  consistent employee reporting.

---

### Risk 3 — Insider Access Without Business Justification

**Risk Statement:** Due to insufficient access monitoring, an insider could access
patient records without business justification, resulting in a privacy violation and
potential HIPAA breach.

| | Likelihood | Impact | Score |
|---|---|---|---|
| Inherent | 3 | 4 | 12 |
| Residual | 3 | 4 | 12 |
| Target (high-effort) | 2 | 4 | 8 |

**Existing Controls:** None beyond employee trust; no formal access monitoring in
place.

**Treatment Strategy:** Mitigate

- *Low effort:* Implement access logging for patient records with quarterly manual
  review.
- *High effort:* Deploy a SIEM (likely via a managed security service provider (MSSP)
  given limited in-house capacity) for real-time access monitoring, paired with annual
  access-policy training.

---

### Risk 4 — Weak Passwords / Unauthorized EHR Access

**Risk Statement:** Due to weak or reused passwords, an attacker could gain
unauthorized access to the EHR system, resulting in exposure or manipulation of
patient records.

| | Likelihood | Impact | Score |
|---|---|---|---|
| Inherent | 3 | 5 | 15 |
| Residual | 3 | 5 | 15 |
| Target (high-effort) | 1 | 5 | 5 |

**Existing Controls:** Minimum 8-character password with one required number; no
password rotation policy.

**Treatment Strategy:** Mitigate

- *Low effort:* Strengthen password policy (12+ characters, mixed case/number/special
  character, quarterly rotation).
- *High effort:* Add multi-factor authentication (MFA) and SIEM-based access logging
  for the EHR system, likely via a managed security service provider (MSSP) given
  limited in-house capacity.

*Target rationale: MFA combined with active SIEM monitoring is treated as closing off
the remaining practical attack paths for credential-based access to this system,
justifying the drop to a likelihood of 1.*

---

### Risk 5 — Lost or Stolen Portable Medical Device

**Risk Statement:** Due to lack of encryption on portable medical devices, a lost or
stolen device could expose patient data, resulting in a reportable PHI breach.

| | Likelihood | Impact | Score |
|---|---|---|---|
| Inherent | 3 | 4 | 12 |
| Residual | 3 | 4 | 12 |
| Target (high-effort) | 1 | 2 | 2 |

**Existing Controls:** Devices are inventoried quarterly — a detective control that
identifies a missing device after the fact, but does not prevent loss or protect data
on the device itself.

**Treatment Strategy:** Mitigate

- *Low effort:* Enable AES-256 encryption on all portable medical devices.
- *High effort:* Move to weekly device inventory checks and add asset-tracking/alarm
  tags that trigger if a device leaves the premises.

---

### Risk 6 — Equipment Failure

**Risk Statement:** Due to aging server hardware without redundancy, equipment failure
could cause loss of access to patient records, resulting in disrupted patient care.

| | Likelihood | Impact | Score |
|---|---|---|---|
| Inherent | 2 | 4 | 8 |
| Residual | 2 | 4 | 8 |
| Target (high-effort) | 1 | 2 | 2 |

**Existing Controls:** Two aging servers in place, with no true failover between them.

**Treatment Strategy:** Mitigate

- *Low effort:* Configure the existing servers in a RAID 1 array for basic redundancy.
- *High effort:* Replace aging hardware and add server capacity using a formal systems
  development life cycle (SDLC) process to ensure security requirements are built in
  from procurement through deployment, and evaluate RAID 5/6/10 for stronger fault
  tolerance.

---

### Risk 7 — Compromised Credentials / Billing System

**Risk Statement:** Due to compromised credentials, an attacker could gain
unauthorized access to the financial/billing system, resulting in financial loss or
fraudulent billing activity.

| | Likelihood | Impact | Score |
|---|---|---|---|
| Inherent | 4 | 3 | 12 |
| Residual | 3 | 3 | 9 |
| Target (high-effort) | 2 | 3 | 6 |

**Existing Controls:** MFA is enforced on financial system access.

**Treatment Strategy:** Mitigate

- *Low effort:* Implement a credential-handling policy with employee training to
  reduce exposure risk.
- *High effort:* Introduce separation of duties and zero-trust access principles to
  reduce both likelihood and impact.

*Note: this risk is primarily financial/fraud-related rather than patient-care- or
PHI-centric, which the impact scale above does not score cleanly — see "known
limitation" note in the Methodology section.*

---

### Risk 8 — Cloud Storage Misconfiguration

**Risk Statement:** Due to misconfigured cloud storage settings, cloud-hosted EHR
backups could be exposed publicly, resulting in a large-scale PHI breach.

| | Likelihood | Impact | Score |
|---|---|---|---|
| Inherent | 4 | 5 | 20 |
| Residual | 4 | 5 | 20 |
| Target (high-effort) | 2 | 4 | 8 |

**Existing Controls:** In-house IT staff, without dedicated cloud security expertise,
manage the practice's Platform-as-a-Service (PaaS) cloud configuration.

**Treatment Strategy:** Mitigate

- *Low effort:* Shift from a self-managed PaaS model to a SaaS EHR model, transferring
  configuration risk to the vendor.
- *High effort:* Above, plus formal cloud security training for in-house IT staff.

---

### Risk 9 — Shadow AI (Credential / Access Exposure)

**Risk Statement:** Due to a lack of policy or technical controls on AI tool usage,
staff could paste PHI, credentials, or system access details into an unsanctioned
public AI tool, resulting in loss of control over that information outside the
organization.

| | Likelihood | Impact | Score |
|---|---|---|---|
| Inherent | 5 | 5 | 25 |
| Residual | 5 | 5 | 25 |
| Target (high-effort) | 1 | 4 | 4 |

**Existing Controls:** None currently in place.

**Treatment Strategy:** Mitigate

- *Low effort:* Establish an AI use policy and quarterly training on associated risks.
- *High effort:* Deploy an internally hosted, air-gapped AI model alongside the policy
  and training.

---

### Risk 10 — Natural Disaster

**Risk Statement:** Due to the practice's reliance on a single physical location, a
natural disaster could damage on-site infrastructure, resulting in extended disruption
to patient care and records access.

| | Likelihood | Impact | Score |
|---|---|---|---|
| Inherent | 1 | 4 | 4 |
| Residual | 1 | 4 | 4 |
| Target (accepted, no further action) | 1 | 4 | 4 |

**Existing Controls:** Quarterly off-site data backups.

**Treatment Strategy:** Accept

- Given the low likelihood and the mitigating effect of existing off-site backups on
  potential impact, further investment is not proportional to the residual risk at
  this time. This determination should be revisited if the practice's physical
  location, disaster history, or backup posture changes.

---

## Summary — Risks Ranked by Residual Score

| Rank | Risk | Residual Score | Target Score (High-Effort) |
|---|---|---|---|
| 1 | Shadow AI (credential/access exposure) | 25 | 4 |
| 2 | Ransomware / EHR System | 20 | 12 |
| 2 | Cloud Storage Misconfiguration | 20 | 8 |
| 4 | Phishing / Email Compromise | 16 | 8 |
| 5 | Weak Passwords / EHR Access | 15 | 5 |
| 6 | Insider Access Without Justification | 12 | 8 |
| 6 | Lost or Stolen Portable Device | 12 | 2 |
| 8 | Compromised Credentials / Billing | 9 | 6 |
| 9 | Equipment Failure | 8 | 2 |
| 10 | Natural Disaster | 4 | 4 |

Risk 4 (weak passwords) is a useful example of target likelihood dropping further than
target impact — the high-effort control (MFA + SIEM) is treated as closing off the
practical paths to gaining access in the first place, even though the impact of a
successful compromise (full EHR record exposure) remains unchanged regardless of how
an attacker got in.
