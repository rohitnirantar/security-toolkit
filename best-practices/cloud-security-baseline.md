# Cloud Security Baseline (Azure, AWS, general)

A starter checklist for a new or inherited cloud environment. Verify service names and settings against the provider's current documentation; they change.

## 1. Identity and access

- [ ] Root/global-admin accounts: MFA (hardware key), no daily use, alerts on sign-in
- [ ] SSO with the corporate identity provider; no local users where avoidable
- [ ] Least-privilege roles; avoid broad built-in roles (Owner, AdministratorAccess) for day-to-day work
- [ ] Time-bound elevation (Entra PIM / AWS IAM Identity Center with approval)
- [ ] No long-lived access keys; use roles, managed identities and workload identity federation
- [ ] Conditional access / SCPs and Azure Policy to enforce guardrails

## 2. Account / subscription structure

- [ ] Separate production, non-production, security/logging and shared-services accounts/subscriptions
- [ ] Management groups / AWS Organizations with policy inheritance
- [ ] Block unused regions and risky services using policy

## 3. Logging and detection

- [ ] **AWS**: CloudTrail (all regions, org trail, log-file validation) to a locked-down bucket in a logging account; GuardDuty; Security Hub; Config
- [ ] **Azure**: Activity Log and Entra sign-in/audit logs to Log Analytics/Sentinel; Microsoft Defender for Cloud; diagnostic settings on key resources
- [ ] Alerts: root/global-admin use, policy changes, new access keys, disabled logging, public exposure of storage

## 4. Network

- [ ] No public management ports (SSH 22, RDP 3389, database ports) open to `0.0.0.0/0`; use Bastion/SSM Session Manager/JIT
- [ ] Private endpoints/VPC endpoints for PaaS services; default-deny security groups/NSGs
- [ ] WAF in front of public web apps; DDoS protection where warranted

## 5. Data protection

- [ ] Storage buckets/containers **private by default**; block public access at account level
- [ ] Encryption at rest with provider or customer-managed keys; TLS 1.2+ in transit
- [ ] Secrets in Key Vault / Secrets Manager, not in code, environment files or images
- [ ] Versioning, soft-delete and backup for critical data

## 6. Workloads

- [ ] Hardened images, automatic patching, EDR/CWPP on VMs
- [ ] Container image scanning and minimal base images; no privileged containers
- [ ] Infrastructure as code, scanned in CI (Checkov, tfsec/Trivy, KICS)

## 7. Governance

- [ ] Resource tagging (owner, environment, data classification)
- [ ] Cost anomaly alerts (also a security signal: crypto-mining)
- [ ] Regular posture review (CIS Benchmarks for AWS/Azure, Defender for Cloud / Security Hub scores)

## High-value quick wins

1. MFA on root/global admin, and remove standing admin access
2. Turn on organisation-wide audit logging to a protected location
3. Block public storage and close management ports
4. Enable the native threat detection service (GuardDuty / Defender for Cloud)
5. Remove or rotate old access keys

## Standards

CIS Benchmarks for AWS and Azure; NIST CSF 2.0 `PR.PS`, `PR.IR`, `DE.CM`; ISO/IEC 27017 (cloud controls); Cloud Security Alliance Cloud Controls Matrix.
