# Reports

## 🏗️ Overview

This folder contains exported PDF reports of the Splunk dashboards created during the SOC lab project. These reports provide visual evidence of the detection logic, alerts, and monitoring capabilities implemented across both phases of the lab.

The dashboards were designed to support security monitoring and investigation by visualizing authentication events, process execution activity, outbound network behavior, and external reconnaissance attempts.

---

## 📊 Included Reports

### 🔹 Brute Force Monitoring Dashboard
Visualizes failed login attempts and authentication spikes using Windows Security Logs.

---

### 🔹 Suspicious Process Execution Monitoring Dashboard
Displays suspicious process activity and PowerShell execution events captured through Sysmon logs.

---

### 🔹 Suspicious Outbound Network Activity Dashboard
Shows outbound network connections and abnormal network activity generated from the Windows system.

---

### 🔹 Port Scan Network Reconnaissance Monitoring Dashboard
Visualizes external reconnaissance activity performed from the Kali Linux attacker machine against the Windows target using Windows Firewall logs.

---


## 📌 Note

The dashboards and reports were generated directly from Splunk after successful log ingestion, attack simulation, and detection rule implementation.