# SOC Lab – Splunk Queries

## Overview
This document contains Splunk queries used to detect suspicious activities in the SOC lab environment.

- **Data Source:** Ubuntu Server logs  
- **Purpose:** Detect attacks generated from Kali Linux  

---

## 1. Failed SSH Login Attempts (Brute Force Detection)

### Query
```spl
index=ubuntu "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
```

### Purpose
Detect repeated failed SSH login attempts and identify the source IP address.

---

## Detection Logic

- Searches for log entries containing `"Failed password"`
- Extracts source IP using `rex`
- Counts number of failed attempts per IP
- Helps identify brute-force attack patterns

---

## Expected Output

| src_ip        | count |
|--------------|------|
| 192.168.56.103 | 2486   |

> Note: Only one attacker IP was used in this lab environment. In real networks, multiple IPs may trigger the same alert.

---

## Notes

- Ensure logs are properly forwarded to Splunk
- Index name (`ubuntu`) may vary depending on configuration
- This query can be extended into an alert by setting a threshold (e.g. count > 5)
