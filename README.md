# SOC Home Lab – Security Monitoring Project

## Overview
This project simulates a small SOC environment to demonstrate practical skills in system monitoring, intrusion detection, and log analysis. The lab integrates **Kali Linux** as an attacker, **Ubuntu Server** as the victim, **Snort IDS** for intrusion detection, and **Splunk SIEM** for log collection and analysis.

---

## Lab Architecture
Kali Linux (Attacker) ──▶ Victim (Ubuntu Server)
│
▼
Logs → Splunk SIEM (Windows Host)
│
▼
Snort IDS Alerts

- **Kali Linux**: used to simulate attacks (port scans, brute-force attempts).  
- **Victim Machine**: collects logs and demonstrates vulnerabilities.  
- **Snort IDS**: detects network-based attacks and generates alerts.  
- **Splunk SIEM**: centralizes logs, visualizes alerts, and enables investigation.

---

## Attacks Simulated
- Port scanning using Nmap  
- SSH brute-force attacks using Hydra  
- Simulated abnormal traffic patterns  

---

## Log Collection & Detection
- System and authentication logs are collected from the victim machine and forwarded to Splunk.  
- Example detection queries used in Splunk:
