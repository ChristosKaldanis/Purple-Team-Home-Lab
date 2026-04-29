# 🔴🔵 Purple Team Home Lab
### Attack Simulation & Detection Engineering with Wazuh SIEM

![Status](https://img.shields.io/badge/Status-Active-brightgreen)
![Version](https://img.shields.io/badge/Version-1.0-blue)
![MITRE](https://img.shields.io/badge/MITRE%20ATT%26CK-10%20Techniques-red)
![Detection](https://img.shields.io/badge/Detection%20Coverage-100%25-brightgreen)

---

## 📋 Overview

A fully functional Purple Team home lab built to simulate real-world cyber attacks, practice threat detection, and develop custom SIEM detection rules using **Wazuh**.

**Key Achievement:** Improved Wazuh detection coverage from **37% → 100%** through custom rule development.

---

## 🏗️ Lab Architecture

```
┌─────────────────────────────────────────────────┐
│             HOME LAB — 192.168.106.0/24          │
│                                                   │
│  ┌─────────────┐    ┌──────────────────────────┐ │
│  │ Kali Linux  │───▶│   Metasploitable 3        │ │
│  │ (Attacker)  │    │   192.168.106.134         │ │
│  │ .128        │    │   Wazuh Agent             │ │
│  └─────────────┘    └────────────┬─────────────┘ │
│         │                        │               │
│         │           ┌────────────▼─────────────┐ │
│         └──────────▶│   Wazuh SIEM Server      │ │
│                     │   192.168.106.130         │ │
│                     │   Wazuh Manager + Dashboard │ │
│                     └─────────────────────────┘ 
```

---

## 🎯 Attack Scenarios — v1.0

| # | Exploit | CVE | Severity | CVSS | Result |
|---|---------|-----|----------|------|--------|
| 01 | ProFTPD mod_copy RCE | CVE-2015-3306 | 🔴 Critical | 10.0 | Root via chain |
| 02 | PwnKit Privilege Escalation | CVE-2021-4034 | 🔴 Critical | 7.8 | Root obtained |
| 03 | SQL Injection — Payroll App | N/A | 🟠 High | 8.8 | DB dumped |
| 04 | Drupal RCE (Drupalgeddon2) | CVE-2018-7600 | 🟠 High | 9.8 | Shell obtained |
| 05 | SSH Brute Force | N/A | 🟡 Medium | 7.5 | Credentials found |

---

## 🛡️ Detection Engineering

### Before vs After Custom Rules

| Attack | Before | After | Rule ID |
|--------|--------|-------|---------|
| Nmap Scan | ✅ Detected | ✅ Detected | 40101 |
| SSH Brute Force | ✅ Detected | ✅ Detected | 5763 |
| ProFTPD RCE | ❌ Missed | ✅ Detected | 100001 |
| PwnKit Privesc | ❌ Missed | ✅ Detected | 100002/3 |
| SQL Injection | ❌ Missed | ✅ Detected | 100004 |
| Drupal RCE | ❌ Missed | ✅ Detected | 100005 |
| New User Created | ✅ Detected | ✅ Detected | 5902 |
| SMB Enumeration | ❌ Missed | ✅ Detected | 100007 |

```
Detection Rate Before:  37% (3/8)
Detection Rate After:  100% (8/8)
```

---

## 🗂️ Repository Structure

```
purple-team-home-lab/
│
├── README.md
│
├── exploits/
│   ├── 01-proftpd/          ← CVE-2015-3306
│   ├── 02-pwnkit/           ← CVE-2021-4034
│   ├── 03-sqli/             ← Payroll App SQLi
│   ├── 04-drupal/           ← CVE-2018-7600
│   └── 05-ssh-bruteforce/   ← Hydra attack
│
├── detection/
│   ├── custom-rules/        ← Wazuh XML rules
│   └── screenshots/         ← Dashboard evidence
│
├── evidence/
│   ├── screenshots/         ← Exploit evidence
│   └── logs/               ← Captured logs
│
├── mitre/
│   └── attack_mapping.md   ← MITRE ATT&CK mapping
│
└── report/
    └── Purple_Team_Report.pdf
```

---

## 🔧 Tools Used

| Tool | Purpose |
|------|---------|
| Wazuh 4.7.5 | SIEM & Detection Engineering |
| Kali Linux 2024 | Attack Platform |
| Nmap 7.95 | Reconnaissance & CVE Scanning |
| Metasploit 6.x | Exploitation Framework |
| Hydra | Brute Force Testing |
| sqlmap | SQL Injection Automation |
| enum4linux | SMB Enumeration |

---

## 🗺️ MITRE ATT&CK Coverage

| Tactic | Technique | Tool |
|--------|-----------|------|
| Reconnaissance | T1595 Active Scanning | nmap |
| Initial Access | T1190 Exploit Public App | Metasploit |
| Execution | T1059 Unix Shell | Meterpreter |
| Persistence | T1136 Local Account | useradd |
| Privilege Escalation | T1068 Exploit for PrivEsc | PwnKit |
| Credential Access | T1110 Brute Force | Hydra |
| Discovery | T1046 Network Service Scan | nmap |
| Discovery | T1135 Network Share Discovery | enum4linux |
| Collection | T1005 Local Data | Meterpreter |

---

## 📄 Report

📥 [Full Purple Team Assessment Report](report/Purple_Team_Report.pdf)

---

## 🚀 Releases

### v1.0 — Initial Assessment (April 2026)
- 5 exploits executed
- 7 custom Wazuh rules developed
- 37% → 100% detection coverage improvement

### v2.0 — Coming Soon
- Tomcat WAR deployment
- Shellshock exploitation
- Automated attack simulation scripts
- Threat hunting exercises

---

## ⚠️ Disclaimer

*This project was conducted in an isolated lab environment for educational purposes only. All systems were owned and operated by the analyst. No unauthorized systems were accessed.*

---

## 👤 Author

**[Your Name]**  
Aspiring Cybersecurity Analyst  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](YOUR_LINKEDIN_URL)
