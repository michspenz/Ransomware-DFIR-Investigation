# Attack Timeline — Meridian Financial Services

All timestamps derived from PCAP analysis and forensic artifact correlation.

| Time (Relative) | Stage | Description |
|-----------------|-------|-------------|
| T+0s | Phishing Delivery | Victim receives phishing email with malicious invoice attachment |
| T+806s | Document Download | `Invoice_March2024.docm` retrieved from `meridian-invoices.com` over HTTP |
| T+~806s | Macro Execution | Macro-enabled document opened by Philip Green; malware staging begins |
| T+~806s | Staging Artifact | `~tmp_invoice_march.docm` written to `%TEMP%` |
| T+1258s | C2 Establishment | TLS Client Hello initiated to `185.220.101.47` |
| T+1320s–1440s | C2 Beaconing | Periodic TLSv1.2 Application Data sent at ~60s intervals |
| T+2520s | Lateral Movement | SMB2 Negotiate Protocol Request sent to `192.168.1.88` |
| T+2520s | Credential Reuse | NTLMSSP authentication observed during SMB pivot |
| T+2640s | Data Exfiltration | DNS query to `g.api.mega.co.nz`; encrypted upload to MEGA initiated |
| T+2642s | Exfil Traffic | Outbound connection to MEGA endpoint `185.235.81.22` |
| T+post-exfil | Defense Evasion | Windows Defender policy tampered via registry |
| T+post-exfil | Anti-Forensics | `vssadmin delete shadows /all /quiet` executed — shadow copies destroyed |
| T+post-exfil | Encryption | LockBit 2.0 encrypts business files, appending `.lockbit` extension |
| T+final | Extortion | Ransom notes deployed across filesystem; desktop wallpaper replaced |
