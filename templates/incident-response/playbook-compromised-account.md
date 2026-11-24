# Playbook: Compromised Account

| Field | Value |
|---|---|
| Default severity | P2 (P1 if the account is privileged, a service account with broad access, or data exfiltration is confirmed) |
| Primary ATT&CK techniques | T1078 Valid Accounts, T1110 Brute Force, T1539 Steal Web Session Cookie, T1098 Account Manipulation, T1114.003 Email Forwarding Rule, T1136 Create Account |
| Last reviewed | 2026-11-23 |

## Triggers

- Impossible-travel or anomalous sign-in alert; sign-in from anonymising infrastructure
- Many failed sign-ins followed by a success
- MFA fatigue (burst of push prompts) or MFA method added unexpectedly
- User reports activity they did not perform; unfamiliar inbox rules or sent mail
- Credentials found in a breach dump or paste

## 1. Triage

- [ ] Identify the account type (user, admin, service, guest) and what it can reach
- [ ] Pull sign-in logs for the last 7-30 days: IPs, locations, user agents, applications, MFA results, failures
- [ ] Decide: true positive, benign (user travelling, VPN), or unknown. Contact the user **through a known-good channel**, not by replying to a message from the account

## 2. Contain

- [ ] Reset the password and **revoke all active sessions and refresh tokens**
- [ ] Review and remove attacker-registered MFA methods and devices; re-enrol the user in person or via verified process
- [ ] Block the attacker IPs/ASNs; add a conditional-access block if warranted
- [ ] For service accounts and API keys: rotate the secret and review where it is stored and used
- [ ] If privileged: treat as P1, check for new admins, role assignments, changed policies and created credentials

## 3. Investigate

- [ ] What did the attacker access? Mailbox, files, SaaS apps, cloud resources (audit logs)
- [ ] Look for persistence:
  - Inbox rules (forwarding, auto-delete, move-to-folder) and mailbox delegation
  - OAuth app consents / enterprise applications
  - New MFA methods, app passwords, API tokens, SSH keys
  - New accounts or role assignments
- [ ] Look for lateral movement from the account (email sent to internal users, shared links, Teams/Slack messages)
- [ ] Establish the initial cause: phishing, password reuse, password spray, token theft, malware (infostealer), insider

## 4. Recover and harden

- [ ] Remove persistence found; confirm no further activity for at least 7 days
- [ ] If infostealer malware is suspected, reimage the device before the user signs in again
- [ ] Enforce phishing-resistant MFA for privileged users; block legacy authentication; require compliant devices
- [ ] Reduce standing privilege (just-in-time access)
- [ ] Notify affected parties if their data or messages were accessed

## Useful questions for the user

1. When did you last sign in normally, and from where?
2. Did you receive MFA prompts you did not initiate, or approve one by accident?
3. Did you click a link or enter your password on a page after receiving an email or message?
4. Do you reuse this password anywhere else?
5. Have you installed any new software or browser extensions recently?

## Detection ideas

See [detection/kql/failed-then-successful-signin.kql](../../detection/kql/failed-then-successful-signin.kql) for a starting query.
