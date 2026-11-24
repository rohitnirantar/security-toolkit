# Risk Scoring Guide

How the [risk register](risk-register.csv) calculates risk. Simple, consistent and explainable beats sophisticated and ignored.

## Method

**Risk = Likelihood x Impact**, each on a 1-5 scale, giving a score of 1-25. Score **inherent risk** (no controls considered), list the **existing controls**, then score **residual risk** (with controls). The gap shows what your controls are worth; the residual score drives decisions.

## Likelihood

| Score | Label | Guide |
|---|---|---|
| 1 | Rare | Not expected in the next 3+ years |
| 2 | Unlikely | Could happen once in 1-3 years |
| 3 | Possible | Could happen once a year |
| 4 | Likely | Several times a year |
| 5 | Almost certain | Monthly or more, or already happening |

## Impact

Use the **highest** applicable dimension.

| Score | Label | Financial | Operational | Data / compliance |
|---|---|---|---|---|
| 1 | Negligible | Under `<amount>` | Minutes of disruption, no customer effect | No sensitive data, no regulatory interest |
| 2 | Minor | `<amount>` | Hours, internal teams only | Limited internal data |
| 3 | Moderate | `<amount>` | Up to 1 day, some customers affected | Confidential data, reportable to a regulator |
| 4 | Major | `<amount>` | Multi-day outage of a key service | Large-scale personal data, regulatory action likely |
| 5 | Severe | `<amount>` | Prolonged loss of critical operations | Systemic breach, licence or legal jeopardy |

*Set the monetary bands with Finance so they match the organisation's actual risk appetite.*

## Rating bands

| Score | Rating | Expected response |
|---|---|---|
| 1-4 | Low | Accept and monitor |
| 5-9 | Medium | Treat within the normal plan; owner reviews quarterly |
| 10-16 | High | Treatment plan with owner and date; management reports monthly |
| 17-25 | Critical | Immediate action; executive sponsor informed |

## Treatment options

| Option | Meaning |
|---|---|
| Mitigate | Add or improve controls to reduce likelihood or impact |
| Transfer | Share the risk, e.g. insurance or contract (liability is not the same as transfer of responsibility) |
| Avoid | Stop the activity that creates the risk |
| Accept | Formal, documented decision by someone with authority, with a review date |

## Register fields

| Field | Notes |
|---|---|
| `id` | Stable ID (`R-001`); never reuse |
| `risk` | Written as *cause, event, consequence*: "Because X, Y could happen, resulting in Z" |
| `asset` | What is at risk |
| `owner` | A role accountable for the risk (not a team mailbox) |
| `likelihood`, `impact`, `inherent_score` | Before controls |
| `existing_controls` | What reduces the risk today |
| `residual_*` | After controls |
| `treatment`, `action`, `due` | The plan and its date |
| `status` | Open, In treatment, Accepted, Closed |
| `last_reviewed` | Review at least quarterly for High/Critical |

## Common mistakes

- Scoring the control, not the risk ("MFA not enabled" is a gap; the risk is account takeover and its consequence)
- Risks with no owner or no due date
- Everything scored "Medium"; calibrate against a few reference risks everyone agrees on
- Accepting risk without a named approver and a review date
- Never updating the register after incidents, audits or changes

## Mapping to frameworks

- ISO/IEC 27001:2022 clauses 6.1.2 (risk assessment) and 6.1.3 (risk treatment, Statement of Applicability)
- NIST CSF 2.0 `GV.RM` (risk management strategy) and `ID.RA` (risk assessment); see the [mapping](nist-csf2-iso27001-mapping.md)
