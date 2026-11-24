# KQL Cheatsheet for Security (Microsoft Sentinel / Defender)

Kusto Query Language reads top to bottom, piping each result into the next operator. Table and column names below are those of common Sentinel/Defender schemas; confirm in your workspace, since connectors vary.

## Core operators

| Operator | Purpose | Example |
|---|---|---|
| `where` | Filter rows | `where TimeGenerated > ago(24h)` |
| `project` | Choose columns | `project TimeGenerated, Account, Computer` |
| `extend` | Add a computed column | `extend Hour = hourofday(TimeGenerated)` |
| `summarize` | Aggregate | `summarize count() by Account` |
| `bin()` | Bucket values | `summarize count() by bin(TimeGenerated, 1h)` |
| `top` / `sort` | Rank | `top 10 by Count desc` |
| `distinct` | Unique values | `distinct IPAddress` |
| `join` | Combine tables | `join kind=inner (Other) on Key` |
| `union` | Stack tables | `union SigninLogs, AADNonInteractiveUserSignInLogs` |
| `parse_json()` | Read JSON strings | `extend p = parse_json(Properties)` |
| `mv-expand` | Expand arrays to rows | `mv-expand Targets` |
| `let` | Variables and sub-queries | `let lookback = 7d;` |
| `render` | Chart | `render timechart` |

String operators: `==` (exact, case-sensitive), `=~` (case-insensitive), `contains`, `has` (whole-term, faster), `startswith`, `endswith`, `in`, `!in`, `matches regex`. Prefer `has` over `contains` for performance when matching whole terms.

Always filter on **time first**, then on other columns, to keep queries fast.

## Starter queries

### Failed sign-ins by user and IP (Entra ID)
```kql
SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType != "0"
| summarize Failures = count(), Apps = make_set(AppDisplayName) by UserPrincipalName, IPAddress
| where Failures > 10
| sort by Failures desc
```

### Sign-ins from outside expected countries
```kql
SigninLogs
| where TimeGenerated > ago(7d) and ResultType == "0"
| extend Country = tostring(LocationDetails.countryOrRegion)
| where Country !in ("AU", "NZ")   // replace with your expected countries
| summarize Logons = count() by UserPrincipalName, Country
| sort by Logons desc
```

### Windows failed logons (Event 4625) by source
```kql
SecurityEvent
| where TimeGenerated > ago(1h) and EventID == 4625
| summarize Attempts = count(), Targets = dcount(TargetUserName) by IpAddress
| where Attempts > 20
| sort by Attempts desc
```
A high `Targets` value with few attempts per account suggests password spraying.

### Process creation with encoded PowerShell (Defender for Endpoint)
```kql
DeviceProcessEvents
| where Timestamp > ago(24h)
| where FileName in~ ("powershell.exe", "pwsh.exe")
| where ProcessCommandLine has_any ("-enc", "-EncodedCommand", "-ec")
| project Timestamp, DeviceName, AccountName, ProcessCommandLine, InitiatingProcessFileName
```

### New inbox forwarding or delete rules (Office 365)
```kql
OfficeActivity
| where TimeGenerated > ago(7d)
| where Operation in ("New-InboxRule", "Set-InboxRule", "UpdateInboxRules")
| project TimeGenerated, UserId, ClientIP, Operation, Parameters
```

### Administrative role assignments in Entra ID
```kql
AuditLogs
| where TimeGenerated > ago(7d)
| where OperationName has "Add member to role"
| extend Actor = tostring(InitiatedBy.user.userPrincipalName)
| project TimeGenerated, OperationName, Actor, TargetResources
```

### Security events cleared (Event 1102 / 104)
```kql
Event
| where TimeGenerated > ago(7d)
| where EventID in (1102, 104)
| project TimeGenerated, Computer, EventID, RenderedDescription
```

### Activity trend by hour
```kql
SigninLogs
| where TimeGenerated > ago(3d)
| summarize Count = count() by bin(TimeGenerated, 1h)
| render timechart
```

## Tips

- Use `take 10` to preview a table before writing a long query.
- Save useful queries as **analytics rules** (scheduled) with MITRE tactics/techniques mapped, and as **hunting queries**.
- `ago(1d)`, `datetime(2026-01-01)`, `now()`, `between (a .. b)` handle time ranges.
- Use `//` for comments.
- Learn the schema with `TableName | getschema`.

More: [detection/kql](../detection/kql/failed-then-successful-signin.kql).
