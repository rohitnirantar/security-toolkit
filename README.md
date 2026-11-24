# Security Toolkit

Practical, original security templates, best practices, cheatsheets and detection rules, written to be copied, adapted and used. Grows a little every day.

**Focus areas:** incident response, governance/risk/compliance (GRC), detection engineering, and day-to-day security operations.

> Content is educational and starter-level. Review and adapt everything to your own environment, legal obligations and risk appetite before relying on it. Rules and queries are marked `experimental` until validated against real telemetry.

## Contents

### Templates: incident response

| File | Use it for |
|---|---|
| [IR plan template](templates/incident-response/ir-plan-template.md) | Roles, severity matrix, communications, evidence handling |
| [Post-incident report](templates/incident-response/incident-report-template.md) | Blameless review: timeline, root cause, actions, metrics |
| [Ransomware playbook](templates/incident-response/playbook-ransomware.md) | Triage, containment, recovery, decision points |
| [Phishing playbook](templates/incident-response/playbook-phishing.md) | Header analysis, scoping, purge, hardening |
| [Compromised account playbook](templates/incident-response/playbook-compromised-account.md) | Session revocation, persistence hunting, hardening |

### Templates: GRC

| File | Use it for |
|---|---|
| [Risk scoring guide](templates/grc/risk-scoring-guide.md) | A simple 5x5 likelihood x impact method |
| [Risk register](templates/grc/risk-register.csv) | Worked example register with inherent and residual scores |
| [Information security policy](templates/grc/information-security-policy.md) | Top-level policy aligned to ISO 27001 and NIST CSF |
| [Vendor security assessment](templates/grc/vendor-security-assessment.md) | Tiering and a right-sized supplier questionnaire |
| [NIST CSF 2.0 to ISO 27001 mapping](templates/grc/nist-csf2-iso27001-mapping.md) | Indicative category-level crosswalk |

### Best practices

| File | Topic |
|---|---|
| [Identity and access](best-practices/identity-and-access.md) | MFA, privileged access, joiner-mover-leaver |
| [Logging and monitoring](best-practices/logging-and-monitoring.md) | What to log, retention, detection engineering loop |
| [Vulnerability management](best-practices/vulnerability-management.md) | Prioritisation (KEV, EPSS), SLAs, metrics |
| [Backup and recovery](best-practices/backup-and-recovery.md) | 3-2-1-1-0, immutability, restore testing |
| [Cloud security baseline](best-practices/cloud-security-baseline.md) | Azure and AWS starter checklist |

### Cheatsheets

| File | Topic |
|---|---|
| [KQL for security](cheatsheets/kql-sentinel.md) | Sentinel and Defender queries |
| [Linux triage](cheatsheets/linux-triage.md) | First-response commands |
| [Windows triage](cheatsheets/windows-triage.md) | First-response PowerShell and event IDs |
| [Nmap and Wireshark](cheatsheets/nmap-wireshark.md) | Scanning and packet-analysis filters |

### Detection content

| File | Technique |
|---|---|
| [Detection overview](detection/README.md) | How the rules are organised and converted |
| [PowerShell encoded command](detection/sigma/proc_creation_win_powershell_encoded_command.yml) | T1059.001, T1027 |
| [Certutil download](detection/sigma/proc_creation_win_certutil_download.yml) | T1105 |
| [Shadow copy deletion](detection/sigma/proc_creation_win_shadow_copy_deletion.yml) | T1490 |
| [Failed then successful sign-in (KQL)](detection/kql/failed-then-successful-signin.kql) | T1110, T1078 |

### Learning

| File | Contents |
|---|---|
| [Learning overview](learning/README.md) | Approach and primary sources |
| [Frameworks at a glance](learning/frameworks-at-a-glance.md) | CIA, NIST CSF 2.0, ISO 27001, CIS, ATT&CK |
| [Learning log](learning/log.md) | Dated daily notes and topic backlog |


## Related projects

- [soc-triage-agent](https://github.com/rohitnirantar/soc-triage-agent): agentic SOC alert triage with MITRE ATT&CK mapping and explainable scoring.

## Conventions and licence

See [CONTRIBUTING.md](CONTRIBUTING.md) for how content is added. Released under the [MIT licence](LICENSE). Framework names (NIST, ISO, MITRE ATT&CK, CIS) belong to their owners; this repo links to them and does not reproduce their documents.
