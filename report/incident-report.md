# Incident Report — Meridian Financial Services Ransomware Attack

## Executive Summary

On or around March 2024, Meridian Financial Services suffered a ransomware attack
attributed to the LockBit 2.0 threat actor group. The attack originated from a
macro-enabled phishing document opened by employee Philip Green. The attacker
established command-and-control communication, moved laterally across the internal
network, exfiltrated sensitive business data to MEGA cloud storage, destroyed
recovery mechanisms, and encrypted critical business files. The incident resulted
in full compromise of the affected workstation and potential exposure of confidential
financial, payroll, and client data.

---

## Incident Details

| Field | Value |
|-------|-------|
| Organization | Meridian Financial Services |
| Affected User | Philip Green |
| Affected Host | Philip Green's workstation (`192.168.1.45`) |
| Internal Pivot Target | `192.168.1.88` |
| Incident Type | Ransomware — Data Encryption + Exfiltration |
| Malware Family | LockBit 2.0 |
| Victim ID | `4A9F2E8B-7C31-4D56-A091-F3E28C107B44` |
| Exfiltration Destination | MEGA (`g.api.mega.co.nz`) |
| C2 Server | `185.220.101.47` |
| Severity | Critical |
| Status | Post-incident — Investigation Complete |

---

## Affected Data

The following categories of sensitive data were encrypted and likely exfiltrated:

- Employee payroll and salary records
- Client lists and engagement documents
- Corporate and personal tax returns
- Quarterly financial reports
- Shared client database (`Shared_ClientDB.accdb`)
- Internal budget and revenue projections

---

## Impact Assessment

| Impact Area | Description |
|-------------|-------------|
| Data Confidentiality | High — sensitive financial and client data exfiltrated to MEGA |
| Data Integrity | High — files encrypted, shadow copies destroyed |
| Data Availability | Critical — all business files rendered inaccessible |
| Recovery Capability | Severely limited — VSS deleted, no local backups confirmed |
| Regulatory Risk | High — potential GDPR/data protection violations depending on jurisdiction |

---

## Root Cause

The root cause of the incident was successful execution of a macro-enabled Word
document (`Invoice_March2024.docm`) delivered via phishing email. The macro
executed a payload that established an outbound C2 channel, enabling the attacker
to conduct all subsequent malicious activity. Contributing factors include:

- User execution of untrusted macro-enabled document
- Insufficient email filtering controls
- Windows Defender weakened prior to or during attack
- Absence of network segmentation preventing lateral movement
- No offsite or immutable backup preventing full data loss

---

## Recommendations

| Priority | Recommendation |
|----------|----------------|
| Critical | Restore affected systems from clean backups or reimage |
| Critical | Reset all credentials for Philip Green and any accounts accessible from `192.168.1.88` |
| Critical | Block IOCs at perimeter — domains, IPs listed in `iocs/iocs.csv` |
| High | Enforce macro execution policies via Group Policy — disable macros from internet-sourced documents |
| High | Deploy immutable/offsite backups — VSS alone is insufficient |
| High | Enable and harden Windows Defender — review tampered registry keys |
| High | Implement network segmentation to limit lateral SMB movement |
| Medium | Conduct phishing awareness training for all staff |
| Medium | Deploy EDR solution with behavioral detection capabilities |
| Medium | Monitor for outbound connections to cloud storage platforms (MEGA, etc.) |

---

## Investigator Notes

This report was produced as part of a DFIR investigation conducted on forensic
evidence including a disk image (`meridian_workstation.E01`) and packet capture
(`meridian_incident.pcap`). All findings are based on forensic artifact analysis
and network traffic correlation. Full technical findings are documented in
`meridian-ransomware-report.md`.
