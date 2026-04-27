# 🛡️ Cyber Defense Home Lab — Wazuh SIEM + Vulnerability Assessment

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![SIEM](https://img.shields.io/badge/SIEM-Wazuh_4.x-blue)
![Framework](https://img.shields.io/badge/Framework-MITRE_ATT%26CK-red)
![Target](https://img.shields.io/badge/Target-Metasploitable3-orange)

## 📋 Project Overview
Deployed a fully functional cyber defense home lab using **Wazuh SIEM** 
to monitor, detect, and analyze security events across multiple virtual 
machines. Performed vulnerability assessment on a **Metasploitable3** 
target and identified two critical vulnerabilities — a DoS vector and 
an HTTP-based attack surface.

## 🎯 Objectives
- Deploy and configure Wazuh SIEM (Manager + Agents)
- Build an isolated multi-VM lab environment
- Perform network scanning and vulnerability discovery
- Correlate findings with MITRE ATT&CK framework
- Document detection capabilities of the SIEM

## 🖥️ Lab Architecture

| VM               | Role              | OS              | IP            |
|------------------|-------------------|-----------------|---------------|
| Wazuh Manager    | SIEM / Dashboard  | Ubuntu 22.04    | 192.168.106.130 |
| Metasploitable3  | Vulnerable Target | Ubuntu 14.04    | 192.168.106.134 |
| Kali Linux       | Attacker          | Kali 2024.x     | 192.168.106.128 |


> 🔗 [Full Architecture Details](architecture/lab-topology.md)

## 🔍 Vulnerabilities Discovered

| # | Vulnerability     | Type      | CVSS  | MITRE ATT&CK | Detected by Wazuh |
|---|-------------------|-----------|-------|--------------|-------------------|
| 1 | [DoS Attack](vulnerability-assessment/vuln-01-dos-attack.md)   | DoS       | X.X   | T1499        | ✅ Yes            |
| 2 | [HTTP Attack](vulnerability-assessment/vuln-02-http-attack.md) | Web Attack| X.X   | T1190        | ✅ Yes            |

## 📊 Key Results
- ✅ Wazuh successfully detected both vulnerabilities
- ✅ Real-time alerts generated with correct severity levels
- ✅ Active response triggered on DoS attempt
- 📸 [View Screenshots](screenshots/)

## 🛠️ Tools Used
| Tool        | Purpose                        |
|-------------|-------------------------------|
| Wazuh 4.x   | SIEM, log analysis, alerting  |
| Nmap        | Network & vulnerability scan  |
| Metasploit  | Exploitation framework        |
| VirtualBox  | Virtualization platform       |
| Kali Linux  | Attack simulation             |



## 📚 References
- [Wazuh Documentation](https://documentation.wazuh.com)
- [MITRE ATT&CK](https://attack.mitre.org)
- [Metasploitable3](https://github.com/rapid7/metasploitable3)
