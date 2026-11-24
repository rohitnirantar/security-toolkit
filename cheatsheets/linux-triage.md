# Linux Triage Commands

A first-response checklist for a suspected-compromised Linux host. **Order of volatility**: capture what disappears first (memory, network connections, running processes) before disk-based artefacts. Run from trusted binaries where possible (statically-compiled tools from read-only media), as a compromised host can lie. Record the time and every command you run.

> Only run these on systems you are authorised to investigate. Prefer your EDR's collection features or a forensic image when the case may become legal.

## 0. Preserve

```bash
date -u; uname -a; hostname; uptime
whoami; id
```

## 1. Processes

```bash
ps auxwwf                       # full tree, wide output
ps -eo pid,ppid,user,lstart,cmd --sort=lstart
ls -l /proc/<pid>/exe           # real binary (look for "(deleted)")
ls -l /proc/<pid>/cwd
cat /proc/<pid>/cmdline | tr '\0' ' '
```
Red flags: processes running from `/tmp`, `/dev/shm`, `/var/tmp`; binaries marked `(deleted)`; unusual parent/child pairs; names mimicking kernel threads.

## 2. Network

```bash
ss -tulpnae                     # listening sockets and owning process
ss -tnp state established       # live connections
ip addr; ip route
cat /etc/resolv.conf; cat /etc/hosts
```
Red flags: shells or interpreters (`bash`, `python`, `nc`) with outbound sockets; listeners on unexpected ports.

## 3. Users and authentication

```bash
last -Faiw | head -50           # successful logins
lastb -Faiw | head -50          # failed logins (needs root)
who -a; w
cat /etc/passwd | awk -F: '$3==0 {print}'      # all UID 0 accounts
grep -E 'sudo|su\[' /var/log/auth.log /var/log/secure 2>/dev/null | tail -100
find / -name authorized_keys -exec ls -l {} \; 2>/dev/null
```

## 4. Persistence

```bash
crontab -l; ls -la /etc/cron* /var/spool/cron*
systemctl list-unit-files --state=enabled
systemctl list-timers --all
ls -la /etc/systemd/system /usr/lib/systemd/system | head -50
cat /etc/rc.local 2>/dev/null
ls -la ~/.bashrc ~/.profile /etc/profile.d/
cat /etc/ld.so.preload 2>/dev/null     # should normally not exist
```

## 5. Files

```bash
find / -xdev -type f -mtime -2 -not -path "/proc/*" 2>/dev/null | head -100    # modified in last 2 days
find / -xdev -perm -4000 -type f 2>/dev/null                                   # SUID binaries
find /tmp /dev/shm /var/tmp -type f -ls 2>/dev/null
sha256sum <suspicious file>
```
Check package integrity:
```bash
rpm -Va 2>/dev/null | head       # RPM-based
debsums -c 2>/dev/null | head    # Debian-based (install debsums)
```

## 6. Logs

```bash
journalctl --since "2 days ago" -p warning | less
tail -200 /var/log/auth.log      # or /var/log/secure
ls -la /var/log; last -x | head  # look for gaps or truncated logs
```
Web servers: check access/error logs for webshell requests (unusual `POST`s to upload directories, long query strings, `cmd=`).

## 7. Containment (after capturing evidence)

```bash
# Network isolation example (keep your SSH session):
iptables -I OUTPUT -j DROP ; iptables -I OUTPUT -p tcp --sport 22 -j ACCEPT
```
Prefer isolation through your EDR or network controls. Do not delete files; move suspicious ones into a quarantine directory and note the original path and hash.

## Triage mnemonic

**P**rocesses → **N**etwork → **U**sers → **P**ersistence → **F**iles → **L**ogs

Related: [Windows triage](windows-triage.md), [ransomware playbook](../templates/incident-response/playbook-ransomware.md).
