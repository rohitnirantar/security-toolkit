# Identity and Access Management: Best Practices

Identity is the new perimeter: most breaches involve stolen or misused credentials. Prioritise the items near the top.

## Checklist

| Priority | Practice | Why |
|---|---|---|
| 1 | **MFA everywhere**, starting with admins, remote access, email and cloud consoles | Blocks most password-only attacks |
| 1 | **Phishing-resistant MFA** (FIDO2 security keys, passkeys) for admins and high-risk users | Push/SMS/TOTP can be phished or fatigued |
| 1 | Block **legacy authentication** (basic auth, IMAP/POP/SMTP auth where not needed) | Bypasses MFA |
| 1 | Separate **admin accounts** from daily accounts; no email or browsing from admin accounts | Limits blast radius of phishing |
| 2 | **Least privilege** and role-based access; review access every 6 months (privileged: quarterly) | Stops privilege creep |
| 2 | **Just-in-time / time-bound** privileged access (PIM/PAM) | No standing god-mode accounts |
| 2 | **Joiner-mover-leaver** process tied to HR; disable accounts on exit the same day | Orphaned accounts are a classic entry point |
| 2 | Break-glass accounts: 2 cloud-only accounts, long random passwords stored offline, excluded from conditional access, alerts on any use | Avoid lockout without creating a backdoor |
| 3 | Conditional access: require compliant device, block risky sign-ins and unexpected countries | Context-aware control |
| 3 | Service accounts: unique per service, no interactive logon, rotated secrets; prefer managed identities and workload identity federation | Secrets in code are routinely leaked |
| 3 | Monitor: impossible travel, new MFA methods, new admin role assignments, OAuth consent grants | Detection of takeover and persistence |

## Passwords (when you still need them)

- Follow NIST SP 800-63B: favour **length** (minimum 8 with MFA, aim for 15+ for single-factor), check against breached/common password lists, allow paste and password managers, **do not force periodic rotation** without evidence of compromise, and do not use composition rules.
- Provide a company password manager.
- Rate-limit and alert on password spraying (many accounts, few attempts each).

## Active Directory / Entra ID basics

- Tier your admin model; domain admins never log on to workstations.
- Protect `krbtgt`, rotate after compromise, remove unneeded Kerberos delegation, disable NTLM where possible, enable LDAP signing/channel binding.
- Review service principals, app registrations and consented permissions regularly.

## Common failures

- MFA enabled but with an exclusion group that nobody reviews
- Shared admin accounts
- Long-lived API keys without owners or expiry
- Dormant accounts (no sign-in for 90 days) left enabled

## Standards

NIST CSF 2.0 `PR.AA`; ISO/IEC 27001:2022 A 5.15-5.18, 8.2, 8.5; CIS Controls v8 5 (Account Management) and 6 (Access Control Management).
