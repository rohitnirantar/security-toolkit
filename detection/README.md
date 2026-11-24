# Detection Content

Original detection rules, mapped to MITRE ATT&CK.

| Rule | Format | Technique | Level |
|---|---|---|---|
| [PowerShell encoded command](sigma/proc_creation_win_powershell_encoded_command.yml) | Sigma | T1059.001, T1027 | Medium |
| [Certutil download](sigma/proc_creation_win_certutil_download.yml) | Sigma | T1105 | High |
| [Shadow copy deletion](sigma/proc_creation_win_shadow_copy_deletion.yml) | Sigma | T1490 | High |
| [Failed then successful sign-in](kql/failed-then-successful-signin.kql) | KQL | T1110, T1078 | Medium |

## Status

Rules are marked `experimental`: written from public technique descriptions and **not yet validated against production telemetry**. Treat them as starting points, test in your environment, and tune for false positives before alerting on them.

## Converting Sigma rules

Sigma rules are vendor-neutral. Convert with [`sigma-cli`](https://github.com/SigmaHQ/sigma-cli) and the backend for your SIEM, for example:

```bash
pip install sigma-cli
sigma plugin install splunk        # or microsoft365defender, elasticsearch, ...
sigma convert -t splunk -p splunk_windows detection/sigma/proc_creation_win_certutil_download.yml
```

## Conventions

- File names: `<logsource-category>_<product>_<behaviour>.yml`
- Each rule has a unique lowercase UUID `id`, ATT&CK `tags`, realistic `falsepositives`, and a `level`.
- Rule IDs must be unique.
