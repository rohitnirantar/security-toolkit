# Incident Response Plan Template

> Copy this file, replace every `<placeholder>`, delete guidance in *italics*, and have the plan approved by management.
> Aligned in structure with NIST SP 800-61 Rev. 3 (incident response as part of cyber risk management) and ISO/IEC 27035.

| Field | Value |
|---|---|
| Organisation | `<name>` |
| Plan owner | `<role, not a person>` |
| Version / date | `<1.0 / YYYY-MM-DD>` |
| Next review | `<date; at least annually and after every major incident>` |

## 1. Purpose and scope

*One paragraph: what this plan covers (systems, data, locations, third parties) and what it does not.*

## 2. Definitions

- **Event**: any observable occurrence in a system or network.
- **Incident**: an event, or series of events, that actually or potentially compromises confidentiality, integrity or availability, or violates policy.
- **Major incident**: an incident meeting any P1 criterion in section 5.

## 3. Roles and responsibilities

| Role | Responsibility | Primary | Backup |
|---|---|---|---|
| Incident Commander | Owns decisions, severity, and the timeline | `<name/contact>` | `<name/contact>` |
| Technical Lead | Investigation, containment, eradication | | |
| Communications Lead | Internal updates, customers, regulators, media | | |
| Legal / Privacy | Notification duties, privilege, evidence handling | | |
| HR | Insider cases, employee communications | | |
| Executive Sponsor | Budget, risk-acceptance and business-impact decisions | | |

*Keep an out-of-band contact list (printed or in a system that does not depend on the corporate network).*

## 4. Incident lifecycle

1. **Prepare**: tooling, logging, runbooks, contacts, exercises.
2. **Detect and report**: how staff and monitoring raise an incident (`<channel>`, `<phone>`).
3. **Triage and analyse**: confirm, classify, scope, assign severity.
4. **Contain**: stop the spread, preserve evidence.
5. **Eradicate and recover**: remove the cause, restore from known-good, monitor.
6. **Learn**: post-incident review within 5 working days, tracked actions.

## 5. Severity matrix

| Severity | Criteria (any) | Response target | Escalate to |
|---|---|---|---|
| P1 Critical | Confirmed data breach of regulated/sensitive data; ransomware or destructive attack; loss of a critical service; active attacker with privileged access | Start within 15 min, 24x7 | Exec sponsor, Legal, Comms |
| P2 High | Compromised account with sensitive access; malware on multiple hosts; suspected data exposure | Start within 1 hour | Security manager |
| P3 Medium | Single-host malware, policy violation with limited impact | Same business day | Team lead |
| P4 Low | Informational, failed attack, false positive | Within 3 business days | None |

*Tune the thresholds to your organisation; the point is that severity is defined before the incident.*

## 6. Communication

- **Internal**: status update cadence per severity (for example P1 every 60 min).
- **External**: all customer, regulator and media communication goes through the Communications Lead and Legal.
- **Regulatory clocks**: list the notification duties that apply (for example GDPR 72 hours to the supervisory authority, sector-specific rules) and who owns each. *Confirm with counsel; do not copy this line without checking your obligations.*
- Use a **dedicated, access-controlled channel** per major incident. Assume the corporate chat may be compromised if the attacker has domain access.

## 7. Evidence handling

- Record who collected what, when, from where, and with which tool.
- Hash collected artefacts (for example SHA-256) and store them read-only.
- Prefer forensic images or EDR-collected packages over ad-hoc copying.
- Keep a chain-of-custody log if legal action is possible.

## 8. Playbooks

Link scenario playbooks here:

- [Ransomware](playbook-ransomware.md)
- [Phishing](playbook-phishing.md)
- [Compromised account](playbook-compromised-account.md)

## 9. Testing and maintenance

- Tabletop exercise at least twice a year; technical restore test at least annually.
- Update the plan after every P1/P2 incident and every organisational change.
- Track exercise findings as dated, owned actions.

## 10. Approval

| Name | Role | Date |
|---|---|---|
| | | |
