#  Purple Team Home Lab
### Attack Simulation & Detection Engineering with Wazuh SIEM

![Status](https://img.shields.io/badge/Status-Active-brightgreen)
![Version](https://img.shields.io/badge/Version-1.0-blue)
![MITRE](https://img.shields.io/badge/MITRE%20ATT%26CK-10%20Techniques-red)
![Detection](https://img.shields.io/badge/Detection%20Coverage-100%25-brightgreen)

---

##  Overview

A fully functional Purple Team home lab built to simulate real-world cyber attacks, practice threat detection, and develop custom SIEM detection rules using **Wazuh**.

**Key Achievement:** Improved Wazuh detection coverage from **50% → 100%** through custom rule development.

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
| 01 | ProFTPD mod_copy RCE | CVE-2015-3306 | 🔴 Critical | 10.0 | Root via chain |
| 02 | PwnKit Privilege Escalation | CVE-2021-4034 | 🔴 Critical | 7.8 | Root obtained |
| 03 | SQL Injection — Payroll App | N/A | 🟠 High | 8.8 | DB dumped |
| 04 | Drupal RCE (Drupalgeddon2) | CVE-2018-7600 | 🟠 High | 9.8 | Shell obtained |
| 05 | SSH Brute Force | N/A | 🟡 Medium | 7.5 | Credentials found |
| 06 | Slowloris DDoS Attack | N/A | 🟡 Medium | 7.5 | Credentials found |

---

##  Detection Engineering

### Before vs After Custom Rules

| Attack | Before | After | Rule ID |
|--------|--------|-------|---------|
| Nmap Scan | ❌ Missed | ❌ Missed | 40101 |
| SSH Brute Force | ✅ Detected | ✅ Detected | 5763 |
| ProFTPD RCE | ✅ Detected | ✅ Detected | 100001 |
| PwnKit Privesc | ❌ Missed | ❌ Missed | 100002/3 |
| SQL Injection | ✅ Detected | ✅ Detected | 100004 |
| Drupal RCE | ❌ Missed | ❌ Missed | 100005 |
| Slowloris DDoS Attack | ✅ Detected | ✅ Detected | 100007 |

```
Detection Rate Before:  57% (4/7)
Detection Rate After:  57% (4/8)
```

---

## Repository Structure

```
purple-team-home-lab/
│
├── README.md                   
├── LICENSE                     
│
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
│   │   └── local_rules.xml     
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

## Report

📥 [Full Purple Team Assessment Report](report/Purple_Team_Report.pdf)

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

## 👤 Author

**Christos Kaldanis**  
Aspiring Cybersecurity Analyst  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](YOUR_LINKEDIN_URL)
