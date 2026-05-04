# Mini SOC Lab using Splunk SIEM

## 🔍 Overview

This project demonstrates the design and implementation of a **Security Operations Center (SOC) lab** using Splunk SIEM. The lab simulates real-world attack scenarios and showcases detection, alerting, and monitoring capabilities across multiple layers including authentication, endpoint, and network.

The project is implemented in two phases:

- **Phase 1:** Single-host simulation (Windows acting as both attacker and target)
- **Phase 2:** Multi-machine SOC simulation (Kali Linux as attacker, Windows as target)

---

## 🏗️ Architecture

### Phase 1 — Single Host Simulation

- Windows 10 (Attacker + Target)
- Ubuntu Server (Splunk SIEM)

### Phase 2 — Realistic SOC Simulation

- Kali Linux (Attacker)
- Windows 10 (Target + Log Source)
- Ubuntu Server (Splunk SIEM)

### Data Flow
Kali Linux → Windows Target → Splunk Universal Forwarder → Splunk SIEM


---

## 🛠️ Tools & Technologies

- Splunk Enterprise (SIEM)
- Splunk Universal Forwarder
- Windows 10
- Kali Linux
- Ubuntu Server
- Sysmon
- Windows Firewall Logs
- VMware Workstation

---

## 📊 Data Sources

| Source | Purpose |
|------|--------|
| Windows Security Logs (EventCode 4625) | Brute force detection |
| Sysmon (EventCode 1, 3) | Process and network activity |
| Windows Firewall Logs | External attack visibility |

---

## ⚔️ Attack Scenarios & Detection

### 🔹 1. Brute Force Attack Detection

- Simulated multiple failed login attempts
- Data Source: Windows Security Logs (EventCode 4625)

**Detection Logic:**
- Multiple failed logins within a defined time window

---

### 🔹 2. Suspicious Process Execution

- Simulated attacker-like commands (PowerShell, system enumeration)
- Data Source: Sysmon EventCode 1

**Detection Logic:**
- Suspicious command-line patterns
- High-frequency process execution

---

### 🔹 3. Outbound Network Activity (Phase 1)

- Simulated outbound connections from Windows
- Data Source: Sysmon EventCode 3

---

### 🔹 4. Network Reconnaissance (Phase 2 - Kali Attack)

- Performed Nmap scan from Kali to Windows
- Data Source: Windows Firewall Logs

**Detection Logic:**
- High volume of connection attempts
- Multiple destination ports targeted from a single source IP

---

## 🚨 Alerting

Alerts were configured in Splunk using:

- Scheduled searches (every 5 minutes)
- Threshold-based triggering
- Throttling to reduce alert noise

---

## 📊 Dashboards

Dashboards were created for:

- Authentication monitoring (brute force detection)
- Endpoint activity monitoring (process execution)
- Network monitoring (connection tracking and anomaly detection)
- External attacker identification (Kali source IP detection)

---

## 🧠 MITRE ATT&CK Mapping

| Attack | Technique |
|------|----------|
| Brute Force | T1110 |
| PowerShell Execution | T1059.001 |
| Network Reconnaissance | T1046 |

---

## 📁 Project Structure
```
mini-soc-splunk-lab/
├── architecture/
├── phase-1-single-host-simulation/
├── phase-2-realistic-soc-simulation/
├── detections/
├── configs/
├── reports/
└── references/
```

---

## 💼 Key Skills Demonstrated

- SIEM implementation and configuration
- Log ingestion and normalization
- SPL (Search Processing Language)
- Detection engineering
- Alert configuration and tuning
- Security monitoring and analysis
- Multi-machine SOC architecture design

---

## 📌 Conclusion

This project demonstrates the ability to design and implement a functional SOC lab, simulate realistic attack scenarios, and build effective detection and monitoring mechanisms using Splunk.

---

