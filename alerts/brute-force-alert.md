# SOC Lab – Brute Force Alert

## Overview
This document describes the alert configured in Splunk to detect SSH brute-force attacks in the SOC lab.

- **Data Source:** Ubuntu Server logs (`/var/log/auth.log`)  
- **Detection Query:** Failed SSH login attempts  
- **Purpose:** Automatically notify analysts when repeated login failures indicate a potential brute-force attack  

---

## Alert Details

| Field                 | Value |
|-----------------------|-------|
| Alert Name            | SSH Brute Force Detection |
| Query                 | ```spl index=ubuntu "Failed password" \| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)" \| stats count by src_ip \| where count > 5``` |
| Trigger Condition     | More than 5 failed login attempts from a single IP |
| Alert Type            | Real-time |
| Severity              | High |
| Action on Trigger     | Logs event and add to Triggered Alerts |

---

## Detection Logic
1. Search for `"Failed password"` in Ubuntu logs.  
2. Extract the source IP using `rex`.  
3. Count the number of failed attempts per IP.  
4. Trigger alert if count exceeds threshold (5).  

---

## Purpose and Use
- Provides **real-time visibility** into brute-force attacks.  
- Helps analysts respond quickly and block malicious IPs.  
- Demonstrates **end-to-end SOC workflow**: attack → detection → alerting.  

---

## Notes
- Threshold (5 failed attempts) is adjustable based on environment.  
- Ensure logs are correctly forwarded to Splunk and indexed before alerting.  
