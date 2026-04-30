#  Purple Team Home Lab
### Attack Simulation & Detection Engineering with Wazuh SIEM

![Status](https://img.shields.io/badge/Status-Active-brightgreen)
![Version](https://img.shields.io/badge/Version-1.0-blue)
![MITRE](https://img.shields.io/badge/MITRE%20ATT%26CK-10%20Techniques-red)


---

##  Overview

This project focuses on enhancing Wazuh's threat detection capabilities by developing custom detection rules for real-world attacks and known vulnerabilities. The main objective was to create high-quality, custom Wazuh rules capable of detecting critical exploits such as ProFTPD mod_copy Remote Code Execution (CVE-2015-3306), Drupalgeddon (CVE-2018-7600), SQL Injection attempts, and Command Injection techniques. These rules were designed with high severity levels, proper MITRE ATT&CK mappings, and optimized regular expressions to improve detection accuracy while reducing false positives.



---

##  Lab Architecture

```
┌──────────────────────────────────────────────────────┐
│             HOME LAB — 192.168.106.0/24              │
│                                                      │
│  ┌─────────────┐    ┌──────────────────────────┐     │
│  │ Kali Linux  │───▶│   Metasploitable 3             │
│  │ (Attacker)  │    │   192.168.106.134              │
│  │ .128        │    │   Wazuh Agent                  │
│  └─────────────┘    └────────────┬─────────────┘     │
│         │                        │                   │
│         │           ┌────────────▼────────────────┐  │
│         └──────────▶│   Wazuh SIEM Server           │
│                     │   192.168.106.130              │
│                     │   Wazuh Manager + Dashboard    │
│                     └─────────────────────────────┘  |
```

---

##  Attack Scenarios — v1.0

| # | Exploit | CVE | Severity | CVSS | Result |
|---|---------|-----|----------|------|--------|
| 01 | ProFTPD mod_copy RCE | CVE-2015-3306 |  Critical | 10.0 | Root via chain |
| 02 | PwnKit Privilege Escalation | CVE-2021-4034 |  Critical | 7.8 | Root obtained |
| 03 | SQL Injection — Payroll App | N/A |  High | 8.8 | DB dumped |
| 04 | Drupal RCE (Drupalgeddon) | CVE-2018-7600 |  High | 9.8 | Shell obtained |
| 05 | SSH Brute Force | N/A |  Medium | 7.5 | Credentials found |
| 06 | Slowloris DDoS Attack | CVE-2007-6750 |  Medium | 7.5 | Credentials found |

---

##  Detection Engineering

### Before vs After Custom Rules

| Attack | Before | After | Rule ID |
|--------|--------|-------|---------|
| Nmap Scan | Partial | Partial | 40101 |
| SSH Brute Force |  Detected |  Detected | 5763 |
| ProFTPD RCE |  Detected |  Detected | 11201 |
| PwnKit Privesc |  Missed |  Missed | 31106/31171 |
| SQL Injection |  Detected |  Detected | 100004 |
| Drupal RCE |  Missed |  Missed | 100005 |
| Slowloris DDoS Attack |  Detected |  Detected | 31101/31151 |

```

DETECTION LIMITATION:

Target: Metasploitable 3 (Ubuntu 14.04, kernel 3.13)
Issue:  Legacy OS incompatible with Wazuh 4.x agent
        and modern IDS tooling (Suricata)

Result: Network-level attack payloads (FTP commands,
        HTTP parameters) not captured in system logs
        
COMPENSATING CONTROLS IMPLEMENTED:
- Session-level detection via syslog (SSH, FTP sessions)
- Wazuh built-in rules detect brute force patterns
- Manual log analysis confirms attack execution

RECOMMENDATION:
Upgrade target systems to supported OS versions to
enable full EDR/SIEM coverage

```

---

## Repository Structure

```
purple-team-home-lab/
│
├── README.md                   
├── LICENSE
|                  
├── setup-wazuh/
|    └── README.md
|
├── exploits/
│   ├── 01-proftpd/
│   │   └── README.md
│   ├── 02-pwnkit/
│   │   └── README.md
│   ├── 03-sqli/
│   │   └── README.md
│   ├── 04-drupal/
│   │   └── README.md
│   ├── 05-ssh-bruteforce/
│   │   └── README.md
│   └── 06-slowloris/
│       └── README.md
│
├── detections/
│   ├── custom-rules/
│   │   └── custom_rules.xml     
│
├── evidence/
│   └── (exploit proof screenshots)
│
├── mitre/
│   └── attack_mapping.md
```

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Wazuh 4.7.5 | SIEM & Detection Engineering |
| Kali Linux 2025.4 | Attack Platform |
| Nmap 7.95 | Reconnaissance & CVE Scanning |
| Metasploit 6.4.99-dev | Exploitation Framework |
| Hydra | Brute Force Testing |
| sqlmap | SQL Injection Automation |


---

## MITRE ATT&CK Coverage

| Tactic | Technique | Tool |
|--------|-----------|------|
| Reconnaissance | T1595 Active Scanning | nmap |
| Initial Access | T1190 Exploit Public App | Metasploit |
| Execution | T1059 Unix Shell | Meterpreter |
| Privilege Escalation | T1068 Exploit for PrivEsc | PwnKit |
| Credential Access | T1110 Brute Force | Hydra |
| Discovery | T1046 Network Service Scan | nmap |
| Collection | T1005 Local Data | Meterpreter |





---

## Releases

### v1.0 — Initial Assessment (April 2026)
- 6 exploits executed
- 7 custom Wazuh rules developed

### v2.0 — Coming Soon


---

## Disclaimer

*This project was conducted in an isolated lab environment for educational purposes only. All systems were owned and operated by the analyst. No unauthorized systems were accessed.*

---

## Author

**Christos Kaldanis**  
Aspiring Cybersecurity Analyst  

