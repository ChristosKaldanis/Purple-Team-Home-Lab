# 🛡️ Cyber Defense Home Lab — Wazuh SIEM + Vulnerability Assessment

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![SIEM](https://img.shields.io/badge/SIEM-Wazuh_4.x-blue)
![Framework](https://img.shields.io/badge/Framework-MITRE_ATT%26CK-red)
![Target](https://img.shields.io/badge/Target-Metasploitable3-orange)
![Platform](https://img.shields.io/badge/Platform-VMware®Workstation17Pro-lightgrey)

---

## 📋 Project Overview

This project documents the design, deployment, and operation of a **cyber defense home lab** built around the **Wazuh open-source SIEM platform**. The lab simulates a realistic enterprise environment with multiple virtual machines — including an attacker node, a vulnerable target (Metasploitable3), and monitored endpoints.

A full **vulnerability assessment** was conducted against the Metasploitable3 target using Nmap and Metasploit, resulting in the discovery of **five exploitable vulnerabilities**: a Denial-of-Service (DoS) vector and an HTTP-based attack surface. Both were successfully detected and alerted by the Wazuh SIEM.

> ⚠️ **Disclaimer:** This lab is conducted in an **isolated, private network** for educational purposes only. No systems outside the lab environment were targeted.

---

## 🎯 Objectives

- Deploy and configure **Wazuh SIEM** (Manager + Indexer + Dashboard)
- Build a multi-VM isolated lab network
- Perform **network scanning and vulnerability discovery** on Metasploitable3
- Validate **detection capabilities** of Wazuh against real vulnerabilities
- Map findings to the **MITRE ATT&CK framework**
- Document the full process for reproducibility and portfolio purposes

---

## 🖥️ Lab Architecture

| VM                  | Role                        | OS                  | IP Address       |
|---------------------|-----------------------------|---------------------|------------------|
| **Wazuh Manager**   | SIEM / Dashboard / Indexer  | Ubuntu 22.04 LTS    | `[192.168.106.130]` |
| **Metasploitable3** | Vulnerable Target           | Ubuntu 14.04        | `[192.168.106.134]` |
| **Kali Linux**      | Attacker / Scanner          | Kali Linux 2025.4   | `[192.168.106.128]` |


> 📐 Network Type: Host-Only / NAT (isolated from internet)
> 🔗 [Full Architecture Details](architecture/lab-topology.md) | [VM Inventory](architecture/vm-inventory.md)

---

## 🔍 Exploits Executed

| # | Exploit | Type | Severity | MITRE ATT&CK | CVE | Wazuh Detection |
|---|---------------|------|----------|--------------|-----|-----------------|
| 1 | [DoS Attack Vector](vulnerability-assessment/vuln-01-dos-attack.md) | Denial of Service | 🔴 High | [T1499](https://attack.mitre.org/techniques/T1499/) | `[CVE-XXXX-XXXX]` | ✅ Detected |
| 2 | [HTTP-Based Attack](vulnerability-assessment/vuln-02-http-attack.md) | Web Exploitation | 🟠 Medium-High | [T1190](https://attack.mitre.org/techniques/T1190/) | `[CVE-XXXX-XXXX]` | ✅ Detected |

> 🔗 [Full Nmap Scan Results](vulnerability-assessment/nmap-scan-results.md)

---

## 📊 Key Results & Findings

- ✅ Wazuh SIEM **successfully detected both vulnerabilities** in real-time
- ✅ Correct **alert severity levels** assigned by Wazuh rules
- ✅ **Active response** triggered automatically on DoS detection
- ✅ Full **alert correlation** with MITRE ATT&CK techniques
- ✅ Dashboard visualizations confirmed log ingestion from all agents
- 📸 [View Evidence Screenshots](screenshots/)

---

## 🛠️ Tools & Technologies

| Tool              | Version    | Purpose                                  |
|-------------------|------------|------------------------------------------|
| **Wazuh**         | 4.x        | SIEM, log analysis, alerting, IDS        |
| **Nmap**          | 7.x        | Network scanning, vulnerability scripts  |
| **Metasploitable3** | Latest   | Intentionally vulnerable target VM       |
| **Kali Linux**    | 2025.4     | Attack simulation and scanning platform  |
| **OpenSSH**       | —          | Remote management of VMs                 |

---

## 📁 Repository Structure

```
wazuh-homelab-cybersecurity/
├── README.md                            ← You are here
├── architecture/
│   ├── lab-topology.md                  ← Network diagram & design
│   └── vm-inventory.md                  ← VM specs & configuration
├── setup/
│   ├── 01-wazuh-manager-install.md      ← Wazuh Manager setup
│   ├── 02-agent-deployment.md           ← Agent deployment (Win/Linux)
│   └── 03-network-configuration.md      ← Network & firewall config
├── vulnerability-assessment/
│   ├── nmap-scan-results.md             ← Full scan output & analysis
│   ├── vuln-01-dos-attack.md            ← DoS vulnerability report
│   └── vuln-02-http-attack.md           ← HTTP attack vulnerability report
├── detections/
│   ├── wazuh-alerts-analysis.md         ← SIEM detection analysis
│   └── custom-rules/                    ← Custom Wazuh XML rules
├── screenshots/                         ← Evidence & proof-of-concept images
└── conclusions.md                       ← Lessons learned & next steps
```

---

## 🚀 How to Reproduce

1. Clone this repository
2. Follow the [Wazuh Manager Setup Guide](setup/01-wazuh-manager-install.md)
3. Deploy agents per the [Agent Deployment Guide](setup/02-agent-deployment.md)
4. Configure the network as described in [Network Configuration](setup/03-network-configuration.md)
5. Run the Nmap scans from [Vulnerability Assessment](vulnerability-assessment/nmap-scan-results.md)

> **Requirements:** VMware® Workstation 17 Pro (version:17.5.2/build-23775571), minimum 16GB RAM, 100GB disk space

---

## 📚 References

- [Wazuh Official Documentation](https://documentation.wazuh.com)
- [MITRE ATT&CK Framework](https://attack.mitre.org)
- [Metasploitable3 by Rapid7](https://github.com/rapid7/metasploitable3)
- [Nmap Scripting Engine (NSE)](https://nmap.org/book/nse.html)
- [CVE Database](https://cve.mitre.org)

---

## 👤 Author

**Christos Kaldanis**
Cybersecurity Enthusiast | Blue Team | SOC Analyst (Aspiring)

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](www.linkedin.com/in/christos-kaldanis-677107310)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black)](https://github.com/YOURUSERNAME)

---

*This project was built for educational purposes as part of a personal cybersecurity learning journey.*
