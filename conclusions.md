# Conclusions

## Project Summary

This Purple Team Home Lab project simulated a realistic attack chain against an isolated environment and demonstrated both offensive exploitation techniques and defensive detection engineering using Wazuh SIEM.

---

## What Was Achieved

### Offensive (Red Team)

A full attack chain was executed from initial reconnaissance to root-level compromise:

| Phase | Action | Result |
|-------|--------|--------|
| Reconnaissance | nmap CVE scan with decoys | 6 open ports, 10+ CVEs identified |
| Initial Access | ProFTPD mod_copy RCE (CVE-2015-3306) | Shell as www-data |
| Privilege Escalation | PwnKit (CVE-2021-4034) | Full root access |
| Web Exploitation | SQL Injection — payroll_app.php | Database dumped |
| Web Exploitation | Drupalgeddon (CVE-2018-7600) | Remote shell obtained |
| Credential Attack | SSH Brute Force — Hydra | Credentials identified |
| DoS Simulation | Slowloris (CVE-2007-6750) | Web server made unavailable |

### Defensive (Blue Team)

Every attack was analyzed from the defender's perspective:

- Reviewed Wazuh SIEM alerts for each attack scenario
- Identified detection gaps where attacks went undetected
- Developed 7 custom detection rules to close those gaps
- Validated each rule by re-executing the corresponding attack


---

## Detection Coverage


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

## Key Lessons Learned

### On Attacks

**ProFTPD + PwnKit chain** was the most impactful finding. Starting from a completely unauthenticated position, it was possible to achieve full root access in under 5 minutes by chaining two publicly available exploits. This highlights the critical importance of patch management.

**SQL Injection** remains one of the most common and preventable vulnerabilities. The payroll application had no input sanitization whatsoever, allowing both authentication bypass and full database extraction with a single tool run.

**Slowloris DoS** is a low-complexity, high-impact attack. A single attacker with minimal resources can render a web server completely unavailable by exploiting HTTP connection handling behavior.

### On Detection

**Default SIEM rules are not enough.** Out of 8 attack scenarios, only 3 were detected by Wazuh's default ruleset. This is a realistic reflection of enterprise environments where detection coverage is often assumed but rarely validated.

**Custom rules require understanding the attack.** Writing effective detection rules requires knowledge of exactly what evidence an attack leaves behind — in FTP logs, web server logs, file system events, or process activity. This is precisely the skill gap that Purple Team exercises are designed to address.

**Detection validation is ongoing.** Rules written today may not detect variants of the same attack tomorrow. Regular Purple Team exercises are essential to maintain detection coverage over time.

---






## Skills Demonstrated

This project required and developed skills across multiple cybersecurity domains:

**Technical Skills**
- Network reconnaissance and vulnerability identification
- Exploitation of real CVEs using Metasploit and manual techniques
- Privilege escalation techniques on Linux systems
- Web application attack techniques (SQLi, RCE)
- SIEM configuration and rule development
- Log analysis and alert triage

**Analytical Skills**
- Mapping attacks to MITRE ATT&CK framework
- Identifying detection gaps through systematic testing
- Correlating multiple log sources to reconstruct attack timelines
- Risk assessment and CVSS scoring

**Documentation Skills**
- Professional penetration test report writing
- Technical writing for both executive and technical audiences
- Evidence collection and chain of custody documentation

---


## References

- [MITRE ATT&CK Framework](https://attack.mitre.org)
- [Wazuh Documentation](https://documentation.wazuh.com)
- [CVE-2015-3306 — ProFTPD mod_copy](https://nvd.nist.gov/vuln/detail/CVE-2015-3306)
- [CVE-2021-4034 — PwnKit](https://nvd.nist.gov/vuln/detail/CVE-2021-4034)
- [CVE-2018-7600 — Drupalgeddon](https://nvd.nist.gov/vuln/detail/CVE-2018-7600)
- [CVE-2007-6750 — Slowloris](https://nvd.nist.gov/vuln/detail/CVE-2007-6750)
- [PTES — Penetration Testing Execution Standard](http://www.pentest-standard.org)

---

*This project was conducted entirely within an isolated lab environment for educational purposes.*
*All systems were owned and operated by the author. No unauthorized access occurred.*
