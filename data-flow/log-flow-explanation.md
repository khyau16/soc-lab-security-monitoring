# SOC Lab – Log Flow Explanation

## Overview
This document explains how logs are generated, processed, and visualized in the SOC lab environment.

The lab simulates a real-world Security Operations Center (SOC) workflow:
**Attack → Log Generation → Detection → Alerting**

---

## Architecture Flow

Kali Linux (Attacker)  
→ Ubuntu Server (Victim)  
→ Snort IDS  
→ Syslog  
→ Splunk SIEM  

---

## Step-by-Step Log Flow

### 1. Attack Execution (Kali Linux)
- Attacker machine launches activities such as:
  - Nmap scan
  - SSH brute-force (Hydra)
- These actions target the Ubuntu server

---

### 2. Log Generation (Ubuntu Server)
- The Ubuntu server records events in system logs:
  - `/var/log/auth.log` → SSH login attempts
  - `/var/log/syslog` → system-level events

- Example events:
  - Failed SSH login attempts
  - Connection attempts from attacker IP

---

### 3. Intrusion Detection (Snort IDS)
- Snort monitors incoming network traffic
- Detects suspicious patterns such as:
  - Port scanning
  - Brute-force attempts

- Alerts are generated in:
  - `snort.alert`
  - `snort.alert.fast`

---

### 4. Log Forwarding (Syslog / Forwarder)
- Logs from Ubuntu and Snort are forwarded to Splunk
- Methods include:
  - Syslog forwarding
  - Splunk Universal Forwarder

- Purpose:
  - Centralize logs for analysis

---

### 5. Log Ingestion (Splunk SIEM)
- Splunk receives and indexes logs into defined indexes:
  - Example: `ubuntu`, `ubuntu_network`

- Extracts useful fields such as:
  - Source IP
  - Timestamp
  - Event type

---

### 6. Detection & Analysis (Splunk Search)
- SPL queries are used to detect suspicious behavior

Example:
```spl
index=ubuntu "Failed password"
| stats count by src_ip
| where count > 5
```

- Identifies brute-force attack patterns

---

### 7. Alerting (Splunk Alerts)
- Detection queries are converted into alerts
- Trigger conditions:
  - e.g. more than 5 failed login attempts

- Alerts can:
  - Notify analysts
  - Trigger response actions

---

## Data Flow Summary

| Stage            | Component        | Output                          |
|------------------|----------------|----------------------------------|
| Attack           | Kali Linux      | Malicious traffic               |
| Log Generation   | Ubuntu Server   | System logs                     |
| Detection        | Snort IDS       | Alert files                     |
| Forwarding       | Syslog          | Centralized logs                |
| Ingestion        | Splunk          | Indexed events                  |
| Analysis         | Splunk Search   | Detection results               |
| Alerting         | Splunk Alerts   | Security alerts                 |

---

## Key Takeaways

- Demonstrates full SOC workflow from attack to alert
- Shows integration of multiple security tools
- Highlights importance of centralized logging and monitoring
- Enables detection of real-world attack techniques

---

## Notes

- This lab environment is isolated and controlled
- Designed for learning and demonstration purposes only
