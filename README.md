# Ransomware DFIR Investigation — Meridian Financial Services

A Digital Forensics & Incident Response (DFIR) investigation of a simulated LockBit 2.0 ransomware attack against Meridian Financial Services.

## Case Summary

A business user opened a malicious macro-enabled Word document (`Invoice_March2024.docm`) delivered via phishing. The attack resulted in full enterprise encryption, data exfiltration, and anti-forensics activity.

## Investigation Scope

- Forensic image analysis (E01 format)
- Packet capture analysis and repair
- Malware attribution
- IOC extraction
- Full attack timeline reconstruction

## Attack Chain

| Stage | Activity |
|-------|----------|
| 1 | Phishing delivery via malicious `.docm` |
| 2 | Macro execution, malware staging |
| 3 | C2 beaconing to `185.220.101.47` |
| 4 | SMB lateral movement to `192.168.1.88` |
| 5 | Data exfiltration via MEGA |
| 6 | Windows Defender tampering |
| 7 | Shadow copy deletion |
| 8 | LockBit 2.0 encryption |
| 9 | Ransom note deployment |

## Key IOCs

| Type | Value |
|------|-------|
| Malicious domain | `meridian-invoices.com` |
| C2 IP | `185.220.101.47` |
| Exfil IP | `185.235.81.22` |
| Exfil platform | `g.api.mega.co.nz` |
| Malware family | LockBit 2.0 |
| Ransom extension | `.lockbit` |

## Tools Used

- Kali Linux
- ewfmount / fsstat
- tshark / pcapfix
- grep / find

## Files

- `meridian-ransomware-report.md` — Full DFIR report with commands, outputs, and findings
