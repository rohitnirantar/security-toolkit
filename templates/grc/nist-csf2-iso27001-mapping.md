# NIST CSF 2.0 to ISO/IEC 27001:2022 Mapping (Indicative)

> **This is my own category-level mapping for study and quick orientation. It is not an official crosswalk.** Official, detailed mappings are published by NIST in the [CSF 2.0 Informative References](https://www.nist.gov/cyberframework/informative-references) and the NIST CSF 2.0 Reference Tool. Always verify against the standards before using this for an audit or certification.
>
> ISO references are to **clauses 4-10** (management system requirements) and **Annex A controls** (5.x Organizational, 6.x People, 7.x Physical, 8.x Technological) in ISO/IEC 27001:2022.

CSF 2.0 has 6 Functions and 22 Categories. Mapping is many-to-many; the lists below show the closest matches.

## GOVERN (GV)

| CSF category | Description | ISO 27001:2022 |
|---|---|---|
| GV.OC Organizational Context | Mission, stakeholders, legal and regulatory context | Clauses 4.1-4.3; A 5.31 |
| GV.RM Risk Management Strategy | Risk appetite, strategy and priorities | Clauses 6.1.1-6.1.3, 8.2, 8.3 |
| GV.RR Roles, Responsibilities and Authorities | Accountability and resourcing | Clause 5.3; A 5.2, 5.3, 5.4 |
| GV.PO Policy | Establish, communicate and enforce policy | Clause 5.2; A 5.1, 5.36 |
| GV.OV Oversight | Review strategy and performance | Clauses 9.1-9.3; A 5.35 |
| GV.SC Cybersecurity Supply Chain Risk Management | Supplier risk management | A 5.19, 5.20, 5.21, 5.22, 5.23 |

## IDENTIFY (ID)

| CSF category | Description | ISO 27001:2022 |
|---|---|---|
| ID.AM Asset Management | Inventory and classify assets | A 5.9, 5.10, 5.11, 5.12, 5.13 |
| ID.RA Risk Assessment | Understand threats, vulnerabilities and risk | Clauses 6.1.2, 8.2; A 5.7, 8.8 |
| ID.IM Improvement | Learn and improve from assessments and incidents | Clauses 10.1, 10.2; A 5.27, 5.35 |

## PROTECT (PR)

| CSF category | Description | ISO 27001:2022 |
|---|---|---|
| PR.AA Identity Management, Authentication and Access Control | Manage identities, credentials and access | A 5.15, 5.16, 5.17, 5.18, 7.2, 8.2, 8.3, 8.5 |
| PR.AT Awareness and Training | Train personnel | A 6.3; Clause 7.3 |
| PR.DS Data Security | Protect data at rest, in transit and in use | A 5.14, 7.10, 8.10, 8.11, 8.12, 8.13, 8.24 |
| PR.PS Platform Security | Secure hardware, software and services | A 8.7, 8.9, 8.19, 8.25-8.28, 8.32 |
| PR.IR Technology Infrastructure Resilience | Resilient architecture | A 5.30, 7.5, 7.11, 8.14, 8.20, 8.21, 8.22 |

## DETECT (DE)

| CSF category | Description | ISO 27001:2022 |
|---|---|---|
| DE.CM Continuous Monitoring | Monitor assets for anomalies | A 7.4, 8.15, 8.16 |
| DE.AE Adverse Event Analysis | Analyse anomalies and indicators | A 5.7, 5.25, 8.16 |

## RESPOND (RS)

| CSF category | Description | ISO 27001:2022 |
|---|---|---|
| RS.MA Incident Management | Manage and prioritise responses | A 5.24, 5.25, 5.26 |
| RS.AN Incident Analysis | Investigate and preserve evidence | A 5.27, 5.28 |
| RS.CO Incident Response Reporting and Communication | Coordinate with stakeholders | A 5.5, 5.6, 5.26, 6.8 |
| RS.MI Incident Mitigation | Contain and eradicate | A 5.26 |

## RECOVER (RC)

| CSF category | Description | ISO 27001:2022 |
|---|---|---|
| RC.RP Incident Recovery Plan Execution | Restore operations | A 5.29, 5.30, 8.13, 8.14 |
| RC.CO Incident Recovery Communication | Communicate recovery progress | A 5.5, 5.26, 6.8 |

## How to use this

- **Gap analysis**: take an existing ISO 27001 control set and see which CSF categories are thinly covered (for example, CSF 2.0 added `GV`, which is spread across clauses 4-5 and 9-10 in ISO).
- **Reporting**: express ISO control status in CSF Function terms for executives.
- **Study aid**: see how the two frameworks overlap; they differ in nature (CSF is an outcome-based framework; ISO 27001 is a certifiable management-system standard with a Statement of Applicability).

## Known limits

- Category-level only; subcategory-level mapping (for example `PR.AA-05`) needs the official references.
- Controls often map to several categories; I listed the closest, not every possible link.
- Control numbers refer to the 2022 edition (93 Annex A controls); the 2013 edition numbering differs.
