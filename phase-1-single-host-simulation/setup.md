# Phase 1 — Environment Setup

## 🏗️ Overview

This phase sets up a single-host SOC simulation environment where a Windows machine acts as both the attacker and the target system. Logs generated from the system are forwarded to Splunk SIEM for analysis, detection, and visualization.

For architecture details, refer to:
[Phase 1 Architecture](../architecture/phase-1-architecture.md)

---

## 🖥️ Virtual Machines

### Windows 10 VM
- Role: Attacker + Target
- Used to simulate:
  - Brute force login attempts
  - Suspicious process execution
  - Outbound network activity
- Installed components:
  - Sysmon
  - Splunk Universal Forwarder

### Ubuntu Server VM
- Role: SIEM Server
- Installed component:
  - Splunk Enterprise

---

## ⚙️ Splunk Enterprise Setup (Ubuntu)

- Installed Splunk Enterprise on Ubuntu Server
- Accessed Splunk Web UI via:
  http://<ubuntu_ip>:8000
- Enabled receiving data on port:
  9997 (Splunk Forwarder Port)

---

## 🔄 Splunk Universal Forwarder Setup (Windows)

- Installed Splunk Universal Forwarder on Windows VM
- Configured forwarder to send logs to:
  <ubuntu_ip>:9997

---

## 📊 Log Sources Configuration

### Windows Event Logs
- Security
- System
- Application

### Sysmon Logs
- EventCode 1 → Process Creation
- EventCode 3 → Network Connections

---

## 📝 inputs.conf Configuration

The following configuration was used on the Windows machine:

[WinEventLog://Security]
disabled = false
index = windows_logs

[WinEventLog://System]
disabled = false
index = windows_logs

[WinEventLog://Application]
disabled = false
index = windows_logs

[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = false
index = sysmon_logs
start_from = oldest
current_only = 0

---

## 🔍 Verification

The setup was verified using the following checks:

- Confirm forwarder connection:
  splunk list forward-server
  ![Splunk list forward-server result](splunk-list-forward-server.png)

- Verify Windows logs ingestion:
  index=windows_logs
  ![splunk windows logs](splunk-windows-logs.png)

- Verify Sysmon logs ingestion:
  index=sysmon_logs
  ![splunk sysmon logs](splunk-sysmon-logs.png)

Successful log ingestion confirms that the environment is ready for detection and monitoring.