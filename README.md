# SOC Homelab – Malware Detection with Splunk & Sysmon

## 📌 Overview
This project demonstrates a basic SOC (Security Operations Center) homelab where malicious activity is generated and detected using **Splunk SIEM** and **Sysmon** on a Windows endpoint.

The goal of this lab is **not exploitation**, but to understand how attacker activity generates telemetry and how defenders analyze it.

---

## 🧪 Lab Environment

### Attacker Machine
- OS: Kali Linux
- Role: Simulated attacker

### Target Machine
- OS: Windows 10
- Tools: Sysmon, Splunk Universal Forwarder

### SIEM
- Splunk Enterprise
- Index: `endpoint`

### Network Configuration
- Virtual Machine Network: **Internal / Host-Only**
- Purpose: Isolated environment for safe testing

---

## 🔧 Tools Used
- Splunk Enterprise
- Splunk Add-on for Sysmon
- Sysmon (Process & Network logging)
- Nmap
- Metasploit (msfvenom – lab use only)

---

## 🎯 Attack Simulation
The following activities were performed to generate telemetry:
- Network scanning from attacker machine
- Execution of a simulated malicious executable
- Establishment of a reverse TCP connection
- Post-exploitation command execution

---

## 🔍 Detection & Analysis
Telemetry generated from the attack was analyzed in Splunk, focusing on:
- Process creation (Sysmon Event ID 1)
- Network connections (Sysmon Event ID 3)
- Parent-child process relationships
- Suspicious command execution

Detailed analysis can be found in:
➡️ `analysis/detection-analysis.md`

---

## 📸 Screenshots
Screenshots are provided to demonstrate:
- Lab topology
- Log ingestion into Splunk
- Malicious process execution
- Network connections
- Process relationships

---

## 🚨 Disclaimer
This project is for **educational and defensive security purposes only**.  
All testing was performed in an isolated lab environment.

---

## 👤 Author
SOC Analyst (Entry Level)  
