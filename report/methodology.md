# Investigation Methodology

## Overview

This investigation followed a structured Digital Forensics & Incident Response
(DFIR) methodology, combining forensic disk image analysis with network packet
capture investigation to reconstruct the full attack chain.

---

## Evidence Acquired

| Evidence Item | Type | Description |
|---------------|------|-------------|
| `meridian_workstation.E01` | Forensic disk image | EnCase E01 format — NTFS filesystem |
| `meridian_incident.pcap` | Packet capture | Network traffic during incident window |

---

## Phase 1 — Evidence Validation

- Verified integrity and format of acquired evidence files
- Confirmed E01 image as valid EnCase/EWF format via `file` command
- Identified and resolved initial archive corruption issue
- Validated PCAP file and repaired corruption using `pcapfix`

## Phase 2 — Forensic Image Processing

- Created mount directories for EWF and filesystem layers
- Mounted E01 image using `ewfmount`
- Identified raw filesystem as NTFS via `fsstat`
- Mounted NTFS filesystem in read-only mode using `mount -o ro,loop`
- Preserved forensic integrity throughout — no writes to evidence

## Phase 3 — Host Artifact Analysis

Conducted targeted enumeration across the mounted filesystem:

- Ransom note discovery — `find` with wildcard pattern matching
- Encrypted file enumeration — `.lockbit` extension search
- Initial access vector identification — `.docm` file discovery
- PowerShell artifact recovery — history file and prefetch analysis
- Malware attribution — keyword grep across filesystem
- Exfiltration configuration — `lb_config.json` analysis
- Anti-forensics evidence — `vssadmin` command grep across multiple artifact sources
- Security control tampering — Windows Defender registry key analysis

## Phase 4 — Network Traffic Analysis

- Loaded repaired PCAP into `tshark` for protocol-level analysis
- Identified phishing infrastructure via DNS query analysis
- Confirmed malware delivery over HTTP
- Isolated C2 traffic by filtering on attacker IP
- Identified TLS beaconing pattern and calculated beacon interval
- Detected SMB lateral movement via `smb2` and `ntlmssp` filter
- Confirmed MEGA exfiltration via DNS and outbound connection analysis

## Phase 5 — Correlation & Timeline Reconstruction

- Cross-referenced host artifacts against network evidence
- Reconstructed full attack chain from initial phishing delivery to encryption
- Calculated time deltas between attack stages using PCAP timestamps
- Mapped attacker techniques to MITRE ATT&CK framework

## Phase 6 — Reporting

- Documented all findings with supporting commands and outputs
- Extracted and structured all IOCs
- Produced incident report with impact assessment and recommendations
- Mapped all observed techniques to MITRE ATT&CK

---

## Tools Used

| Tool | Purpose |
|------|---------|
| `ewfmount` | Mount EnCase E01 forensic image |
| `fsstat` | Identify filesystem type and metadata |
| `mount` | Mount NTFS filesystem read-only |
| `find` | Enumerate files and artifacts across filesystem |
| `grep` | Keyword search across filesystem artifacts |
| `cat` | Read file contents |
| `tshark` | Command-line packet capture analysis |
| `pcapfix` | Repair corrupted PCAP file |

---

## Forensic Principles Applied

- **Read-only mounting** — evidence mounted with `ro` flag throughout, no writes
- **Evidence validation** — file integrity and format confirmed before analysis
- **Documentation** — all commands and outputs recorded verbatim
- **Chain of custody** — evidence handled and processed without modification
