# Suspicious Process Execution Investigation Queries

## 1. Baseline View

This query provides a baseline overview of process execution activity captured by Sysmon.

```
index=sysmon_logs EventCode=1
| stats count by Image
| sort -count
```

---

## 2. Suspicious Command Usage

This query identifies suspicious command usage related to reconnaissance activity and PowerShell execution.

```
index=sysmon_logs EventCode=1
(CommandLine="*whoami*" OR CommandLine="*net user*" OR CommandLine="*powershell*")
```

---

## 3. PowerShell-Focused Detection

This query focuses specifically on PowerShell process execution events.

```
index=sysmon_logs EventCode=1 Image="*powershell.exe"
```

---

## 4. Time-Based Spike Detection

This query detects spikes in PowerShell execution activity over a short time period.

```
index=sysmon_logs EventCode=1 Image="*powershell.exe"
| bucket _time span=5m
| stats count by _time, host
| where count >= 5
```

---

## 5. Rare Process Hunting

This query identifies rarely executed processes that may warrant further investigation.

```
index=sysmon_logs EventCode=1
| stats count by Image
| where count < 3
| sort count
```

---

## 6. Process Activity Over Time

This query visualizes overall process execution activity over time.

```
index=sysmon_logs EventCode=1
| timechart count
```

---

## 7. Top Processes

This query identifies the most frequently executed processes captured by Sysmon.

```
index=sysmon_logs EventCode=1
| stats count by Image
| sort -count
```

---

## 8. PowerShell Activity Over Time

This query visualizes PowerShell execution activity over time.

```
index=sysmon_logs EventCode=1 Image="*powershell.exe"
| timechart count
```

---

## 9. Suspicious PowerShell Activity Table

This query provides a detailed analyst view of suspicious PowerShell executions involving risky flags or encoded commands.

```
index=sysmon_logs EventCode=1 Image="*powershell.exe"
(CommandLine="*-ExecutionPolicy Bypass*" OR CommandLine="*-enc*" OR CommandLine="*-EncodedCommand*")
| table _time, host, Image, CommandLine
```

---

## 10. Parent-Child Process Context

This query displays parent-child process relationships to provide additional execution context during investigations.

```
index=sysmon_logs EventCode=1
| table _time, Image, ParentImage, CommandLine
```