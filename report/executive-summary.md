# Executive Summary — Meridian Financial Services Ransomware Incident

**Prepared for:** Executive Leadership, Meridian Financial Services
**Classification:** Confidential
**Date:** March 2024

---

## What Happened

Meridian Financial Services suffered a targeted ransomware attack that resulted in
the encryption of critical business files, theft of sensitive data, and destruction
of recovery mechanisms. The attack began when employee Philip Green opened a
malicious document disguised as an invoice. From that single action, the attacker
gained full control of the affected workstation, moved deeper into the internal
network, and deployed LockBit 2.0 — one of the most prolific ransomware operations
in recent history.

---

## Business Impact

The attack had three distinct consequences:

**1. Data Theft**
Before encrypting files, the attacker stole sensitive business data and uploaded
it to an external cloud service. Compromised data includes client records, employee
salary information, corporate and personal tax returns, and financial reports.
This data is now in the attacker's possession regardless of whether a ransom is paid.

**2. Operational Disruption**
All critical files on the affected workstation were encrypted and rendered
inaccessible. The attacker also deleted Windows recovery points, eliminating
the fastest path to restoration.

**3. Potential Regulatory Exposure**
The confirmed exfiltration of client and employee data may trigger notification
obligations under applicable data protection regulations. Legal counsel should
assess exposure immediately.

---

## How It Started

A single phishing email carrying a malicious Microsoft Word document was all
it took. The document was designed to appear as a legitimate invoice. When opened,
it silently executed malicious code in the background while displaying normal
content to the user. This is a common and effective attack technique that bypasses
most standard email security controls when users are not adequately trained to
recognize it.

---

## What the Attacker Did

Once inside, the attacker moved methodically:

- Established a covert communication channel to an external server
- Moved laterally to another internal system
- Stole sensitive business data before triggering encryption
- Disabled Windows security tools to avoid detection
- Deleted backup recovery points to prevent restoration
- Deployed ransomware across the environment

The entire sequence from initial access to full encryption occurred within a
single session, consistent with a professional, operationally mature threat actor.

---

## Immediate Actions Required

| Priority | Action |
|----------|--------|
| Critical | Isolate all affected systems from the network immediately if not already done |
| Critical | Reset credentials for all accounts on affected systems |
| Critical | Engage legal counsel regarding data breach notification obligations |
| Critical | Do not pay the ransom without legal and security consultation — payment does not guarantee data deletion |
| High | Restore systems from the most recent clean backup available |
| High | Block all identified attacker infrastructure at the network perimeter |

---

## How to Prevent Recurrence

The root cause was a combination of human and technical factors, both addressable:

- **User awareness training** — staff must be able to identify phishing attempts
- **Macro execution controls** — Microsoft Office should be configured to block
  macros in documents sourced from the internet
- **Immutable backups** — backups must be stored offsite or in a format the
  attacker cannot delete
- **Endpoint detection** — security tooling capable of detecting behavioral
  anomalies would have flagged this attack at multiple stages
- **Network segmentation** — limiting which systems can communicate with each
  other reduces the attacker's ability to move laterally

---

## Conclusion

This attack was preventable. The attacker exploited a well-known technique against
a user who had no reason to suspect the document was malicious. The technical
controls that should have caught or slowed the attack were either absent or
successfully disabled. The full technical investigation is documented separately.
This summary is intended to inform leadership decision-making and guide the
immediate response.

---

*Full technical findings: `report/meridian-ransomware-report.md`*
*IOCs for network blocking: `iocs/iocs.csv`*
*Remediation detail: `report/incident-report.md`*
