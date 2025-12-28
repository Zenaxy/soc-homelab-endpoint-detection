# Detection Rules – Endpoint Malware Activity

## 🎯 Purpose
This document defines detection logic used to identify suspicious endpoint behavior observed during the malware simulation lab.

The goal is to detect abnormal process execution and network activity using Sysmon telemetry in Splunk.

---

## 🚨 Detection Rule 1 – Suspicious Process Execution

### Description
Detects execution of suspicious or non-standard executable files spawning command-line interpreters such as `cmd.exe`.

### Data Source
- Sysmon Event ID: 1 (Process Creation)

### Detection Logic
- Parent process is a non-standard executable
- Child process is `cmd.exe`

### Example SPL Query
```spl
index=endpoint EventCode=1
ParentImage="*.exe"
Image="*\\cmd.exe"
