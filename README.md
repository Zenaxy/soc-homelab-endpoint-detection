# SOC Homelab – Endpoint Malware Detection with Splunk & Sysmon

## 📌 Overview
This project demonstrates a **SOC (Security Operations Center) homelab** focused on **endpoint detection and log analysis** using **Splunk SIEM** and **Sysmon** on a Windows endpoint.

The purpose of this lab is **not exploitation**, but to **simulate attacker activity** in a controlled environment and **analyze the telemetry** generated from that activity — just like a real SOC analyst would.

---

## 🎯 Objectives
- Simulate basic attacker behavior in an isolated lab
- Generate endpoint telemetry using Sysmon
- Ingest and analyze logs in Splunk
- Identify suspicious behavior using process and network analysis
- Practice SOC-style detection thinking

---

## 🧪 Lab Environment

### Attacker Machine
- **OS:** Kali Linux  
- **Role:** Simulated attacker (telemetry generation only)

### Target Machine
- **OS:** Windows 10  
- **Tools Installed:**
  - Sysmon
  - Splunk Universal Forwarder

### SIEM
- **Platform:** Splunk Enterprise  
- **Index:** `endpoint`

### Network Configuration
- **VM Network:** Host-Only / Internal Network  
- **Purpose:** Fully isolated lab for safe testing

---

## 🔧 Tools Used
- Splunk Enterprise
- Splunk Add-on for Sysmon
- Sysmon (Endpoint telemetry)
- Nmap (Network scanning simulation)
- Metasploit Framework (msfvenom – lab use only)

---

## 🧠 Attack Simulation (Telemetry Generation)

The following activities were performed **only to generate logs for analysis**:

1. Network scanning from Kali Linux using Nmap
2. Execution of a simulated malicious executable on Windows
3. Establishment of a reverse TCP connection
4. Execution of basic system commands via the simulated shell

> ⚠️ All activities were conducted in an isolated homelab environment.

---

## 🔍 Detection & Analysis

Telemetry was analyzed in Splunk using Sysmon logs, focusing on:

- **Process Creation** (Sysmon Event ID 1)
- **Network Connections** (Sysmon Event ID 3)
- Parent-child process relationships
- Suspicious command execution behavior

Detailed analysis is available here:  
➡️ `analysis/detection-analysis.md`

Detection logic and rules are documented here:  
➡️ `analysis/detection-rule.md`

---

## 📸 Screenshots Included
Screenshots are provided to demonstrate:
- Lab topology
- Splunk log ingestion
- Suspicious process execution
- Network connections
- Process tree analysis

---

## 🚨 Disclaimer
This project is for **educational and defensive security purposes only**.  
No real-world systems were targeted.  
All testing was performed in an **isolated virtual lab environment**.

---
