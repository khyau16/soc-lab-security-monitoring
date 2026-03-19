# SOC Lab – Attack Commands

## Overview
This document outlines the attack simulations performed in the SOC lab environment.

- **Attacker:** Kali Linux  
- **Target:** Ubuntu Server  
- **Purpose:** Generate logs for monitoring and detection in Splunk  

---

## 1. Network Reconnaissance (Nmap Scan)

### Basic Port Scan
```bash
nmap -sS 192.168.56.102
```

### Service & Version Detection
```bash
nmap -A 192.168.56.102
```

### Purpose
Identify open ports and services running on the target system.  
This helps simulate reconnaissance activity commonly performed before an attack.

---

## 2. SSH Brute Force Attack

### Command
```bash
hydra -l ubuntu -P /usr/share/wordlists/rockyou.txt ssh://192.168.56.102
```

### Purpose
Simulate a brute-force attack against the SSH service to generate:
- Multiple failed login attempts  
- Authentication logs in `/var/log/auth.log`  
- Detectable events in Splunk  

---

## Expected Outcome

- Logs generated on the Ubuntu server  
- Snort detects suspicious activity 
- Splunk ingests logs and enables detection queries  
- Alerts triggered based on defined rules  

---

## Notes

- This lab is conducted in a **controlled environment only**
