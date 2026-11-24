# Information Security Policy (Template)

> A short top-level policy that management signs. Detailed rules live in supporting standards and procedures. Replace `<placeholders>`, remove clauses that do not apply, and have Legal and management review it.
> Supports ISO/IEC 27001:2022 clause 5.2 and Annex A 5.1, and NIST CSF 2.0 `GV.PO`.

| Field | Value |
|---|---|
| Owner | `<role, e.g. CISO>` |
| Approved by | `<executive>` on `<date>` |
| Version | `<1.0>` |
| Review cycle | Annually, and after significant change or incident |
| Applies to | All employees, contractors and third parties with access to `<organisation>` information or systems |

## 1. Purpose

To protect the confidentiality, integrity and availability of `<organisation>` information and systems, meet legal, regulatory and contractual obligations, and support the organisation's objectives.

## 2. Principles

1. **Risk-based**: security controls are chosen from risk assessment, not habit.
2. **Least privilege**: people and systems get only the access they need, only for as long as needed.
3. **Defence in depth**: no single control is relied on alone.
4. **Secure by default**: systems are configured securely before use.
5. **Accountability**: every asset has an owner; actions are attributable to individuals.
6. **Continual improvement**: lessons from incidents, audits and exercises are acted on.

## 3. Roles

| Role | Responsibility |
|---|---|
| Executive management | Approves this policy, provides resources, accepts residual risk |
| Security lead (CISO) | Maintains the security programme, standards and risk register; reports to management |
| Asset / system owners | Classify assets, approve access, ensure controls operate |
| Line managers | Ensure staff know and follow the policy |
| All personnel | Follow policy, protect credentials, report incidents promptly |

## 4. Policy statements

### 4.1 Asset management and classification
- Assets (information, devices, applications, cloud services) are inventoried with a named owner.
- Information is classified (`Public`, `Internal`, `Confidential`, `Restricted`) and handled according to its label.

### 4.2 Access control
- Access is granted by role, approved by the owner, and reviewed at least every 6 months (quarterly for privileged access).
- Multi-factor authentication is required for remote access, administrative access and cloud services holding non-public data.
- Shared accounts are prohibited unless risk-accepted and technically attributable; access is removed on leaving or role change.

### 4.3 Cryptography and data protection
- Data is encrypted in transit and at rest in line with the cryptography standard.
- Secrets (passwords, keys, tokens) are stored in an approved secrets manager, never in source code or chat.

### 4.4 Secure operations
- Systems are patched according to the vulnerability management standard.
- Malware protection and endpoint detection are installed on supported endpoints and servers.
- Changes are approved, tested and reversible.
- Backups follow the 3-2-1 principle, with at least one immutable or offline copy, and are test-restored regularly.

### 4.5 Logging and monitoring
- Security-relevant events from identity, endpoint, network, and critical applications are logged centrally, protected from tampering and retained per the logging standard.

### 4.6 Supplier security
- Suppliers that handle `<organisation>` data or provide critical services are assessed before onboarding and periodically, with security obligations in contracts.

### 4.7 Incident management
- Suspected incidents are reported immediately to `<channel>`. The incident response plan defines roles, severity levels, and notification duties.

### 4.8 Business continuity
- Critical services have documented recovery objectives (RTO/RPO) and tested recovery plans.

### 4.9 Acceptable use and awareness
- Personnel complete security awareness training at onboarding and annually, and comply with the acceptable use standard.

### 4.10 Compliance
- Legal, regulatory and contractual requirements are identified and tracked: `<list, e.g. GDPR, PCI DSS, local law>`.

## 5. Exceptions

Exceptions need a written business justification, compensating controls, a named risk owner's approval, and an expiry date.

## 6. Enforcement

Breaches of this policy may result in disciplinary action, contract termination, or legal action, as allowed by law and agreements.

## 7. Related documents

- [Risk scoring guide](risk-scoring-guide.md)
- [Incident response plan template](../incident-response/ir-plan-template.md)
- [Vendor security assessment](vendor-security-assessment.md)

## 8. Approval

| Name | Role | Signature | Date |
|---|---|---|---|
| | | | |
