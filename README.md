# SOC Lab using Splunk SIEM

## 🔍 Project Overview

This project demonstrates the design and implementation of a Security Operations Center (SOC) lab using Splunk SIEM. The lab simulates realistic cyber attack scenarios and showcases detection engineering, alerting, log analysis, and security monitoring across authentication, endpoint, and network layers.

The project was developed in two phases to progressively build a more realistic SOC environment.

---

# 🏗️ Lab Architecture

## Phase 1 — Single-Host SOC Simulation

- Windows 10 VM acting as both attacker and target
- Ubuntu Server running Splunk Enterprise SIEM

This phase focused on:
- Log ingestion
- Detection engineering
- Alert creation
- Dashboard visualization
- Endpoint and authentication monitoring

---

## Phase 2 — Multi-Machine SOC Simulation

- Kali Linux VM acting as attacker
- Windows 10 VM acting as target and log source
- Ubuntu Server running Splunk Enterprise SIEM

This phase introduced:
- External attacker simulation
- Network reconnaissance detection
- Windows Firewall log monitoring
- More realistic SOC visibility

---

## 🔄 Data Flow

```text
Kali Linux → Windows Target → Splunk Universal Forwarder → Splunk SIEM
```

---

# 🛠️ Technologies Used

- Splunk Enterprise
- Splunk Universal Forwarder
- Windows 10
- Kali Linux
- Ubuntu Server
- Sysmon
- Windows Firewall Logs
- VMware Workstation
- Nmap
- PowerShell

---

# 📊 Data Sources

| Data Source | Purpose |
|---|---|
| Windows Security Logs (EventCode 4625) | Failed login and brute force detection |
| Sysmon Event ID 1 | Process creation monitoring |
| Sysmon Event ID 3 | Outbound network connection monitoring |
| Windows Firewall Logs | External attacker and port scan visibility |

---

# ⚔️ Attack Simulations & Detections

## 🔹 1. Brute Force Attack Detection

### Scenario
Simulated repeated failed login attempts against a Windows account.

### Data Source
- Windows Security Logs
- EventCode 4625

### Detection Logic
- Multiple failed logins within a defined time window
- Threshold-based alerting

### MITRE ATT&CK
- T1110 — Brute Force

---

## 🔹 2. Suspicious Process Execution Detection

### Scenario
Simulated attacker-like process execution using PowerShell and reconnaissance commands.

### Data Source
- Sysmon Event ID 1

### Detection Logic
- PowerShell execution monitoring
- Encoded command detection
- Suspicious command-line arguments
- Process execution spikes

### MITRE ATT&CK
- T1059.001 — PowerShell
- T1033 — System Owner/User Discovery

---

## 🔹 3. Suspicious Outbound Network Connection Detection

### Scenario
Simulated suspicious outbound network connections initiated from Windows processes.

### Data Source
- Sysmon Event ID 3

### Detection Logic
- Outbound connections from suspicious processes
- External destination monitoring
- Connection spike detection

### MITRE ATT&CK
- T1071 — Application Layer Protocol

---

## 🔹 4. Network Reconnaissance Detection (Kali Linux Attack)

### Scenario
Performed Nmap-based port scanning from Kali Linux against the Windows target.

### Data Source
- Windows Firewall Logs

### Detection Logic
- High volume of connection attempts
- Multiple destination ports targeted
- Source IP correlation
- Port scan behavior analysis

### MITRE ATT&CK
- T1046 — Network Service Scanning

---

# 🚨 Alerting

Alerts were configured in Splunk using:

- Scheduled searches
- Threshold-based triggering
- 5-minute execution intervals
- Alert throttling to reduce duplicate notifications

---

# 📊 Dashboards

Custom Splunk dashboards were created for:

- Authentication monitoring
- Failed login analysis
- Process execution monitoring
- PowerShell activity monitoring
- Outbound network monitoring
- External attacker identification
- Port scan visualization

Dashboard exports are available in the `reports/` directory.

---

# 📁 Project Structure

```text
mini-soc-splunk-lab/
├── architecture/
├── phase-1-single-host-simulation/
├── phase-2-realistic-soc-simulation/
├── detections/
├── configs/
├── reports/
├── references/
└── README.md
```

---

# 🧠 MITRE ATT&CK Coverage

| Detection | Technique ID | Technique |
|---|---|---|
| Brute Force Detection | T1110 | Brute Force |
| PowerShell Execution Detection | T1059.001 | PowerShell |
| Suspicious Command Usage | T1033 | System Owner/User Discovery |
| Outbound Network Monitoring | T1071 | Application Layer Protocol |
| Network Reconnaissance Detection | T1046 | Network Service Scanning |

Detailed ATT&CK mappings are available in:

```text
references/mitre-attack-mapping.md
```

---

# 📌 Key Learning Outcomes

This project provided hands-on experience in:

- Building a functional SOC lab environment
- Configuring centralized log collection
- Developing custom SPL detections
- Simulating realistic attack scenarios
- Creating actionable alerts and dashboards
- Investigating endpoint and network activity
- Mapping detections to MITRE ATT&CK techniques

---

# 📷 Screenshots and Reports

Dashboard screenshots and exported reports are included throughout the repository and within the `reports/` directory respectively.

---

# 📌 Conclusion

This project demonstrates the implementation of a functional SOC lab capable of ingesting logs, detecting suspicious activity, generating alerts, and visualizing security events using Splunk SIEM across both host-based and network-based attack scenarios.