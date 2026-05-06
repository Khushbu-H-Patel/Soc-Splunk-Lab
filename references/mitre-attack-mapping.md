# MITRE ATT&CK Mapping

## 🏗️ Overview

This document maps the attack simulations and detections implemented in the SOC lab project to the MITRE ATT&CK framework. The mapping demonstrates how the simulated attack activity aligns with known adversary techniques and how corresponding detections were implemented using Splunk, Sysmon, Windows Event Logs, and Windows Firewall logs.

---

## 📊 MITRE ATT&CK Mapping Table

| Detection / Simulation | MITRE ATT&CK Technique | Technique ID | Data Source |
|---|---|---|---|
| Brute Force Login Attempts | Brute Force | T1110 | Windows Security Logs |
| Suspicious PowerShell Execution | Command and Scripting Interpreter: PowerShell | T1059.001 | Sysmon Event ID 1 |
| Suspicious Command Usage (`whoami`, `net user`) | System Owner/User Discovery | T1033 | Sysmon Event ID 1 |
| Suspicious Outbound Network Connections | Application Layer Protocol | T1071 | Sysmon Event ID 3 |
| External Network Connections | Network Service Scanning | T1046 | Sysmon Event ID 3 |
| Kali Linux Port Scanning / Network Reconnaissance | Network Service Scanning | T1046 | Windows Firewall Logs |
| PowerShell Encoded Commands | Obfuscated Files or Information | T1027 | Sysmon Event ID 1 |
| Parent-Child Process Investigation | Process Discovery | T1057 | Sysmon Event ID 1 |

---

## 🎯 Detection Coverage

The project demonstrates detection coverage across multiple attack categories, including:

- Authentication attacks
- PowerShell abuse
- Endpoint process monitoring
- Outbound network activity
- Network reconnaissance and port scanning

The combination of Sysmon telemetry, Windows Event Logs, Windows Firewall logs, and Splunk SIEM enabled detection and visualization of both host-based and network-based attack activity.

---

## 🔍 Data Sources Used

### Windows Security Logs
Used for:
- Failed login monitoring
- Authentication event analysis

---

### Sysmon Logs
Used for:
- Process creation monitoring
- PowerShell activity detection
- Outbound network connection monitoring
- Parent-child process analysis

---

### Windows Firewall Logs
Used for:
- External connection monitoring
- Port scan detection
- Network reconnaissance analysis