# Nmap and Wireshark Cheatsheet

> Scan only systems you own or have **written permission** to test. Unauthorised scanning can be illegal and may disrupt services.

## Nmap

### Host discovery
```bash
nmap -sn 192.168.1.0/24            # ping sweep (no port scan)
nmap -sn -PR 192.168.1.0/24        # ARP discovery on local network
```

### Port scanning
```bash
nmap 192.168.1.10                  # top 1000 TCP ports
nmap -p- 192.168.1.10              # all 65535 TCP ports
nmap -p 22,80,443 192.168.1.10
nmap -sU --top-ports 50 192.168.1.10   # UDP (slow)
nmap -sS 192.168.1.10              # SYN scan (needs root)
nmap -Pn 192.168.1.10              # skip host discovery (host blocks ping)
```

### Service and OS detection
```bash
nmap -sV 192.168.1.10              # service versions
nmap -sV --version-intensity 5 -O 192.168.1.10
nmap -A 192.168.1.10               # -sV -O -sC --traceroute (noisy)
```

### Scripts (NSE)
```bash
nmap -sC 192.168.1.10                          # default scripts
nmap --script vuln 192.168.1.10                # vulnerability checks (can be intrusive)
nmap --script smb-os-discovery,smb-security-mode -p 445 192.168.1.10
nmap --script ssl-enum-ciphers -p 443 example.internal
nmap --script http-title -p 80,443,8080 192.168.1.0/24
```

### Timing and output
```bash
nmap -T3 ...                       # default; -T4 faster on reliable networks; -T0/-T1 slow and stealthy
nmap -oA scan-results 192.168.1.0/24   # save normal, XML and grepable output
nmap --open 192.168.1.0/24             # only show open ports
```

### Common port reminders

| Port | Service | Note |
|---|---|---|
| 22 | SSH | Brute-force target |
| 53 | DNS | Tunnelling, zone transfer |
| 80 / 443 | HTTP(S) | Web apps |
| 88 | Kerberos | Domain controllers |
| 135, 139, 445 | RPC / NetBIOS / SMB | Lateral movement, ransomware spread |
| 389 / 636 | LDAP / LDAPS | Directory |
| 1433 / 3306 / 5432 | MSSQL / MySQL / PostgreSQL | Should rarely face the internet |
| 3389 | RDP | Heavily targeted; never expose directly |
| 5985 / 5986 | WinRM | Remote management |

## Wireshark

### Capture filters (BPF, set before capturing)
```
host 10.0.0.5
net 10.0.0.0/24
port 53
tcp port 443 and host 10.0.0.5
not arp and not broadcast
```

### Display filters (applied after capture)

| Goal | Filter |
|---|---|
| By IP | `ip.addr == 10.0.0.5` |
| Source / destination | `ip.src == 10.0.0.5`, `ip.dst == 10.0.0.5` |
| Protocol | `dns`, `http`, `tls`, `smb2`, `kerberos` |
| TCP port | `tcp.port == 443` |
| SYN packets (scans) | `tcp.flags.syn == 1 && tcp.flags.ack == 0` |
| Resets | `tcp.flags.reset == 1` |
| DNS queries for a name | `dns.qry.name contains "example"` |
| DNS errors | `dns.flags.rcode != 0` |
| HTTP requests | `http.request` |
| HTTP POSTs | `http.request.method == "POST"` |
| TLS handshakes with SNI | `tls.handshake.type == 1` (see `tls.handshake.extensions_server_name`) |
| Retransmissions | `tcp.analysis.retransmission` |
| Exclude noise | `!(arp || dns || mdns || ssdp)` |
| Combine | `ip.addr == 10.0.0.5 && tcp.port == 80` |

### Useful features
- **Follow TCP stream**: right-click a packet, then Follow, then TCP Stream.
- **Statistics, Conversations / Endpoints**: who talked to whom, how much.
- **Statistics, Protocol Hierarchy**: what protocols dominate.
- **File, Export Objects, HTTP**: extract transferred files (analyse in a sandbox).
- Add `frame.time_delta_displayed` as a column to spot beaconing (regular intervals).

### Suspicious patterns
- Regular, fixed-interval connections to the same external host (beaconing)
- DNS with very long or random-looking subdomains, or large TXT responses (tunnelling)
- Large outbound transfers to unfamiliar hosts at odd hours
- Many SYNs to many ports/hosts from one source (scanning)
- Cleartext credentials (FTP, Telnet, HTTP Basic)

Related: [Windows triage](windows-triage.md), [Linux triage](linux-triage.md).
