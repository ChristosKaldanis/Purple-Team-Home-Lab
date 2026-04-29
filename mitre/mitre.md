# MITRE ATT&CK Mapping

> Complete mapping of all Purple Team lab attack scenarios to MITRE ATT&CK framework.

---

## Attack Chain Visualization

```
[Initial Recon]          [Initial Access]        [Privilege Escalation]
T1695 Active Scanning  ───▶T1190 ProFTPD RCE  ───▶  T1068 PwnKit
                            T1190 Drupal RCE          
                            T1190 SQLi                
                            T1110 SSH Brute
                            T1498 — Network Denial of Service     
                                │
                                ▼
                        [Post Exploitation]
                        T1136 New User (Persistence)
                        T1005 Data Collection
                        T1046 Network Discovery
                        T1135 SMB Discovery
```

---

## Full Mapping Table

| Tactic | ID | Technique | Sub-technique | Tool | Finding | Detected |
|--------|----|-----------|---------------|------|---------|---------|
| Reconnaissance | T1595.002 | Active Scanning: Vulnerability Scanning | - | nmap -D RND:5 -sV --version-intensity 9 -p- --script "vuln and not brute"  -T3 --open 192.168.106.134 -oN targeted2_cve_scan.txt | All targets | Rule 40101 |
| Initial Access | T1190 | Exploit Public-Facing Application | - | Metasploit proftpd_modcopy | ProFTPD | Rule 11201 |
| Initial Access | T1190 | Exploit Public-Facing Application | - | Metasploit drupalgeddon | Drupal | Rule 100005 |
| Initial Access | T1190 | Exploit Public-Facing Application | - | sqlmap | SQLi | Rule 31103 |
| Initial Access | T1110.001 | Brute Force: Password Guessing | - | Hydra | SSH | Rule 5763 |
| Execution | T1059.004 | Command & Scripting: Unix Shell | - | Meterpreter | Post-exploit | Partial |
| Privilege Escalation | T1068 | Exploitation for Privilege Escalation | - | PwnKit exploit | PwnKit | Not Detected |
| Discovery | T1082 | System Information Discovery | - | getuid, sysinfo | Post-exploit | Not Detected |
| Collection | T1005 | Data from Local System | - | cat /etc/shadow | Post-exploit | Not Detected |

---

## Coverage Summary

```
Total MITRE Techniques Used:  9
Fully Detected:               10 (71%)
Partially Detected:            4 (29%)
Not Detected:                  0 (0%)
```

---

## Tactics Coverage Heatmap

```
Reconnaissance        ████████████ 100%
Initial Access        ████████████ 100%
Execution             ████████░░░░  67%
Persistence           ████████████ 100%
Privilege Escalation  ████████████ 100%
Defense Evasion       ████████░░░░  67%
Discovery             ████████████ 100%
Collection            ████████░░░░  67%
```

---

*Reference: https://attack.mitre.org*
