# Post-Incident Report Template

> Blameless format. Focus on how systems and processes allowed the incident, not on who made a mistake.
> Complete within 5 working days of closing the incident.

## Summary

| Field | Value |
|---|---|
| Incident ID | `INC-YYYY-NNN` |
| Severity | P1 / P2 / P3 / P4 |
| Status | Open / Contained / Closed |
| Incident Commander | `<role>` |
| Detected | `<UTC timestamp>` |
| Contained | `<UTC timestamp>` |
| Resolved | `<UTC timestamp>` |
| Detection source | SIEM alert / EDR / user report / third party / other |

**One-paragraph summary** (what happened, impact, current state):

> ...

## Impact

- Systems / accounts affected: ...
- Data affected (type, volume, sensitivity): ...
- Business impact (downtime, cost, customers): ...
- Notification obligations triggered (regulators, customers) and when met: ...

## Timeline (UTC)

| Time | Event | Source |
|---|---|---|
| | Initial access | |
| | First detection | |
| | Containment started | |
| | Eradication complete | |
| | Service restored | |

## Root cause

- **Initial access vector**: ...
- **Contributing factors** (control gaps, misconfigurations, process failures): ...
- **MITRE ATT&CK techniques observed**: `T....` ...

*Use "5 whys" until you reach something you can fix at the system or process level.*

## What went well

-

## What went poorly

-

## Detection and response metrics

| Metric | Value |
|---|---|
| Time to detect (initial access to detection) | |
| Time to acknowledge | |
| Time to contain | |
| Time to recover | |

## Corrective and preventive actions

| # | Action | Owner (role) | Due | Priority | Status |
|---|---|---|---|---|---|
| 1 | | | | | |

## Indicators of compromise

| Type | Value | Context |
|---|---|---|
| IP / domain / hash / account | | |

*Share IOCs only through approved channels; defang URLs and IPs in documents (`hxxps://`, `1.2.3[.]4`).*

## Lessons for the plan and playbooks

-
