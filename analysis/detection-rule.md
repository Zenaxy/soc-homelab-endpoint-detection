Siap. Di bawah ini **`analysis/detection-rule.md`** yang **SELARAS 100%** dengan README dan `detection-analysis.md` kamu.
Ini **siap copy–paste ke GitHub** (format Markdown, gaya SOC/Blue Team).

---

````md
# Detection Rules – Endpoint Malware Activity (Splunk & Sysmon)

This document defines detection rules derived from observed attacker telemetry in the SOC Homelab environment.
The rules are designed to identify suspicious endpoint behavior using Sysmon logs ingested into Splunk.

These detections focus on **behavior-based indicators**, not static signatures.

---

## 🛡️ Rule 1 – Suspicious Process Creation (Non-Standard Executable Spawning CMD)

### 🎯 Purpose
Detect execution of suspicious binaries that spawn command-line interpreters, a common malware behavior.

---

### 🔍 Log Source
- Sysmon
- Event ID: **1** (Process Create)

---

### 🧠 Detection Logic
Malware often spawns `cmd.exe` or `powershell.exe` to execute post-exploitation commands.
A non-standard executable acting as the parent process is considered suspicious.

---

### 🔎 Splunk Query
```spl
index=endpoint EventCode=1
| where ParentImage!="C:\\Windows\\System32\\cmd.exe"
| search Image="*\\cmd.exe"
| table _time Image ParentImage CommandLine User Computer
````

---

### 🚨 Severity

**High**

---

### ⚠️ Possible False Positives

* Custom IT automation tools
* Legitimate scripts bundled in installers

---

### ✅ Analyst Response

* Validate parent process reputation
* Check file hash against threat intelligence
* Review command-line arguments
* Correlate with network activity (Event ID 3)

---

### 🧩 MITRE ATT&CK Mapping

* **T1059** – Command and Scripting Interpreter

---

---

## 🌐 Rule 2 – Suspicious Outbound Network Connection (Reverse Shell Behavior)

### 🎯 Purpose

Detect suspicious outbound connections initiated by uncommon executables.

---

### 🔍 Log Source

* Sysmon
* Event ID: **3** (Network Connection)

---

### 🧠 Detection Logic

Endpoints rarely initiate outbound connections to non-standard ports from unknown executables.
This behavior is consistent with reverse shell activity.

---

### 🔎 Splunk Query

```spl
index=endpoint EventCode=3
| where DestinationPort > 1024
| table _time Image SourceIp DestinationIp DestinationPort Protocol
```

---

### 🚨 Severity

**Critical**

---

### ⚠️ Possible False Positives

* Custom internal applications
* Developer testing tools

---

### ✅ Analyst Response

* Identify destination IP ownership
* Check if the executable is signed
* Correlate with process creation events
* Isolate endpoint if confirmed malicious

---

### 🧩 MITRE ATT&CK Mapping

* **T1071** – Application Layer Protocol
* **T1041** – Exfiltration Over C2 Channel

---

---

## 🧬 Rule 3 – Process Tree Anomaly (Suspicious Parent-Child Relationship)

### 🎯 Purpose

Identify abnormal process chains indicative of malware execution.

---

### 🔍 Log Source

* Sysmon
* Event ID: **1**

---

### 🧠 Detection Logic

Malware often spawns multiple system utilities in a short timeframe for enumeration.

---

### 🔎 Splunk Query

```spl
index=endpoint EventCode=1
| stats count by ParentImage Image
| where count > 2
```

---

### 🚨 Severity

**Medium**

---

### ⚠️ Possible False Positives

* Software installers
* IT management tools

---

### ✅ Analyst Response

* Review execution timeline
* Validate parent process legitimacy
* Cross-check with user activity

---

### 🧩 MITRE ATT&CK Mapping

* **T1106** – Native API
* **T1082** – System Information Discovery

---

## 🧠 Summary

These detection rules demonstrate how basic attacker behavior generates detectable endpoint telemetry.
By correlating process creation and network activity, SOC analysts can identify malicious behavior without relying on payload signatures.

This approach reflects real-world SOC detection engineering practices.

```

---

## ✅ Ini sudah memenuhi standar portofolio SOC karena:
✔ Selaras dengan README  
✔ Selaras dengan detection-analysis  
✔ Ada **logic + query + response + MITRE**  
✔ Tidak offensive (aman & profesional)  
✔ Recruiter bisa langsung baca dan paham mindset kamu  

---

### Next recommended step (opsional tapi keren):
- Tambah folder `screenshots/` dan rename:
  - `01-nmap-scan.png`
  - `02-malware-execution.png`
  - `03-sysmon-eventid1.png`
  - `04-sysmon-eventid3.png`
  - `05-process-tree.png`

Kalau mau, aku bisa:
- 🔍 Review final repo kamu
- 🎤 Simulasikan interview SOC pakai repo ini
- ✍️ Bantu bikin LinkedIn post dari project ini

Tinggal bilang mau lanjut ke mana 👌
```
