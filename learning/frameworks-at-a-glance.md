# Security Frameworks at a Glance

A quick-reference for terms and frameworks that come up constantly. Not a substitute for the standards themselves.

## Foundations

- **CIA triad**: Confidentiality (only authorised access), Integrity (data is accurate and unaltered), Availability (systems and data usable when needed).
- **Defence in depth**: layered controls so one failure does not mean compromise.
- **Least privilege / need to know**: minimum access for the shortest necessary time.
- **Zero Trust**: never trust, always verify; authenticate and authorise every request using identity, device health and context, assuming the network is hostile (NIST SP 800-207).
- **Shared responsibility** (cloud): the provider secures the cloud; you secure what you put in it. The split varies by IaaS, PaaS, SaaS.
- **AAA**: Authentication (who are you), Authorisation (what may you do), Accounting (what did you do).

## Risk vocabulary

| Term | Meaning |
|---|---|
| Asset | Anything of value (data, systems, people, reputation) |
| Threat | Something that can cause harm (ransomware gang, insider, flood) |
| Vulnerability | A weakness a threat can exploit |
| Risk | Likelihood x impact of a threat exploiting a vulnerability |
| Control | A safeguard that reduces risk: preventive, detective, corrective; administrative, technical, physical |
| Residual risk | What remains after controls |
| Risk appetite / tolerance | How much risk the organisation is willing to accept |
| SLE / ARO / ALE | Single Loss Expectancy x Annual Rate of Occurrence = Annualised Loss Expectancy |
| RTO / RPO | Recovery Time Objective (how fast) / Recovery Point Objective (how much data loss) |

See also: [risk scoring guide](../templates/grc/risk-scoring-guide.md).

## NIST Cybersecurity Framework 2.0 (2024)

Six Functions: **Govern**, **Identify**, **Protect**, **Detect**, **Respond**, **Recover**. Govern is new in 2.0 and wraps the others (strategy, policy, roles, supply chain). Also defines Implementation Tiers (1-4) and Profiles (current vs. target). Voluntary and outcome-based.

Mapping to ISO: [CSF 2.0 to ISO 27001 mapping](../templates/grc/nist-csf2-iso27001-mapping.md).

## ISO/IEC 27001:2022

A certifiable **Information Security Management System (ISMS)** standard.

- **Clauses 4-10** (mandatory): context, leadership, planning (risk assessment and treatment), support, operation, performance evaluation, improvement.
- **Annex A**: 93 controls in 4 themes: Organizational (37), People (8), Physical (14), Technological (34).
- **Statement of Applicability (SoA)**: lists which Annex A controls apply and why/why not.
- Companion standards: 27002 (control guidance), 27005 (risk), 27035 (incident management), 27017 (cloud), 27701 (privacy).

## CIS Critical Security Controls v8

18 prioritised safeguards, grouped in Implementation Groups (IG1 basic hygiene, IG2, IG3). Good practical starting list: inventory of assets, inventory of software, data protection, secure configuration, account management, access control, vulnerability management, audit logs, email and browser protections, malware defences, data recovery, network infrastructure management, network monitoring, awareness training, service provider management, application software security, incident response, penetration testing.

## MITRE ATT&CK

A knowledge base of adversary behaviour. **Enterprise** matrix tactics (the "why"), in rough attack order:

1. Reconnaissance
2. Resource Development
3. Initial Access
4. Execution
5. Persistence
6. Privilege Escalation
7. Defense Evasion
8. Credential Access
9. Discovery
10. Lateral Movement
11. Collection
12. Command and Control
13. Exfiltration
14. Impact

Techniques (`T1059`) and sub-techniques (`T1059.001`) describe the "how". Use ATT&CK to map detections, assess coverage and structure threat hunting and reporting.

## Lockheed Martin Cyber Kill Chain

Reconnaissance, Weaponisation, Delivery, Exploitation, Installation, Command and Control, Actions on Objectives. Older and linear; ATT&CK is more detailed, but the kill chain is useful for explaining attack stages.

## Incident response lifecycle

NIST SP 800-61: Preparation; Detection and Analysis; Containment, Eradication and Recovery; Post-Incident Activity. Revision 3 (2025) aligns incident response with the CSF 2.0 functions. See the [IR plan template](../templates/incident-response/ir-plan-template.md).

## Other frameworks to know

| Framework | One line |
|---|---|
| SOC 2 | Audit report on a service organisation's controls (Trust Services Criteria: security, availability, processing integrity, confidentiality, privacy) |
| PCI DSS | Card-data security standard (v4.0.1 current at time of writing; verify) |
| NIST SP 800-53 | Large catalogue of security and privacy controls (US federal) |
| NIST SP 800-171 | Protecting controlled unclassified information in non-federal systems |
| Essential Eight (ASD) | Eight prioritised mitigation strategies with maturity levels (Australia) |
| OWASP Top 10 | Most critical web application risks; ASVS for verification |
| COBIT | IT governance framework |
| FAIR | Quantitative cyber-risk model (frequency and magnitude of loss) |

## Study tip

Learn each framework by answering: **Who publishes it? Is it certifiable? What problem does it solve? What would an auditor ask for?**
