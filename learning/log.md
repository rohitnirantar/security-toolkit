# Learning Log

A running, dated log of things I learn. Newest first. Keep entries short: what I learned, why it matters, a source. Longer notes graduate into their own file under the right folder and get linked here.

## How to add an entry

```markdown
### YYYY-MM-DD: Short title
- **Learned**: ...
- **Why it matters**: ...
- **Source / try it**: ...
```

---

### 2026-11-23: Why this repo exists
- **Learned**: Collecting other people's PDFs shows what I have read, not what I can do. Writing templates, rules and checklists from understanding shows the second.
- **Why it matters**: Each file here is something I can use at work or in an interview, and each can be improved over time.
- **Source / try it**: Start with the [incident response plan template](../templates/incident-response/ir-plan-template.md) and the [Sigma rules](../detection/README.md).

### 2026-11-23: Risk is a sentence, not a label
- **Learned**: Write a risk as "Because X, Y could happen, resulting in Z". "No MFA" is a control gap; the risk is account takeover and what follows.
- **Why it matters**: Cause, event and consequence make it clear who owns it, what the controls should be and how to score impact.
- **Source / try it**: [Risk scoring guide](../templates/grc/risk-scoring-guide.md)

### 2026-11-23: Detection engineering loop
- **Learned**: Technique, then required log source, then rule, then test, then tune. A rule that was never tested against real telemetry is a hypothesis.
- **Why it matters**: Sets the discipline for the [detection folder](../detection/README.md); rules stay `experimental` until validated.
- **Source / try it**: Atomic Red Team tests for the matching ATT&CK technique.

## Backlog (topics to cover next)

- [ ] Sigma rules for Linux (auditd) and cloud (CloudTrail, Entra audit logs)
- [ ] Splunk SPL cheatsheet
- [ ] STRIDE threat model worked example
- [ ] Secure coding checklist (OWASP ASVS highlights)
- [ ] Data classification and handling standard
- [ ] Business continuity plan and BIA template
- [ ] Tabletop exercise scenarios (ransomware, insider, cloud key leak)
- [ ] SOC shift handover template and alert-triage runbooks (link with [soc-triage-agent](https://github.com/rohitnirantar/soc-triage-agent))
