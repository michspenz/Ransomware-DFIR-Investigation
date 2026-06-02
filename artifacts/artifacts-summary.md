# Forensic Artifacts Summary — Meridian Financial Services

## Host Artifacts

| Artifact | Location | Significance |
|----------|----------|--------------|
| `Invoice_March2024.docm` | `Downloads/` | Initial access vector — malicious phishing document |
| `~tmp_invoice_march.docm` | `AppData/Local/Temp/` | Staging copy written during macro execution |
| `lb_config.json` | `AppData/Local/Temp/` | LockBit configuration — confirmed MEGA as exfil target |
| `ConsoleHost_history.txt` | `AppData/Roaming/Microsoft/Windows/PowerShell/PSReadLine/` | PowerShell command history — attacker activity logged |
| `POWERSHELL.EXE-7B9D2A1F.pf` | `Windows/Prefetch/` | Prefetch file confirming PowerShell execution |
| `Restore-My-Files.txt` | Multiple directories | Ransom note deployed broadly across filesystem |
| `LockBit_Wallpaper.bmp` | `Desktop/` | Ransomware wallpaper replacement artifact |
| `CASE_ATTRIBUTION.txt` | Filesystem root | Attribution artifact confirming LockBit 2.0 |
| Windows Defender registry key | `HKLM\SOFTWARE\Policies\Microsoft\Windows Defender` | Evidence of Defender policy tampering |
| `vssadmin` in CMD/PS history + System.evtx | Multiple | Shadow copy deletion command confirmed across three artifact sources |

## Encrypted Files

| File | Sensitivity |
|------|-------------|
| `Employee_Salaries_CONFIDENTIAL.xlsx` | High — payroll data |
| `Client_List_2024.xlsx` | High — client PII |
| `AuditTrail_Q1.pdf` | High — financial audit records |
| `GreenPhilip_1040_2023.pdf` | High — personal tax return |
| `MeridianFinancial_Corp_Return.pdf` | High — corporate tax return |
| `Shared_ClientDB.accdb` | Critical — shared client database |
| `Budget_Planning_2024.xlsx` | Medium — internal financial planning |
| `Q1_FinancialReport_Final.xlsx` | Medium — quarterly financials |

## Network Artifacts

| Artifact | Value |
|----------|-------|
| Phishing domain | `meridian-invoices.com` |
| Malware delivery | HTTP GET `/Invoice_March2024.docm` |
| C2 server | `185.220.101.47` — TLS beaconing |
| Lateral movement target | `192.168.1.88` — SMB/NTLMSSP |
| Exfil platform | MEGA — `g.api.mega.co.nz` / `185.235.81.22` |

## Tools & Techniques (MITRE ATT&CK Mapped)

| Technique | ID | Evidence |
|-----------|----|----------|
| Phishing: Spearphishing Attachment | T1566.001 | `Invoice_March2024.docm` |
| User Execution: Malicious File | T1204.002 | DOCM macro execution |
| Command and Scripting: PowerShell | T1059.001 | Prefetch + PS history |
| Encrypted Channel: Asymmetric Crypto | T1573.002 | TLS C2 beaconing |
| Lateral Movement: SMB/Windows Admin Shares | T1021.002 | SMB2 + NTLMSSP traffic |
| Exfiltration to Cloud Storage | T1567.002 | MEGA upload |
| Impair Defenses: Disable or Modify Tools | T1562.001 | Defender registry tampering |
| Inhibit System Recovery | T1490 | VSS deletion |
| Data Encrypted for Impact | T1486 | LockBit 2.0 encryption |
