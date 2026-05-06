# Network Reconnaissance Investigation Queries

## 1. Basic Verification Query

This query confirms that Windows Firewall logs are being ingested and parsed correctly in Splunk.

```
index=windows_firewall_logs RECEIVE
| rex field=_raw "(?<action>ALLOW|DROP)\s+(?<protocol>\w+)\s+(?<src_ip>\d+\.\d+\.\d+\.\d+)\s+(?<dst_ip>\d+\.\d+\.\d+\.\d+)\s+(?<src_port>\d+)\s+(?<dst_port>\d+)"
| where isnotnull(src_ip)
| table _time, action, protocol, src_ip, dst_ip, src_port, dst_port
| sort -_time
```

---

## 2. Focus on Kali Attacker

This query filters firewall logs to show only traffic from the Kali attacker machine.

```
index=windows_firewall_logs RECEIVE
| rex field=_raw "(?<action>ALLOW|DROP)\s+(?<protocol>\w+)\s+(?<src_ip>\d+\.\d+\.\d+\.\d+)\s+(?<dst_ip>\d+\.\d+\.\d+\.\d+)\s+(?<src_port>\d+)\s+(?<dst_port>\d+)"
| where src_ip="192.168.79.136"
| table _time, action, protocol, src_ip, dst_ip, src_port, dst_port
| sort -_time
```

---

## 3. Network Activity Over Time

This query visualizes firewall log activity over time and helps identify spikes during scanning activity.

```
index=windows_firewall_logs RECEIVE
| rex field=_raw "(?<action>ALLOW|DROP)\s+(?<protocol>\w+)\s+(?<src_ip>\d+\.\d+\.\d+\.\d+)\s+(?<dst_ip>\d+\.\d+\.\d+\.\d+)\s+(?<src_port>\d+)\s+(?<dst_port>\d+)"
| where isnotnull(src_ip)
| timechart count
```

---

## 4. Top Source IPs

This query identifies the source IP addresses generating the highest number of firewall events.

```
index=windows_firewall_logs RECEIVE
| rex field=_raw "(?<action>ALLOW|DROP)\s+(?<protocol>\w+)\s+(?<src_ip>\d+\.\d+\.\d+\.\d+)\s+(?<dst_ip>\d+\.\d+\.\d+\.\d+)\s+(?<src_port>\d+)\s+(?<dst_port>\d+)"
| where isnotnull(src_ip)
| where NOT dst_ip="224.0.0.252"
| stats count by src_ip
| sort -count
```

---

## 5. Top Targeted Ports

This query shows which destination ports were targeted most frequently during network reconnaissance.

```
index=windows_firewall_logs RECEIVE
| rex field=_raw "(?<action>ALLOW|DROP)\s+(?<protocol>\w+)\s+(?<src_ip>\d+\.\d+\.\d+\.\d+)\s+(?<dst_ip>\d+\.\d+\.\d+\.\d+)\s+(?<src_port>\d+)\s+(?<dst_port>\d+)"
| where isnotnull(src_ip)
| where NOT dst_ip="224.0.0.252"
| stats count by dst_port
| sort -count
```

---

## 6. Kali Scan Activity Summary

This query summarizes the number of events and unique ports targeted by the Kali attacker.

```
index=windows_firewall_logs RECEIVE
| rex field=_raw "(?<action>ALLOW|DROP)\s+(?<protocol>\w+)\s+(?<src_ip>\d+\.\d+\.\d+\.\d+)\s+(?<dst_ip>\d+\.\d+\.\d+\.\d+)\s+(?<src_port>\d+)\s+(?<dst_port>\d+)"
| where src_ip="192.168.79.136"
| stats count dc(dst_port) as unique_ports by src_ip, dst_ip
```

---

## 7. Allowed vs Dropped Connections

This query summarizes firewall actions to show whether traffic was allowed or dropped.

```
index=windows_firewall_logs RECEIVE
| rex field=_raw "(?<action>ALLOW|DROP)\s+(?<protocol>\w+)\s+(?<src_ip>\d+\.\d+\.\d+\.\d+)\s+(?<dst_ip>\d+\.\d+\.\d+\.\d+)\s+(?<src_port>\d+)\s+(?<dst_port>\d+)"
| where isnotnull(action)
| stats count by action
```

---

## 8. Investigation Table

This query provides a detailed analyst view of firewall events, including source IP, destination IP, protocol, and ports.

```
index=windows_firewall_logs RECEIVE
| rex field=_raw "(?<action>ALLOW|DROP)\s+(?<protocol>\w+)\s+(?<src_ip>\d+\.\d+\.\d+\.\d+)\s+(?<dst_ip>\d+\.\d+\.\d+\.\d+)\s+(?<src_port>\d+)\s+(?<dst_port>\d+)"
| where isnotnull(src_ip)
| where NOT dst_ip="224.0.0.252"
| table _time, action, protocol, src_ip, dst_ip, src_port, dst_port
| sort -_time
```