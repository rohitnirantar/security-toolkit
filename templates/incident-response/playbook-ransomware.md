# Playbook: Ransomware

| Field | Value |
|---|---|
| Default severity | P1 |
| Primary ATT&CK techniques | T1486 Data Encrypted for Impact, T1490 Inhibit System Recovery, T1489 Service Stop, T1078 Valid Accounts, T1021 Remote Services, T1567 Exfiltration Over Web Service |
| Last reviewed | 2026-11-23 |

## Triggers

- EDR/AV detection of ransomware or mass file modification
- Users report renamed/unreadable files or a ransom note
- Backup deletion, shadow-copy deletion (`vssadmin delete shadows`, `wmic shadowcopy delete`) or backup-agent stopped
- Sudden spike in file-share write activity or CPU on file servers

## 1. Triage (first 15 minutes)

- [ ] Declare a P1, name an Incident Commander, open the dedicated channel (out-of-band if domain compromise is suspected)
- [ ] Identify patient zero and the set of affected hosts, shares and accounts
- [ ] Capture the ransom note and a sample of encrypted files (read-only copies)
- [ ] Note the file extension and ransom-note filename; they help identify the family

## 2. Contain (stop the spread first)

- [ ] **Isolate affected hosts from the network** using EDR network containment or by unplugging/disabling the NIC. Prefer isolation over shutdown: powering off loses volatile memory that may contain encryption keys or attacker tooling. If isolation is impossible and encryption is actively running, shutting down may still be the right call. The Incident Commander decides.
- [ ] Disable or reset the compromised accounts, including any privileged and service accounts that touched affected hosts
- [ ] Block attacker infrastructure (IPs, domains) at the firewall, proxy and DNS
- [ ] Isolate file servers and, if needed, whole network segments
- [ ] **Protect backups**: disconnect or lock backup repositories and verify they are not reachable from the compromised domain
- [ ] Assume the attacker has domain-level access until proven otherwise: plan for a credential reset (including `krbtgt` twice, and service accounts)

## 3. Investigate

- [ ] Determine initial access (phishing, exposed RDP/VPN, vulnerable edge device, stolen credentials, supply chain)
- [ ] Determine whether data was **exfiltrated** before encryption (double extortion). Review proxy/firewall egress logs, cloud-sync tools, `rclone`/`MEGAsync`/`WinSCP` usage
- [ ] Hunt for persistence and lateral movement: new accounts, scheduled tasks, services, remote-management tools, GPO changes
- [ ] Collect memory and disk evidence from at least one affected host before reimaging
- [ ] Search the environment for the same indicators on hosts not yet encrypted

## 4. Eradicate and recover

- [ ] Rebuild affected systems from known-good images; do not "clean" and reuse
- [ ] Patch or close the initial access path before reconnecting anything
- [ ] Restore data from verified, offline or immutable backups; scan restored data
- [ ] Restore in priority order agreed with the business (identity, core services, then the rest)
- [ ] Reset all credentials, secrets, API keys and certificates that may have been exposed
- [ ] Increase monitoring on restored systems for at least 30 days

## 5. Communicate

- [ ] Legal and Communications engaged at declaration
- [ ] Determine breach-notification duties if data exfiltration is plausible
- [ ] Consider reporting to law enforcement and national CERT
- [ ] **Do not decide on ransom payment at the technical level.** It is an executive and legal decision; involve counsel, insurers and law enforcement, and check sanctions exposure before any contact with the actor

## 6. After the incident

- [ ] Post-incident report within 5 working days ([template](incident-report-template.md))
- [ ] Test restoration regularly, keep one backup copy offline or immutable
- [ ] Review: MFA on all remote access, EDR coverage, segmentation, privileged-access tiering, patch SLAs for edge devices

## Decision points

| Question | Who decides |
|---|---|
| Shut down vs isolate | Incident Commander with Technical Lead |
| Take business-critical systems offline | Incident Commander with Executive Sponsor |
| Notify regulators / customers | Legal with Executive Sponsor |
| Engage third-party IR firm | Executive Sponsor |
| Ransom payment | Executive leadership with Legal, insurer, law enforcement |
