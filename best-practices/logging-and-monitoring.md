# Logging and Monitoring: Best Practices

You cannot detect or investigate what you did not log. Log with detection and investigation use cases in mind, not "everything".

## What to collect (minimum viable set)

| Source | Key events |
|---|---|
| Identity (Entra ID/AD/Okta) | Sign-ins (success/fail, MFA result, IP, device), role changes, MFA method changes, app consents, password resets |
| Windows endpoints/servers | Security log: 4624/4625 logon, 4672 special privileges, 4688 process creation with command line, 4697/7045 service install, 4698 scheduled task, 4720/4728/4732 account/group changes, 1102 log cleared |
| Linux | auth log / journald (SSH, sudo), auditd (exec, file changes on sensitive paths) |
| EDR | Detections, process trees, network connections, response actions |
| Network | Firewall allow/deny, DNS queries, proxy/web logs, VPN, NetFlow |
| Email | Delivery, URL clicks, attachments, mailbox rule changes, forwarding |
| Cloud control plane | Azure Activity Log, AWS CloudTrail, GCP Audit Logs (management and data events for sensitive stores) |
| Applications | Authentication, authorisation failures, admin actions, input-validation errors |

Enable **PowerShell script block logging (4104)** and **command-line process auditing**. They are the highest-value Windows settings for detection.

## Principles

1. **Centralise** into a SIEM or log platform; local logs are the first thing an attacker deletes.
2. **Synchronise time** (NTP) everywhere; an incident timeline built on skewed clocks is useless.
3. **Protect logs**: restricted write/delete access, integrity controls, separate admin boundary from what is logged.
4. **Retention**: hot searchable 30-90 days, archive 12 months or as regulation requires (check your sector). Attackers are often present for weeks before detection.
5. **Normalise and enrich** (asset owner, criticality, user department, geo-IP, threat intel).
6. **Detect on behaviour, map to ATT&CK**, and measure coverage by technique.
7. **Tune**: every alert needs an owner, a runbook link, and a false-positive review. Retire or fix rules with a persistently high false-positive rate.
8. **Test**: use atomic tests or purple teaming to confirm detections actually fire.

## Detection engineering loop

`Threat/ATT&CK technique → required log source → rule (Sigma/KQL) → test → deploy → tune → measure`

Example rules in this repo: [detection/](../detection/README.md).

## Metrics

| Metric | Meaning |
|---|---|
| Log source coverage | % of critical assets sending logs |
| ATT&CK technique coverage | Techniques with at least one tested detection |
| Mean time to detect / acknowledge / respond | Operational effectiveness |
| False positive rate per rule | Signal quality |
| Alert backlog age | Capacity vs. volume |

## Common failures

- Logging enabled but never forwarded
- Command-line auditing off, so process-creation events lack the arguments
- Cloud data-plane events (storage reads) disabled for cost reasons on the most sensitive accounts
- Alerts routed to a mailbox nobody reads

## Standards

NIST CSF 2.0 `DE.CM`, `DE.AE`; ISO/IEC 27001:2022 A 8.15, 8.16, 8.17 (clock synchronisation); CIS Controls v8 8 (Audit Log Management).
