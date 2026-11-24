# Windows Triage Commands

First-response checks for a suspected-compromised Windows host. Run in an elevated PowerShell where noted. Capture volatile data first and keep a log of what you ran. Prefer EDR live-response where available.

> Only investigate systems you are authorised to examine.

## 1. Baseline

```powershell
Get-Date -Format o; hostname; whoami /all
Get-ComputerInfo | Select-Object OsName, OsVersion, CsDomain, OsLastBootUpTime
```

## 2. Processes

```powershell
Get-CimInstance Win32_Process |
  Select-Object ProcessId, ParentProcessId, Name, ExecutablePath, CommandLine |
  Sort-Object ParentProcessId | Format-Table -AutoSize

Get-Process | Sort-Object CPU -Descending | Select-Object -First 15 Name, Id, CPU, Path
```
Red flags: Office apps spawning `powershell`/`cmd`; scripts or binaries run from `%TEMP%`, `%APPDATA%`, `C:\Users\Public`; unsigned binaries with system-sounding names; `rundll32`/`regsvr32`/`mshta` with remote URLs.

## 3. Network

```powershell
Get-NetTCPConnection -State Established |
  Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort,
    @{n='Process';e={(Get-Process -Id $_.OwningProcess).ProcessName}}, OwningProcess

Get-NetTCPConnection -State Listen | Select-Object LocalAddress, LocalPort, OwningProcess
Get-DnsClientCache | Select-Object -First 50 Entry, Data
```

## 4. Accounts and logons

```powershell
Get-LocalUser | Select-Object Name, Enabled, LastLogon, PasswordLastSet
Get-LocalGroupMember Administrators
net session                      # inbound SMB sessions
query user                       # logged-on users

# Recent logons (4624) and failures (4625)
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4624,4625; StartTime=(Get-Date).AddDays(-2)} -MaxEvents 200 |
  Select-Object TimeCreated, Id, Message
```
Logon types: 2 interactive, 3 network, 4 batch, 5 service, 7 unlock, 10 RemoteInteractive (RDP), 11 cached.

## 5. Persistence

```powershell
Get-ScheduledTask | Where-Object State -ne 'Disabled' |
  Select-Object TaskPath, TaskName, @{n='Action';e={$_.Actions.Execute + ' ' + $_.Actions.Arguments}}

Get-CimInstance Win32_Service | Where-Object StartMode -eq 'Auto' |
  Select-Object Name, State, PathName, StartName

Get-ItemProperty 'HKLM:\Software\Microsoft\Windows\CurrentVersion\Run','HKCU:\Software\Microsoft\Windows\CurrentVersion\Run'
Get-ChildItem "$env:APPDATA\Microsoft\Windows\Start Menu\Programs\Startup"
Get-CimInstance -Namespace root\subscription -ClassName __EventConsumer     # WMI persistence
```
Sysinternals **Autoruns** gives a fuller view (`autorunsc -a * -s -h -c`).

## 6. Event logs worth checking

| Log / Event ID | Meaning |
|---|---|
| Security 4624 / 4625 | Logon success / failure |
| Security 4672 | Special privileges assigned (admin logon) |
| Security 4688 | Process created (needs command-line auditing) |
| Security 4698 / 4702 | Scheduled task created / updated |
| Security 4720 / 4732 | User created / added to local group |
| Security 1102 | Audit log cleared |
| System 7045 | New service installed |
| PowerShell/Operational 4104 | Script block logging |
| Sysmon 1, 3, 11, 13 | Process, network, file create, registry (if Sysmon is deployed) |

```powershell
Get-WinEvent -FilterHashtable @{LogName='System'; Id=7045; StartTime=(Get-Date).AddDays(-7)} |
  Select-Object TimeCreated, Message
Get-WinEvent -FilterHashtable @{LogName='Microsoft-Windows-PowerShell/Operational'; Id=4104; StartTime=(Get-Date).AddDays(-2)} -MaxEvents 50 |
  Select-Object TimeCreated, Message
```

## 7. Files

```powershell
Get-ChildItem C:\Users -Recurse -Include *.exe,*.dll,*.ps1,*.bat,*.vbs -ErrorAction SilentlyContinue |
  Where-Object LastWriteTime -gt (Get-Date).AddDays(-3) |
  Select-Object FullName, LastWriteTime, Length

Get-FileHash <path> -Algorithm SHA256
Get-AuthenticodeSignature <path>
```

## 8. Contain

- Isolate via EDR network containment. Locally: `Disable-NetAdapter -Name "Ethernet" -Confirm:$false` (this cuts your remote session too).
- Do not reboot until volatile evidence (memory, network state) is captured.

## Triage mnemonic

**P**rocesses → **N**etwork → **A**ccounts → **P**ersistence → **L**ogs → **F**iles

Related: [Linux triage](linux-triage.md), [KQL cheatsheet](kql-sentinel.md).
