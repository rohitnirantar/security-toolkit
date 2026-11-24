# Playbook: Phishing

| Field | Value |
|---|---|
| Default severity | P3 (P2 if a credential was entered or an attachment was run; P1 if privileged account compromise or wide spread) |
| Primary ATT&CK techniques | T1566.001 Spearphishing Attachment, T1566.002 Spearphishing Link, T1204 User Execution, T1056 Input Capture, T1539 Steal Web Session Cookie |
| Last reviewed | 2026-11-23 |

## Triggers

- User reports a suspicious email (report button or mailbox)
- Email gateway or Defender-type alert for malicious URL/attachment
- Proxy/DNS hit on a known phishing domain
- Multiple users receive the same message

## 1. Triage

- [ ] Acknowledge the reporter and tell them not to interact further
- [ ] Obtain the **original message as an attachment (.eml/.msg)**, not a forward, so headers survive
- [ ] Review headers: `From`, `Return-Path`, `Reply-To`, `Received` chain, `Authentication-Results` (SPF, DKIM, DMARC)
- [ ] Identify indicators: sender address and domain, URLs, attachment hashes, subject, message-ID
- [ ] Analyse safely: detonate URLs/attachments in a sandbox; never open them on a corporate workstation. Defang indicators in notes

## 2. Scope

- [ ] Search all mailboxes for the same sender, subject, URL or attachment hash
- [ ] List recipients and who **clicked or opened** (proxy, DNS, safe-links, EDR logs)
- [ ] For each clicker: did they submit credentials or run an attachment?

## 3. Contain

- [ ] Block sender, domain, URLs and hashes at gateway, proxy and DNS
- [ ] Purge or quarantine the message from all mailboxes (soft-delete first, log what was removed)
- [ ] **Credential entered**: force password reset, revoke sessions and refresh tokens, review MFA methods registered and mailbox rules (see [compromised account playbook](playbook-compromised-account.md))
- [ ] **Attachment executed**: isolate the host with EDR and treat as malware (escalate)

## 4. Eradicate and recover

- [ ] Remove malicious inbox rules, OAuth app consents and forwarding set by the attacker
- [ ] Reimage hosts where malicious code ran
- [ ] Confirm no further sign-ins from attacker IPs or unusual locations

## 5. Communicate and improve

- [ ] Thank the reporter; give feedback on the outcome
- [ ] Send a short warning to staff if the campaign is widespread
- [ ] Add detections for the technique used (lookalike domain, QR code, HTML smuggling, OAuth consent phishing)
- [ ] Review email controls: SPF/DKIM/DMARC with enforcement, external-sender banners, attachment sandboxing, link rewriting, phishing-resistant MFA (FIDO2/passkeys)

## Quick header-analysis checklist

| Check | Suspicious sign |
|---|---|
| `From` vs `Return-Path` / `Reply-To` | Different domains |
| `Authentication-Results` | `spf=fail`, `dkim=none/fail`, `dmarc=fail` |
| Domain | Lookalike (`rn` for `m`, added hyphen, wrong TLD), newly registered |
| URL | Display text differs from href; URL shorteners; unusual redirects |
| Content | Urgency, payment or credential request, unexpected attachment (HTML, ISO, OneNote, macro-enabled Office) |

## Evidence to keep

Original `.eml`, header analysis notes, indicator list (defanged), list of recipients/clickers, actions taken with timestamps.
