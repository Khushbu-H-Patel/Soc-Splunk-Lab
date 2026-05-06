# Brute Force Investigation Queries

## 1. Target Account Extraction

This query extracts the actual account targeted during the failed login attempt.

```
index=windows_logs EventCode=4625
| rex field=_raw "Account For Which Logon Failed:\s+Security ID:\s+\S+\s+Account Name:\s+(?<target_user>\w+)"
| table Account_Name, target_user
```

---

## 2. Analyst-Level Source Analysis

This query identifies which account was targeted and the source address associated with the failed login attempts.

```
index=windows_logs EventCode=4625
| rex field=_raw "Account For Which Logon Failed:\s+Security ID:\s+\S+\s+Account Name:\s+(?<target_user>\w+)"
| stats count by target_user, Source_Network_Address
| sort -count
```

---

## 3. Failed Login Trend

This query visualizes failed login attempts over time.

```
index=windows_logs EventCode=4625
| timechart count
```

---

## 4. Targeted Accounts

This query shows which accounts were targeted most frequently.

```
index=windows_logs EventCode=4625
| rex field=_raw "Account For Which Logon Failed:\s+Security ID:\s+\S+\s+Account Name:\s+(?<target_user>\w+)"
| stats count by target_user
| sort -count
```

---

## 5. Source of Attack

This query identifies the source network address associated with failed login activity.

```
index=windows_logs EventCode=4625
| stats count by Source_Network_Address
| sort -count
```

---

## 6. Failed Logins Table

This query provides a detailed investigation table of failed login events.

```
index=windows_logs EventCode=4625
| rex field=_raw "Account For Which Logon Failed:\s+Security ID:\s+\S+\s+Account Name:\s+(?<target_user>\w+)"
| table _time, target_user, Source_Network_Address
```