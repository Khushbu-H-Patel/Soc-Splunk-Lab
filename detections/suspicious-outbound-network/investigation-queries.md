# Suspicious Outbound Network Connection Investigation Queries

## 1. All Network Connections

This query provides baseline visibility into network connections captured by Sysmon.

```
index=sysmon_logs EventCode=3
| stats count by DestinationIp, Image
| sort -count
```

---

## 2. External Connections

This query filters out localhost traffic and focuses on external destination IPs.

```
index=sysmon_logs EventCode=3
NOT (DestinationIp="127.0.0.1" OR DestinationIp="::1")
| stats count by DestinationIp, Image
| sort -count
```

---

## 3. Rare Destination Detection

This query identifies rarely contacted destination IPs that may require further investigation.

```
index=sysmon_logs EventCode=3
| stats count by DestinationIp
| where count < 3
| sort count
```

---

## 4. Time-Based Spike Detection

This query detects spikes in outbound network activity within a 5-minute window.

```
index=sysmon_logs EventCode=3
| bucket _time span=5m
| stats count by _time
| where count >= 10
```

---

## 5. Network Activity Over Time

This query visualizes outbound network activity over time.

```
index=sysmon_logs EventCode=3
| timechart count
```

---

## 6. Top Destination IPs

This query identifies the destination IPs receiving the highest number of connections.

```
index=sysmon_logs EventCode=3
| stats count by DestinationIp
| sort -count
```

---

## 7. Processes Making Connections

This query shows which processes are generating network connections.

```
index=sysmon_logs EventCode=3
| stats count by Image
| sort -count
```

---

## 8. Suspicious PowerShell Connections

This query provides detailed visibility into PowerShell-generated network connections.

```
index=sysmon_logs EventCode=3 Image="*powershell.exe"
| table _time, Image, DestinationIp, DestinationPort
```

---

## 9. External Connections Only

This query provides a simplified view of external destination IP activity.

```
index=sysmon_logs EventCode=3
NOT (DestinationIp="127.0.0.1" OR DestinationIp="::1")
| stats count by DestinationIp
```