# MITRE ATT&CK Mapping

> Complete mapping of all Purple Team lab attack scenarios to MITRE ATT&CK framework.

---

## Attack Chain Visualization

```
[Initial Recon]          [Initial Access]        [Privilege Escalation]
T1595 Active Scan  ───▶  T1190 ProFTPD RCE  ───▶  T1068 PwnKit
T1590 Service Disc        T1190 Drupal RCE          
                          T1190 SQLi                
                          T1110 SSH Brute           
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
| Reconnaissance | T1595.002 | Active Scanning: Vulnerability Scanning | - | nmap --script vulners | All targets | ✅ Rule 40101 |
| Reconnaissance | T1590.005 | Gather Victim Network Info: IP Addresses | - | nmap -sV | All targets | ✅ Rule 40101 |
| Initial Access | T1190 | Exploit Public-Facing Application | - | Metasploit proftpd_modcopy | F01 ProFTPD | ✅ Rule 100001 |
| Initial Access | T1190 | Exploit Public-Facing Application | - | Metasploit drupalgeddon2 | F04 Drupal | ✅ Rule 100005 |
| Initial Access | T1190 | Exploit Public-Facing Application | - | sqlmap | F03 SQLi | ✅ Rule 100004 |
| Initial Access | T1110.001 | Brute Force: Password Guessing | - | Hydra | F05 SSH | ✅ Rule 5763 |
| Execution | T1059.004 | Command & Scripting: Unix Shell | - | Meterpreter | Post-exploit | ✅ Partial |
| Persistence | T1136.001 | Create Account: Local Account | - | useradd | Post-exploit | ✅ Rule 100006 |
| Privilege Escalation | T1068 | Exploitation for Privilege Escalation | - | PwnKit exploit | F02 PwnKit | ✅ Rule 100002/3 |
| Discovery | T1046 | Network Service Scanning | - | nmap | Recon phase | ✅ Rule 40101 |
| Discovery | T1135 | Network Share Discovery | - | enum4linux | F06 SMB | ✅ Rule 100007 |
| Discovery | T1082 | System Information Discovery | - | uname -a, sysinfo | Post-exploit | ⚠️ Partial |
| Collection | T1005 | Data from Local System | - | cat /etc/shadow | Post-exploit | ⚠️ Partial |
| Defense Evasion | T1562.001 | Disable Security Tools | - | Disable Defender | Windows VM | ⚠️ Partial |

---

## Coverage Summary

```
Total MITRE Techniques Used:  14
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
