# Vendor Security Assessment (Template)

> A right-sized questionnaire plus a tiering method. Do not send every vendor the same 300-question spreadsheet; match depth to risk.

## Step 1: Tier the vendor

Score each question Yes = 1 point. Add up.

| # | Question | Points |
|---|---|---|
| 1 | Will the vendor store or process **personal, confidential or regulated** data? | |
| 2 | Will the vendor have **network, admin or API access** to our systems? | |
| 3 | Would an outage of this vendor **stop a critical business process**? | |
| 4 | Is the data volume large (e.g. more than 10,000 records)? | |
| 5 | Is the vendor hard to replace within 30 days? | |

| Total | Tier | Assessment depth |
|---|---|---|
| 0-1 | Tier 3 (Low) | Security page review, contract clauses |
| 2-3 | Tier 2 (Medium) | Short questionnaire (Step 2) plus evidence |
| 4-5 | Tier 1 (High) | Full questionnaire, certification/audit report review, follow-up call, annual reassessment |

## Step 2: Questionnaire (Tier 1 and 2)

Request evidence, not just answers ("Yes" with no document earns no credit).

### Governance
1. Do you hold ISO/IEC 27001 certification or a SOC 2 Type II report? (Provide the certificate/report; check scope, date and exceptions.)
2. Is there a named security owner and a documented security policy approved by management?
3. Are staff screened and trained on security at least annually?

### Access control
4. Is MFA required for all administrative and remote access, and for customer-tenant access by your staff?
5. Is access role-based, reviewed periodically, and removed on departure?
6. How is access to our data by your support staff controlled and logged?

### Data protection
7. Is our data encrypted in transit (TLS 1.2+) and at rest? Who controls the keys?
8. Where is our data stored and processed (countries, sub-processors)?
9. How is data segregated from other customers?
10. What are the retention and deletion terms at contract end? Is deletion certified?

### Secure development and operations
11. Do you follow a secure SDLC (code review, SAST/DAST, dependency scanning)?
12. How often do you perform independent penetration tests? Can you share an executive summary?
13. What is your vulnerability patching SLA for critical issues?
14. Is production logging enabled and are logs protected and monitored?

### Resilience
15. What are your RTO and RPO? When did you last test restore?
16. Do you have a business continuity and disaster recovery plan?

### Incident management
17. Do you have a documented incident response plan, tested in the last 12 months?
18. How quickly will you notify us of an incident affecting our data? (Contract should state hours, not "promptly".)
19. Have you had a security incident in the last 24 months? Summarise and lessons learned.

### Subcontractors
20. Which sub-processors handle our data, and how do you assess them?

## Step 3: Score and decide

| Result | Meaning | Action |
|---|---|---|
| **Pass** | Controls adequate for tier; evidence provided | Approve; set reassessment date |
| **Conditional** | Gaps with credible remediation plan | Approve with tracked actions and deadlines; add to risk register |
| **Fail** | Material gaps or no evidence | Do not onboard, or require remediation first; escalate for risk acceptance |

## Step 4: Contract clauses to request

- Right to audit or receive audit reports
- Breach notification within a defined time (e.g. 24-72 hours)
- Data processing terms, sub-processor approval, data return and deletion at exit
- Security requirements matching your policy; liability and insurance
- Business continuity and exit assistance

## Assessment record

| Field | Value |
|---|---|
| Vendor | |
| Service | |
| Business owner | |
| Tier | |
| Assessed by / date | |
| Result | Pass / Conditional / Fail |
| Open actions | |
| Next review | |

Related: [Risk scoring guide](risk-scoring-guide.md), [NIST CSF 2.0 to ISO 27001 mapping](nist-csf2-iso27001-mapping.md) (supply chain: `GV.SC` and Annex A 5.19-5.23).
