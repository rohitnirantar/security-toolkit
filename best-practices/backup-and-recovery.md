# Backup and Recovery: Best Practices

Backups are the control that decides whether ransomware is a bad day or a business-ending event.

## The 3-2-1-1-0 rule

- **3** copies of data
- **2** different media/storage types
- **1** copy offsite
- **1** copy offline or **immutable** (cannot be altered or deleted, even by an admin account)
- **0** errors after **verified restore tests**

## Practices

| Practice | Detail |
|---|---|
| Define **RTO and RPO** per system | Agreed with the business; they drive backup frequency and recovery architecture |
| Separate credentials and admin plane | Backup infrastructure must not be controlled by the production domain admin accounts; enforce MFA on the backup console |
| Immutability | Object lock/WORM, hardened Linux repository, or offline tape; set retention long enough to cover dwell time (30 days minimum is common; longer for critical systems) |
| Encrypt backups | Protect keys separately from the data they protect |
| Back up **identity** and **configuration** | AD/Entra configuration, network device configs, infrastructure as code, SaaS data (Microsoft 365, Google Workspace, Salesforce) |
| **Test restores** | At least quarterly for critical systems, with an annual full recovery exercise; record actual time vs RTO |
| Monitor backup jobs | Alert on failures, abnormal change rates (possible encryption), deletion of restore points |
| Document recovery order | Identity and DNS first, then core services, then applications |
| Protect the runbook | Store recovery documentation and credentials outside the environment being recovered |

## Cloud notes

- Cloud providers back up the platform, not your data; use shared-responsibility thinking.
- Enable soft-delete, versioning and object lock on storage, with deletion protection, and restrict who can disable them.
- Use a separate account/subscription (with limited access) for backup copies.

## Recovery test record

| Date | System | Backup used | RTO target | Actual | Data verified | Issues / actions |
|---|---|---|---|---|---|---|
| | | | | | | |

## Common failures

- Backups exist but have never been restored
- Backup server joined to the production domain with the same admin credentials
- Retention shorter than attacker dwell time, so every restore point is infected
- SaaS data assumed to be backed up by the vendor

## Standards

NIST CSF 2.0 `PR.DS`, `PR.IR`, `RC.RP`; ISO/IEC 27001:2022 A 8.13, 8.14, 5.29, 5.30; CIS Controls v8 11 (Data Recovery).

Related: [Ransomware playbook](../templates/incident-response/playbook-ransomware.md).
